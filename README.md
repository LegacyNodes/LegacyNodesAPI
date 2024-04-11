# LegacyNodesAPI
## Introduction

This API provides access to real-time information about your server, including server status, resource usage, owner details, and configuration settings.

## Base URL
- https://panel.legacynodes.com/api/client/servers/[serverID]

## Authentication

All requests to the API must include two parameters for authentication:

- `apiKey`: Your unique API key.
- `serverId`: The ID of your server.

#### How To Get Your API Key
 - Head over to https://panel.legacynodes.com/account/api to generate your own unique API key

#### How To Get Your Server ID
- Go to your server Settings page
- Find `Debug Information`
- ![image](https://github.com/LegacyNodes/LegacyNodesAPI/assets/81554085/14f8642f-effe-4070-af45-e616557eeb97)
- Copy the Server ID by clicking on it

## Endpoints

### 1. Get Server Resources

Retrieve the current server details and resources.

- **URL**: `/resources`
- **Method**: `GET`
- **Parameters**:
  - `apiKey` (required): Your API key.
  - `serverId` (required): ID of your server.

#### Response

A successful response will return a JSON object containing server details and resource usage.

```json
{
  "object": "stats",
  "attributes": {
    "current_state": "running",
    "is_suspended": false,
    "resources": {
      "memory_bytes": 504975360,
      "cpu_absolute": 0.648,
      "disk_bytes": 58648315,
      "network_rx_bytes": 220185,
      "network_tx_bytes": 132902,
      "uptime": 181234042
    }
  }
}
```

### 2. Get Server Details

Retrieve detailed information about the server.

- **URL**: `/server`
- **Method**: `GET`
- **Parameters**:
  - `apiKey` (required): Your API key.
  - `serverId` (required): ID of your server.

#### Response

A successful response will return a JSON object containing detailed server information.

```json
{
  "object": "server",
  "attributes": {
    "server_owner": true,
    "identifier": "d904e051",
    "internal_id": 20,
    "uuid": "UUID",
    "name": "Node1",
    "node": "UK01",
    "is_node_under_maintenance": false,
    "sftp_details": {
      "ip": "IP",
      "port": "PORT"
    },
    "description": "",
    "limits": {
      "memory": 2560,
      "swap": 0,
      "disk": 5120,
      "io": 500,
      "cpu": 100,
      "threads": null,
      "oom_disabled": true
    },
    "invocation": "java -Xms128M -XX:MaxRAMPercentage=95.0 -Dterminal.jline=false -Dterminal.ansi=true -jar server.jar",
    "docker_image": "ghcr.io/pterodactyl/yolks:java_8",
    "egg_features": [
      "eula",
      "java_version",
      "pid_limit"
    ],
    "feature_limits": {
      "databases": 1,
      "allocations": 1,
      "backups": 1
    },
    "status": null,
    "is_suspended": false,
    "is_installing": false,
    "is_transferring": false,
    "relationships": {
      "allocations": {
        "object": "list",
        "data": [
          {
            "object": "allocation",
            "attributes": {
              "id": "ID",
              "ip": "IP",
              "ip_alias": "IP_ALIAS",
              "port": "PORT",
              "notes": null,
              "is_default": true
            }
          }
        ]
      },
      "variables": {
        "object": "list",
        "data": [
          {
            "object": "egg_variable",
            "attributes": {
              "name": "Minecraft Version",
              "description": "The version of minecraft to download. \r\n\r\nLeave at latest to always get the latest version. Invalid versions will default to latest.",
              "env_variable": "MINECRAFT_VERSION",
              "default_value": "latest",
              "server_value": "1.8.8",
              "is_editable": true,
              "rules": "nullable|string|max:20"
            }
          },
          {
            "object": "egg_variable",
            "attributes": {
              "name": "Server Jar File",
              "description": "The name of the server jarfile to run the server with.",
              "env_variable": "SERVER_JARFILE",
              "default_value": "server.jar",
              "server_value": "server.jar",
              "is_editable": true,
              "rules": "required|regex:/^([\\w\\d._-]+)(\\.jar)$/"}},{"object":"egg_variable","attributes":{"name":"Build Number","description":"The build number for the paper release.\r\n\r\nLeave at latest to always get the latest version. Invalid versions will default to latest.","env_variable":"BUILD_NUMBER","default_value":"latest","server_value":"latest","is_editable":true,"rules":"required|string|max:20"}}]}}},"meta":{"is_server_owner":true,"user_permissions":["*"]}
  }
}
```

## Error Handling

In case of errors, the API will return appropriate HTTP status codes along with error messages in the response body.

### Error Responses
- **401 Unauthorized**: If the provided API key or server ID is invalid.
- **404 Not Found**: If the server ID does not exist.



