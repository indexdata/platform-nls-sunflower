# FOLIO complete platform: Sunflower++ with reading room circulation

Copyright (C) 2015-2025 The Open Library Foundation/Index Data

This software is distributed under the terms of the Apache License,
Version 2.0. See the file "[LICENSE](LICENSE)" for more information.

## Introduction

This is the "complete" Stripes "platform". It contains the metadata
required to build a full FOLIO "Sunflower++" environment: the FOLIO
Sunflower release plus the additional features needed for reading room
circulation.

Please see the
[quick start guide](https://github.com/folio-org/stripes/blob/master/doc/quick-start.md)
for more information.

The `stripes.config.js` is a configuration for a specific tenant. In
general, a platform supports multiple tenants, each of which may
include a different set of the available modules.  You can copy the
`stripes.config.js` file to be your `stripes.config.js.local`
configuration file.

The `yarn.lock` and `*-install.json` files in this repository can be
used to build a FOLIO system with the components that represent the
latest, compatible set of FOLIO releases.

## Installation

Install platform dependencies
```
$ yarn config set @folio:registry https://repository.folio.org/repository/npm-folio/
$ yarn install
```

## Build and serve

To build and serve `platform-complete` in isolation for development purposes, run the "start" package script.
```
$ yarn start
```

The default configuration assumes an Okapi instance is running on https://nls-sunflower-okapi.folio-dev.indexdata.com with tenant "nls".  The options `--okapi` and `--tenant` can be provided to match your environment.
```
$ yarn start --okapi http://localhost:9130 --tenant diku
```

To build a `platform-complete` bundle for production, modify `stripes.config.js` with your Okapi and tenant, then run the "build" script, passing it the name of the desired directory to place build artifacts.
```
$ yarn build ./output
```

See the [build](https://github.com/folio-org/stripes-cli/blob/master/doc/commands.md#build-command) and [serve](https://github.com/folio-org/stripes-cli/blob/master/doc/commands.md#serve-command) command reference in `stripes-cli` for a list of available options.

## Build stripes using the Dockerfile
The included Dockerfile allows for building a container that serves the stripes platform using Nginx. Pass in the Okapi URL and tenant ID as build arguments. The defaults are shown below:

```
docker build -f docker/Dockerfile --no-cache=true \
  --build-arg OKAPI_URL=http://localhost:9130 \
  --build-arg TENANT_ID=diku -t stripes .
```
The nginx server name can be passed to the container at runtime. The default value is `localhost` if no argument is passed. For example, to have nginx use `127.0.0.1` as the server name:
```
docker run stripes 127.0.0.1
```

## Additional information

[Finding what module versions are included in a flower release.](doc/finding-module-versions.md)

[Finding which flower release a given installation runs.](https://lotus.docs.folio.org/docs/settings/system_software_versions/system_software_versions/)

See project [FOLIO](https://issues.folio.org/browse/FOLIO)
at the [FOLIO issue tracker](https://dev.folio.org/guidelines/issue-tracker/).

Other FOLIO Developer documentation is at [dev.folio.org](https://dev.folio.org/)
