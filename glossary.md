---
layout: default
---

# Glossary

Below is a glossary of terms relevant to this Sinpoia Phase 1 Work Cycle.

## Profile and Resource Templates

Metadata profiles, generally referred to as "Profiles" in the Sinopia 
are JSON documents that specify Sinopia Editor interactions. They  conceptually overlap with shape expressions or application profiles in some core areas; namely:
* they specify in a machine-actionable way the actions of a form for taking in a known data shape or subset of data;
* they do basic data validation (i.e. is the provided value for a key a `string`);
* they add specific user-driven actions, like external data API lookups, controlled values drop-downs or save blocks, for the editor displaying that form.
