---
title: "Esquema de suscripción de Azure Event Grid"
description: "Describe las propiedades de suscripción a un evento con Azure Event Grid."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 03/09/2018
ms.author: babanisa
ms.openlocfilehash: 888196225ec5998405113842344469d02a2cf5c7
ms.sourcegitcommit: a0be2dc237d30b7f79914e8adfb85299571374ec
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2018
---
# <a name="event-grid-subscription-schema"></a>Esquema de suscripción de Event Grid

Para crear una suscripción de Event Grid, se envía una solicitud a la operación de suscripción Crear evento. Utilice el siguiente formato:

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2018-01-01
``` 

Por ejemplo, con el fin de crear una suscripción de eventos para una cuenta de almacenamiento denominada "`examplestorage`" en un grupo de recursos llamado `examplegroup`, utilice el formato siguiente:

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2018-01-01
``` 

En el artículo se describen las propiedades y el esquema del cuerpo de la solicitud.
 
## <a name="event-subscription-properties"></a>Propiedades de la suscripción de eventos

| Propiedad | type | DESCRIPCIÓN |
| -------- | ---- | ----------- |
| de destino | objeto | El objeto que define el punto de conexión. |
| filter | objeto | Un campo opcional para filtrar los tipos de eventos. |

### <a name="destination-object"></a>Objeto de destino

| Propiedad | type | DESCRIPCIÓN |
| -------- | ---- | ----------- |
| endpointType | string | El tipo de punto de conexión de la suscripción (webhook/HTTP, centro de eventos o cola). | 
| endpointUrl | string | Dirección URL de destino de los eventos en esta suscripción a eventos. | 

### <a name="filter-object"></a>Objeto de filtro

| Propiedad | type | DESCRIPCIÓN |
| -------- | ---- | ----------- |
| includedEventTypes | array | Realiza la correspondencia cuando el tipo de evento del mensaje de evento es una coincidencia exacta con uno de estos nombres de tipo de evento. Genera un error cuando el nombre del evento no coincide con los nombres de tipo de evento registrados para el origen del evento. El valor predeterminado coincide con todos los tipos de evento. |
| subjectBeginsWith | string | Un filtro de coincidencia de prefijo en el campo de asunto del mensaje del evento. El valor predeterminado o una cadena vacía coincide con todos los tipos de evento. | 
| subjectEndsWith | string | Un filtro de coincidencia de sufijo en el campo de asunto del mensaje del evento. El valor predeterminado o una cadena vacía coincide con todos los tipos de evento. |
| subjectIsCaseSensitive | string | Controla la coincidencia que distingue mayúsculas de minúsculas en los filtros. |


## <a name="example-subscription-schema"></a>Esquema de suscripción de ejemplo

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "Microsoft.Storage.BlobCreated", "Microsoft.Storage.BlobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a>Pasos siguientes

* Para ver una introducción a Event Grid, consulte el artículo acerca de [qué es Event Grid](overview.md).