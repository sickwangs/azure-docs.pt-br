---
title: Migrar um banco de dados usando Importar e Exportar no Banco de Dados do Azure para PostgreSQL | Microsoft Docs
description: Descreve como extrair um banco de dados PostgreSQL para um arquivo de script e importar os dados para o banco de dados de destino desse arquivo.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 11/03/2017
ms.openlocfilehash: 937423d0b844f6ce30e532bbae12b85071a6f8d4
ms.sourcegitcommit: 38c9176c0c967dd641d3a87d1f9ae53636cf8260
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2017
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a>Migrar seu banco de dados PostgreSQL usando exportar e importar
Use [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) para extrair um banco de dados PostgreSQL para um arquivo de script, e [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) para importar os dados para o banco de dados de destino desse arquivo.

## <a name="prerequisites"></a>Pré-requisitos
Para seguir este guia de instruções, você precisa:
- Um [Servidor de Banco de Dados do Azure para PostgreSQL](quickstart-create-server-database-portal.md) com regras de firewall a fim de permitir o acesso e um banco de dados sob ele.
- O utilitário de linha de comando [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) instalado
- O utilitário de linha de comando [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) instalado

Execute estas etapas para exportar e importar o banco de dados PostgreSQL.

## <a name="create-a-script-file-using-pgdump-that-contains-the-data-to-be-loaded"></a>Criar um arquivo de script usando pg_dump que contém os dados a serem carregados
Para exportar seu banco de dados PostgreSQL existente localmente ou em uma VM para um arquivo de script sql, execute o seguinte comando em seu ambiente existente:
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
Por exemplo, se você tiver um servidor local e um banco de dados chamado **testdb** nele:
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-the-data-on-target-azure-database-for-postrgesql"></a>Importar os dados no Banco de Dados do Azure de destino para PostrgeSQL
Você pode usar a linha de comando psql e o parâmetro --dbname (-d) para importar os dados para o servidor do Banco de Dados do Azure para PostgreSQL e carregar o arquivo sql.
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
Este exemplo usa um utilitário psql e um arquivo de script chamado **testdb.sql** da etapa anterior para importar dados para o banco de dados **mypgsqldb** no servidor de destino **mypgserver-20170401.postgres.database.azure.com**.
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a>Próximas etapas
- Para migrar um banco de dados PostgreSQL usando dump e restore, veja [Migrar seu banco de dados PostgreSQL usando dump e restore](howto-migrate-using-dump-and-restore.md)
