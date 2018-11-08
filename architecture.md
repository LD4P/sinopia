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

![](assets/img/SinopiaProfileEditor.png)
<small>[link to diagram, requires Draw.io Google Drive Add-on to Edit](https://drive.google.com/file/d/19MjuEht4oKJC3ICoKHDJAut8vog7EL7w/view?usp=sharing)</small>

### Sinopia Front-End

![](https://docs.google.com/drawings/d/e/2PACX-1vQBuR2eZU4EIGjU93rTpO_Nmg39tUzLvvHs6tNmnVVAAl0fAmgrgQPWGnIxAMydUkb4bgvIyIPXUGjU/pub?w=1605&h=710)
<small>[link to diagram](https://docs.google.com/drawings/d/1AeO7_UqecQoPGgrDIdsfTJi6_PRkHnldqHRIbfP8ZCo/edit)</small>

### Sinopia Server & Data Materialization

![](assets/img/SinopiaServer.png)
<small>[link to diagram, requires Draw.io Google Drive Add-on to Edit](https://drive.google.com/file/d/1hqLoObnmQ-HEtgJSqfN0SoKZH9OmO3xb/view?usp=sharing)</small>

### Integration Points & Interfaces (External ReST APIs or other)

WIP. See [the work here](/sinopia/external-data) that is specifically about Sinopia Editor & QA-inspired Lookup API interactions.

# Dataflow & Interaction Diagram

These are a list of "dataflow" and sequence diagrams to help unravel the expected and supported Sinopia system interactions. These are a level or two below some of the UX/UI work, focusing on the underlying systems.

### Overall 'Dataflow' Diagrams

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

### Loading Profile

Option 1: Select Profile from Most Used
   1. Profile pulled from database
   2. Profile loaded into Editor
   3. User redirected to Editor with that Profile (next step)

Option 2: Search & Select Profile
  1. Enter Profile search term (label, author, date, keyword) in Profiles search
  2. View Profile results (list of Profile metadata)
  3. User selects profile
  4. Profile pulled from database
  5. Profile loaded into Editor
  6. User redirected to Editor with that Profile (next step)

### Edit Existing Profile


### Delete Existing Profile


### Create New Entity

![](https://docs.google.com/drawings/d/e/2PACX-1vSUaCxlon2o5G0hCCrP5Eg5GcZEK8mtRcpWrs1zO0PMTlF2i5z4ThH44nwGUWicr5o9b3Ufb0NT0c05/pub?w=2027&h=723)
<small>[link to diagram](https://docs.google.com/drawings/d/14hRHdepWbYrZn5jzfBxXY210H_a3FutAYZV5Mj82ZM4/edit)</small>

### Create New Entity with Context


### Edit Existing Entity


### Delete Existing Entity


### Sinopia / QA Form Type-Ahead


### Sinopia / QA Form Contextual Lookup

![](https://docs.google.com/drawings/d/e/2PACX-1vQCnqjIjNHRo_giEM2_Dw9s85cXA2gQt2ew9pWVxWwiDCWYAikJL9Bs5Oyj1Pc4kRl9x69rRLenrd1i/pub?w=1152&h=717)
<small>[link to diagram](https://docs.google.com/drawings/d/1Bo-hCtPg1gQVJZWtVdbJGLo74_GM4RL7tfotnU6HTPs/edit)</small>

### Sinopia / QA External Keyword Search


### Sinopia / Internal Form Type-Ahead


### Sinopia / Internal Form Contextual Lookup


### Sinopia / Internal Keyword Search


### Sinopia / Internal Faceted Search

# Original Whiteboard Photos

See https://drive.google.com/drive/u/1/folders/1ynnPhdQGRDMkrpEpcmsjxBD5TqpovoBS
