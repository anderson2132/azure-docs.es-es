---
title: "Volcado y restauración en Azure Database for PostgreSQL"
description: "Describe cómo extraer una base de datos de PostgreSQL en un archivo de volcado y cómo restaurar desde un archivo creado por pg_dump en Azure Database for PostgreSQL."
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: 6ea839c10bffc9a024af38132081f2c9bd7dfc0a
ms.sourcegitcommit: c765cbd9c379ed00f1e2394374efa8e1915321b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2018
---
# <a name="migrate-your-postgresql-database-using-dump-and-restore"></a>Migración de una base de datos de PostgreSQL mediante volcado y restauración
Puede usar [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) para extraer una base de datos de PostgreSQL a un archivo de volcado y [pg_restore](https://www.postgresql.org/docs/9.3/static/app-pgrestore.html) para restaurar la base de datos de PostgreSQL desde un archivo de almacenamiento creado por pg_dump.

## <a name="prerequisites"></a>requisitos previos
Para seguir esta guía, necesitará:
- Un [servidor de Azure Database for PostgreSQL](quickstart-create-server-database-portal.md) con reglas de firewall para permitir el acceso a las bases de datos que hay en él.
- Utilidades de línea de comandos [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) y [pg_restore](https://www.postgresql.org/docs/9.6/static/app-pgrestore.html) instaladas

Siga estos pasos para realizar un volcado y restaurar la base de datos de PostgreSQL:

## <a name="create-a-dump-file-using-pgdump-that-contains-the-data-to-be-loaded"></a>Creación de un archivo de volcado mediante pg_dump con los datos que se van a cargar
Para hacer una copia de seguridad de una base de datos de PostgreSQL existente en el entorno local o en una máquina virtual, ejecute el comando siguiente:
```bash
pg_dump -Fc -v --host=<host> --username=<name> --dbname=<database name> > <database>.dump
```
Por ejemplo, si tiene un servidor local y una base de datos llamada **testdb** en él:
```bash
pg_dump -Fc -v --host=localhost --username=masterlogin --dbname=testdb > testdb.dump
```

## <a name="restore-the-data-into-the-target-azure-database-for-postrgesql-using-pgrestore"></a>Restauración de los datos a la instancia de Azure Database for PostrgeSQL con pg_restore
Después de crear la base de datos de destino, puede usar el comando pg_restore y el parámetro -d, --dbname para restaurar los datos en la base de datos de destino desde el archivo de volcado.
```bash
pg_restore -v –-host=<server name> --port=<port> --username=<user@servername> --dbname=<target database name> <database>.dump
```
En este ejemplo, restaure los datos del archivo de volcado **testdb.dump** en la base de datos **mypgsqldb** en el servidor de destino **mydemoserver.postgres.database.azure.com**.
```bash
pg_restore -v --host=mydemoserver.postgres.database.azure.com --port=5432 --username=mylogin@mydemoserver --dbname=mypgsqldb testdb.dump
```

## <a name="next-steps"></a>pasos siguientes
- Para migrar una base de datos de PostgreSQL mediante exportación e importación, consulte [Migración de una base de datos de PostgreSQL mediante exportación e importación](howto-migrate-using-export-and-import.md).