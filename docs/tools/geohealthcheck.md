# GeoHealthCheck

*Status: ready*

A tool to monitor availability of spatial services. The tool will query a list of configured spatial services at intervals and report on availability using charts. The tool can also send out notifications in case of disruptions.

The tool can be compared to (and is often combined with) generic web availability tools such as Zabbix, Uptimerobot, Nagios. The generic tools are used to identify if the service is up, GeoHealthCheck will go a level deeper, identify which layers are available in a getcapabilities response and ask random maps to individual layers to identify if a service is properly running.

## Cookbook

The cookbook assunes docker desktop installed. Alternatively you can create a personal account at https://demo.geohealthcheck.org (click `register` in the login page). Start a local GeoHealthCheck container:

```
docker run --name ghc -p80:80 geopython/geohealthcheck
```

- Visit http://localhost
- Login as user: `admin`, password: `admin`
- Click `ADD +` on the top bar right, select `WMS`
- Add a WMS url, for example `https://maps.isric.org/mapserv?map=/map/wrb.map`
- On the next screen click `add` for `WMS Drilldown` (so all layers are validated)
- Click `Save` and `test`
- When finished, click `Details` to see the test result
