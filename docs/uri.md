URI policy
==========

## The role of URIs

The [Unified Resource Identifier](https://www.rfc-editor.org/rfc/rfc3986) is a
standard set by The Internet Society, that has been in development for more that
30 years. It is a unique sequence of characters that identifies a logical or
physical resource used by web technologies. 

## Types of URIs

There are two types of URIs that are important to identify: Unified Resource
Names (URNs) and Unified Resource Locators (URLs). 

## URN

URNs are logical identifiers, simply providing a name for a resource. A URN does
not indicate where to find or access the resource, only gives it a name. URNs
start with the characters `urn:` to which follows a namespace and then a
succession of other strings that identify sub-categories or paths down to the
particular resource name.
  
The `lex:` namespace is used in some countries to identify legislation
documents. As an example, a URN to a European Directive:
`urn:lex:eu:council:directive:2010-03-09;2010-19-UE`

URNs are used to identify books, media works, trade items, shipping vessels and
many other resources. In the context of data provision over the internet that
are less used, as they do not provide location. However, they can be useful to
identify other resources somehow associated with the data in question.

### URL

In its turn, the URL not only identifies a resource, it also provides a location
and the mechanism to interact with it. These are the most commonly used URIs in
the Semantic Web and in digital data exchange in general.

A URL is composed by three broad
components:

- **Protocol**: identifies a specific data exchange mechanism, for instance
  Hyper Text Transfer Protocol (HTTP) or File Transfer Protocol (FTP). It
composes the first segment of the URL and is followed by the characters `://`.
Examples: `http://`, `file://`.

- **Authority**: an individual or institution responsible for the resource and
  usually the infrastructure that may provide it on the internet. E.g.
`isric.org`.

- **Path**: the relative path to the resource within the institutional
  infrastructure. E.g. `/locations/id/123`.

Although meant to locate resource, URLs may not always do so and be simply used
as identifiers. They remain useful as identifiers as they express an authority
over the resource. URLs that do not locate a resource are termed as "non
dereferenceable", meaning that when a computer programme attempts to use it no
result is obtained.

## Selecting a URI structure

Before making any data available on the internet, say to publish the result of a
transformation into RDF, you must devise an appropriate URI structure. This is
particularly important with RDF, as every non-literal element in a knowledge
graph must correspond to a URI. But even outside the Semantic Web, URIs are very
useful, as
they provide unique identifiers on the World Wide Web (WWW) to your datasets,
even to each individual datum.

A simple approach is to construct your URIs with three building blocks: 

1. Use a sub-domain of your institutional domain to
identify a single project or dataset. E.g. `soil.my-institute.org`.

2. Add a path that starts with a name or identifier of the class
to which the data instance belongs. This can be a database table, or a OWL or
UML class. E.g. `/profile`.

3. Complete the path with a number or string that unequivocally identifies the
   data instance within the class. If you work with relational databases this
may be the table primary key. An example: `#prof1`. 

The complete template for this approach looks like:

```
http://project.institution.org/class#identifier
``` 

### The WoSIS example

ISRIC is currently working on a pilot service providing data from the [World
Soil Information Service](https://www.isric.org/explore/wosis) (WoSIS) as RDF
compliant with the [GloSIS Web Ontology](https://github.com/rapw3k/glosis). You
may browse these data at
[virtuoso.isric.org](https://virtuoso.isric.org/describe/?url=http%3A%2F%2Fwosis.isric.org%2Fdataset%23CU-SOTER&sas=SAME_AS_OFF&sid=11).

In this example the service is identified in the authority segment of the the
URI (`wosis.isric.org`). Then short identifiers for GloSIS classes make the
prefix of the URI path, (`site`, `profile`, `layer`, etc). The path suffix is
composed by an hash followed by the WoSIS primary key. 

Some examples currently used with WoSIS data:

  - `http://wosis.isric.org/site#72007`
  - `http://wosis.isric.org/profile#72007`
  - `http://wosis.isric.org/layer#64448`
  - `http://wosis.isric.org/observation#4357805`
  - `http://wosis.isric.org/result#4357805`

## Questions

- Does your institution already has a URI policy?

- Is it applied to data provision?

- If not, can you elaborate a proposal?

## Further reading

- [Best Practices URI Construction](https://www.w3.org/2011/gld/wiki/223_Best_Practices_URI_Construction)

- [URIs, URLs, and URNs: Clarifications and Recommendations 1.0](https://www.w3.org/TR/uri-clarification/)

- [On Linking Alternative Representations To Enable Discovery And Publishing](https://www.w3.org/2001/tag/doc/alternatives-discovery.html)
