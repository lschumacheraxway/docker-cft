# AMPLIFY Transfer CFT Docker

AMPLIFY Transfer CFT 3.6 Docker image

## Before you begin

This document assumes a basic understanding of core Docker concepts such as containers, container images, and basic Docker commands.
If needed, see [Get started with Docker](https://docs.docker.com/get-started/) for a primer on container basics.

### Prerequisites

- Docker version 17.11 or higher

## How to use the Transfer CFT Dockerfile file

The Dockerfile contains all commands required to assemble a Transfer CFT image.

### Dockerfile parameters

The following parameters are available in the Dockerfile file. Use these parameters to customize the Transfer CFT image and service. The values can be a string, number, or null.
  
 **Parameter**             |  **Values**  |  **Description**
 ------------------------- | :----------: | --------------- 
CFT_FQDN                   |  \<string>   |  Host address of the local server.
CFT_INSTANCE_ID            |  \<string>   |  Name of the Transfer CFT instance.
CFT_INSTANCE_GROUP         |  \<string>   |  The Transfer CFT instance's group.
CFT_CATALOG_SIZE           |  \<number>   |  Catalog size.
CFT_COM_SIZE               |  \<number>   |  Communication file size.
CFT_PESIT_PORT             |  \<number>   |  Port number of the PeSIT protocol called PESITANY.
CFT_PESITSSL_PORT          |  \<number>   |  Port number of the PeSIT protocol called PESITSSL.
CFT_SFTP_PORT              |  \<number>   |  Port number of the SFTP protocol.
CFT_COMS_PORT              |  \<number>   |  Port number of the synchronous communication media called COMS.
CFT_COPILOT_PORT           |  \<number>   |  Port number for the Transfer CFT UI server that listens for incoming unsecured and secured (SSL) connections.
CFT_COPILOT_CG_PORT        |  \<number>   |  Port number for the Transfer CFT UI server used to connect to Central Governance.
CFT_RESTAPI_PORT           |  \<number>   |  Port number used to connect to the REST API server.
CFT_CG_ENABLE              |  "YES"/"NO"  |  Connectivity with Central Governance.
CFT_CG_HOST                |  \<string>   |  Host address of the Central Governance server.
CFT_CG_PORT                |  \<number>   |  Listening port of the Central Governance server.
CFT_CG_SHARED_SECRET       |  \<string>   |  Shared secret needed to register with the Central Governance server.
CFT_CG_POLICY              |  \<string>   |  Central Governance configuration policy to apply at Transfer CFT registration.
CFT_CG_PERIODICITY         |  \<number>   |  Central Governance interval between notifications.
CFT_CG_AGENT_NAME          |  \<string>   |  Central Governance agent name.
CFT_JVM                    |  \<number>   |  Amount of memory that the Secure Relay JVM can use.
CFT_KEY                    |  \<string>   |  A command that returns the Transfer CFT license key.
CFT_CFTDIRRUNTIME          |  \<string>   |  Location of the Transfer CFT runtime.

### How to build the Docker image

#### 1. Build the Docker image from your Dockerfile

##### 1.1. Build using a local Transfer CFT package

1) Download the Transfer CFT product package from [Axway Support](https://support.axway.com/)

The Dockerfile is compatible with Transfer CFT 3.6 base version and its updates.

From the [Axway Support](https://support.axway.com/), download the latest package for linux-x86-64.

2) Build the Docker image from your Dockerfile

From the folder where the Dockerfile is located, using the downloaded package as a build argument, run the command:
```console
docker build --build-arg INSTALL_KIT=Transfer_CFT_3.6_Install_linux-x86-64_BN12603000.zip -t cft/cft:3.6 .
```

##### 1.2. Build using a Transfer CFT package stored on your own HTTP server

1) Download the Transfer CFT product package from [Axway Support](https://support.axway.com/)

The Dockerfile is compatible with Transfer CFT 3.6 base version and its updates.

From the [Axway Support](https://support.axway.com/), download the latest package for linux-x86-64 and make it available in your network.

2) Build the Docker image from your Dockerfile

From the folder where the Dockerfile is located, run the command:

```console
docker build --build-arg URL_BASE=https://network.package.location/ -t cft/cft:3.6 .
```
*Note* You can customize the VERSION_BASE, RELEASE_BASE arguments from the Dockerfile to build a Docker image based on a different Transfer CFT version/level.

#### 2. Check that the Docker image is successfully created

Run the command:

```console
docker images --filter reference=cft/cft
```

You should get an output like:
```console

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
cft/cft           3.6                 6049bb6d4d17        3 days ago          622MB
```

### Connecting to interfaces

When you start the Transfer CFT container for the first time, a user/password pair is created, which you can find in the container logs.

The information displays as:

```
    ------------------------
        UI user created 
    username: admin 
    pass: PASS
    ------------------------
```

Access the Transfer CFT REST API documentation by connecting to: 

```
https://CFT_FQDN:1768/cft/api/v1/ui/index.html
```

Access the Transfer CFT UI by connecting to:

```
https://CFT_FQDN:1768/cft/ui
```

Access the former Transfer CFT UI (Copilot UI) by connecting to:

```
http://CFT_FQDN:1766/index.html
```

## Copyright

Copyright (c) 2019 Axway Software SA and its affiliates. All rights reserved.

## License

All files in this repository are licensed by Axway Software SA and its affiliates under the Apache License, Version 2.0, available at http://www.apache.org/licenses/.
