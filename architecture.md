---
layout: default
---

Here are various views, diagrams, and notes on the overall Sinopia architecture. This page is likely to change (and change often) as we work through implementations in our current work cycle. A lot of the following has overlap with the defined [Sinopia Data Models](/sinopia/models).

All of the following diagrams should be accessible in [this open Google drive folder as well](https://drive.google.com/drive/folders/12MOb3GjBYBK3KZEN0QdGBMuerot7627q?usp=sharing).

# Conceptual Architectural

This is a high-level diagram of the full Sinopia system and it's components. Where feasible at a high level, sub-system interactions and protocols are documented here:

![](https://docs.google.com/drawings/d/e/2PACX-1vQj9BkBgdCu70D8wCyFigqIuy6Uw9vjN2C3K3tPsLpSPB8_4Hz-Cm9bqdEPR6r4xHiIiY4TFkPjiurq/pub?w=1256&h=720)
<small>[link to diagram](https://docs.google.com/drawings/d/1FdgAeWT2xAaXBWLw2MWHK1tIEC1q_ls56VX3gPiZUcM/edit)</small>

# Architectural Components

### Sinopia Profile Editor

![](https://docs.google.com/drawings/d/e/2PACX-1vSHdVxkwgq4ImystEwHxPwDgpW8tFVdgEkoglEZtwWQwKt3Ah4Kc0w-J-VQdeRgdhpzKTBPX_trMcm9/pub?w=1441&h=854)
<small>[link to diagram, requires Draw.io Google Drive Add-on to Edit](https://drive.google.com/file/d/19MjuEht4oKJC3ICoKHDJAut8vog7EL7w/view?usp=sharing)</small>

### Sinopia Front-End

![](https://docs.google.com/drawings/d/e/2PACX-1vQBuR2eZU4EIGjU93rTpO_Nmg39tUzLvvHs6tNmnVVAAl0fAmgrgQPWGnIxAMydUkb4bgvIyIPXUGjU/pub?w=1605&h=710)
<small>[link to diagram](https://docs.google.com/drawings/d/1AeO7_UqecQoPGgrDIdsfTJi6_PRkHnldqHRIbfP8ZCo/edit)</small>

### Sinopia Server & Data Materialization

![](https://docs.google.com/drawings/d/e/2PACX-1vTvA-mXmVizhINLd34bhFDIyKzYC39HkR6vFG-Z2fUr-P196Mf-juH2CqOUq0A4twkhT_-umyi7xJaq/pub?w=1269&h=1080)
<small>[link to diagram, requires Draw.io Google Drive Add-on to Edit](https://drive.google.com/file/d/1hqLoObnmQ-HEtgJSqfN0SoKZH9OmO3xb/view?usp=sharing)</small>

### Integration Points & Interfaces (External ReST APIs or other)

We are publishing the [Sinopia Client](https://github.com/LD4P/sinopia_server/tree/master/sinopia_client) as an node.js module that can be imported into Javascript 
source code. This allows any Javascript-based project to integrate 
the Sinopia Server into their systems and provides a Swagger API for interacting 
with the Sinopia Stack.

See [the work here](/sinopia/external-data) that is specifically about Sinopia Editor & QA-inspired Lookup API interactions.

# Dataflow & Interaction Diagram

These are a list of "dataflow" and sequence diagrams to help unravel the expected and supported Sinopia system interactions. These are a level or two below some of the UX/UI work, focusing on the underlying systems.

### Overall 'Dataflow' Diagram

![](https://docs.google.com/drawings/d/e/2PACX-1vTQL_vTX8eLbk9xdLOqvFjkNjQM_L8tmDpGrHNFfeeN9KK66m64kV34BHMu9DNoUBwllaGKLDACV_vH/pub?w=4797&h=1804)
<small>[link to diagram](https://docs.google.com/drawings/d/1FoMgCn6FqAHN0W_lpkZOZF4G5ezkSxf6iWrBgg1SLQw/edit)</small>

### Login & First Steps
1. Authentication
2. Administrative Landing Page (website)
   1. Favorites or Most Used Profiles List
   2. Profiles Search
   3. WIP or Draft Data Entry (Stretch)
   4. Internal Instance Data Search
3. Authorization

### Create New Profile

### Loading Resource Template contained in a Profile

Option 1: Select Resource Template from a List
   1. Resource Template pulled from database
   2. Profile loaded into Editor
   3. User redirected to Editor with that Profile (next step)

Option 2: Search & Select Resource Templates
  1. Enter Profile search term (label, author, date, keyword) in Resource 
     Template search
  2. View search results 
  3. User selects Resource Template
  4. Resource Template pulled from database
  5. Resource Template loaded into Editor
  6. User redirected to Editor with that Resource Template loaded 

### Edit Existing Profile

Editing an existing Profile is done in these steps:
  1. Load an existing Profile file from your local file system
     in the [Sinopia Profile Editor][PRO_EDIT].
  1. Make changes to the loaded resource templates and export to 
     your local filesystem.
  1. Create a pull request on the 
[Sinopia Sample Profiles](https://github.com/LD4P/sinopia_sample_profiles) 
     Github repository 
  1. Log into Sinopia
  1. Go to the **Linked Data Editor** and then click on the 
     **Import Resource Template** tab
  1. The existing Resource Templates in the Profile will be overridden, new
     Resource Templates in the Profile will be added to the Sinopia Server


### Delete Existing Resource Template

Deleting an existing resource template from Sinopia is not part of the MVP
scoped work on the editor. Sinopia administrators will be able to manually delete 
resource templates from the Sinopia Server.

### Create New Entity
The Linked Data Editor is used to create a new entities in Sinopia. When a 
Resource Template is loaded into the Editor and data is entered by the user, the
user can save the RDF at which point a new entity is created in Sinopia with the
generated RDF from the user interface.   

![](https://docs.google.com/drawings/d/e/2PACX-1vSUaCxlon2o5G0hCCrP5Eg5GcZEK8mtRcpWrs1zO0PMTlF2i5z4ThH44nwGUWicr5o9b3Ufb0NT0c05/pub?w=2027&h=723)
<small>[link to diagram](https://docs.google.com/drawings/d/14hRHdepWbYrZn5jzfBxXY210H_a3FutAYZV5Mj82ZM4/edit)</small>

### Create New Entity with Context
As part of the MVP, users can also 
click on the **Mint URI** button for a Property Template and a new entity will
be created in Sinopia with that entity's data saved in Sinopia Server, and that
new entity's URI associated as a RDF Object in the calling Resource Template RDF
context. 

### Edit Existing Entity

WIP.

### Delete Existing Entity

WIP.

### Sinopia / QA Form Type-Ahead

The React `InputLookupQA` component uses a configuration JSON feed to 
query authorities in the Questioning Authority lookup service.  


### Sinopia / Library of Congress Type-Ahead
The React `InputListLOC` component uses a configurable JSON feed to
query specific Library of Congress resources typically from their 
Linked Data service at [http://id.loc.gov](http://id.loc.gov/).

### Sinopia / QA Form Contextual Lookup

![](https://docs.google.com/drawings/d/e/2PACX-1vQCnqjIjNHRo_giEM2_Dw9s85cXA2gQt2ew9pWVxWwiDCWYAikJL9Bs5Oyj1Pc4kRl9x69rRLenrd1i/pub?w=1152&h=717)
<small>[link to diagram](https://docs.google.com/drawings/d/1Bo-hCtPg1gQVJZWtVdbJGLo74_GM4RL7tfotnU6HTPs/edit)</small>

### Sinopia / QA External Keyword Search

### Sinopia / Internal Form Type-Ahead

WIP.

### Sinopia / Internal Form Contextual Lookup

WIP.

### Sinopia / Internal Keyword Search

WIP.

### Sinopia / Internal Faceted Search

WIP.

# Original Whiteboard Photos

See https://drive.google.com/drive/u/1/folders/1ynnPhdQGRDMkrpEpcmsjxBD5TqpovoBS

[HOME]: https://sinopia.io/
[EDITOR]: https://sinopia.io/editor
[PRO_EDIT]: https://profile-editor.sinopia.io/
