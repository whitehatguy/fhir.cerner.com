---
title: Person | DSTU 2 API
---

# Person

* TOC
{:toc}

## Overview

The Person resource identifies an individual outside of a specific health care context providing a mechanism to link person resources across different facilities or organizations.

The following fields are returned if valued:

* [Person id](http://hl7.org/fhir/dstu2/resource-definitions.html#Resource.id){:target="_blank"}
* [Identifier (Cerner alias Federated Person Principal)](http://hl7.org/fhir/DSTU2/person-definitions.html#Person.identifier){:target="_blank"}
* [Name](http://hl7.org/fhir/DSTU2/person-definitions.html#Person.name){:target="_blank"}
* [Telecom](http://hl7.org/fhir/DSTU2/person-definitions.html#Person.telecom){:target="_blank"}
* [Gender](http://hl7.org/fhir/DSTU2/person-definitions.html#Person.gender){:target="_blank"}
* [Date of birth](http://hl7.org/fhir/DSTU2/person-definitions.html#Person.birthDate){:target="_blank"}
* [Address](http://hl7.org/fhir/DSTU2/person-definitions.html#Person.address){:target="_blank"}
* [Active](http://hl7.org/fhir/DSTU2/person-definitions.html#Person.active){:target="_blank"}

## Terminology Bindings

<%= terminology_table(:person, :dstu2) %>

## Search

Search for Persons that meet supplied query parameters:

    GET /Person?:parameters

### Authorization Types

<%= authorization_types(practitioner: true, patient: true, system: true) %>

### Parameters

 Name         | Required?                                         | Type       | Description
--------------|---------------------------------------------------|------------|------------------------------------------------------------------------------------
 `_id`        | No, if populated all other parameters are ignored | [`token`]  | The logical resource id associated with the resource.
 `identifier` | Yes, or `_id`                                     | [`token`]  | The person identifier.  Example: `urn:oid:2.16.840.1.113883.3.13.6|01022228`

Notes:

- `identifier` value must include both a system and a code. Example: `identifier=urn:oid:2.16.840.1.113883.3.13.6|URN:CERNER:...:PI98N2FK5TN`

### Headers

 <%= headers %>

### Example

#### Request

    GET https://fhir-open.sandboxcerner.com/dstu2/0b8a0111-e8e6-4c26-a91c-5069cbc6b1ca/Person?identifier=urn%3Aoid%3A2.16.840.1.113883.3.13.6%7Curn%3Acerner%3Aidentity-federation%3Arealm%3A687f29dd-69dd-4de5-acb1-fd8a2241ef3a%3Aprincipal%3AEC4Ax54P8GI

#### Response

<%= headers status: 200 %>
<%= json(:dstu2_person_bundle) %>

### Errors

The common [errors] may be returned.

## Retrieve by id

List an individual Person by its id:

    GET /Person/:id

### Authorization Types

<%= authorization_types(practitioner: true, patient: true, system: true) %>

### Headers

<%= headers %>

### Example

#### Request

    GET https://fhir-open.sandboxcerner.com/dstu2/0b8a0111-e8e6-4c26-a91c-5069cbc6b1ca/Person/4342009

#### Response

<%= headers status: 200 %>
<%= json(:dstu2_person_entry) %>

### Errors

The common [errors] may be returned.

### Person Combines Example

Cerner Millennium supports the ability to logically merge a person record into another person record when both records are describing the same person. This is known
as a "person combine". If necessary, this merging can later be undone by performing a "person uncombine". When the requested person record has been combined into another
record, an inactive Person entry will be returned which has a link to the current Person entry. Entries for combined patients will only be returned when retrieving
the entries directly by id. They will not be returned when searching with other parameters.

The ability to perform person combine or uncombine operations is not available through the Cerner Ignite platform.

#### Request

    GET https://fhir-open.sandboxcerner.com/dstu2/0b8a0111-e8e6-4c26-a91c-5069cbc6b1ca/Person/4860007

#### Response

<%= headers status: 200 %>
<%= json(:dstu2_combined_person_entry) %>

### Errors

The common [errors] may be returned.

[`token`]: http://hl7.org/fhir/DSTU2/search.html#token
[errors]: ../../#client-errors
