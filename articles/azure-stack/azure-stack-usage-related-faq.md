---
title: "Preguntas más frecuentes relacionadas con el uso de API | Microsoft Docs"
description: "Lista de medidores de Azure Stack, en comparación con los códigos de error, el tiempo notificado y el tiempo de uso y la API de uso de Azure."
services: azure-stack
documentationcenter: 
author: brenduns
manager: femila
editor: 
ms.assetid: 847f18b2-49a9-4931-9c09-9374e932a071
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2018
ms.author: alfredop
ms.openlocfilehash: 855d74698f2109fa426d34044cbc89b83c224e6f
ms.sourcegitcommit: 9d317dabf4a5cca13308c50a10349af0e72e1b7e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="frequently-asked-questions-in-azure-stack-usage-api"></a>Preguntas frecuentes sobre la API de uso de Azure Stack
En este artículo se responde a algunas preguntas frecuentes sobre la API de uso de Azure Stack.

## <a name="what-meter-ids-can-i-see"></a>¿Qué identificadores de medidor veo?
Se informa del uso para los siguientes proveedores de recursos:

| **Proveedor de recursos** | **Id. de medidor** | **Nombre de medidor** | **Unidad** | **Información adicional** |
| --- | --- | --- | --- | --- |
| **Red** |F271A8A388C44D93956A063E1D2FA80B |Uso de la dirección IP estática |Direcciones IP| Número de direcciones IP usadas. Si llama a la API de utilización con una granularidad diaria, el medidor devolverá la dirección IP multiplicada por el número de horas. |
| |9E2739BA86744796B465F64674B822BA |Uso de la dirección IP dinámica |Direcciones IP| Número de direcciones IP usadas. Si llama a la API de utilización con una granularidad diaria, el medidor devolverá la dirección IP multiplicada por el número de horas. |
| **Storage** |B4438D5D-453B-4EE1-B42A-DC72E377F1E4 |TableCapacity |GB\*horas |Capacidad total utilizada por las tablas |
| |B5C15376-6C94-4FDD-B655-1A69D138ACA3 |PageBlobCapacity |GB\*horas |Capacidad total consumida por blobs en páginas |
| |B03C6AE7-B080-4BFA-84A3-22C800F315C6 |QueueCapacity |GB\*horas |Capacidad total consumida por la cola |
| |09F8879E-87E9-4305-A572-4B7BE209F857 |BlockBlobCapacity |GB\*horas |Capacidad total consumida por blobs en bloques |
| |B9FF3CD0-28AA-4762-84BB-FF8FBAEA6A90 |TableTransactions |Recuento de solicitudes en decenas de millar |Solicitudes de Table service (por decenas de millar) |
| |50A1AEAF-8ECA-48A0-8973-A5B3077FEE0D |TableDataTransIn |Datos de entrada en GB |Entrada de datos de Table service en GB |
| |1B8C1DEC-EE42-414B-AA36-6229CF199370 |TableDataTransOut |Salida en GB |Salida de datos de Table service en GB |
| |43DAF82B-4618-444A-B994-40C23F7CD438 |BlobTransactions |Número de solicitudes en decenas de millar |Solicitudes de Blob service (por decenas de millar) |
| |9764F92C-E44A-498E-8DC1-AAD66587A810 |BlobDataTransIn |Datos de entrada en GB |Entrada de datos de Blob service en GB |
| |3023FEF4-ECA5-4D7B-87B3-CFBC061931E8 |BlobDataTransOut |Salida en GB |Salida de datos de Blob service en GB |
| |EB43DD12-1AA6-4C4B-872C-FAF15A6785EA |QueueTransactions |Número de solicitudes en decenas de millar |Solicitudes de Queue service (por decenas de millar) |
| |E518E809-E369-4A45-9274-2017B29FFF25 |QueueDataTransIn |Datos de entrada en GB |Entrada de datos de Queue service en GB |
| |DD0A10BA-A5D6-4CB6-88C0-7D585CEF9FC2 |QueueDataTransOut |Salida en GB |Salida de datos de Queue service en GB |
| **Proveedor de recursos de SQL**            | CBCFEF9A-B91F-4597-A4D3-01FE334BED82 | DatabaseSizeHourSqlMeter   | MB\*horas   | Capacidad total de BD en la creación. Si llama a la API de utilización con una granularidad diaria, el medidor devolverá los MB multiplicados por el número de horas. |
| **Proveedor de recursos de MySql**          | E6D8CFCD-7734-495E-B1CC-5AB0B9C24BD3 | DatabaseSizeHourMySqlMeter | MB\*horas    | Capacidad total de BD en la creación. Si llama a la API de utilización con una granularidad diaria, el medidor devolverá los MB multiplicados por el número de horas. |
| **Proceso** |FAB6EB84-500B-4A09-A8CA-7358F8BBAEA5 |Horas de tamaño de la máquina virtual base |Total de núcleos virtuales | Número de núcleos virtuales multiplicado por las horas que se ejecutó la VM |
| |9CD92D4C-BAFD-4492-B278-BEDC2DE8232A |Horas de tamaño de la máquina virtual Windows |Total de núcleos virtuales | Número de núcleos virtuales multiplicado por las horas que se ejecutó la VM |
| |6DAB500F-A4FD-49C4-956D-229BB9C8C793 |Horas de tamaño de la máquina virtual |Horas de la máquina virtual |Captura de la máquina virtual base y Windows. No se ajusta para los núcleos |
| **Key Vault** |EBF13B9F-B3EA-46FE-BF54-396E93D48AB4 |Transacciones de Key Vault | Recuento de solicitudes en decenas de millar| Número de solicitudes de API de REST recibidas por plan de datos de Key Vault |
| **App Service** |190C935E-9ADA-48FF-9AB8-56EA1CF9ADAA  | App Service   | Total de núcleos virtuales  | Número de núcleos virtuales utilizados para ejecutar el servicio de aplicaciones |
|             | 67CC4AFC-0691-48E1-A4B8-D744D1FEDBDE | Funciones: solicitudes de proceso      | 10 solicitudes              | Se aplica a funciones  |
|             | 957E9F36-2C14-45A1-B6A1-1723EF71A01D | Horas de App Service compartido          | 1 hora                   |                       |
|             | 539CDEC7-B4F5-49F6-AAC4-1F15CFF0EDA9 | Horas de App Service gratuito            | 1 hora                   |                       |
|             | 88039D51-A206-3A89-E9DE-C5117E2D10A6 | Horas de App Service para instancias pequeñas estándar  | 1 hora                   |                       |
|             | 83A2A13E-4788-78DD-5D55-2831B68ED825 | Horas de App Service para instancias medianas estándar | 1 hora                   |                       |
|             | 1083B9DB-E9BB-24BE-A5E9-D6FDD0DDEFE6 | Horas de App Service para instancias grandes estándar  | 1 hora                   |                       |
|             | 264ACB47-AD38-47F8-ADD3-47F01DC4F473 | SSL SNI                           | Por enlace SSL SNI      | Se aplica a App Service |
|             | 60B42D72-DC1C-472C-9895-6C516277EDB4 | SSL de IP                            | Por enlace SSL basada en IP | Se aplica a App Service |

## <a name="how-do-the-azure-stack-usage-apis-compare-to-the-azure-usage-apihttpsmsdnmicrosoftcomlibraryazure1ea5b323-54bb-423d-916f-190de96c6a3c-currently-in-public-preview"></a>¿Cómo se comparan las API de uso de Azure Stack con la [API de uso de Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) (actualmente en versión preliminar pública)?
* La API de uso de inquilinos es coherente con la API de Azure, con una excepción: actualmente, la marca *showDetails* no se admite en Azure Stack.
* La API de uso de proveedor solo se aplica a Azure Stack.
* Actualmente, la [API RateCard](https://msdn.microsoft.com/en-us/library/azure/mt219004.aspx) disponible en Azure no se encuentra disponible en Azure Stack.

## <a name="what-is-the-difference-between-usage-time-and-reported-time"></a>¿Cuál es la diferencia entre el tiempo notificado y el tiempo de uso?
Los informes de datos de uso tienen dos valores de tiempo principales:

* **Hora de notificación**. La hora cuando el evento de uso entró en el sistema de uso
* **Tiempo de uso**. El tiempo durante el que se ha usado el recurso de Azure Stack

Puede que vea una discrepancia en los valores de tiempo de uso y tiempo notificado para un evento de uso específico. El retraso puede ser de hasta varias horas en cualquier entorno.

Actualmente, solo se puede consultar mediante el *tiempo notificado*.

## <a name="what-do-these-usage-api-error-codes-mean"></a>¿Qué significan estos códigos de error de la API de uso?
| **Código de estado HTTP** | **Código de error** | **Descripción** |
| --- | --- | --- |
| 400/Solicitud incorrecta |*NoApiVersion* |No se proporcionó el parámetro de consulta de la *api-version*. |
| 400/Solicitud incorrecta |*InvalidProperty* |Falta una propiedad o hay un valor no válido. El mensaje en el código de error en el cuerpo de respuesta identifica la propiedad que falta. |
| 400/Solicitud incorrecta |*RequestEndTimeIsInFuture* |El valor de *ReportedEndTime* no puede ser un tiempo futuro. En el futuro no se permiten valores para este argumento. |
| 400/Solicitud incorrecta |*SubscriberIdIsNotDirectTenant* |Una llamada de API del proveedor ha usado un identificador de suscripción que no es un inquilino válido del autor de la llamada. |
| 400/Solicitud incorrecta |*SubscriptionIdMissingInRequest* |Falta el identificador de suscripción del autor de la llamada. |
| 400/Solicitud incorrecta |*InvalidAggregationGranularity* |Se solicitó una granularidad de agregación no válida. Los valores válidos son daily y hourly. |
| 503 |*ServiceUnavailable* |Se produjo un error recuperable porque el servicio está ocupado o la llamada se está limitando. |

## <a name="next-steps"></a>Pasos siguientes
[Facturación y contracargo del cliente en Azure Stack](azure-stack-billing-and-chargeback.md)

[API de uso de recursos del proveedor](azure-stack-provider-resource-api.md)

[API de uso de recursos del inquilino](azure-stack-tenant-resource-usage-api.md)
