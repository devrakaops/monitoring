# DevOps Monitoring

## Introduction 

आज के समय में लगभग हर Application, Website, API, Microservice, Container और Kubernetes Cluster को 24x7 उपलब्ध (Available) रहना होता है।

यदि कोई Application अचानक Slow हो जाए, Server Down हो जाए, Memory Full हो जाए, Database Crash हो जाए या Users को Error आने लगे, तो DevOps Team, SRE Team और Operations Team को तुरंत पता चलना चाहिए।

यहीं पर **Monitoring** हमारी मदद करता है।

Monitoring DevOps का एक बहुत महत्वपूर्ण हिस्सा है क्योंकि यह हमें System, Infrastructure और Applications की Health और Performance को लगातार देखने और समझने की क्षमता देता है।

यदि Monitoring न हो, तो हमें किसी समस्या का पता तभी चलेगा जब User शिकायत करेगा।

लेकिन यदि Monitoring सही तरीके से लागू की गई हो, तो हम User को समस्या आने से पहले ही Issue को Detect और Resolve कर सकते हैं।

---

# Monitoring क्या है?

Monitoring का मतलब है किसी System, Application, Infrastructure, Server या Service को लगातार Observe (देखना), Track करना और उसकी Health तथा Performance को Measure करना।

सरल भाषा में:

> Monitoring हमें Real-Time में यह समझने में मदद करता है कि हमारे Systems और Applications के अंदर क्या चल रहा है।

Monitoring की मदद से हम कई महत्वपूर्ण प्रश्नों के उत्तर प्राप्त कर सकते हैं:

* क्या Server सही से काम कर रहा है?
* क्या CPU अधिक उपयोग हो रहा है?
* क्या Memory खत्म होने वाली है?
* क्या Disk भर रही है?
* क्या Application Slow हो गई है?
* क्या Users को Error मिल रहे हैं?
* क्या Database पर अधिक Load है?
* क्या कोई Service Down हो गई है?
* क्या कोई Pod Crash हो रहा है?

Monitoring हमें Problems को जल्दी Detect करने और उन्हें जल्दी Resolve करने में मदद करता है।

---

# Monitoring क्यों जरूरी है?

Monitoring केवल Data Collect करने के लिए नहीं होती।

Monitoring का मुख्य उद्देश्य है:

* Reliability बढ़ाना
* Availability बढ़ाना
* Performance बेहतर करना
* Downtime कम करना
* User Experience बेहतर बनाना

---

# 1. Real-Time Visibility

Monitoring हमें Real-Time में System की स्थिति दिखाती है।

हम तुरंत देख सकते हैं:

* CPU Usage
* Memory Usage
* Disk Usage
* Network Traffic
* Application Performance
* Service Health

इससे Team को पता रहता है कि System के अंदर अभी क्या चल रहा है।

---

# 2. Early Problem Detection

अधिकांश Problems अचानक नहीं आतीं।

उनके आने से पहले कुछ संकेत दिखाई देते हैं।

जैसे:

* CPU लगातार बढ़ रहा है
* Memory लगातार भर रही है
* Disk Space कम हो रही है
* Application Response Time बढ़ रहा है

Monitoring इन संकेतों को पहले ही Detect कर लेती है।

इससे बड़ी समस्या बनने से पहले समाधान किया जा सकता है।

---

# 3. Faster Troubleshooting

जब Production में कोई Issue आता है, तो Monitoring Root Cause ढूंढने में बहुत मदद करती है।

उदाहरण:

यदि Website Slow हो गई है तो Monitoring हमें बता सकती है:

* CPU High है?
* Memory कम है?
* Database Slow है?
* Network Issue है?
* Application Error दे रही है?

इससे Troubleshooting का समय काफी कम हो जाता है।

---

# 4. High Availability

हर Company चाहती है कि उसकी Services हमेशा Available रहें।

Monitoring की मदद से:

* Failures जल्दी Detect होते हैं
* Alerts तुरंत मिलते हैं
* Engineers जल्दी Response कर पाते हैं

जिससे Downtime कम होता है।

---

# 5. Performance Optimization

Monitoring हमें Performance Bottlenecks ढूंढने में मदद करती है।

उदाहरण:

* Slow Database Queries
* High CPU Usage
* High Memory Consumption
* Slow APIs
* Overloaded Servers

इन जानकारियों की मदद से हम Performance Improve कर सकते हैं।

---

# 6. Cost Optimization

Cloud और Data Center Resources महंगे होते हैं।

Monitoring की मदद से हम देख सकते हैं:

* कौन से Servers Underutilized हैं
* कौन से Resources Waste हो रहे हैं
* कहां Scaling की जरूरत है

इससे Infrastructure Cost कम की जा सकती है।

---

# 7. Better User Experience

Users हमेशा Fast और Reliable Applications चाहते हैं।

Monitoring की मदद से:

* Faster Response Time मिलता है
* Downtime कम होता है
* Application Performance बेहतर रहती है

जिससे Customer Satisfaction बढ़ती है।

---

# 8. Continuous Improvement

Monitoring लगातार Data Collect करती रहती है।

इस Data की मदद से Organizations:

* Applications Improve करती हैं
* Infrastructure Optimize करती हैं
* Deployment Process Improve करती हैं
* Reliability बढ़ाती हैं

---

# Monitoring के प्रकार (Types of Monitoring)

Monitoring को कई Categories में बांटा जा सकता है।

Beginner Level पर आपको मुख्य रूप से चार प्रकार समझने चाहिए।

---

# 1. Infrastructure Monitoring

Infrastructure Monitoring का Focus Server और Hardware Resources पर होता है।

यह Monitoring हमें बताती है:

* Server Healthy है या नहीं
* CPU कितना उपयोग हो रहा है
* Memory कितनी उपयोग हो रही है
* Disk Space कितनी बची है
* Network कैसा काम कर रहा है

---

## Common Infrastructure Metrics

* CPU Usage
* Memory Usage
* Disk Usage
* Disk I/O
* Network Traffic
* Network Errors
* System Load
* Uptime

---

## Example

मान लीजिए एक Ubuntu Server पर Application चल रही है।

Monitoring Dashboard दिखाता है:

```text
CPU Usage = 95%
Memory Usage = 90%
Disk Usage = 85%
```

इसका मतलब है कि Server पर बहुत अधिक Load है और जल्द ही Performance Issues आ सकते हैं।

---

# 2. Application Monitoring

Application Monitoring का Focus Application की Health और Performance पर होता है।

यह Monitoring हमें बताती है:

* Application Healthy है या नहीं
* कितने Requests आ रहे हैं
* Response कितना समय ले रहा है
* कितने Errors आ रहे हैं

---

## Common Application Metrics

* Request Rate
* Response Time
* Error Rate
* API Latency
* Active Users
* Application Availability

---

## Example

यदि किसी Website का Normal Response Time:

```text
200ms
```

होता है और अचानक:

```text
2000ms
```

हो जाता है,

तो Monitoring हमें तुरंत संकेत देगी कि Application में Performance Issue है।

---

# 3. Log Monitoring

Logs किसी भी System या Application की सबसे महत्वपूर्ण Information होती हैं।

जब भी कोई Event होता है, Error आती है, Service Start होती है या Crash होती है, तो Logs Generate होते हैं।

---

## Log Monitoring हमें बताती है:

* Application Crash क्यों हुई?
* Database Connection Fail क्यों हुआ?
* User Login क्यों Fail हुआ?
* API Error क्यों दे रही है?

---

## Common Log Sources

* Application Logs
* System Logs
* Database Logs
* Security Logs
* Web Server Logs

---

## Linux Log Locations

```text
/var/log/
/var/log/nginx/
/var/log/mysql/
```

---

## System Logs देखने के लिए

```bash
journalctl
```

Logs Root Cause Analysis के लिए सबसे महत्वपूर्ण Source होते हैं।

---

# 4. User Experience Monitoring

User Experience Monitoring का Focus Users पर होता है।

यह देखने का प्रयास करती है कि User Application का उपयोग करते समय कैसा अनुभव प्राप्त कर रहा है।

---

## Common UX Metrics

* Page Load Time
* User Journey
* Session Duration
* Click Rate
* Conversion Rate
* Error Screens

---

## Example

हो सकता है Server और Application दोनों Healthy हों,

लेकिन User की Website 10 Seconds में खुल रही हो।

इस स्थिति में Infrastructure Monitoring Problem नहीं दिखाएगी, लेकिन User Experience Monitoring Problem पकड़ लेगी।

---

# Metrics-Based Monitoring vs Log-Based Monitoring

Monitoring को समझने के लिए यह अंतर जानना बहुत जरूरी है।

---

# Metrics-Based Monitoring

Metrics Numeric Data होते हैं।

उदाहरण:

```text
CPU = 70%
Memory = 60%
Disk = 80%
```

Metrics हमें बताते हैं:

> System में क्या हो रहा है?

---

## Common Metrics Tools

* Prometheus
* Node Exporter
* Grafana

---

# Log-Based Monitoring

Logs Detailed Event Information देते हैं।

उदाहरण:

```text
Database Connection Failed
```

या

```text
Authentication Error
```

Logs हमें बताते हैं:

> Problem क्यों हो रही है?

---

## Common Log Monitoring Tools

* Loki
* Promtail
* Grafana

---

# Monitoring Architecture

एक सामान्य Monitoring Architecture में चार मुख्य Components होते हैं:

1. Metrics Collection
2. Log Collection
3. Data Storage
4. Data Visualization

---

# Prometheus

## Prometheus क्या है?

Prometheus एक Open Source Monitoring और Alerting Tool है।

यह Metrics Collect, Store और Query करने के लिए उपयोग किया जाता है।

आज Kubernetes और Cloud Native दुनिया में Prometheus सबसे लोकप्रिय Monitoring Tool माना जाता है।

---

## Prometheus की Responsibilities

* Metrics Collect करना
* Metrics Store करना
* Metrics Query करना
* Alert Generate करना

---

## Default Port

```text
9090
```

---

## Configuration File

```text
/etc/prometheus/prometheus.yml
```

---

## Prometheus क्या Monitor कर सकता है?

* CPU Usage
* Memory Usage
* Disk Usage
* Network Statistics
* Kubernetes Metrics
* Application Metrics

---

# Exporters

## Exporters क्या होते हैं?

Prometheus सीधे हर Application या Operating System को नहीं समझ सकता।

इसलिए Exporters का उपयोग किया जाता है।

Exporters Metrics Collect करके Prometheus Format में उपलब्ध कराते हैं।

---

# Node Exporter

यह Linux Server की Metrics Collect करता है।

---

## Collect करता है

* CPU Metrics
* Memory Metrics
* Disk Metrics
* Network Metrics

---

## Default Port

```text
9100
```

---

# MySQL Exporter

Collect करता है:

* Queries
* Connections
* Buffer Pool Metrics
* Database Performance Metrics

---

# Blackbox Exporter

Collect करता है:

* Website Availability
* API Availability
* DNS Monitoring
* SSL Monitoring

---

# Kubernetes Exporter

Collect करता है:

* Pod Status
* Node Health
* Resource Usage
* Cluster Metrics

---

# Loki

## Loki क्या है?

Loki एक Open Source Log Aggregation System है।

इसका मुख्य काम Logs को Collect, Store और Query करना है।

---

## Loki की Responsibilities

* Logs Store करना
* Logs Query करना
* Logs Search करना
* Centralized Log Management

---

## Default Port

```text
3100
```

---

## Health Endpoint

```text
http://IP:3100/ready
```

---

## Metrics Endpoint

```text
http://IP:3100/metrics
```

---

# Promtail

## Promtail क्या है?

Promtail एक Log Collection Agent है।

यह Servers और Applications की Log Files को पढ़ता है और Loki को भेजता है।

---

## Responsibilities

* Logs Read करना
* Log Changes Monitor करना
* Logs Collect करना
* Loki को Forward करना

---

## Configuration File

```text
/etc/promtail/config.yml
```

---

# Grafana

## Grafana क्या है?

Grafana एक Open Source Visualization Dashboard Tool है।

यह Monitoring Data को Graphs, Charts और Dashboards के रूप में दिखाता है।

---

## महत्वपूर्ण बात

Grafana स्वयं Metrics या Logs Store नहीं करता।

Grafana केवल दूसरे Data Sources से Data लेकर Visualize करता है।

---

## Common Data Sources

* Prometheus
* Loki

---

## Grafana की Responsibilities

* Dashboard Creation
* Visualization
* Alert Management
* Metrics Analysis
* Log Analysis

---

## Default Port

```text
3000
```

---

# Alerts and Notifications

Monitoring तभी पूरी मानी जाती है जब Alerts Configure किए जाएं।

यदि Engineer हर समय Dashboard देखता रहे तो Monitoring का उद्देश्य पूरा नहीं होगा।

इसलिए Monitoring Tools Automatically Alerts भेजते हैं।

---

## Example Alerts

* CPU > 90%
* Memory > 85%
* Disk > 80%
* Website Down
* Pod Crash
* Database Down
* API Failure

---

## Notification Channels

* Email
* Slack
* PagerDuty
* Microsoft Teams

---

# Complete Monitoring Flow

## Metrics Monitoring Flow

```text
Server
   │
   ▼
Exporters
   │
   ▼
Prometheus
   │
   ▼
Grafana
   │
   ▼
Alerts
```

---

## Log Monitoring Flow

```text
Application Logs
       │
       ▼
    Promtail
       │
       ▼
      Loki
       │
       ▼
    Grafana
       │
       ▼
     Alerts
```

---


