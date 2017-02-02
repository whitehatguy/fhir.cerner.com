---
title: MedicationStatement | DSTU 2 API
---

# MedicationStatement

* TOC
{:toc}

## Overview

A record of a medication that is being consumed by a patient. A MedicationStatement may indicate that the patient may be taking the medication now, or has taken the medication in the past or will be taking the medication in the future. The source of this information can be the patient, significant other (such as a family member or spouse), or a clinician.

## Terminology Bindings

<%= terminology_table(:medication_statement, :dstu2) %>

### Contained Medication Bindings

<%= terminology_table(:contained_medication, :dstu2) %>

### Contained Practitioner Bindings

<%= terminology_table(:medication_statement_contained_practitioner, :dstu2) %>

## Extensions

* [Patient friendly displays]

## Search

Search for MedicationStatements that meet supplied query parameters:

    GET /MedicationStatement?:parameters

_Implementation Notes_

* [MedicationStatement.informationSource] may be a reference to a contained Practitioner or RelatedPerson.
* [MedicationStatement.medication] may be a reference to a contained Medication.

### Parameters


 Name           | Required? | Type          | Description
----------------|-----------|---------------|-----------------------------------------------------------------------------------------------
`patient`       | Y         | [`reference`] | The identifier of a patient to list statements for. Example: `12345`
`status`        | N         | [`token`]     | The status of the medication statement, may be a list separated by commas.  Example: `active,completed`
`effectivedate` | N         | [`date`]      | The date-time which should fall within the period the patient was taking (or not taking) the medication. Must be prefixed by 'ge'  Example: `ge2015-01-01`
[`_count`]      | N         | [`number`]    | The maximum number of results to return. Defaults to `50`.

### Headers

To successfully GET a ResourceExample, the following headers must be provided. Authorization must be provided if accessing the closed endpoint.

        Accept-Type: application/json+fhir
        Authorization: <OAuth2 Bearer Token>

### Example

#### Request

    GET https://fhir-open.sandboxcerner.com/dstu2/d075cf8b-3261-481d-97e5-ba6c48d3b41f/MedicationStatement?patient=4342008&_count=50

#### Response
<%= headers 200 %>
<%= json(:dstu2_resource_example_bundle) %>

### Errors

The following [`errors`] are possible.

## Retrieve by id

List an individual MedicationStatement by its id:

    GET /MedicationStatement/:id

_Implementation Notes_

* Add any retrieve by id implementation notes here.

### Headers

[//]: # (Required. Add all the required headers for the request.)

To successfully GET a ResourceExample, the following headers must be provided. Authorization must be provided if accessing the closed endpoint.

        Accept-Type: application/json+fhir
        Authorization: <OAuth2 Bearer Token>

### Example

[//]: # (Required section. Please populate the fields below with an example.)

#### Request

    GET https://fhir-open.sandboxcerner.com/dstu2/d075cf8b-3261-481d-97e5-ba6c48d3b41f/MedicationStatement/21369961

#### Response

<%= headers 200 %>
<%= json(:dstu2_medication_statement_entry) %>

### Errors

The following [`errors`] are possible.

## Create

Create a new MedicationStatement.

    POST /MedicationStatement

_Implementation Notes_

* [MedicationStatement.status] must be set to `active`.
* [MedicationStatement.wasNotTaken] set to `true` is not supported.
* If [MedicationStatement.medication] is a reference, it must refer to a contained Medication with the code field populated and at most one product.ingredient.

### Headers

To successfully POST a MedicationStatement, the following headers must be provided. MedicationStatement creation is supported from the closed endpoint only.

    Content-Type: application/json+fhir
    Authorization: <OAuth2 Bearer Token>

### Body Fields

<%= definition_table(:medication_statement, :create, :dstu2) %>

#### Contained Medication Body Fields

<%= definition_table(:contained_medication, :create, :dstu2) %>

### Example

#### Request

    POST https://fhir-ehr.sandboxcerner.com/dstu2/d075cf8b-3261-481d-97e5-ba6c48d3b41f/MedicationStatement/

#### Body

<%= json(:dstu2_medication_statement_create) %>

#### Response

<%= headers 201 %>
<pre class="terminal">
    #TODO: Replace with headers from successful create to your resource.
    Connection → Keep-Alive
    Content-Encoding → gzip
    Content-Length → 20
    Content-Type → text/html; charset=UTF-8
    Date → Wed, 13 Jan 2016 21:45:47 GMT
    Keep-Alive → timeout=15, max=100
    Last-Modified → Tue, 15 Dec 2015 19:13:20 GMT
    Status → 201 Created
    access-control-allow-methods → DELETE, GET, POST, PUT, OPTIONS, HEAD
    access-control-allow-origin → *
    access-control-expose-headers → ETag, Content-Location, Location, X-Request-Id, WWW-Authenticate, Date
    access-control-max-age → 0
    cache-control → no-cache
    etag → W/"0"
    location → https://fhir-ehr.sandboxcerner.com/dstu2/d075cf8b-3261-481d-97e5-ba6c48d3b41f/MedicationStatement/20465903
    server-response-time → 1260.984596
    strict-transport-security → max-age=631152000
    vary → Origin,User-Agent,Accept-Encoding
    x-content-type-options → nosniff
    x-frame-options → SAMEORIGIN
    x-request-id → 682c633c-b20f-4f6f-8fae-c58b3aeffe04
    x-runtime → 1.260940
    x-xss-protection → 1; mode=block
</pre>

The `ETag` response header indicates the current `If-Match` version to use on subsequent updates.

### Errors

The following [`errors`] are possible.

## Update

Update a MedicationStatement.

    PUT /MedicationStatement

_Implementation Notes_

* The only supported change is to update the [MedicationStatement.status] to `completed`.

### Headers

To successfully PUT a MedicationStatement, the following headers must be provided. MedicationStatement updates are supported from the closed endpoint only.

    Content-Type: application/json+fhir
    Authorization: <OAuth2 Bearer Token>
    If-Match: W/"<Current version of the MedicationStatement resource>"

### Body fields

<%= definition_table(:medication_statement, :update, :dstu2) %>

### Example

#### Request

    PUT https://fhir-ehr.sandboxcerner.com/dstu2/d075cf8b-3261-481d-97e5-ba6c48d3b41f/MedicationStatement/

#### Body

<%= json(:dstu2_medication_statement_update) %>

### Response

<%= headers 200 %>
<pre class="terminal">
    #TODO: Replace with headers from a successful update to a ResourceExample
    Connection → Keep-Alive
    Content-Encoding → gzip
    Content-Length → 20
    Content-Type → text/html; charset=UTF-8
    Date → Wed, 13 Jan 2016 21:50:53 GMT
    Keep-Alive → timeout=15, max=100
    Last-Modified → Tue, 15 Dec 2015 19:13:20 GMT
    Status → 200 OK
    access-control-allow-methods → DELETE, GET, POST, PUT, OPTIONS, HEAD
    access-control-allow-origin → *
    access-control-expose-headers → ETag, Content-Location, Location, X-Request-Id, WWW-Authenticate, Date
    access-control-max-age → 0
    cache-control → no-cache
    etag → W/"1"
    server-response-time → 653.7616069999999
    strict-transport-security → max-age=631152000
    vary → Origin,User-Agent,Accept-Encoding
    x-content-type-options → nosniff
    x-frame-options → SAMEORIGIN
    x-request-id → 9dba8326-899a-406f-a125-3fc3d6605dad
    x-runtime → 0.653722
    x-xss-protection → 1; mode=block
</pre>

The `ETag` response header indicates the current `If-Match` version to use on subsequent updates.

### Errors

The following [`errors`] are possible.

[`reference`]: http://hl7.org/fhir/DSTU2/search.html#reference
[`token`]: http://hl7.org/fhir/DSTU2/search.html#token
[`date`]: http://hl7.org/fhir/DSTU2/search.html#date
[`_count`]: http://hl7.org/fhir/DSTU2/search.html#count
[`number`]: http://hl7.org/fhir/DSTU2/search.html#number
[MedicationStatement.informationSource]: http://hl7.org/fhir/DSTU2/medicationstatement-definitions.html#MedicationStatement.informationSource
[MedicationStatement.medication]: http://hl7.org/fhir/DSTU2/medicationstatement-definitions.html#MedicationStatement.medication_x_
[MedicationStatement.status]: http://hl7.org/fhir/DSTU2/medicationstatement-definitions.html#MedicationStatement.status
[MedicationStatement.wasNotTaken]: http://hl7.org/fhir/DSTU2/medicationstatement-definitions.html#MedicationStatement.wasNotTaken
