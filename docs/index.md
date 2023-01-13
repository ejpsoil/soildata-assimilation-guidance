---
title: Introduction
summary: 
authors:
    - Paul van Genuchten
date: 2022-11-10
---

# Introduction

This WIKI is a collaborative effort to collect and describe hands-on good practices on data assimilation and dissemination in the [Soil](https://agrovoc.fao.org/browse/agrovoc/en/page/c_7156) domain, with a focus on Europe. The [INSPIRE](https://inspire.ec.europa.eu/) directive has been and is an important effort for standardisation in the environmental data domain, therefore this WIKI has a lot of links to INSPIRE sources. Because INSPIRE adopts industry standards, this WIKI does reference common standards from ISO, Open Geospatial Consortium, Global Soils Partnership, IANA and W3C, giving it a global relevance.

For data assimilation 3 aspects are important:

- Data dissemination; the process of making data discoverable and available
- Data harmonization; the process of adopting or transforming data to a common data model
- Data consumption; the process of collecting (harmonised) data from various sources

## Organisation of the articles

[Toner et al, 2022](https://www.isric.org/index.php/utilise/community-practice) identified 6 steps in a typical soil information workflow from a data producer perspective and a separate category for the data user perspective. These steps form a relevant categorisation of the articles in this wiki. Much of the articles apply to the producer categories `4) Data organisation` and `6) data and info sharing` and [7) Soil Information User Consideration](consumer.md). We've labeled each of the articles as to which step in the workflow they apply.

![Soil information workflow](https://www.isric.org/sites/default/files/Soil%20information%20workflow_circular_notext.jpg)

This wiki lists a series of options for publishing data according to the Technical Guidelines and/or the Good Practices dedicated to use cases from the Soil domain. For each option recipes on various technologies are provided. The practices are categorized at 3 levels:

- Minimal, based on a minimal effort
- Traditional, following initial technical guidelines
- Experimental, following recent and upcoming good practices

The practices cover 7 topics.

- [Identification and namespaces](identification.md)
- [Data harmonization](etl.md)
- [Code lists](codelists.md)
- [Metadata and Discovery](metadata.md)
- [View services](view.md)
- [Download services](download.md)
- [Quality of service](QOS.md)

!!! info

    Disclaimer: References to products and approaches are examples. We do not aim to provide a complete listing, nor endorse a specific technology or service provider. Please consult any alternative software provider to what extent INSPIRE is supported in their products. In that scenario consider to contribute your experiences to this WIKI. 

## Reading guide

While reading the document you may realize; if INSPIRE offers so many options, then consuming and combining data on the client side will be a challenge, a client needs to be aware of all these practices and conventions. But consider that despite the various technical options (which could also be bridged by intermediaries) there are certain aspects that are constant in any of the implementations; any implementation covers some form of data discovery, harmonization, view and download services. But also, aspects such as identifier persistence and adoption of code lists, as we will explain.

When selecting one of the available options, consider the following aspects:

- The minimal implementation will have limitations for end users (for example having to download the full dataset, if they are only interested in a small section). On the other hand, minimal implementations tend to be less complex in setup which makes understanding the implementation easier.
- The traditional implementation has the most active users, so dedicated documentation and tooling is available with high Technical Readiness Level (TRL). However, the technology is based on conventions of almost 20 years ago, some conventions are outdated with current IT practices.
- An experimental approach brings the risk of incomplete documentation and tools. Also there is less evidence on conformance to the directive. But it also gives opportunity to use current technologies and engage with the community to design the next iteration of INSPIRE.

Before selecting an option evaluate the following aspects in your organization.

- What are current IT tools and conventions used in the organization to understand which of the approaches fits best with the current knowledge and experience
- Combine an implementation of INSPIRE with business cases that generate direct benefit for your organization or partners. For example, adoption of the open data directive, better documentation and reporting of service levels, improved archival of data, discoverability on search engines.
- Assess the projected audience. Verify that the complexity and nature of the implementation matches with the expectations and capabilities of that audience.

We recommend to start with a minimal implementation and validate it with the provided [compliance test tooling](https://inspire.ec.europa.eu/work-programme/validation-and-conformity-testing). From there, extend the implementation while continuing the tests with each iteration. In this scenario you are able to focus on the important aspects and prevent caveats early on in the process.

For background reading on terminology and general principles described in this wiki (like data modelling, ontologies and the INSPIRE model), please see EJP Soil Deliverable 6.1 chapter 3.
