---
title: Binary | DSTU 2 API
---

# Binary

* TOC
{:toc}

## Retrieve by id

List an individual Binary by its id:

    GET /Binary/:id

_Implementation Notes - Binary for [DiagnosticReport]_

* Requires both Binary.read and DiagnosticReport.read OAuth2 scopes.
* Accepts `html`, `text/html` or `application/xhtml+xml` mime types, in addition to JSON

### Response

Retrieving the Binary resource with the JSON mime type

    GET: [...]/Binary/TR-5927259
    Accept: application/json+fhir

<%= headers 200, 'Content-Type': 'application/json+fhir' %>
<%= json(:dstu2_binary_json_entry) %>

Retrieving the Binary resource with its native mime type

    GET: [...]/Binary/TR-5927259
    Accept: text/html

<%= headers 200, 'Content-Type': 'text/html' %>
<%= html(:dstu2_binary_html) %>

## Operation: autogen-ccd-if

Generates the Continuity of Care Document (CCD) as a Binary for the supplied query parameters: 

    GET /Binary/$autogen-ccd-if?:parameters

_Implementation Notes_

* Requires both Binary.read and DocumentReference.read OAuth2 scopes.
* Accepts `application/xml` mime type, in addition to `application/json+fhir`

### Parameters

 Name     | Required? | Type          | Description
----------|-----------|---------------|-------------------------------------------------
`patient` | Yes       | [`reference`] | A reference to the patient that is the subject of the CCD. Example: `14067892`
`start`   | No        | [`date`]      | The start of the date range for which the CCD is to be generated. If not provided, then all records upto the end or current date are considered. Example: `2014-09-24T12:00:00.000Z`
`end`     | No        | [`date`]      | The end of the date range for which the CCD is to be generated. If not provided, then all records upto the current date are considered. Example: `2016-09-24T12:00:00.000Z`

Notes:   

- The `start` and `end` parameters:  
  - must be a valid [dateTime] with a time and prefixed with either `eq` or nothing.

### Response

Retrieving the resource with the JSON mime type

    GET: [...]/Binary/$autogen-ccd-if?patient=1316024
    Accept: application/json+fhir

<%= headers 200, 'Content-Type': 'application/json+fhir' %>
<%= json(:dstu2_binary_ccd_json_entry) %>

Retrieving the Binary resource with its native mime type

    GET: [...]/Binary/$autogen-ccd-if?patient=1316024
    Accept: application/xml

<%= headers 200, 'Content-Type': 'application/xml' %>
<%= html(:dstu2_binary_ccd_xml) %>

[DiagnosticReport]: ../diagnostic-report
[`reference`]: http://hl7.org/fhir/DSTU2/search.html#reference
[`date`]: http://hl7.org/fhir/DSTU2/search.html#date
[dateTime]: http://hl7.org/fhir/DSTU2/datatypes.html#dateTime
