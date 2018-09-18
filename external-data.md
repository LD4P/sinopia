---
layout: default
---

# Sinopia <=> External Data Expectations

## External Data API Expectations

### Configuration & Context
* For all of the below, can "select" single authority source, subset of authority sources, or all available authority sources for single GET request.
* Authentication & Authorization is open question.
* Rate limiting and other throughput limits is open question.

### GET => **Fetch**:
* *In* (payload or param): URI
* *200 Out* (payload, preference JSON): All RDF statements with URI as subject in External Store; date & context of statements?

### GET => **Lookup** (Type-ahead *Query*):
* *In* (payload or param): String
* *200 Out* (payload, preference JSON): Array of URIs, Match Score, Labels, Contextual Info (Type);

### GET => **Browse** (Browse *Query*):
* *In* (payload or param): Field + String
* *200 Out* (payload, preference JSON): Array of URIs, Match Score, Labels, Contextual Info (Type);

### GET => **Search** (Multi-field search *Query*):
* *In* (payload or param): Array of Fields + Strings
* *200 Out* (payload, preference JSON): Array of URIs, Match Score, Labels, Contextual Info (Type);

### Error responses
To be written up.

## Sinopia Search Lookup Interactions (Proposed)

### Search for available data => Search Query / Browse
**Sinopia Search Client:**
  1. If needed, break apart API calls by source.
  2. Call API(s) for **Browse** with search string.
  3. Use **Browse** default data to break apart API(s) responses for display of responses.
  4. Follow Selection responses below

### Select to View
  1. User selects "see more" for a given result.
  2. Call API(s) for **Fetch** or to dereference for the selected value's URI from **Browse** results.
  3. Display RDF in module.

### Select to Edit
  1. User selects "edit" for a given result.
  2. Check Permissions to Edit a resource (if internal, if in their graph).
  3. If true: Ask user to select Profile & following steps. If false: say they cannot edit, ask if they want to clone.
  4. Call API(s) for **Fetch** or to dereference for the selected value's URI from **Browse** results.
  5. Map RDF to selected Profile.
  6. Present User the Editor with mapped data pre-populated for the existing resource.

### Select to Clone
  1. User selects "clone" for a given result.
  2. Check Permissions to Clone a resource (if they have a graph that can work within).
  3. If true: Ask user to select Profile & following steps. If false: say they need a graph to work within.
  4. Call API(s) for **Fetch** or to dereference for the selected value's URI from **Browse** results.
  5. Map RDF to selected Profile.
  6. Present User the Editor with mapped data pre-populated for a new resource(s), with sameAs links to **Fetch** URI.

NB: The above for **Clone** and **Edit** presumes one resource (one URI) populated into a field to edit; it does not handle recursion or graph traversal for editing multiple resources at this time.


## Sinopia Editor Lookup Interactions (Proposed)

### Link to “External” URI via Type-ahead from Single Form Field to Single Field
**Sinopia Lookup Client:**
  1. Configuration management (auth, API settings).
  2. Call API for **Lookup** with form field type-ahead string.
  3. Use **Lookup** default response data for URI, label, type?
  4. Save selected & mapped data in client.

### Link to “External” URI via Type-ahead from Single Form Field to Multiple Fields
**Sinopia Lookup Client:**
  1. Configuration management (auth, API settings).
  2. Call API for **Lookup** with form field type-ahead string.
  3. Use **Lookup** default response data for URI, label, type for type-ahead starter field.
  4. Call API for **Fetch** above to retrieve RDF.
**Sinopia Mapper Client:**
  1. Map RDF from **Fetch** to determined other form fields
  2. Save selected & mapped data in client.

### Link to “External” URI via Browse & Select from Single Form Field to Single Field
**Sinopia Lookup Client:**
  1. Configuration management (auth, API settings).
  2. Call API for **Browse** with form field string.
**Sinopia Lookup Browse Module:**
  1. Use **Browse** default response data for URI, label, type, context to display to user.
  2. If User selects "see more", display context data. (*Fetch for full RDF?*)
  2. When User selects value, respond with **Browse** default response data for selected value's URI, label, type.
**Sinopia Lookup Client:**
  2. Save selected & mapped data in client.

### Link to “External” URI via Browse & Select from Single Form Field to Multiple Fields
**Sinopia Lookup Client:**
  1. Configuration management (auth, API settings).
  2. Call API for **Browse** with form field string.
**Sinopia Lookup Browse Module:**
  1. Use **Browse** default response data for URI, label, type, context to display to user.
  2. If User selects "see more", display context data. (*Fetch for full RDF?*)
  2. When User selects value, respond with **Browse** default response data for selected value's URI, label, type.
  4. Call API for **Fetch** above to retrieve RDF for selected value's URI.
**Sinopia Mapper Client:**
  1. Map RDF from **Fetch** to determined other form fields
  2. Save selected & mapped data in client.
**Sinopia Lookup Client:**
  2. Save selected & mapped data in client.

### Link to “External” URI via Browse & Select from Multiple Fields to Single Field
**Sinopia Lookup Client:**
  1. Configuration management (auth, API settings).
  2. Call API for **Search** with form fields & related strings.
**Sinopia Lookup Browse Module:**
  1. Use **Search** default response data for URI, label, type, context to display to user.
  2. If User selects "see more", display context data. (*Fetch for full RDF?*)
  2. When User selects value, respond with **Browse** default response data for selected value's URI, label, type.
**Sinopia Lookup Client:**
  2. Save selected & mapped data in client.

### Link to “External” URI via Browse & Select from Multiple Field to Multiple Fields
**Sinopia Lookup Client:**
  1. Configuration management (auth, API settings).
  2. Call API for **Search** with form fields & related strings.
**Sinopia Lookup Browse Module:**
  1. Use **Search** default response data for URI, label, type, context to display to user.
  2. If User selects "see more", display context data. (*Fetch for full RDF?*)
  2. When User selects value, respond with **Browse** default response data for selected value's URI, label, type.
  4. Call API for **Fetch** above to retrieve RDF for selected value's URI.
**Sinopia Mapper Client:**
  1. Map RDF from **Fetch** to determined other form fields
  2. Save selected & mapped data in client.
**Sinopia Lookup Client:**
  2. Save selected & mapped data in client.
