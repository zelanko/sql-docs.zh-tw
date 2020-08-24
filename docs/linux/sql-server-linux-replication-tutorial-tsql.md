---
title: 教學課程：設定複寫 (T-SQL)
description: 在 Linux 上，使用 Transact-SQL (T-SQL) 搭配兩個 SQL Server 執行個體來設定 SQL Server 快照式複寫。
ms.custom: seo-dt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
titleSuffix: SQL Server on Linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: cc1a6ab577a471b69394cf35149f457972aece68
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088835"
---
# <a name="configure-replication-with-t-sql"></a>搭配 T-SQL 設定複寫

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)] 

在本教學課程中，於 Linux 上使用 Transact-SQL 搭配兩個 SQL Server 執行個體來設定 SQL Server 快照式複寫。 發行者和散發者將會是相同的執行個體，且訂閱者將會位於個別的執行個體上。

> [!div class="checklist"]
> * 在 Linux 上啟用 SQL Server 複寫代理程式
> * 建立範例資料庫
> * 針對 SQL Server 代理程式存取設定快照集資料夾
> * 設定散發者
> * 設定發行者
> * 設定發行集和發行項
> * 設定訂閱者 
> * 執行複寫作業

所有複寫設定都可以搭配[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)來加以設定。

## <a name="prerequisites"></a>Prerequisites
若要完成本教學課程，您將會需要：

- 具有 Linux 上的 SQL Server 最新版本的兩個 SQL Server 執行個體
- 用來發出 T-SQL 查詢以設定複寫的工具，例如 SQLCMD 或 SSMS

   請參閱[使用 SSMS 來管理 Linux 上的 SQL Server](./sql-server-linux-manage-ssms.md)。

   >[!NOTE]
   >[!INCLUDE[SQL Server 2017](../includes/sssqlv14-md.md)] ([CU18](https://support.microsoft.com/help/4527377)) 和更新版本支援 Linux 上的 SQL Server 執行個體進行 SQL Server 複寫。

## <a name="detailed-steps"></a>詳細步驟

1. 在 Linux 上啟用 SQL Server 複寫代理程式。 在兩部主機電腦上，於終端機中執行下列命令。 

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   sudo systemctl restart mssql-server
   ```

1. 建立範例資料庫與資料表。 在發行者上，建立範例資料庫和資料表以作為發行的發行項。

   ```sql
   CREATE DATABASE Sales
   GO
   USE [SALES]
   GO 
   CREATE TABLE CUSTOMER([CustomerID] [int] NOT NULL, [SalesAmount] [decimal] NOT NULL)
   GO 
   INSERT INTO CUSTOMER (CustomerID, SalesAmount) VALUES (1,100),(2,200),(3,300)
   ```

   在另一個 SQL Server 執行個體 (訂閱者) 上建立資料庫以接收發行項。

   ```sql
   CREATE DATABASE Sales
   GO
   ```

1. 建立快照集資料夾以供 SQL Server Agent 對其進行讀取/寫入，在散發者上，建立快照集資料夾並將存取權授與 'mssql' 使用者 

   ```bash
   sudo mkdir /var/opt/mssql/data/ReplData/
   sudo chown mssql /var/opt/mssql/data/ReplData/
   sudo chgrp mssql /var/opt/mssql/data/ReplData/
   ```

1. 設定散發者。 在此範例中，發行者也會是散發者。 在發行者上執行下列命令以同時設定散發執行個體。

   ```sql
   DECLARE @distributor AS sysname
   DECLARE @distributorlogin AS sysname
   DECLARE @distributorpassword AS sysname
   -- Specify the distributor name. Use 'hostname' command on in terminal to find the hostname
   SET @distributor = N'<distributor instance name>'--in this example, it will be the name of the publisher
   SET @distributorlogin = N'<distributor login>'
   SET @distributorpassword = N'<distributor password>'
   -- Specify the distribution database. 
   
   use master
   exec sp_adddistributor @distributor = @distributor -- this should be the hostname

   -- Log into distributor and create Distribution Database. In this example, our publisher and distributor is on the same host
   exec sp_adddistributiondb @database = N'distribution', @log_file_size = 2, @deletebatchsize_xact = 5000, @deletebatchsize_cmd = 2000, @security_mode = 0, @login = @distributorlogin, @password = @distributorpassword
   GO

   DECLARE @snapshotdirectory AS nvarchar(500)
   SET @snapshotdirectory = N'/var/opt/mssql/data/ReplData/'

   -- Log into distributor and create Distribution Database. In this example, our publisher and distributor is on the same host
   use [distribution] 
   if (not exists (select * from sysobjects where name = 'UIProperties' and type = 'U ')) 
          create table UIProperties(id int) 
   if (exists (select * from ::fn_listextendedproperty('SnapshotFolder', 'user', 'dbo', 'table', 'UIProperties', null, null))) 
          EXEC sp_updateextendedproperty N'SnapshotFolder', @snapshotdirectory, 'user', dbo, 'table', 'UIProperties' 
   else 
         EXEC sp_addextendedproperty N'SnapshotFolder', @snapshotdirectory, 'user', dbo, 'table', 'UIProperties'
   GO
   ```

1. 設定發行者。 在發行者上執行下列 TSQL 命令。

   ```sql
   DECLARE @publisher AS sysname
   DECLARE @distributorlogin AS sysname
   DECLARE @distributorpassword AS sysname
   -- Specify the distributor name. Use 'hostname' command on in terminal to find the hostname
   SET @publisher = N'<instance name>' 
   SET @distributorlogin = N'<distributor login>'
   SET @distributorpassword = N'<distributor password>'
   -- Specify the distribution database. 

   -- Adding the distribution publishers
   exec sp_adddistpublisher @publisher = @publisher, 
   @distribution_db = N'distribution', 
   @security_mode = 0, 
   @login = @distributorlogin, 
   @password = @distributorpassword, 
   @working_directory = N'/var/opt/mssql/data/ReplData', 
   @trusted = N'false', 
   @thirdparty_flag = 0, 
   @publisher_type = N'MSSQLSERVER'
   GO
   ```

1. 設定發行集作業。 在發行者上執行下列 TSQL 命令。

   ```sql
   DECLARE @replicationdb AS sysname
   DECLARE @publisherlogin AS sysname
   DECLARE @publisherpassword AS sysname
   SET @replicationdb = N'Sales'
   SET @publisherlogin = N'<Publisher login>'
   SET @publisherpassword = N'<Publisher Password>'

   use [Sales]
   exec sp_replicationdboption @dbname = N'Sales', @optname = N'publish', @value = N'true'
   
   -- Add the snapshot publication
   exec sp_addpublication 
   @publication = N'SnapshotRepl', 
   @description = N'Snapshot publication of database ''Sales'' from Publisher ''<PUBLISHER HOSTNAME>''.',
   @retention = 0, 
   @allow_push = N'true', 
   @repl_freq = N'snapshot', 
   @status = N'active', 
   @independent_agent = N'true'

   exec sp_addpublication_snapshot @publication = N'SnapshotRepl', 
   @frequency_type = 1, 
   @frequency_interval = 1, 
   @frequency_relative_interval = 1, 
   @frequency_recurrence_factor = 0, 
   @frequency_subday = 8, 
   @frequency_subday_interval = 1, 
   @active_start_time_of_day = 0,
   @active_end_time_of_day = 235959, 
   @active_start_date = 0, 
   @active_end_date = 0, 
   @publisher_security_mode = 0, 
   @publisher_login = @publisherlogin, 
   @publisher_password = @publisherpassword
   ```

1. 從 Sales 資料表建立發行項：在發行者上執行下列 TSQL 命令。

   ```sql
   use [Sales]
   exec sp_addarticle 
   @publication = N'SnapshotRepl', 
   @article = N'customer', 
   @source_owner = N'dbo', 
   @source_object = N'customer', 
   @type = N'logbased', 
   @description = null, 
   @creation_script = null, 
   @pre_creation_cmd = N'drop', 
   @schema_option = 0x000000000803509D,
   @identityrangemanagementoption = N'manual', 
   @destination_table = N'customer', 
   @destination_owner = N'dbo', 
   @vertical_partition = N'false'
   ```

1. 設定訂閱。 在發行者上執行下列 TSQL 命令。

   ```sql
   DECLARE @subscriber AS sysname
   DECLARE @subscriber_db AS sysname
   DECLARE @subscriberLogin AS sysname
   DECLARE @subscriberPassword AS sysname
   SET @subscriber = N'<Instance Name>' -- for example, MSSQLSERVER
   SET @subscriber_db = N'Sales'
   SET @subscriberLogin = N'<Subscriber Login>'
   SET @subscriberPassword = N'<Subscriber Password>'

   use [Sales]
   exec sp_addsubscription 
   @publication = N'SnapshotRepl', 
   @subscriber = @subscriber,
   @destination_db = @subscriber_db, 
   @subscription_type = N'Push', 
   @sync_type = N'automatic', 
   @article = N'all', 
   @update_mode = N'read only', 
   @subscriber_type = 0

   exec sp_addpushsubscription_agent 
   @publication = N'SnapshotRepl', 
   @subscriber = @subscriber,
   @subscriber_db = @subscriber_db, 
   @subscriber_security_mode = 0, 
   @subscriber_login = @subscriberLogin,
   @subscriber_password = @subscriberPassword,
   @frequency_type = 1,
   @frequency_interval = 0, 
   @frequency_relative_interval = 0, 
   @frequency_recurrence_factor = 0, 
   @frequency_subday = 0, 
   @frequency_subday_interval = 0, 
   @active_start_time_of_day = 0, 
   @active_end_time_of_day = 0, 
   @active_start_date = 0, 
   @active_end_date = 19950101
   GO
   ```

1. 執行複寫代理程式作業。 執行下列查詢以取得作業清單：

   ```sql
   SELECT name, date_modified FROM msdb.dbo.sysjobs order by date_modified desc
   ```

   執行快照式複寫作業以產生快照集：

   ```sql
   USE msdb;   
   --generate snapshot of publications, for example
   EXEC dbo.sp_start_job N'PUBLISHER-PUBLICATION-SnapshotRepl-1'
   GO
   ```

   執行快照式複寫作業以產生快照集：

   ```sql
   USE msdb;
   --distribute the publication to subscriber, for example
   EXEC dbo.sp_start_job N'DISTRIBUTOR-PUBLICATION-SnapshotRepl-SUBSCRIBER'
   GO
   ```

1. 連線訂閱者並查詢複寫資料。    

   在訂閱者上，執行下列查詢來檢查複寫是否正常運作：

   ```sql
   SELECT * from [Sales].[dbo].[CUSTOMER]
   ```

在本教學課程中，您已在 Linux 上使用 Transact-SQL 搭配兩個 SQL Server 執行個體來設定 SQL Server 快照式複寫。

> [!div class="checklist"]
> * 在 Linux 上啟用 SQL Server 複寫代理程式
> * 建立範例資料庫
> * 針對 SQL Server 代理程式存取設定快照集資料夾
> * 設定散發者
> * 設定發行者
> * 設定發行集和發行項
> * 設定訂閱者 
> * 執行複寫作業

## <a name="see-also"></a>另請參閱

如需複寫的詳細資訊，請參閱 [SQL Server 複寫文件](../relational-databases/replication/sql-server-replication.md)。

## <a name="next-steps"></a>後續步驟

[概念：Linux 上的 SQL Server 複寫](sql-server-linux-replication.md)

[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。
