# OGC API Features from a proxied WFS using ldproxy

*Status: ready*

[ldproxy](https://ldproxy.net) is an open source product by [interactive instruments](https://www.interactive-instruments.de). The team has an important role in the development of the suite of new OGC API's and the implementation of ldproxy is an important aspect of that process.

## Quick start

- Run the image

  ```
  docker run -p7080:7080 -v${PWD}:/ldproxy/data iide/ldproxy
  ```

- Navigate to https://localhost:7080/manager/
- Login as usr:admin pwd:admin (set new password)
- You arrive in the 'services' page, create a new service with `plus` button top right
- We're setting up LDProxy to act as a proxy to provide OGC API Features over an existing WFS. Select type `WFS`
- Provide a name and a WFS url (for example https://maps.isric.org/mapserv?map=/map/wosis_latest.map&request=getcapabilities&service=wfs)
- Click `ADD`. You return to the list of services, select the one you've just created and click on the `home` button top right to open it.
- Click `Access the data`, select a `collection` to visualise the items of the collection.

With a [tunnel](../utils/localtunnel.md), you can test the local service using [inspire OGC API Features validator](https://inspire.ec.europa.eu/validator).

## Read more

- [Github](https://github.com/interactive-instruments/ldproxy)
- [Docker](https://hub.docker.com/r/iide/ldproxy)
- [Documentation](https://docs.ldproxy.net)
- [Report testbed Spatial data on the web](https://github.com/geo4web-testbed/topic4/blob/master/spatial-data-on-the-web-using-sdi-report.pdf)

