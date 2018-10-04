---
layout: default
---

# Sinopia Functional Requirements & Constraints

Sinopia user requirements are captured and prioritized here: https://github.com/ld4p/sinopia/issues. Those GitHub repository issues should be considered the canonical source for Sinopia Phase 1 Work Cycle user requirements. A project board view (mixed with technical and other tickets) is available here: https://waffle.io/LD4P/sinopia.

Below is a brief overview of derived functional requirements to help contextualize our Sinopia Phase 1 Work Cycle [MVP (minimum viable product)](/sinopia/mvp) and [acceptance criteria](/sinopia/acceptance-tests).

## Metadata Profiles Creation & Usage

Metadata profiles, generally referred to as "Profiles" in the Sinopia project, are JSON documents that specify Sinopia Editor interactions vis-a-vis a generated form GUI for entering and interacting with entity data to be saved within Sinopia. For Sinopia Phase 1, we have the following functional requirements & constraints:

* _Constraint:_ Keep development on Profile Editor to minimum.
* _Constraint:_ Limit Profile Editor to only respond with the Profile's JSON to a user for them to save, not save in the Profile system.
* _Constraint:_ Profile Editor should mostly work with pre-existing Profiles (i.e. only perform minor updates that change the Profile JSON specification for backwards compatibility).
* _Requirement:_ Ability to create new and update existing Profiles.
* _Requirement:_ End-user (non-developer) can perform the above actions in a user-friendly, web-based GUI (i.e. the Profile Editor).
* _Requirement:_ The Profile needs to map each generated form field to a:
  1. data input type (i.e. string, URI, integer, hash);
  2. subject resource variable the specific form field input should be asserted against (i.e. what the entered data is describing);
  3. predicate URI the form field represents.
* _Requirement:_ The Profile specification should support:
  * the addition of help text or descriptions for each form field specified.
  * the addition of Profile metadata (e.g. schema and/or content standard adherence; who created the profile; when the profile was created or updated; etc.).
  * translation of entered data to RDF should support translation to classes and predicates from any RDF-based ontology or vocabulary.
  * a default subject resource variable for the Profile or a Profile form field block (delineated group of form fields).
  * the ability to describe multiple subject resource variables across multiple form fields.
  * the ability to specify contextual nodes (including blank nodes) for some form field values.
  * indication if a form field is required and if a form field is repeatable.
  * an optional form field default value.
  * a form field being limited to an external vocabulary (pulled in via Lookup).
  * a form field being limited to controlled values from a provided list of possibly values.
* _Requirement:_ The Profile Editor should support reordering fields and groups of fields within a Profile (and in the derived form view).
* _Request:_ Specify that the allowed values for a field depend on the value entered in another field when metadata is created
* _Request:_ The Profile should support Group related fields into a section and give the section a name
* _Request:_ The Profile Editor should allow importing an existing Profile, then copying those values to an entirely new Profile, as a template-based starting point for creating a derived Profile.
* _Request:_ The Profile should support specification of filtering external lookups (i.e. for a given Lookup endpoint, further subdivide the possibly responses).
* _Request:_ Profiles should be specified as JSON-LD, JSON Schema, and/or ShEx instead of JSON.

## Sinopia Entity Data CRUD (Create, Read, Update, Delete) via Editor Front-end

With a Profile in hand, a user would load that Profile into the Sinopia Editor to then create, update, or possibly delete metadata about Sinopia entities. For Sinopia Phase 1, we have the following functional requirements & constraints:

* _Constraint:_ Development of this editing system must start with the LCNetDev BFE codebase.
* _Constraint:_ The editing system's GUI or front-end application needs to be web-based and served via a web browser.
* _Constraint:_ The editing system must support some sort of basic authentication at the user level with open registration & administrator review.
* _Constraint:_ This editing system should follow DLSS emerging practices around Javascript codebases & general DevOps practices.
* _Constraint:_ The editing system must support some sort of basic but less well defined authorization via group pattern.
* _Constraint:_ The editing system must expose persisted data in a form and method that makes it easily reuseable in later downstream systems (like a discovery layer or a ETL pipeline).
* _Requirement:_ Create and update entities (whatever types they may be, focus on "Instances") in Sinopia via a Form generated according to a Metadata Profile and data persisted in Sinopia system.
* _Constraint:_ The editing system must persist user-entered data and system-generated metadata for lossless retrieval and exposure.
* _Requirement:_ Link entities in Sinopia to external entities (whatever type they may be, focus on "Works") via URI entry.
* _Constraint:_ For external entities linked to within Sinopia, store not only the URI but also the `rdfs:label`.
* _Requirement:_ The Sinopia Editor form must allow Users to enter & save UNICODE characters, non-Roman scripts, non-Latin scripts, diacritics, and right-to-left scripts. This data must be persisted in Sinopia and exposed later without corruption.
* _Requirement:_ The Sinopia Editor form must notify the User when they try to save data missing required fields (as defined by the selected Metadata Profile).
* _Requirement:_ The Sinopia Editor form must validate User-entered data according to the selected Metadata Profile at time of entry at the field-level; if invalid, there should be a clear message to the User about what is invalid.
* _Requirement:_ 'Copy': Ability to import existing (external or internal) data from already cataloged resources into Sinopia Editor Form & use that data as base for creating a new Sinopia resource.
* _Requirement:_ 'Lookup': Sinopia Editor Form must allow type-ahead and in-form contextual lookups on internal and external data for selection of an entity to link to within the form.
* _Constraint:_ The Lookup work must use Cornell's Questioning Authority (QA) work as it's primary external data lookup API.
* _Requirement:_ 'Lookup': Sinopia Editor Form should allow in-form contextual lookups that provide enough contextual information about the look-up results that users can select the correct entity.
* _Requirement:_ The Sinopia Editor Form must allow limiting of Lookups to specified vocabularies (specified in the Metadata Profile) if the specified vocabulary is supported by itself in QA.
* _Requirement:_ If Lookup fails for the User (i.e. the desired entity cannot be found), the User should be able to create the desired entity using an appropriate Metadata Profile within the Sinopia Editor and persist that entity to Sinopia.
* _Requirement:_ 'Clone': Ability to import existing (external or internal) data from already cataloged resources into Sinopia Editor Form & use that data as base for creating an alternate Sinopia resource that has a default `skos:sameAs` reference to the original entity but allows the user to edit that entity's metadata.
* _Constraint:_ Any entities 'imported' (via Copy or Clone, via GUI form or programmatically) into Sinopia becomes a Sinopia entity (i.e. has a namespace based on Sinopia domain and the appropriate authorization group). This does not apply to *pointers to* external URIs (i.e. when a URI is the object of a statement).
* _Request:_ Allow look-ups based on different external entity matching points (i.e. fielded search). This requires work on the QA side.
* _Request:_ The Sinopia Editor Form should support keyboard-based navigation through a form in addition to mouse-driven navigation.
* _Request:_ The Sinopia Editor Form should allow collapsable blocks within the Form, with those blocks specified via the Metadata Profile.
* _Request:_ The Sinopia Editor should allow the ability to save Form Metadata as a draft (i.e. not persisted to Sinopia Server).
* _Request:_ The Sinopia Editor should allow mapping multiple values retrieved via a Lookup to multiple fields within the Editor Form. This requires work on the QA side.

## View, Query & Export Metadata

Upon data being created in Sinopia, or when creating new data that should be linekd externally, there are a number of data exposure requirements. The functional requirements around data exposure (and, to a lesser degree, bulk data import) are listed below:

* _Requirement:_ The Sinopia System must have programmatic interfaces for singleton & bulk load and retrieval of Sinopia entities. This is part of a requirement to make Sinopia an easily integratabtle component in larger data systems.
* _Request:_ Sinopia entities should be dereferenceable, and the data should be viewable in multiple RDF serializations.
* _Requirement:_ Sinopia entities must be searchable via simple keyword search and via limited faceted search by Users looking to create, update, clone, or link to Sinopia resources. This includes both search UIs and Sinopia Editor form lookups.
* _Requirement:_ External entities in QA-supported vocabularies must be searchable via simple keyword search by Users looking to create, update, clone, or link to these resources within Sinopia. This includes both search UIs and Sinopia Editor form lookups.
* _Constraint:_ Sinopia is not building a public discovery interface for Sinopia data.
* Query
Administrative Metadata Facets
Basic BIBFRAME Metadata Facets
Keyword Search across Metadata

## Sinopia Server

Underlying all of the above is a Sinopia Server that manages & persists Sinopia resources. The following are functional requirements derived or inferred based on the above:

* _Requirement:_ CRUD entity (singleton and bulk / graph) within the appropriate authorization group
  * _Proposal:_ Create JSON-LD Graph for resource(s) defined via the Metadata Profile to load into a certain group’s graph with skolemization of any blank nodes from the Sinopia Editor system to persistence.
* _Requirement:_ Atomic & change-aware CRUD of Entity(s) within appropriate Group
  * _Requirement:_ Server must handle or propose pattern to clients for keeping untouched statements about an entity while other statements are added or updated about that same entity (i.e. `GET` before `POST`).
  * _Requirement:_ Server must notify clients when relevant entities have changed between Server requests if the second request is an update (i.e. `PUT`, `POST`, `PATCH`, `DELETE`, etc.).
* _Requirement:_ The server must persist, and should generate, administrative metadata about entities and entity data created within the client. Administrative metadata includes but is not limited to: Who, When, Actions, Entities changed (to statement level), Group, Profile(s) used to create statements about resource.
* _Proposal:_ Export of Sinopia data & metadata should allow (and optimize for) the following:
   * Export all Entities from Group (data and metadata).
   * Export all Entities from the Sinopia server (data and metadata).
* _Proposal:_ The Sinopia Server manages entity URI minting for Sinopia entities, with the Sinopia domain, and an authorization group path, and a relative identifier for the entity as the file path of the URI.
