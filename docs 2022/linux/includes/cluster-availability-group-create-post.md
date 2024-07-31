---
author: rwestMSFT
ms.author: randolphwest
ms.date: 07/16/2024
ms.service: sql
ms.subservice: linux
ms.topic: include
ms.custom:
  - linux-related-content
---
## Add a database to the availability group

Ensure that the database you add to the availability group is in the full recovery model and has a valid log backup. If your database is a test database or a newly created database, take a database backup. On the primary [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)], run the following [!INCLUDE [tsql-md](../../includes/tsql-md.md)] (T-SQL) script to create and back up a database called `db1`:

```sql
CREATE DATABASE [db1];
GO

ALTER DATABASE [db1]
SET RECOVERY FULL;
GO

BACKUP DATABASE [db1]
TO DISK = N'/var/opt/mssql/data/db1.bak';
```

On the primary [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] replica, run the following T-SQL script to add a database called `db1` to an availability group called `ag1`:

```sql
ALTER AVAILABILITY GROUP [ag1]
ADD DATABASE [db1];
```

### Verify that the database is created on the secondary servers

On each secondary [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] replica, run the following query to see if the `db1` database was created and is synchronized:

```sql
SELECT * FROM sys.databases
WHERE name = 'db1';
GO

SELECT DB_NAME(database_id) AS 'database',
    synchronization_state_desc
FROM sys.dm_hadr_database_replica_states;
GO
```
