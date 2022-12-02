# pycsw

An open source python catalogue implementation, used within [CKAN-spatial](https://github.com/ckan/ckanext-spatial) and [GeoNode](https://geonode.org).

Lightweight implementation of CSW and OGC API Records. 

- Website: https://pycsw.org/
- Github: https://github.com/geopython/pycsw
- Docker: https://hub.docker.com/r/geopython/pycsw
- Demo: https://demo.pycsw.org/cite/collections

## Cookbook

```
docker run -d -name pycsw -p 8000:8000 geopython/pycsw
```

- Visit https://localhost
- Prepare a folder of iso19139 files, mount it on the container and load it with pycsw-admin.py