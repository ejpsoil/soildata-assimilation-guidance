# pycsw

*Status: in progress*

An open source python catalogue implementation, used within [CKAN-spatial](https://github.com/ckan/ckanext-spatial) and [GeoNode](https://geonode.org).

Supports CSW (v2 and v3) and OGC API Records. Uses a fixed metadata model and has various metadata model output formats. Capability to harvest metadata from remote sources (CSW, WMS, WFS, SOS, etc)

## Quick start

```
docker run -d -name pycsw -p 8000:8000 geopython/pycsw
```

- Visit https://localhost:8000
- Prepare a folder of iso19139 files, mount it on the container and load it with pycsw-admin.py

## Read more

- Website: https://pycsw.org/
- Github: https://github.com/geopython/pycsw
- Docker: https://hub.docker.com/r/geopython/pycsw
- Demo: https://demo.pycsw.org/cite/collections