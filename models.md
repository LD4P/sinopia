---
layout: default
---

# Sinopia Data Models & Specifications

## Groups

This represents a group of people who decide to operate within the same data namespace. Members of the group have full CRUD privileges of all entities (or metadata resource[s]) within that's groups namespace. These are equated with `ldp:Container` in the Sinopia Server API, and equated with institutions (e.g. Stanford, Cornell) or consortia (e.g. PCC) in the user requirements.

*NB: There are ways to handle having some resources in multiple groups technically, but it is a stretch goal for this work cycle - i.e., we presume that people will edit resources within 1 group at a time.*

* label (string)
* (key, required) namespace or relative identifier within Sinopia (string, controlled values)
* sameAs (group, URI if helpful)
* ... other analytics or metadata?

This is serialized as JSON-LD.

## Descriptive Resource(s)

This represents any entities that are specifically metadata resources created directly or indirectly by users within a group editing within a profile-driven editor interface (singleton GUI or API / bulk load). These are equated with `ldp:RDFSource` in the Sinopia Server API.

The majority of the key values here will be defined by the profile; and the `@context` node for JSON-LD (that maps keys to namespaced predicates) is expected to be an embedded graph value that contains the mappings from the profile(s) used to edit the resource. No resource is expected to be edited by a single profile; in other words, each resource can be updated or added to via multiple profiles.

* label (string)
* (key, required) relative identifier within Sinopia (UUID)
* group / namespace within Sinopia
* sameAs (group)
* ... other analytics or metadata?

This is serialized as JSON-LD.

## Administrative Resources

This represents any entities that are additive administrative metadata resources created indirectly by users (via our system & CRUD API). These are equated with `ldp:Resource` in the Sinopia Server API.

The heart of this is fulfilling user requirements around:
1. tracking who changed an entity, when, and how (to the statement level);
2. what profiles were used to describe an entity (possibly to the statement level);
3. what institutions have what "entities" (to the resource level);
4. and other administrative data as achievable and requested.

* label (string)
* (key, required) relative identifier within Sinopia (UUID)
* group / namespace within Sinopia
* ... other administrative data as determined.

This is serialized as JSON-LD, if appropriate.

## Authorization Resources

This represents authorization resources - i.e. what users can perform what actions (CRUD) to what resources (any of the ones listed here). These are equated with `ldp:Resource` in the Sinopia Server API. These resources align with the Web ACL model; if the user is authenticated, we use that as the agent key to check against; if not, it is considered 'public' agent.

* label (string)
* (key, required) relative identifier within Sinopia (UUID)
* agent (user, group, or public Sinopia URI)
* mode (action URI - generally, CRUD actions available via HTTP)
* access to (group, possibly resource)
* ... other authorization data as determined.

This is serialized as JSON-LD, if appropriate.

## Users

This represents Users - i.e. what users can perform what actions (CRUD) to what resources (any of the ones listed here). These are equated with `ldp:Resource` in the Sinopia Server API. These resources align with the Web ACL model; if the user is authenticated, we use that as the agent key to check against; if not, it is considered 'public' agent.

* label (string)
* (key, required) relative identifier within Sinopia (UUID)
* group (URIs for groups the User is a member of, could be multiple)
* institution (string?)
* email (string / email; possibly used for login)
* Sinopia site password (encrypted string / hash)
* login name (string; if not email)
* authorization (administrator, user; for web application only?)
* ... other user data as determined.

This is serialized as JSON, if appropriate. It is probably stored in the end-user facing application,

## Profile


This is serialized as JSON.
