# voxoculi

Vox Pupuli folks, under the OpenVoxProject umbrella, deal with numerous projects and tools to build and ship the continuation of Open Source Puppet.
Tracking what goes into which component, knowing what is used to build packages, etc. is tedious.

This repository intend to:
* document the various artifacts and sources used for building openvox packages;
* show how they relate to eacrh other;
* allow at a glance to understand how a specific artifact is built;
* in the future, this information may be combined with build-time information to produce Software Bill Of Material (SBOM).

## Scope

Beyond the packages build in the OpenVoxProject organization, this repository welcome documentation of how artifacts for the openvox packages are built for projects outisde the organization.

## Rendering metadata

We currently have a rake task to generate `voxoculi.svg` (the default rake task with build it):

```
$ rake
```

## Extending metadata

All this project is about providing metadata about artifacts and the tools that produce them.  In order to make this process as manageable as possible, update the schema in `schema/shema.yaml` to document your new field before adding them to the various .yaml files.  You can check that all files pass validation with:

```
$ rake lint
```
