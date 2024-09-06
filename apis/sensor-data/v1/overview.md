# Sensor Data

## Introduction

The sensor data service offers REST APIs to third-party sensor manufacturers and data sources to integrate their sensors with iTwin IoT platform.

This document focuses on importing generic sensors into iTwin IoT and concentrates on the persona, where the sensor manufacturers will be able to **push** their data into sensor data service.

### Entities Hierarchy

The first step to visualizing data on the platform is to add a connection to a project, then attach subsequent devices and sensors. Your network is broken up into three distinct levels of entities: Connections, Devices, and Sensors.

A **connection** is simply a connection to your data source. It aggregates the data from all associated devices and sensors and sends the information to the platform. Connections can be hardware-based, such as cell phones or radios, or software-based, such as an API or FTP.

The **device** can then read the array of associated sensors and store their data, or it can house the sensor datasets being transmitted from the file transfer connection.

A **sensor** will physically collect the data from the field and they also represent the data aggregation and storage node in the app.

<img alt="entities hierarchy" src="https://bentleysystems.service-now.com/0a5c837047fd82909091861f536d43dd.iix" width="50%" />

### Prerequisites

To create a Bentley account if you don't already have one, <a href="https://itwiniot.bentley.com/" target="_blank">iTwin IoT</a> and complete the registration process.

Use the following steps to integrate your sensors with the iTwin IoT platform.

1. Create an application in iTwin Platform
2. Obtaining Authorization Token
3. Register an asset in iTwin IoT

## Create an Application in iTwin Platform

Steps to create an application in [iTwin Platform](https://developer.bentley.com/) can be found at [Register a service application](/tutorials/authorize-service/#register-a-service-application).

> During the registration process, you may need to choose `Administration` and `Digital Twin Management` API associations. Additionally, all requests require an `Authorization` header with a valid Bearer token with either the `sensor-data:modify sensor-data:read users:read itwins:read itwins:modify`, or `itwin-platform` scope.

## Obtain Authorization Token

You can use the generated client id, client secret and scopes to [Obtain an access token](/tutorials/authorize-service/#obtain-an-access-token).

## Register an Asset in <a href="https://itwiniot.bentley.com/" target="_blank">iTwin IoT</a>

To create an asset you must have at least one of the following roles assigned in User Management: `Account Administrator`, `Co-Administrator`, or `CONNECT Services Administrator`. Then you can register an asset in [iTwin IoT](https://itwiniot.bentley.com/) and make sure to enable `Allow external team members`. Add the user that got created, while registering an application in iTwin Platform (example@apps.imsoidc.bentley.com) into the created asset with `IoT Creator` role (refer below screenshots).

![client-email](/images/client-email.png 'client-email')

> The address bar in the below screenshot displays the <b>itwin IoT asset id</b> which is needed to make API calls.

![user-roles](/images/user-roles.png 'user-roles')

> When an asset (iTwin) is registered via iTwin IoT, IOT capabilities are set up behind the scenes.

## Create, Update and Delete Node, Device(s), and Sensor(s)

You can use this API to create, update and delete node, device(s) and sensor(s) all together.

If none of the provided [device template](#choosedevicetemplate) or [sensor template](#choosesensortemplate) meet the requirements, you can use `IMPORT_DEVICE_SDE` for device and `GENERIC_SENSOR_SDE` for sensor.

> If you delete a node or device(s) or sensor(s) all the underlying sensor observation will be deleted.

**POST** [https://api.bentley.com/sensor-data/integrations/integrate?projectIds=&lt;Your asset id&gt;](#createconnectiondevicesandsensors)

#### Request parameters

| Name       | Required? | Description        |
| ---------- | --------- | ------------------ |
| projectIds | Yes       | iTwin IoT asset id |

```shell
curl --location 'https://api.bentley.com/sensor-data/integrations/integrate?projectIds=<Your asset id>' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <Your access token>' \
--data '{
    "integration": {
        "changeState": "new",
        "devices": [
            {
                "changeState": "new",
                "props": {
                    "INTEGRATION_ID": "IMPORT_DEVICE_SDE",
                    "NAME": "Device-1"
                },
                "sensors": [
                    {
                        "changeState": "new",
                        "props": {
                            "INTEGRATION_ID": "GENERIC_SENSOR_SDE",
                            "NAME": "Sensor-1",
                            "UNKNOWN_UNITS": {
                                "0": "millimeter",
                                "1": "millimeter"
                            },
                            "UNKNOWN_METRICS": {
                                "0": "Alignment_Left_SD",
                                "1": "Alignment_Right_SD"
                            }
                        }
                    },
                    {
                        "changeState": "new",
                        "props": {
                            "INTEGRATION_ID": "GENERIC_SENSOR_SDE",
                            "NAME": "Sensor-2",
                            "UNKNOWN_UNITS": {
                                "0": "millimeter",
                                "1": "millimeter"
                            },
                            "UNKNOWN_METRICS": {
                                "0": "Alignment_Left_SD",
                                "1": "Alignment_Right_SD"
                            }
                        }
                    }
                ]
            }
        ]
    }
}
 '
```

#### Request definitions

| Name                                          | Type     | Required?  | Description                                                                                                                                                   |
| --------------------------------------------- | -------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| INTEGRATION_ID                                | string   | Yes        | Device id or sensor id obtained from the devices types or sensor types endpoint.                                                                              |
| refId                                         | string   | Yes        | Unique entity id can be used to update or delete devices or sensors.                                                                                          |
| integration[changeState]                      | string   | No         | To create a node set changeState to `new`; to remove set to `remove` (Although this property is not necessary, failing to provide will result in a 422 error) |
| devices[].changeState/ sensors[].changeState  | string   | No         | To create devices and sensors set changeState to `new`; to update set to `update` to remove set to `remove`.                                                  |
| NAME                                          | string   | No         | Device or sensor name                                                                                                                                         |
| LOCATION                                      | object   | No         | X, Y & Z coordinates                                                                                                                                          |
| UNKNOWN_UNITS                                 | object   | No         | Unknown units of a sensor                                                                                                                                     |
| UNKNOWN_METRICS                               | object   | No         | Arbitrary metrics of a sensor                                                                                                                                 |
| KNOWN_UNITS                                   | object   | No         | Known units of a sensor                                                                                                                                       |
| KNOWN_METRICS                                 | object   | No         | Known metrics of a sensor                                                                                                                                     |
| NOTES                                         | string   | No         | Additional information of devices and sensors                                                                                                                 |

### Generic sensors

If you have sensors that you would like to import into iTwin IoT, but the sensors don't match any of the existing iTwin IoT Sensor templates, set `GENERIC_SENSOR_SDE` to the `props.INTEGRATION_ID` property.

Generic sensors MUST have their metrics and units defined on the sensor during the time of creation. Most scenarios which opt to use a generic sensor use free form custom string for both metrics and unit.

> Example of unknown metric and unknown unit

```json
{
  "changeState": "new",
  "refId": "{{$guid}}",
  "props": {
    "NAME": "Unknown metrics and units",
    "INTEGRATION_ID": "GENERIC_SENSOR_SDE",
    "UNKNOWN_UNITS": {
      "0": "abcUnit"
    },
    "UNKNOWN_METRICS": {
      "0": "abc"
    }
  }
}
```

> Example known metric and known unit: <br/>
> Other scenarios might use both known metrics and known units however, the ordering of metrics list slightly differs from a defined sensor template this might look like the sample below.

```json
{
  "changeState": "new",
  "refId": "{{$guid}}",
  "props": {
    "NAME": "Known metrics and units",
    "INTEGRATION_ID": "GENERIC_SENSOR_SDE",
    "KNOWN_UNITS": {
      "0": "Hz",
      "1": "mm"
    },
    "KNOWN_METRICS": {
      "0": "f",
      "1": "cum_distance"
    }
  }
}
```

> Example unknown metric and known unit: </br>
> Final scenarios might use known units with unknown metrics.

```json
{
  "changeState": "new",
  "refId": "{{$guid}}",
  "props": {
    "NAME": "Known metrics and units",
    "INTEGRATION_ID": "GENERIC_SENSOR_SDE",
    "KNOWN_UNITS": {
      "0": "Hz",
      "1": "mm"
    },
    "UNKNOWN_METRICS": {
      "0": "abc",
      "1": "def"
    }
  }
}
```

## Upload Sensor Observations

To upload readings to a specified sensor requires sensor id and timestamp of the observation recorded and an object values containing required supported metrics with a key-value. You can find the required metrics along with units using [Metrics and Units](#metricsandunits).

**POST** <a href="#uploadsensorobservations">https://api.bentley.com/sensor-data/data/upload</a>

```shell
curl --location 'https://api.bentley.com/sensor-data/data/upload' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <Your access token> ' \
--data '{
    "observations": [
        {
            "sensorId": "/api/B08851/node/dynamic/AB10E2/device/D76619/sensor",
            "timestamp": "2024-02-20T04:35:23.653Z",
            "values": {
                "Alignment_Left_SD": 0.23,
                "Alignment_Right_SD": 0.84
            }
        },
    ]
}'
```

#### Request definitions

| Name       | Type     | Required? | Description                                                      |
| ---------- | -------- | --------- | ---------------------------------------------------------------- |
| sensorId   | string   | Yes       | Sensor id                                                        |
| timestamp  | string   | Yes       | The date and time of the recorded observation in ISO date format |
| values     | object   | Yes       | Object containing all required metrics with corresponding value  |

In iTwin IoT, you can confirm the uploaded observations. When you open the asset, navigate to the<code>Data</code> tab, click on the <code>tables</code> , choose the desired sensor, and all of the submitted observations will be shown.

![iTwin IoT Tables](/images/tables.png 'iTwin IoT Tables')

## Choose Device Template

You can see the list of supported Device templates and choose the suitable device template with the help of this REST API.

**GET** <a href="#choosedevicetemplate">https://iiot.bentley.com/api/devices/types?excludeLegacy=true</a>

```shell
curl --location 'https://iiot.bentley.com/api/devices/types?excludeLegacy=true' \
--header 'Authorization: Bearer <Your access token>'
```

## Choose Sensor Template

You can see the list of supported Sensor templates and choose the suitable sensor template with the help of this REST API.

**GET** <a href="#choosesensortemplate">https://iiot.bentley.com/api/sensors/types?excludeLegacy=true</a>

```shell
curl --location 'https://iiot.bentley.com/api/sensors/types?excludeLegacy=true' \
--header 'Authorization: Bearer <Your access token>'
```

In the response you can see the `id` field of the sensor template. Which will be needed to create a new sensor.

## Metrics and Units

To view the catalog of all standard/known metrics and units use this REST request. For example, the temperature sensor above `TEMPERATURE_SDE` Stores readings for a single metric `Temperature` which has a metric Id of `T` the supported units for this metric are Celsius (C) kelvin (K) and Fahrenheit (F).

**GET** <a href="#metricsandunits">https://iiot.bentley.com/api/metrics/types?excludeLegacy=true</a>

```shell
curl --location 'https://iiot.bentley.com/api/metrics/types?excludeLegacy=true' \
--header 'Authorization: Bearer <Your access token>'
```

## Obtain Required Metrics and Supported Units for a Sensor

**POST** <a href="#obtainrequiredmetricsandsupportedunitsforasensor">https://iiot.bentley.com/api/sensors/metrics?projectIds=&lt;Your asset id&gt;</a>

```shell
curl --location 'https://iiot.bentley.com/api/sensors/metrics?projectIds=<Your asset id>&filters=raw' \
--header 'Authorization: Bearer <Your access token> ' \
--header 'Content-Type: application/json' \
--data '{
    "ids": [
        "/api/B08851/node/dynamic/AB10E2/device/D76619/sensor"
    ]
}'
```

## Get Integrations

This API can be used to retrieve information like all devices and sensors of given a node id.

**POST** <a href="#getintegrations">https://iiot.bentley.com/api/integrations/&lt;node id&gt;</a>

```shell
curl --location 'https://iiot.bentley.com/api/integrations/<node id>' \
--header 'Authorization: Bearer <your access_token>' \
--header 'Content-Type: application/json' \
--data ''
```
