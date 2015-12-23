Homie server
============

[![npm version](https://img.shields.io/npm/v/homie-server.svg)](https://www.npmjs.com/package/homie-server) [![Travis CI](https://img.shields.io/travis/marvinroger/homie-server.svg)](https://travis-ci.org/marvinroger/homie-server) [![Coveralls](https://img.shields.io/coveralls/marvinroger/homie-server.svg)](https://coveralls.io/r/marvinroger/homie-server) [![Dependency Status](https://david-dm.org/marvinroger/homie-server.svg?style=flat)](https://david-dm.org/marvinroger/homie-server) [![devDependency Status](https://david-dm.org/marvinroger/homie-server/dev-status.svg?style=flat)](https://david-dm.org/marvinroger/homie-server#info=devDependencies)

Server of homie, an opiniated home automation system using MQTT. The project is currently in alpha.

![homie server screenshot](screenshot.png)

## Features

* OTA updates
* Dashboard

## Usage

`npm install -g homie-server`

Start homie by calling `homie`. You can optionally provide a `--dataDir` argument that will be used to store the homie data. By default, this directory is `<home directory>/.homie`. You can also configure the HTTP server serving the UI with `--uiPort`, defaults to 80.

### Configuration

Three files define the behaviour of homie, and are all contained in the data directory:

1. The `config.json` file. It will contain some configuration like for example whether you use metric or imperial units. Empty for now.

2. The `infrastructure.json` file. This file contains the representation of your homie devices. You can also group devices there.

```json
{
  "devices": [
    {
      "id": "marvin-shutters",
      "name": "Marvin's shutters",
      "location": "Marvin's room",
      "nodes": [{
        "type": "shutters",
        "id": "shutters",
        "name": "Shutters"
      }]
    },
    {
      "id": "marvin-light",
      "name": "Marvin's light",
      "location": "Marvin's room",
      "nodes": [{
        "type": "light",
        "id": "light",
        "name": "Main light"
      }]
    },
  ],
  "groups": [
    {
      "id": "marvin",
      "name": "Marvin's room",
      "devices": ["marvin-shutters", "marvin-light"]
    }
  ]
}

```

3. The `ota/manifest.json` file. It contains a definition of the firmwares for your devices, like so:

```json
{
  "firmwares": [
    {
      "name": "Marvin_s_Room",
      "version": "1.0.0",
      "devices": ["marvin-shutters"]
    }
  ]
}
```

This manifest needs a firmware to be stored in `ota/bin/Marvin_s_Room.bin`, else OTA won't be handled. You can update the manifest while homie is running, it will be hot-loaded.
