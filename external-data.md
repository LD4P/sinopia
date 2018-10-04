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

### GET => **Lookup** (Single field *Query*):
* *In* (payload or param): String as API URL parameter
* *200 Out* (payload, preference JSON): Array of URIs, Match Score, Labels, Contextual Info (Type);

### GET => **Multi-field Lookup** (Multi-field *Query*):
* *In* (payload or param): Array of Strings as API URL parameters
* *200 Out* (payload, preference JSON): Array of URIs, Match Score, Labels, Contextual Info (Type);

### Error responses
To be written up.

## Sinopia Search Lookup Interactions (Proposed)

### Search for available data => Search Query / Browse

**Sinopia Search Client:**
  1. If needed, break apart API calls by source.
  2. Call API(s) for **Lookup** with search string. (or **Multi-field Lookup** if spaces in search string.)
  3. Use **Lookup** default data to break apart API(s) responses for display of responses.
  4. Follow Selection responses below

### Select to View
  1. User selects "see more" for a given result.
  2. Call API(s) for **Fetch** or to dereference for the selected value's URI from **Lookup** results.
  3. Display RDF in module.

### Select to Edit Single Resource
  1. User selects `Edit` for a given result.
  2. Ask User to select a Profile to edit the resource with.
  2. Check Permissions to `Edit a resource` (if a Sinopia resource in their group).
     i. If true: Ask user to `Select Profile` & following steps.
     ii. If false: say they cannot edit, ask if they want to clone.
  3. Call API(s) for **Fetch** or to dereference for the selected value's URI from **Lookup** results.
  4. Map RDF to selected Profile.
  5. Present User the Editor with mapped data pre-populated for the existing resource in the selected Profile.

### Select to Edit Shape based on Profile
  1. User selects `Edit` for a given result.
  2. Ask User to select a Profile to edit the profile-mapped shape with.
  3. Query API(s) for Profile-mapped other resources (through their linking predicates) based on selected value's URI from **Lookup** results.
  4. Call API(s) for **Fetch** or to dereference for all URIs to map to the Profile (or this might be part of 3).
  5. Map RDF to selected Profile.
  6. Check Permissions to `Edit resources` (if all Sinopia resources in their group).
     i. If true: Ask user to `Select Profile` & following steps.
     ii. If false: say they cannot edit, ask if they want to clone the resources they cannot edit.
  7. Present User the Editor with mapped data pre-populated for the existing resource in the selected Profile.

### Select to Clone Single Resource
  1. User selects "clone" for a given result.
  2. Ask User to select a Profile to edit the resource or the profile-mapped shape with.
  2. Check Permissions to Clone a resource (if they have a graph that can work within).
     i. If true: Ask user to select Profile & following steps.
     ii. If false: say they need a graph to work within.
  4. Call API(s) for **Fetch** or to dereference for the selected value's URI from **Lookup** results.
  5. Map RDF to selected Profile (or profile subset / resource map hash).
  6. Present User the Editor with mapped data pre-populated for a new resource(s), with sameAs links to **Fetch** URI.

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
  5. Map RDF from **Fetch** to determined other form fields
  6. Save selected & mapped data in client.

### Link to “External” URI via Browse & Select from Single Form Field to Single Field

**Sinopia Lookup Client:**
  1. Configuration management (auth, API settings).
  2. Call API for **Lookup** with form field string.

**Sinopia Lookup Browse Module:**
  3. Use **Lookup** default response data (paginated for all results) for URI, label, type, context to display to user.
  4. If User selects "see more", display context data. (*Fetch for full RDF?*)
  5. When User selects value, respond with **Lookup** default response data for selected value's URI, label, type.

**Sinopia Lookup Client:**
  6. Save selected & mapped data in client.

### Link to “External” URI via Browse & Select from Single Form Field to Multiple Fields

**Sinopia Lookup Client:**
  1. Configuration management (auth, API settings).
  2. Call API for **Lookup** with form field string.

**Sinopia Lookup Browse Module:**
  3. Use **Lookup** default response data for URI, label, type, context to display to user.
  4. If User selects "see more", display context data. (*Fetch for full RDF?*)
  5. When User selects value, respond with **Lookup** default response data for selected value's URI, label, type.
  6. Call API for **Fetch** above to retrieve RDF for selected value's URI.

**Sinopia Mapper Client:**
  7. Map RDF from **Fetch** to determined other form fields.
  8. Save selected & mapped data in client.

**Sinopia Lookup Client:**
  9. Save selected & mapped data in client.

### Link to “External” URI via Browse & Select from Multiple Fields to Single Field

**Sinopia Lookup Client:**
  1. Configuration management (auth, API settings).
  2. Call API for **Lookup** with all strings from indicated fields.

**Sinopia Lookup Browse Module:**
  3. Use **Lookup** default response data for URI, label, type, context to display to user.
  4. If User selects "see more", display context data. (*Fetch for full RDF?*)
  5. When User selects value, respond with **Lookup** default response data for selected value's URI, label, type.

**Sinopia Lookup Client:**
  6. Save selected & mapped data in client.

### Link to “External” URI via Browse & Select from Multiple Field to Multiple Fields

**Sinopia Lookup Client:**
  1. Configuration management (auth, API settings).
  2. Call API for **Lookup** with all strings from indicated fields.

**Sinopia Lookup Browse Module:**
  3. Use **Lookup** default response data for URI, label, type, context to display to user.
  4. If User selects "see more", display context data. (*Fetch for full RDF?*)
  5. When User selects value, respond with **Lookup** default response data for selected value's URI, label, type.
  6. Call API for **Fetch** above to retrieve RDF for selected value's URI.

**Sinopia Mapper Client:**
  7. Map RDF from **Fetch** to determined other form fields
  8. Save selected & mapped data in client.

**Sinopia Lookup Client:**
  9. Save selected & mapped data in client.
