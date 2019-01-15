---
layout: default
---

# Sinopia JSON Schemas for Resource Templates / Profiles

## Version (next)

Version (next) blah blah.

## Version 0.0.1

Version 0.0.1 JSON Schemas cleanly validate the LC profiles from https://github.com/lcnetdev/verso with a minimum of changes to those profiles. (See https://github.com/LD4P/sinopia_sample_profiles/pull/14 for the changes required)

- https://ld4p.github.io/sinopia/schemas/0.0.1/profile.json
- https://ld4p.github.io/sinopia/schemas/0.0.1/resource-templates-array.json
- https://ld4p.github.io/sinopia/schemas/0.0.1/resource-template.json
- https://ld4p.github.io/sinopia/schemas/0.0.1/property-templates-array.json
- https://ld4p.github.io/sinopia/schemas/0.0.1/property-template.json

special bonus schema
- https://ld4p.github.io/sinopia/schemas/0.0.1/profiles-array.json


## Example ajv validation commands

The following commands validate use the [`ajv CLI library`](https://www.npmjs.com/package/ajv-cli) for JSON schema validation. However, there are [many available JSON Schema validation libraries in numerous languages](https://json-schema.org/implementations.html#validators); just make sure you select one that validates JSON Schema version draft-07.

#### Validate JSON instance against schema(s)

Note: if the schemas themselves aren't valid, the following commands will so indicate.

##### Validate a single file

```
$ ajv validate -s schemas/profiles-array.json -r 'schemas/*.json' -d profiles/v1/all_profiles.json

profiles/v1/all_profiles.json invalid
  [ { keyword: 'format',
      dataPath:
       '[3].Profile.resourceTemplates[1].propertyTemplates[0].valueConstraint.valueDataType.dataTypeURI',
      schemaPath:
       '#/properties/valueConstraint/properties/valueDataType/properties/dataTypeURI/format',
      params: { format: 'uri' },
      message: 'should match format "uri"' } ]
```

```
$ ajv validate -s schemas/profile.json -r 'schemas/*.json' -d "BIBFRAME 2.0 Place.json"

BIBFRAME 2.0 Place.json valid
```

##### Validate all files in a folder

```
$ ajv validate -s schemas/profile -r 'schemas/*.json' -d "profiles/*.json"

profiles/all_profiles.json invalid
[ { keyword: 'type',
    dataPath: '',
    schemaPath: '#/type',
    params: { type: 'object' },
    message: 'should be object' } ]
profiles/BIBFRAME 2.0 Admin Metadata.json valid
profiles/BIBFRAME 2.0 Agents Contribution.json valid
profiles/BIBFRAME 2.0 Agents Primary Contribution.json valid
profiles/BIBFRAME 2.0 Agents.json valid
profiles/BIBFRAME 2.0 Cartographic.json valid
profiles/BIBFRAME 2.0 DDC.json valid
profiles/BIBFRAME 2.0 Edition Information.json valid
profiles/BIBFRAME 2.0 Extra menus.json valid
profiles/BIBFRAME 2.0 Form.json valid
profiles/BIBFRAME 2.0 IBC.json valid
profiles/BIBFRAME 2.0 Identifiers.json valid
profiles/BIBFRAME 2.0 Item.json valid
profiles/BIBFRAME 2.0 Language.json valid
profiles/BIBFRAME 2.0 LCC.json valid
profiles/BIBFRAME 2.0 Load.json valid
profiles/BIBFRAME 2.0 Monograph.json valid
profiles/BIBFRAME 2.0 Moving Image-35mm Feature Film.json valid
profiles/BIBFRAME 2.0 Moving Image-BluRay DVD.json valid
profiles/BIBFRAME 2.0 Notated Music.json valid
profiles/BIBFRAME 2.0 Note.json valid
profiles/BIBFRAME 2.0 Place.json valid
profiles/BIBFRAME 2.0 Prints and Photographs.json valid
profiles/BIBFRAME 2.0 Publication, Distribution, Manufacturer Activity.json valid
profiles/BIBFRAME 2.0 Rare Materials.json valid
profiles/BIBFRAME 2.0 Related Works and Expressions.json valid
profiles/BIBFRAME 2.0 RWO.json valid
profiles/BIBFRAME 2.0 Serial.json valid
profiles/BIBFRAME 2.0 Series Information.json valid
profiles/BIBFRAME 2.0 Sound Recording-Analog.json valid
profiles/BIBFRAME 2.0 Sound Recording-Audio CD-R.json valid
profiles/BIBFRAME 2.0 Sound Recording-Audio CD.json valid
profiles/BIBFRAME 2.0 Title Information.json valid
profiles/BIBFRAME 2.0 Topic.json valid
profiles/PMO Medium of Performance.json valid
```

#### Validate schema itself

```
$ ajv compile -s schemas/property-template

schema schemas/property-template is valid
```

```
$ ajv compile -s schemas/profile

schema schemas/profile is invalid
error: can't resolve reference resource-templates-array from id profile#
```
