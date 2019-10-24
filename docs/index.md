---
title: "edi3 JSON-LD NDR 1.0 Specification"
specID: "json-ld-ndr/1"
status: "![raw](http://rfc.unprotocols.org/spec:2/COSS/raw.svg)"
editors: "[Nis Jespersen](mailto:nis.jespersen@maerskgtd.com)"
contributors: "[Steven Capell](mailto:steve.capell@gmail.com)"
---

## Introduction


## Linked Data Example
This sections illustrates an example of how data is linked via 

### API Payload
The below is a data object which could be passed in the request or reply of an API call. 

```
{
	"@context": "http://edi3.org/cefact-bsp.jsonld",
	"consignment": {
		"identification": "https://www.maersk.com/tracking/#tracking/123456789",
		"includedConsignmentItem": [
			{
				"consignmentItem": {
					"information": "Mangos and bananas",
					"grossWeight": {
						"Value": "12000",
						"Unit": "Kgs"
					}
				}
			}
		],
		"utilizedTransportEquipment": [
			{
				"transportEquipment": {
					"identification": "https://app.bic-boxtech.org/containers?search=MSKU0134962",
					"affixedSeal": {
						"identification": "54234398"
					}
				}
			}
		]
	}
}
```

This JSON object specifies a Consignment and its ConsignmentItem and TransportEquipment. The Consignment is identified by a bookingnumber via linkage to Maersk, who in the role of carrier has issued the booking number. The TransportEquipment number is governed by BIC, available through their boxtech API. 

It also defines a context hosted under edi3.org. The `@context` is json-ld's way of linking payload elements to defined semantics. 

### Semantic Context
The json-ld context file defines the semantics of the elements of the payload json file. Below is an example of how the `cefact-bsp.jsonld` might look. 

```
{
	"@context": {
		"consignment": { 
			"@id": "https://edi3.org/specs/edi3-transport/develop/vocab/Consignment",  
			"@type": "@id" 
		},
		"consignmentItem": "https://edi3.org/specs/edi3-transport/develop/vocab/ConsignmentItem",
		"transportEquipment": {
			"@id": "https://edi3.org/specs/edi3-transport/develop/vocab/TransportEquipment", 
			"@type": "@id" 
		}
	}
}
```
What this means is that the semantic meaning of `consignment` in the payload file is based on the definition available at `http://edi3.org/contexts/Consignment`. It also indicates that the value of `Identification` is to be considered the identifer of the Consignment resource (TODO: link @id to Identifier attribute).

Note that the `@context` can be defined elsewhere too. In fact, it might fit better to have contexts specific to particular API use cases. Also, the context can be defined within the payload json data. 

### Semantic Referencing
The most important role of edi3.org in supporting linked data is to govern and expose the semantics, to be referenced by such contexts. This is documentation which can be generated straight out of the SCRDM, for example:

`GET edi3.org/contexts/Consignment` would return:

| **Consignment** | A separately identifiable collection of goods items to be transported or available to be transported from one consignor to one consignee via one or more modes of transport where each consignment is the subject of one single transport contract. | |
| -------- | --------- | -------- |
| *ConsignmentItem* | A consignment item included in this consignment of goods. | `edi3.org/contexts/ConsignmentItem` |
| *TransportEquipment* | A number of pieces of transport equipment, such as containers or similar unit load devices, in this consignment.|`edi3.org/contexts/TransportEquipment` |
| Identification | A unique identifier for this piece of the consignment. | |

`GET edi3.org/contexts/TransportEquipment` would return:

| **TransportEquipment** | A piece of equipment used to hold, protect or secure cargo for transportation purposes. | |
| -------- | --------- | -------- |
| Identification | A unique identifier for this piece of transport equipment. | |
| *Contained* | A consignment contained in this piece of transport equipment. | `edi3.org/contexts/Consignment` |



## Status



## Glossary

Phrase | Definition
------------ | -------------
|

This service depends on - TBA.

The TBA specification depends on this document. Note, TBA.
 
## Licence

All material published on edi3.org including all parts of this specification are the intellectual property of the UN as per the [UN/CEFACT IPR Policy](https://www.unece.org/fileadmin/DAM/cefact/cf_plenary/plenary12/ECE_TRADE_C_CEFACT_2010_20_Rev2E_UpdatedIPRpolicy.pdf).

This Specification is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 3 of the License, or (at your option) any later version. See http://www.gnu.org/licenses.
 
## Change Process

 This document is governed by the [2/COSS](http://rfc.unprotocols.org/spec:2/COSS/) (COSS).

## Language

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" 
in this document are to be interpreted as described in RFC 2119.

# Billing Process



## State Lifecycle


 
# Related Material

 * 
 * 