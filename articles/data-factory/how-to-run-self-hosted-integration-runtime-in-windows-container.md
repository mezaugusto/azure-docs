---
title: How to run Self-Hosted Integration Runtime in Windows container
description: Learn about how to run Self-Hosted Integration Runtime in Windows container.

ms.author: lle
author: lrtoyou1223
ms.service: data-factory
ms.subservice: integration-runtime
ms.topic: conceptual
ms.custom: seo-lt-2019
ms.date: 01/28/2022
---

# How to run Self-Hosted Integration Runtime in Windows container

[!INCLUDE[appliesto-adf-asa-md](includes/appliesto-adf-asa-md.md)]

This article will explain how to run Self-Hosted Integration Runtime in Windows container.
Azure Data Factory are delivering the official windows container support of Self-Hosted Integration Runtime. You can download the docker build source code and combine the building and running process in your own continuous delivery pipeline. 

## Prerequisites 
- [Windows container requirements](/virtualization/windowscontainers/deploy-containers/system-requirements)
- Docker Version 2.3 and later 
- Self-Hosted Integration Runtime Version 5.2.7713.1 and later 
## Get started 
1.	Install Docker and enable Windows Container 
2.	Download the source code from https://github.com/Azure/Azure-Data-Factory-Integration-Runtime-in-Windows-Container
3.	Download the latest version SHIR in ‘SHIR’ folder 
4.	Open your folder in the shell: 
```console
cd "yourFolderPath"
```

5.	Build the windows docker image: 
```console
docker build . -t "yourDockerImageName" 
```
6.	Run docker container: 
```console
docker run -d -e NODE_NAME="irNodeName" -e AUTH_KEY="IR_AUTHENTICATION_KEY" -e ENABLE_HA=true -e HA_PORT=8060 "yourDockerImageName"    
```
> [!NOTE]
> AUTH_KEY is mandatory for this command. NODE_NAME, ENABLE_HA and HA_PORT are optional. If you don't set the value, the command will use default values. The default value of ENABLE_HA is false and HA_PORT is 8060.

## Container health check 
After 120 seconds startup period, the health checker will run periodically every 30 seconds. It will provide the IR health status to container engine. 

## Limitations
Currently we don't support below features when running Self-Hosted Integration Runtime in Windows container:
- HTTP proxy 
- Encrypted Node-node communication with TLS/SSL certificate 
- Generate and import backup 
- Daemon service 
- Auto update 

### Next steps
- Review [integration runtime concepts in Azure Data Factory](./concepts-integration-runtime.md).
- Learn how to [create a self-hosted integration runtime in the Azure portal](./create-self-hosted-integration-runtime.md).
