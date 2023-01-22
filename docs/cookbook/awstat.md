# AWStat

*Status: in progress*

[AWStat](https://awstats.sourceforge.io/) is a utility to report on service usage. These days there are advanced tools such as Splunk, Elastic Search, Grafana which can report on service usage. These tools are recommended to use if your orchanisation provides it. However if such a tool is not provided AWStat could be an interesting alternative. It is a small utility with some nice vizualisation options to present aggregated usage statistics in a dashboard.

Most of these tools, including AWStats use the Access logs of the webserver to extract and aggregate usefull information. Consider that these applications need a carefull privacy strategy, because ip-adresses from logs can be used to identify users.

## Deploy AWStats

Navigate to an empty folder, place a sample log file in the folder.

```
192.168.2.20 - - [28/Jul/2006:10:27:10 -0300] "GET /cgi-bin/try/ HTTP/1.0" 200 3395
127.0.0.1 - - [28/Jul/2006:10:22:04 -0300] "GET / HTTP/1.0" 200 2216
211.0.23.16 - - [28/Jul/2006:10:27:32 -0300] "GET /hidden/ HTTP/1.0" 404 7218
211.168.17.20 - - [28/Jul/2006:10:27:10 -0300] "GET /cgi-bin/try/ HTTP/1.0" 200 3395
18.12.120.17 - - [28/Jul/2006:10:22:04 -0300] "GET / HTTP/1.0" 200 2216
163.22.12.13 - - [28/Jul/2006:10:27:32 -0300] "GET /hidden/ HTTP/1.0" 404 7218
```

Start a container

```
docker run \
    --detach \
    --restart always \
    --publish 3000:80 \
    --name awstats \
    --volume $(PWD):/var/local/log:ro \
    pabra/awstats
```

Parse the logs:

```
docker exec awstats awstats_updateall.pl now
```

View the dashboard:

http://localhost:3000



## Read more

- [Website](https://www.awstats.org)
- [Docker](https://hub.docker.com/r/pabra/awstats)
- [Configuration](http://www.awstats.org/docs/awstats_config.html)