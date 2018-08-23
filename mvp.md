---
layout: default
---

Work in progress.


## In Scope:
* Baseline profile editor that returns profile to user as JSON (we do not store or automatically load profiles)
* Editor of RDF data driven by a specified profile
* Ability to save RDF data plus administrative metadata (provenance, timestamp, etc.) to sandbox persistence
* Ability to retrieve, update, and add (CRUD) RDF about an entity within the sandbox
* Basic, internal search of entities (label, title, author, entity type, person / institution who described, keyword search)
* Ability to bulk load & retrieve RDF
* Ability to query programmatically entities (scoping of queries is still uncertain; known use case is all data contributed by an institution or consortia)
* Basic, data-type-driven validation

## Not in Scope:
* Conversion to RDF
* Reconciliation (beyond look-ups supported by QA)
* Automated data syncing of sandbox data with any external source
* External discovery layer (i.e. a public search interface)
* Reasoning engines, inferencing, or entailment
* Complex semantic validation

## Uncertain
* SPARQL query endpoint
* SPARQL period
* Share VDE connections
