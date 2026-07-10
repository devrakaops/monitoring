````markdown
# Grafana + Loki + Promtail Troubleshooting Guide
## Issue: Labels Not Appearing in Grafana Explore

### Environment

| Component | Status |
|------------|----------|
| Grafana | Running |
| Loki | Running |
| Promtail | Running |
| Log Source | Apache2 Logs |
| OS | Ubuntu |
| Promtail User | promtail |
| Log Path | /var/log/apache2/*.log |

---

# Architecture

```text
Apache Access Logs
        |
        v
   Promtail
        |
        v
      Loki
        |
        v
    Grafana
```

---

# Problem Statement

Although Grafana, Loki, and Promtail were running successfully, no labels were visible in Grafana Explore.

Expected:

```text
job=apache2
```

Actual:

```text
No labels visible
```

---

# Initial Promtail Configuration

```yaml
server:
  http_listen_port: 9080
  grpc_listen_port: 0

positions:
  filename: /tmp/positions.yaml

clients:
- url: http://localhost:3100/loki/api/v1/push

scrape_configs:
- job_name: system

  static_configs:
  - targets:
      - localhost

    labels:
      job: apache2
      __path__: /var/log/apache2/*.log
```

---

# Troubleshooting Workflow

## Step 1: Verify Loki is Running

```bash
curl http://localhost:3100/ready
```

Expected Output:

```text
ready
```

Result:

✅ Loki Healthy

---

## Step 2: Verify Labels in Loki

```bash
curl -s http://localhost:3100/loki/api/v1/labels
```

Output:

```json
{
  "status":"success",
  "data":[
    "filename",
    "job",
    "service_name"
  ]
}
```

Observation:

- Loki is receiving logs
- Labels exist

Result:

✅ Loki Functional

---

## Step 3: Check Available Job Labels

```bash
curl -G -s \
"http://localhost:3100/loki/api/v1/label/job/values"
```

Output:

```json
{
  "status":"success",
  "data":["auth"]
}
```

Observation:

Expected:

```json
["apache2"]
```

Actual:

```json
["auth"]
```

Meaning:

Promtail is NOT sending Apache logs.

---

## Step 4: Verify Existing Streams in Loki

```bash
curl -G -s \
"http://localhost:3100/loki/api/v1/series" \
--data-urlencode 'match[]={job=~".+"}'
```

Output:

```json
{
  "status":"success",
  "data":[
    {
      "filename":"/var/log/auth.log",
      "job":"auth",
      "service_name":"auth"
    }
  ]
}
```

Observation:

Only auth logs exist.

Apache stream missing.

Result:

❌ Apache logs not reaching Loki

---

## Step 5: Verify Promtail Target Status

```bash
curl http://localhost:9080/targets
```

Output:

```text
system (0/1 ready)

Ready: false

job="apache2"

__path__="/var/log/apache2/*.log"
```

Observation:

Promtail discovered target but could not read it.

Result:

❌ Target Not Ready

---

## Step 6: Verify Apache Logs Exist

```bash
ls -lh /var/log/apache2/
```

Output:

```text
access.log
error.log
other_vhosts_access.log
```

Observation:

Apache logs exist.

Result:

✅ Log files available

---

## Step 7: Verify Promtail Loaded New Configuration

```bash
journalctl -u promtail -n 50
```

Output:

```text
Adding target
key="/var/log/apache2/*.log:{job=\"apache2\"}"
```

Observation:

Promtail loaded latest configuration.

Result:

✅ Configuration Correct

---

## Step 8: Verify File Permissions

### Check Path Permissions

```bash
namei -l /var/log/apache2/access.log
```

Output:

```text
drwxr-xr-- root adm apache2
-rw-r--r-- root adm access.log
```

Observation:

Directory owned by:

```text
root:adm
```

---

### Test Access as Promtail User

```bash
sudo -u promtail cat /var/log/apache2/access.log
```

Output:

```text
Permission denied
```

Observation:

Promtail cannot read Apache logs.

Result:

❌ Root Cause Found

---

# Root Cause

Promtail service runs using:

```bash
ps -ef | grep promtail
```

Output:

```text
promtail 7093 ...
```

Promtail user:

```text
promtail
```

Apache logs:

```text
root:adm
```

Apache directory permissions:

```text
750
```

Promtail is not a member of:

```text
adm
```

Therefore:

```text
Promtail
   |
   X
Cannot Access
   |
Apache Logs
```

Consequences:

- Target Not Ready
- No Log Ingestion
- No Loki Streams
- No Labels in Grafana

---

# Solution 1 (Recommended)

Add Promtail User To adm Group

```bash
usermod -aG adm promtail
```

Verify:

```bash
id promtail
```

Expected:

```text
groups=...,adm
```

Restart Promtail:

```bash
systemctl restart promtail
```

---

# Solution 2 (Lab Environment Only)

Provide World Read Access

```bash
chmod 755 /var/log/apache2
```

or

```bash
chmod o+rx /var/log/apache2
```

Warning:

❌ Not Recommended For Production

---

# Solution 3 (Testing Only)

Run Promtail As Root

Service Example:

```ini
User=root
```

Restart:

```bash
systemctl daemon-reload
systemctl restart promtail
```

Warning:

❌ Avoid In Production

---

# Post-Fix Validation

## Validate Target Status

```bash
curl http://localhost:9080/targets
```

Expected:

```text
system (1/1 ready)

Ready: true
```

---

## Generate Apache Traffic

```bash
for i in {1..50}; do
curl localhost >/dev/null
done
```

---

## Verify Loki Labels

```bash
curl -G -s \
"http://localhost:3100/loki/api/v1/label/job/values"
```

Expected:

```json
{
  "status":"success",
  "data":[
    "apache2",
    "auth"
  ]
}
```

---

## Verify Loki Streams

```bash
curl -G -s \
"http://localhost:3100/loki/api/v1/series" \
--data-urlencode 'match[]={job=~".+"}'
```

Expected:

```json
[
  {
    "job":"apache2"
  },
  {
    "job":"auth"
  }
]
```

---

## Verify Grafana

Open:

```text
Explore
```

Select:

```text
Loki Datasource
```

Query:

```logql
{job="apache2"}
```

Expected:

```text
Apache Logs Visible
```

---

# Common Root Causes When Labels Do Not Appear In Grafana

| Root Cause | Symptoms | Verification |
|------------|-----------|-------------|
| Loki Down | No datasource connection | curl localhost:3100/ready |
| Promtail Down | No ingestion | systemctl status promtail |
| Wrong Path | Target not ready | curl localhost:9080/targets |
| No Logs Generated | Empty stream | tail -f logfile |
| Permission Issue | Target not ready | sudo -u promtail cat logfile |
| Positions File Issue | New logs ignored | Remove positions.yaml |
| Wrong Loki URL | Push failure | journalctl -u promtail |
| Grafana Time Range | No results in Explore | Change to Last 24 Hours |
| Wrong Label Query | Empty Explore | Verify label values API |
| Datasource Misconfigured | Connection error | Save & Test |

---

# Key Learning

Monitoring issues are not always caused by Grafana, Loki, or Promtail configuration.

A healthy monitoring stack can still fail if:

```text
Application Logs
      |
      X
 Permission Denied
      |
 Promtail
      |
 Loki
      |
 Grafana
```

In this incident:

- Grafana was healthy
- Loki was healthy
- Promtail was healthy

The actual issue was:

```text
Linux File Permission
```

This is one of the most common real-world troubleshooting scenarios in Grafana Loki environments.
````
