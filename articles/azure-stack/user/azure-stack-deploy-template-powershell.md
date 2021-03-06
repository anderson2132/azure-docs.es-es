---
title: "Implementación de plantillas con PowerShell en Azure Stack | Microsoft Docs"
description: "Aprenda a implementar una máquina virtual mediante una plantilla de Resource Manager y PowerShell."
services: azure-stack
documentationcenter: 
author: brenduns
manager: femila
editor: 
ms.assetid: 12fe32d7-0a1a-4c02-835d-7b97f151ed0f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/25/2017
ms.author: brenduns
ms.reviewer: 
ms.openlocfilehash: d271b155d65a7dd95a92262da338cf3a272d140b
ms.sourcegitcommit: d1f35f71e6b1cbeee79b06bfc3a7d0914ac57275
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/22/2018
---
# <a name="deploy-templates-in-azure-stack-using-powershell"></a>Implementación de plantillas en Azure Stack con PowerShell

*Se aplica a: sistemas integrados de Azure Stack y Kit de desarrollo de Azure Stack*

Use PowerShell para implementar las plantillas de Azure Resource Manager en el Kit de desarrollo de Azure Stack.  Las plantillas de Resource Manager implementan y aprovisionan todos los recursos para su aplicación en una única operación coordinada.

## <a name="run-azurerm-powershell-cmdlets"></a>Ejecución de cmdlets de AzureRM PowerShell
En este ejemplo, debe ejecutar un script para implementar una máquina virtual en el Kit de desarrollo de Azure Stack mediante una plantilla de Resource Manager.  Antes de continuar, asegúrese de haber [configurado PowerShell](azure-stack-powershell-configure-user.md)  

El disco duro virtual usado en esta plantilla de ejemplo es WindowsServer-2012-R2-Datacenter.

1. Vaya a <http://aka.ms/AzureStackGitHub>, busque la plantilla **101-simple-windows-vm** y guárdela en la siguiente ubicación: c:\\plantillas\\azuredeploy-101-simple-windows-vm.json.
2. En PowerShell, ejecute el siguiente script de implementación. Reemplace *username* y *password* por su nombre de usuario y contraseña. En usos posteriores, incremente el valor del parámetro *$myNum* para evitar sobrescribir su implementación.
   
   ```PowerShell
       # Set Deployment Variables
       $myNum = "001" #Modify this per deployment
       $RGName = "myRG$myNum"
       $myLocation = "local"
   
       # Create Resource Group for Template Deployment
       New-AzureRmResourceGroup -Name $RGName -Location $myLocation
   
       # Deploy Simple IaaS Template
       New-AzureRmResourceGroupDeployment `
           -Name myDeployment$myNum `
           -ResourceGroupName $RGName `
           -TemplateFile c:\templates\azuredeploy-101-simple-windows-vm.json `
           -NewStorageAccountName mystorage$myNum `
           -DnsNameForPublicIP mydns$myNum `
           -AdminUsername <username> `
           -AdminPassword ("<password>" | ConvertTo-SecureString -AsPlainText -Force) `
           -VmName myVM$myNum `
           -WindowsOSVersion 2012-R2-Datacenter
   ```
3. Abra el portal de Azure Stack, haga clic en **Examinar**, haga clic en **Máquinas virtuales** y busque la nueva máquina virtual (*myDeployment001*).


## <a name="next-steps"></a>pasos siguientes
[Implementación de plantillas con Visual Studio](azure-stack-deploy-template-visual-studio.md)

