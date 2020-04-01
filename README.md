# API Evolutions

This repository contains the documentation of a RESTful API offering lightweight Jira-like project management features.

It illustrates all the possible evolutions of an API according to the following listing:
![evolutions](./evolutions-list.png)

## Structure

The commit history is used to illustrate evolutions. In addition, the folder [api-versions](./api-versions) contains all versions of the API. One version is created per commit.

The latest version is [openapi.yaml](./openapi.yaml).

## OpenApi enrichments

### Affiliation

An `x-affiliation` property is introduced. It is required to determine if the data of an object or linked resource can be directly affiliated to the parent object or if is a completely different data.

This property can have two values: __*parent*__ or __*self*__. Default: __*self*__.

An example of such object is given with `"details"` at the lines 3 to 5 of the below figure. The represented resource gives us the `"id"` and `"title"` of a project along with contextual information, that we discuss in the next subsection. Here, the `"details"` object is used to ease human readability. Thus, all the properties that it contains (only `"title"` here) belong to the project, not the `"details"` object itself.

![Example API response with affiliation example](/img/contextual-information.jpeg)

With links, the case is very similar. Consider a __`Card`__ resource with one analytic: its `creationDate`. Then, this field is moved to an __`Analytic`__ resource. Hence, a link __`Card`__ to __`Analytic`__ is added. Yet, it is required to distinguish this link to some data describing the card from links to the operations available on the card (e.g. its deletion), from links to completely different resources such as the list of all cards.

As a result, we distinguish two kinds of affiliations:
* No affiliation (__*self*__): for inner objects and linked resources, the data that they contain do not describe the parent object; for linked operations: they are performed on another resource than the parent resource.
* Affiliation to the parent (__*parent*__): for inner objects and linked resources, the data that they contain described the parent object (as illustrated in the example earlier); for linked operations: they are performed on the resource that contains the link.

## Hints

Places to find ontologies and terms:
- https://lov.linkeddata.es/dataset/lov/terms
- https://schema.org/
- https://www.hydra-cg.com/spec/latest/core/
