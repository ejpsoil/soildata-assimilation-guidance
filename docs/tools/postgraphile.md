# GraphQL with Postgraphile

[GraphQL](https://graphql.org) is a defacto standard for self describing api's on hierarchical data. Graphql provides via its api specification capabilities to query datasets using filters, but also indicate which properties to be returned. The GraphQL website provides a [quick start on Graphql](https://graphql.org/graphql) based on NodeJS.

GraphQL is currently not endorsed as an INSPIRE Good Practice, but it fits many aspects of an INSPIRE download service. GraphQL is a good fit to disseminate measurement and observation data from soil profiles.

At ISRIC we use GraphQL (along WMS/WFS) to disseminate the [WOSIS soil profile database](https://www.isric.org/explore/wosis).

## Postgraphile

[Postgraphile](https://www.graphile.org/postgraphile/) is a NodeJS server application which creates a GraphQL api on any postgres database. For this cookbook we've prepared a docker orchestration which includes a postgres database and a postgraphile container. Also included is PGadmin, which provides a webbased user interface to the database.

## Load some data into the database

## Query a GraphQL endpoint


Website: https://www.graphile.org/postgraphile/