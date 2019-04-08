---
layout: default
---

# Sinopia Technology Implementation
The Sinopia stack uses [Circle-ci][CI] for continuous integration to
validate the code syntax using [eslint](https://eslint.org/) and test the code base using a combination of
[Jest](https://jestjs.io/), [Enzyme](https://github.com/airbnb/enzyme), and
[Puppeteer](https://developers.google.com/web/tools/puppeteer/). [Circle-ci][CI] also
creates [Docker][DOCK] images on Dockerhub that are automatically deployed to Sinopia's AWS
development environment.

## Sinopia Linked Data Editor
A hard fork of the Library of Congress [BIBFRAME Editor](https://github.com/lcnetdev/bfe),
Sinopia's Linked Data Editor is a [node.js][NODE] project that
uses the open-source javascript library [React](https://reactjs.org/) to build
the client-side user interface with supporting [node.js][NODE] libraries like
[Redux](https://redux.js.org/) for managing the data state of the editor.

The Linked Data Editor also implements a [Swagger REST API][SWAG]
for search and look-up interactions with third parties like the Questioning
Authority service from Cornell. The Sinopia Linked Data Editor requires a valid
[JSON Web Tokens (JWT)][JWT] from users that authenticate through
[Amazon Web Service's Cognito](https://aws.amazon.com/cognito/) for create-delete-update
operations for both resource templates and RDF data.

Sinopia's Linked Data Editor source code repository is hosted on Github at
[https://github.com/ld4p/sinopia_editor](https://github.com/LD4P/sinopia_profile_editor).

## Sinopia Profile Editor
Sinopia's Profile Editor is a forked version of Library of Congress
[Profile Editor](https://github.com/lcnetdev/profile-edit) that allows users to
build resource templates contained in profiles and save resulting file to the
local systems. Minimal refactoring was done to this codebase with new Sinopia
branding and user interfaces modifications support the use of
[JSON schema validation](https://json-schema.org/).

Sinopia's Profile Editor source code repository is hosted on Github at
[https://github.com/LD4P/sinopia_profile_editor](https://github.com/LD4P/sinopia_profile_editor).

## Sinopia Server
The Sinopia Server includes a Docker environment that uses the linked-data
platform [Trellis][LDP] as the main technology for managing
both RDF and non-RDF data. The Sinopia Stack uses the [Postgres](https://www.postgresql.org/)
relational-database variant of [Trellis][LDP] for the storage layer with an
[Elasticsearch](https://www.elastic.co/products/elasticsearch) search index for
discovery and search. Create-update-delete operations in [Trellis][LDP] are
controlled by incoming [JWTs][JWT] from the Sinopia Linked Data editor or supporting
tools.

The primary method of interaction between the Sinopia Linked Data Editor and the
Sinopia Server is through a [Swagger REST API][SWAG] client that is published as
a [npm (node package manager)](http://npmjs.com/) package at
https://www.npmjs.com/package/sinopia_server for importing into the
Sinopia Linked Data Editor.

The Sinopia Server's source code repository is hosted on Github at
[https://github.com/LD4P/sinopia_server](https://github.com/LD4P/sinopia_server).

CI: https://circleci.com/
DOCK: https://www.docker.com/
JWT: https://jwt.io/
LDP: https://www.trellisldp.org/
NODE: https://nodejs.org/en/
SWAG: https://swagger.io/
