# GraphQL with Postgraphile

*Status: in progress*

[GraphQL](https://graphql.org) is a defacto standard for self describing API's on hierarchical data. Graphql provides via its API specification capabilities to query datasets using filters, but also indicate which properties to be returned alongside with proper pagination. The GraphQL website provides a [quick start on Graphql](https://graphql.org/graphql) based on NodeJS.

GraphQL is currently not endorsed as an INSPIRE Good Practice, but it fits many aspects of an INSPIRE download service. GraphQL is a good fit to disseminate measurement and observation data from soil profiles.

At ISRIC we use GraphQL (along WMS/WFS) to disseminate the [WOSIS soil profile database](https://www.isric.org/explore/wosis).

## Postgraphile

[Postgraphile](https://www.graphile.org/postgraphile/) is a NodeJS server application which creates a GraphQL API on any postgres database. Besides being 
totally compatible with PostgreSQL it also supports PostGIS and therefore it can easily work as a [Spatial GraphQL API](https://github.com/lcalisto/workshop-spatial-graphql).

For this recipe we've prepared a [docker](../utils/docker.md) orchestration which includes a postgres database and a postgraphile container. Also included is PGadmin, which provides a webbased user interface to the database.

## Load some data into the database

## Query a GraphQL endpoint


- https://www.graphile.org/postgraphile/
- https://github.com/lcalisto/workshop-spatial-graphql
- *work in progress*
