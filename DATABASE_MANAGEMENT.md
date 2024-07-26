<!--
SPDX-FileCopyrightText: 2021 Alliander N.V.

SPDX-License-Identifier: CC-BY-4.0
-->

## Database Management

CoMPAS uses a PostgreSQL database.

## Versioning Overview

### Versioning type
For type of versioning, we prefer [Semantic Versioning](https://semver.org/). This to keep versioning simple. For every changeset CoMPAS is going to ask if it's a major, minor or a patch. This way the version will be adjusted according to the user's needs. An example of distinction can be:
- A changeset is Major in case a full XML section is being added.
- A changeset is Minor is a piece of data is adjusted.
- A changeset is a Patch if a typo is fixed.
But this is up to the user.

Saving the version will be done in combination with the History section (tHitem) of the SCL structure. This history section contains multiple history items, so you can create a provenance section. Please checkout the [Provenance](#provenance-overview) section for more information. Key point is: a tHitem contains the following attributes:
- Version
- Revision
- When
- Who
- What
- Why

This creates provenance, and version is one of them. The version attribute will be used for the latest version.

Another solution could be [Branch Based Versioning](https://simon-maxen.medium.com/branch-based-versioning-5ebf6ca2bccb). This way, a configuration file can be 'branched', and can be 'merged' when the user think it's fine. When merging, a newer version number can be added (can be done in combination with semantic versioning).
This in indeed a fancy way of versioning, but it's too complex for our use cases. We don't see users branching a configuration file and saving it for a couple of days, before merging it. Besides, this kind of versioning isn't supported in BaseX out of the box so we have to create it ourselves. When comparing added value to effort, this isn't what we want.

## Database Rights
In a microservice architecture, a microservice's database should be part of the implementation of that service and cannot be accessed directly by other services. This way, the service is loosely coupled and can be developed/scaled/deployed independently.

## Provenance Overview
If the generation of a substation fails for example, we would like to know the provenance of the file.
This way it's easier to get the cause.

### W3 PROV
Provenance is information about entities, activities, and people involved in producing a piece of data or thing, which can be used to form assessments about its quality, reliability or trustworthiness. The PROV Family of Documents defines a model, corresponding serializations and other supporting definitions to enable the inter-operable interchange of provenance information in heterogeneous environments such as the Web. This document provides an overview of this family of documents. (https://www.w3.org/TR/prov-overview/#Abstract)

W3C does have a full standard for extending files with provenance information, in such a way that it's standardized and it enables the interchangeable of provenance information in environments such as, in our case, XML environments. The design of PROV is based on the recommendations of the [Provenance Incubator Group](https://www.w3.org/2005/Incubator/prov/charter).

### W3 PROV-XML
One of the documents of W3 PROV is PROV-XML. This document converts the PROV standard to XML definitions, and is what we want.
PROV-XML has 6 components to use:
- component 1: entities and activities, and the time at which they were created, used, or ended;
- component 2: derivations of entities from others;
- component 3: agents bearing responsibility for entities that were generated and activities that happened;
- component 4: bundles, a mechanism to support provenance of provenance;
- component 5: properties to link entities that refer to a same thing;
- component 6: collections forming a logical structure for its members.

The component we're most interested in, is component 1. And especially the activities.
There is a [Activity complexType](https://www.w3.org/TR/2013/NOTE-prov-xml-20130430/#term-Activity) defined. An Activity in PROV-XML is defined as:

> something that occurs over a period of time and acts upon or with entities; it may include consuming, processing, transforming, modifying, relocating, using, or generating entities.
> 
This is how we can interpret a edit on a XML file: as an activity.

An activity has a start- and endtime. In our case, that can be the period from opening the file to saving the file. It has a type or activity, which will most of the time be an Edit.

And a set of extra attributes can be added. In the added example, an hostname is added. In our case that's not very handy, because if CoMPAS is ran locally, the hostname doesn't say that much. What makes the most sense at this point is adding a User attribute which is linked to the future oAuth 2.0 authorisation/authentication module.

Example of added PROV section. The UserID attribute is a simplified attribute for identifying the entity doing the activity:
```xml
<prov:document
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns:prov="http://www.w3.org/ns/prov#"
    xmlns:ex="http://example.com/ns/ex#">

  <prov:activity prov:id="ex:a1">
    <prov:startTime>2021-03-16T16:05:00</prov:startTime>
    <prov:endTime>2021-03-16T16:08:00</prov:endTime>
    <prov:type xsi:type="xsd:QName">ex:edit</prov:type>
    <ex:userId>123456</ex:userId>
  </prov:activity>

</prov:document>
```

### IEC-61850-6 hItem (History)
A second option is the History section of a SCL file.
This section is a standard section of a SCL and contains the following fields:
- version
- revision
- when
- who
- what
- why

As you can see, this can be done in combination with [versioning](#versioning-overview).
This is enough for the basic usage that we need. For every version (every edit for example), a new hItem will be added to the SCL.
This way, we don't need to extend the SCL by default. We can just use the standard.

### Final Thoughts
The best way is to use the History section of a SCL file.
It's flexible enough for our basic needs, so we got the version, the when, the who, etc.

In the future it's possible that we need to need something extra, for example an origin CIM file from conversion.
For this we can use the W3C PROV-XML section.
In this case, we can extend the History item with so-called 'private' data, which will be the W3C PROV-XML data.
For more information about the private elements in the SCL structure, take a look at chapter 8.3.6 of the IEC-61850-6 standard.

### Sources
https://www.w3.org/TR/prov-xml
