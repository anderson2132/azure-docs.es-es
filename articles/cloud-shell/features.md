---
title: "Características de Bash en Azure Cloud Shell | Microsoft Docs"
description: "Introducción a las características de Bash en Azure Cloud Shell"
services: Azure
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: juluk
ms.openlocfilehash: 31c7c17b4604532eb513597db5db68a64ae10c93
ms.sourcegitcommit: 782d5955e1bec50a17d9366a8e2bf583559dca9e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2018
---
# <a name="features--tools-for-bash-in-azure-cloud-shell"></a>Características y herramientas para Bash en Azure Cloud Shell

[!INCLUDE [features-introblock](../../includes/cloud-shell-features-introblock.md)]

> [!TIP]
> También hay disponible un artículo sobre Características y herramientas en [PowerShell](features-powershell.md).

Bash in Cloud Shell se ejecuta en `Ubuntu 16.04 LTS`.

## <a name="features"></a>Características

### <a name="secure-automatic-authentication"></a>Protección de la autenticación automática

Bash en Cloud Shell autentica de forma segura y automática el acceso a la cuenta para la CLI de Azure 2.0.

### <a name="ssh-into-azure-linux-virtual-machines"></a>SSH en máquinas virtuales Linux de Azure

La creación de una máquina virtual Linux desde la CLI de Azure 2.0 puede crear una clave SSH predeterminada y colocarla en el directorio `$Home`. Colocar claves SSH en `$Home` permite conexiones SSH a VM Linux de Azure directamente desde Cloud Shell. Las claves se mantienen en acc_<user>.img en el recurso compartido de archivos. Use los procedimientos recomendados cuando use o comparta el acceso a las claves o al recurso compartido de archivos.

### <a name="home-persistence-across-sessions"></a>Persistencia de $Home entre sesiones

Para conservar archivos entre sesiones, la primera vez que se inicia Cloud Shell se explica cómo conectar un recurso compartido de archivos de Azure.
Una vez finalizado, Cloud Shell conectará automáticamente su almacenamiento (montado como `$Home\clouddrive`) para todas las sesiones futuras.
En Bash en Cloud Shell, además, el directorio `$Home` se conserva como .img en el recurso compartido de archivos de Azure.
Los archivos fuera de `$Home` y el estado de la máquina no se conservan entre sesiones.

[Obtenga más información sobre la persistencia de los archivos en Bash en Cloud Shell](persisting-shell-storage.md).

### <a name="deep-integration-with-open-source-tooling"></a>Profunda integración con herramientas de código abierto

Bash de Cloud Shell incluye autenticación configurada previamente para herramientas de código abierto, como Terraform y Ansible. Pruébelo desde los tutoriales de ejemplo.

## <a name="tools"></a>Herramientas

|Categoría   |NOMBRE   |
|---|---|
|Herramientas de Linux            |Bash<br> sh<br> tmux<br> dig<br>               |
|Herramientas de Azure            |[CLI de Azure 2.0](https://github.com/Azure/azure-cli) y [1.0](https://github.com/Azure/azure-xplat-cli)<br> [AzCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Batch Shipyard](https://github.com/Azure/batch-shipyard) <br> [CLI de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cli) <br> [blobxfer](https://github.com/Azure/blobxfer#blobxfer) |
|Editores de texto           |vim<br> nano<br> emacs       |
|Control de código fuente         |git                    |
|Herramientas de compilación            |make<br> maven<br> npm<br> pip         |
|Contenedores             |[CLI de Docker](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Helm](https://github.com/kubernetes/helm)<br> [CLI de DC/OS](https://github.com/dcos/dcos-cli)         |
|Bases de datos              |Cliente de MySQL<br> Cliente de PostgreSql<br> [Utilidad sqlcmd](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli) |
|Otros                  |Cliente de iPython<br> [CLI de Cloud Foundry](https://github.com/cloudfoundry/cli)<br> [Terraform](https://www.terraform.io/docs/providers/azurerm/)<br> [Ansible](https://www.ansible.com/microsoft-azure)| 

## <a name="language-support"></a>Compatibilidad con idiomas

|Idioma   |Versión   |
|---|---|
|.NET       |2.0.0       |
|Go         |1.9        |
|Java       |1.8        |
|Node.js    |8.9.4      |
|PowerShell |[6.0.0](https://github.com/PowerShell/powershell/releases)       |
|Python     |2.7 y 3.5 (predeterminadas)|

## <a name="next-steps"></a>Pasos siguientes
[Guía de inicio rápido de Bash en Cloud Shell](quickstart.md) <br>
[Más información sobre la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/)
