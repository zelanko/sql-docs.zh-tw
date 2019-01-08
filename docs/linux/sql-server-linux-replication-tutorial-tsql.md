---
title: 在 Linux 上設定 SQL Server 複寫 |Microsoft Docs
description: 本教學課程會示範如何在 Linux 上設定 SQL Server 快照式複寫。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9b1d86b56e836a9b9b7bf575d5e9353a962894ce
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52405313"
---
# <a name="configure-replication-with-t-sql"></a>使用 T-SQL 設定複寫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)] 

在本教學課程中，您將設定 SQL Server 快照式複寫在 Linux 上使用兩個使用 Transact SQL 的 SQL Server 執行個體。 「 發行者 」 與 「 散發者 」 會是相同的執行個體，和 「 訂閱者 」 會在個別的執行個體。

> [!div class="checklist"]
> * 啟用在 Linux 上的 SQL Server 複寫代理程式
> * 建立範例資料庫
> * 設定 SQL Server 代理程式存取的快照集資料夾
> * 設定散發者
> * 設定 「 發行者 」
> * 設定發行集和文件
> * 設定訂閱者 
> * 執行複寫作業

可設定所有的複寫組態[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

## <a name="prerequisites"></a>先決條件  
若要完成本教學課程中，您必須：

- Linux 上的 SQL Server 的最新版本的 SQL Server 兩個執行個體
- 若要設定複寫，例如 SQLCMD 或 SSMS 的發出 T-SQL 查詢的工具

  請參閱[使用 SSMS 管理 SQL Server on Linux](./sql-server-linux-manage-ssms.md)。

## <a name="detailed-steps"></a>詳細步驟

1. 啟用 Linux 啟用 「 SQL Server 代理程式使用複寫代理程式上的 SQL Server 複寫代理程式。 在這兩個主機電腦，請在終端機中執行下列命令。 

  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
  sudo systemctl restart mssql-server
  ```

1. 建立範例資料庫和資料表在您的發行者建立範例資料庫和資料表做為發行集發行項。

  ```sql
  CREATE DATABASE Sales
  GO
  USE [SALES]
  GO 
  CREATE TABLE CUSTOMER([CustomerID] [int] NOT NULL, [SalesAmount] [decimal] NOT NULL)
  GO 
  INSERT INTO CUSTOMER (CustomerID, SalesAmount) VALUES (1,100),(2,200),(3,300)
  ```

  其他 SQL Server 執行個體上，「 訂閱者 」 建立的資料庫可接受的文章。

  ```sql
  CREATE DATABASE Sales
  GO
  ```

1. 建立快照集資料夾的讀取/寫入，「 散發者 」 上建立快照集資料夾，並授與存取權 'mssql' 使用者的 SQL Server Agent 

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

1. 在此範例中設定 「 散發者 」、 「 發行者 」 端也會 「 散發者 」。 若要設定的執行個體，以及發佈的 「 發行者 」 端，執行下列命令。

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

1. 設定 「 發行者 」 在 「 發行者 」 上執行下列 TSQL 命令。

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

1. 「 發行者 」 上設定執行作業的發行集的下列 TSQL 命令。

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

1. 建立文件從 sales 資料表執行下列 TSQL 命令在 「 發行者 」 上。

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

1. 訂用帳戶執行下列 TSQL 命令上設定 「 發行者 」。

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
  @subscriber_login =  @subscriberLogin,
  @subscriber_password =  @subscriberPassword,
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

1. 執行複寫代理程式作業

  執行下列查詢，以取得作業的清單：

  ```sql
  SELECT name, date_modified FROM msdb.dbo.sysjobs order by date_modified desc
  ```

  執行快照集的複寫作業，以產生快照集：

  ```sql
  USE msdb;  
  --generate snapshot of publications, for example
  EXEC dbo.sp_start_job N'PUBLISHER-PUBLICATION-SnapshotRepl-1'
  GO
  ```

  執行快照集的複寫作業，以產生快照集：

  ```sql
  USE msdb;  
  --distribute the publication to subscriber, for example
  EXEC dbo.sp_start_job N'DISTRIBUTOR-PUBLICATION-SnapshotRepl-SUBSCRIBER'
  GO
  ```

1. 連接訂閱者及查詢複寫的資料 

  在訂閱者上，檢查複寫運作藉由執行下列查詢：

  ```sql
  SELECT * from [Sales].[dbo].[CUSTOMER]
  ```

在本教學課程中，您可以設定 SQL Server 快照式複寫在 Linux 上使用兩個使用 Transact SQL 的 SQL Server 執行個體。

> [!div class="checklist"]
> * 啟用在 Linux 上的 SQL Server 複寫代理程式
> * 建立範例資料庫
> * 設定 SQL Server 代理程式存取的快照集資料夾
> * 設定散發者
> * 設定 「 發行者 」
> * 設定發行集和文件
> * 設定訂閱者 
> * 執行複寫作業

## <a name="see-also"></a>另請參閱

如需複寫的詳細資訊，請參閱 < [SQL Server 複寫的文件](../relational-databases/replication/sql-server-replication.md)。

## <a name="next-steps"></a>後續步驟

[概念：在 Linux 上的 SQL Server 複寫](sql-server-linux-replication.md)

[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。
