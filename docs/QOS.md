---
title: Overview Quality of Service
summary: 
authors:
    - Paul van Genuchten
date: 2022-11-10
---

# Overview Quality of Service 

Via the quality of service conventions data providers report about the quality of their services. Aspects which are monitored are:

- Availability (how long was a service down or offline in a period)
- Performance and capacity (a period in which performance and capacity requirements are not met, is considered downtime)
- Usage (how much is the service used)

Measuring and reporting about Quality of Service is an aspect of step `7) Soil Information User Consideration` in the [soil information workflow](https://www.isric.org/index.php/utilise/community-practice).


There is no minimal, traditional or experimental approach on how to measure these quality indicators. Consult your IT department or hosting company which tools they are used to work with. Confirm with them to extend and/or share with you these measurements for the requested parameters.

To know the availability of a service, it requires to permanently monitor the availability of the service (excluding the maintenance windows). A basic alive-test every 5 minutes is sufficient. Many software exists for availability monitoring, such as [Zabbix](https://zabbix.com/), [Nagios](https://nagios.org/), [CheckMK](https://checkmk.com/), [pingdom](https://www.pingdom.com/). A special mention for the Python based [GeoHealthCheck](https://geohealthcheck.org/) package, which includes the capability on WMS/WFS services to drill down to the data level starting from the GetCapabilities operation.

| Cookbook | Software | Description |
| --- | --- | --- |
| [GeoHealthCheck](cookbook/geohealthcheck.md) | [GeoHealthCheck](https://geohealthcheck.org/) | A utility to report on availability of a service |
| [AWStats](cookbook/awstats.md) | [AWStat](https://awstats.sourceforge.io/)  | A utility to report on service usage |
| [Capacity tests with jmeter](cookbook/jmeter.md) | [jmeter](https://jmeter.apache.org/) | Utility for performance and capacity testing |

To know the capacity and performance of the service it is optimal to perform some load tests prior to moving to production. A common mistake is to provide a WMS service to a big vector dataset. When requesting that dataset on a national level, the server runs into problems drawing all the features at once. An alternative approach to evaluate performance is to extract the access logs of the service into an aggregation tool like [Kibana](https://www.elastic.co/kibana) and evaluate the number of requests exceeding the limits.

To capture the usage of a service you can extract the usage logs and import them in a tool like Kibana, [Splunk](https://www.splunk.com/) or [AW stats](https://awstats.sourceforge.io/). Defining rules to extract the requested layer name from a WMS request is useful. Mind that not all requests are GET requests, some WFS requests use POST, which may need some configuration on the webserver to enable POST parameter logging. Make sure the logging includes the 'Referer' and 'User-agent' parameters, which allows to differentiate types of uses. Finally consider there is a [GDPR](https://eur-lex.europa.eu/eli/reg/2016/679/oj) privacy aspect to collecting access logs. Consider to exclude the IP address of the user and define a maximal retention for access logs.

