---
title: 設定可用性群組中的 SQL Server 散發資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 05/23/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- remote Distributors [SQL Server replication]
- transactional replication, configuring distribution
- distribution databases [SQL Server replication], sizing
- Distributors [SQL Server replication], configuring
- distribution databases [SQL Server replication], about distribution databases
- distribution databases [SQL Server replication]
- merge replication [SQL Server replication], configuring distribution
ms.assetid: 94d52169-384e-4885-84eb-2304e967d9f7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1af1ffe2423fad7e8b9b2b07f2085bdf0efed1f2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615377"
---
# <a name="set-up-replication-distribution-database-in-always-on-availability-group"></a>設定 Always On 可用性群組中的複寫散發資料庫

本文說明如何在 Always On 可用性群組 (AG) 中設定 SQL Server 複寫散發資料庫。

SQL Server 2017 CU 6 透過下列機制引進 AG 中的複寫散發資料庫支援：

- 散發資料庫 AG 需要有接聽程式。 發行者新增散發者時，會使用接聽程式名稱作為散發者名稱。
- 所建立的複寫作業是將接聽程式名稱當成散發者名稱。
- 新的作業會監視散發資料庫的狀態 (AG 中的主要或次要)，以及根據散發資料庫狀態來停用或啟用複寫作業。

根據下面所述的步驟在 AG 中設定散發資料庫之後，可以在散發資料庫 AG 容錯移轉之前和之後正確地執行複寫組態和執行階段作業。

## <a name="supported-scenarios"></a>支援的案例

- 設定要包含在 AG 中的散發資料庫。
- 在 AG 容錯移轉之前和之後設定複寫 (例如發行集和訂閱)。
- 在容錯移轉之前和之後運作的複寫作業。
- 在散發資料庫位於 AG 時移除散發者和發行者的複寫。
- 新增或移除現有散發資料庫 AG 中的節點。
- 散發者可以有多個散發資料庫。 每個散發資料庫都可以在自己的 AG 中，而且不可以在任何 AG 中。 多個散發資料庫可以共用 AG。
- 發行者和散發者需要位在不同的 SQL Server 執行個體上。

## <a name="limitations-or-exclusions"></a>限制或排除

- 不支援本機散發者。 例如，發行者和散發者必須是不同的 SQL Server 執行個體。 使用自己作為散發者的發行者 (也稱為 本機散發者) 無法支援 AG 中的散發資料庫。
- 不支援 Oracle 發行者。
- 合併式複寫不受到支援。
- 不支援與立即或已排入佇列更新訂閱者的異動複寫。
- 不支援點對點複寫。
- 所有裝載散發資料庫複本的 SQL Server 執行個體都必須是 SQL Server 2017 CU 6 或更新版本。 
- 所有裝載散發資料庫複本的 SQL Server 執行個體都必須是相同的版本，但進行升級時的短時間範圍期間除外。
- 散發資料庫必須處於完整復原模式。
- 若要復原，以及允許交易記錄截斷，請設定完整和交易記錄備份。
- 散發資料庫 AG 必須設定接聽程式。
- 散發資料庫 AG 中的次要複本可以同步或非同步。 建議並偏好使用同步模式。
- 不支援雙向異動複寫。


   >[!NOTE]
   >在次要複本上執行任何複寫預存程序 (例如：`sp_dropdistpublisher`、`sp_dropdistributiondb`、`sp_dropdistributor`、`sp_adddistributiondb`、`sp_adddistpublisher`) 之前，請確定複本已完全同步。

- 散發資料庫 AG 中的所有次要複本都必須可供讀取。
- 散發資料庫 AG 中的所有節點都需要使用相同的網域帳戶來執行 SQL Server Agent，而且此網域帳戶需要具有每個節點的相同權限。
- 如果使用 Proxy 帳戶執行任何複寫代理程式，Proxy 帳戶需要存在於散發資料庫 AG 中的每個節點，並且具有每個節點的相同權限。
- 變更所有參與散發資料庫 AG 的複本中的散發者或散發資料庫屬性。
- 在所有參與散發資料庫 AG 的複本中，透過 msdb 預存程序或 SQL Server Management Studio 進行複寫作業變更。
- 在發行者上設定散發者需要使用指令碼來完成。 無法使用複寫精靈。 支援將複寫精靈和屬性工作表用於其他用途。
- 設定散發資料庫的 AG 只能透過指令碼完成。
- 在 AG 中設定散發資料庫需要是新的複寫組態。 不支援將現有散發資料庫切換為 AG。 而且從散發資料庫中取出 AG 之後，就無法再當成有效的散發資料庫運作，應該予以卸除。

## <a name="configuration-architecture"></a>組態架構

本文中的範例使用下列伺服器名稱和設定。

- DIST1、DIST2、DIST3 是散發者伺服器；
- PUB 是發行者伺服器；
- 形成散發資料庫 AG 之後，接聽程式名稱是 DISTLISTENER；
- DIST1 會是散發資料庫 AG 的初始主要複本。

## <a name="configure-distributor-distribution-database-and-publisher"></a>設定散發者、散發資料庫和發行者

此範例會設定新的散發者和發行者，並在 AG 中放置散發資料庫。

### <a name="distributors-workflow"></a>散發者工作流程

1. 使用 `sp_adddistributor @@servername`，將 DIST1、DIST2、DIST3 設定為散發者。 透過 `@password`，指定 `distributor_admin` 的密碼。 DIST1、DIST2 和 DIST3 的 `@password` 應該相同。
2. 使用 `sp_adddistributiondb` 在 DIST1 上建立散發資料庫。 散發資料庫的名稱是 `distribution`。 將 `distribution` 資料庫的復原模式從簡單變更為完整。
3. 使用 DIST1、DIST2 和 DIST3 上的複本，建立 `distribution` 資料庫的 AG。 最好所有複本都同步。 設定可供讀取或允許讀取的次要複本。 此時，散發資料庫是 AG、DIST1 是主要複本，而 DIST2 和 DIST3 是次要複本。
4. 針對 AG，設定名為 `DISTLISTENER` 的接聽程式。
5. 若要復原，以及允許交易記錄截斷，請設定完整和交易記錄備份。
6. 在 DIST2 和 DIST3 上，執行：

   ```sql
   sp_adddistributiondb 'distribution'
   ```

1. 若要在 DIST1 上將 `PUB` 新增為發行者，請執行：
   
   ```sql
   sp_adddistpublisher @publisher= 'PUB', @distribution_db= 'distribution', @working_directory= '<network path>'
   ```

   `@working_directory` 的值應該是與 DIST1、DIST2 和 DIST3 無關的網路路徑。

1. 在 DIST2 和 DIST3 上，執行：  

   ```sql
   sp_adddistpublisher @publisher= 'PUB', @distribution_db= 'distribution', @working_directory= '<network path>'
   ```

   `@working_directory` 的值應該與上一個步驟相同。

### <a name="publisher-workflow"></a>發行者工作流程

若要將 `distribution` 資料庫 AG 接聽程式新增為散發者，請在 PUB 上執行： 

   ```sql
   sp_adddistributor @distributor = 'DISTLISTENER', @password = <distributor_admin password> 
   ```

   @password 的值應該是在散發者工作流程中設定散發者時所指定的值。

## <a name="remove-distributor-and-publisher"></a>移除散發者和發行者

此範例會在散發資料庫位於 AG 時移除發行者和散發者。

### <a name="publisher-workflow"></a>發行者工作流程

在 PUB 上，卸除此發行者的所有訂閱和發行集，然後呼叫 `sp_dropdistributor`。

### <a name="distributors-workflow"></a>散發者工作流程

在此範例中，DIST1 是 `distribution` 資料庫 AG 的目前主要複本。 DIST2 和 DIST3 是次要複本。

1. 在 DIST2 和 DIST3 上，執行：

   ```sql
   sp_dropdistpublisher 'PUB',  @no_checks = 1
   ```

1. 在 DIST1 上，執行：

   ```sql
   sp_dropdistpublisher 'PUB'
   ```

1. 刪除 AG。
2. 在 DIST2 和 DIST3 上，使用復原還原資料庫，以將 `distribution` 資料庫變更為 read_write 模式。
   
   ```sql
   RESTORE DATABASE distribution WITH RECOVERY, KEEP_REPLICATION
   ```

1. 若要卸除 `distribution` 資料庫，以及保留快照集目錄，請執行： 

   ```sql
   sp_dropdistributiondb 'distribution' , @former_ag_secondary=1
   ```

  此程序會移除這個複本上的所有懸空作業。

1. 若要卸除 DIST1 上的 `distribution` 資料庫，請執行：

   ```sql
   sp_dropdistributiondb 'distribution'
   ``` 

1. 如果 AG 中沒有其他散發資料庫，則請在 DIST1、DIST2 和 DIST3 上執行 `sp_dropdistributor`。

## <a name="add-a-replica-to-distribution-database-ag"></a>將複本新增至散發資料庫 AG

此範例會將新的散發者新增至具有 AG 中散發資料庫的現有複寫組態。 在此範例中，現有散發資料庫是在 AG 中。 DIST1 和 DIST2 是散發者、`distribution` 是 AG 中的散發資料庫，而 PUB 是發行者。 將 DIST3 新增為 AG 中的複本。

### <a name="distributors-workflow"></a>散發者工作流程

1. DIST3 應該透過 `sp_adddistributor @@servername` 設定為散發者。 應該透過 @password 參數指定 `distributor_admin` 的密碼。 密碼應該與針對 DIST1 和 DIST2 所指定的密碼相同。
2. 將 DIST3 新增至目前散發資料庫的 AG。
3. 在 DIST3 上，執行：

   ```sql
   sp_adddistributiondb 'distribution'
   ```

1. 在 DIST3 上，執行： 

   ```sql
   sp_adddistpublisher @publisher= 'PUB', @distribution_db= 'distribution', @working_directory= '<network path>'
   ```

   `@working_directory` 的值應該與針對 DIST1 和 DIST2 所指定的密碼相同。

## <a name="remove-a-replica-from-distribution-database-ag"></a>移除散發資料庫 AG 中的複本

此範例會移除目前散發資料庫 AG 中的散發者，而散發資料庫 AG 中的其餘複本不受影響。 在此範例中，散發資料庫是在 AG 中。 DIST1、DIST2 和 DIST3 是散發者、`distribution` 是 AG 中的散發資料庫，而 PUB 是發行者。 移除 AG 中的 DIST3。

### <a name="distributors-workflow"></a>散發者工作流程

1. 請確定 DIST3 是 `distribution` 資料庫 AG 的次要複本。
2. 移除 `distribution` 資料庫 AG 中的 DIST3。
3. 在 DIST3 上，使用復原還原資料庫，以將 `distribution` 資料庫變更為 read_write 模式。 例如，執行下列命令：  
   
   ```sql
   RESTORE DATABASE distribution WITH RECOVERY, KEEP_REPLICATION.
   ```
   
1. 若要移除 DIST3 上的所有孤立作業，請執行： 

   ```sql
   sp_dropdistpublisher 'PUB', @no_checks = 1
   ```

1. 在 DIST3 上，執行：

   ```sql
   sp_dropdistributiondb 'distribution', @former_ag_secondary=1
   ```

1. 在 DIST3 上，執行： 

   ```sql
   sp_dropdistributor
   ```

## <a name="remove-a-publisher-from-distribution-database-ag"></a>移除散發資料庫 AG 中的發行者

此範例會移除散發者的目前散發資料庫 AG 中的發行者，而此散發資料庫 AG 所服務的其餘發行者不受影響。 在此範例中，現有組態於 AG 中有散發資料庫。 DIST1、DIST2 和 DIST3 是散發者、`distribution` 是 AG 中的散發資料庫，而 PUB1 和 PUB2 是 `distribution` 資料庫所服務的發行者。 此範例會移除這些散發者中的 PUB1。

### <a name="publisher-workflow"></a>發行者工作流程

在 PUB1 上，卸除此發行者的所有訂閱和發行集，然後呼叫 `sp_dropdistributor`。

### <a name="distributor-workflow"></a>散發者工作流程

DIST1 是 `distribution` 資料庫 AG 的目前主要複本。

1. 在 DIST2 和 DIST3 上，執行：

   ```sql
   sp_dropdistpublisher 'PUB1',  @no_checks = 1
   ```

1. 在 DIST1 上，執行：

   ```sql
   sp_dropdistpublisher 'PUB1'
   ```

1. 此時，在 DIST2 或 DIST3 上，可能有與 PUB1 相關的孤立作業。 只要容錯移轉至 DIST2 和 DIST3，`Monitor and sync replication agent jobs` 作業就會移除與 PUB1 之所有發行集相關的孤立作業。

## <a name="add-subscription"></a>新增訂用帳戶

此範例是有關在散發者之間適當地設定訂閱者資訊。 此範例會新增訂閱者。 DIST1 是 AG 中散發資料庫的目前主要複本，而 DIST2 和 DIST3 是 AG 中散發資料庫的次要複本。 訂閱者名稱是 SUB。

### <a name="publisher-workflow"></a>發行者工作流程

在 PUB 上，新增訂用帳戶，就像一般對訂閱者 `SUB` 執行地一樣。

### <a name="distributor-workflow"></a>散發者工作流程

在 DIST2 和 DIST3 上，如果以前未向 DIST2 或 DIST3 註冊 'SUB' 的已連結伺服器，則請予以新增。 以下是已連結伺服器建立的範例 TSQL -

   ```sql 
   EXEC master.dbo.sp_addlinkedserver@server =N'SUB', @srvproduct=N'SQL Server'
   /* For security reasons the linked server remote logins password is changed with ######## */
   EXEC master.dbo.sp_addlinkedsrvlogin@rmtsrvname=N'SUB', @useself=N'True',@locallogin=NULL,@rmtuser=NULL,@rmtpassword=NULL
   ```

## <a name="add-a-pull-subscription"></a>新增提取訂閱

### <a name="subscriber-workflow"></a>訂閱者工作流程

若要使用 AG 中的散發資料庫新增發行集的提取訂閱，請使用 `sp_addpullsubscription_agent` 之 `@distributor` 參數中的 AG 接聽程式名稱。

## <a name="sample-t-sql-create-distribution-db-in-ag"></a>AG 中的範例 T-SQL 建立散發資料庫

下列指令碼會啟用可用性群組中的散發資料庫。 

```sql
--- WorkFlow to Enable Distribution Database In AG.

-- SECTION 1 ---- CONFIGURE THE DISTRIBUTOR SERVERS

-- Step1 - Configure the Distribution DB nodes (AG Replicas) to act as a distributor
:Connect SQLNode1
sp_adddistributor @distributor = @@ServerName, @password = 'Pass@word1'
Go 
:Connect SQLNode2
sp_adddistributor @distributor = @@ServerName, @password = 'Pass@word1'
Go

-- Step2 - Configure the Distribution Database
:Connect SQLNode1
USE master
EXEC sp_adddistributiondb @database = 'DistributionDB', @security_mode = 1;
GO
Alter Database [DistributionDB] Set Recovery Full
Go
Backup Database [DistributionDB] to Disk = 'Nul'
Go
-- Step 3 - Create AG for the Distribution DB.
:Connect SQLNode1
USE [master]
GO
CREATE ENDPOINT [Hadr_endpoint] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)   
    FOR DATA_MIRRORING (ROLE = ALL, AUTHENTICATION = WINDOWS NEGOTIATE
, ENCRYPTION = REQUIRED ALGORITHM AES)
GO

:Connect SQLNode2
USE [master]
GO
CREATE ENDPOINT [Hadr_endpoint] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)   
    FOR DATA_MIRRORING (ROLE = ALL, AUTHENTICATION = WINDOWS NEGOTIATE
, ENCRYPTION = REQUIRED ALGORITHM AES)
GO

:Connect SQLNode1
-- Create the Availability Group
CREATE AVAILABILITY GROUP [DistributionDB_AG]
FOR DATABASE [DistributionDB]
REPLICA ON 'SQLNode1'
WITH (ENDPOINT_URL = N'TCP://SQLNode1.contoso.com:5022', 
         FAILOVER_MODE = AUTOMATIC, 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
         BACKUP_PRIORITY = 50, 
         SECONDARY_ROLE(ALLOW_CONNECTIONS = ALL), 
         SEEDING_MODE = AUTOMATIC),
N'SQLNode2' WITH (ENDPOINT_URL = N'TCP://SQLNode2.contoso.com:5022', 
     FAILOVER_MODE = AUTOMATIC, 
     AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
     BACKUP_PRIORITY = 50, 
     SECONDARY_ROLE(ALLOW_CONNECTIONS = ALL), 
     SEEDING_MODE = AUTOMATIC);
 GO


:Connect SQLNode2
ALTER AVAILABILITY GROUP [DistributionDB_AG] JOIN
GO  
ALTER AVAILABILITY GROUP [DistributionDB_AG] GRANT CREATE ANY DATABASE
Go

--STEP4 - Create the Listener for the Availability Group. This is very important.
:Connect SQLNode1

USE [master]
GO
ALTER AVAILABILITY GROUP [DistributionDB_AG]
ADD LISTENER N'DistributionDBList' (
WITH IP
((N'10.0.0.8', N'255.255.255.0')) , PORT=1500);
GO

-- STEP 5 - Enable SQLNode1 also as a Distributor
:CONNECT SQLNODE2
EXEC sp_adddistributiondb @database = 'DistributionDB', @security_mode = 1;
GO

--STEP 6 - On all Distributor Nodes Configure the Publisher Details 
:CONNECT SQLNODE1
EXEC sp_addDistPublisher @publisher = 'SQLNode4', @distribution_db = 'DistributionDB', 
    @working_directory = '\\sqlfileshare\Dist_Work_Directory\'
GO
:CONNECT SQLNODE2
EXEC sp_addDistPublisher @publisher = 'SQLNode4', @distribution_db = 'DistributionDB', 
    @working_directory = '\\sqlfileshare\Dist_Work_Directory\'
GO

-- SECTION 2 ---- CONFIGURE THE PUBLISHER SERVER
:CONNECT SQLNODE4
EXEC sp_addDistributor @distributor = 'DistributionDBList', -- Listener for the Distribution DB.    
    @password = 'Pass@word1'
Go

-- SECTION 3 ---- CONFIGURE THE SUBSCRIBERS 
-- On Publisher, create the publication as one would normally do.
-- On the Secondary replicas of the Distribution DB, add the Subscriber as a linked server.
:CONNECT SQLNODE2
EXEC master.dbo.sp_addlinkedserver @server = N'SQLNODE5', @srvproduct=N'SQL Server'
 /* For security reasons the linked server remote logins password is changed with ######## */
EXEC master.dbo.sp_addlinkedsrvlogin @rmtsrvname=N'SQLNODE5',@useself=N'True',@locallogin=NULL,@rmtuser=NULL,@rmtpassword=NULL 
```

## <a name="see-also"></a>另請參閱  
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [保護散發者](../../relational-databases/replication/security/secure-the-distributor.md)  
  
## <a name="next-steps"></a>後續步驟
 [檢視及修改散發者和發行者屬性](view-and-modify-distributor-and-publisher-properties.md)  
 [停用發行和散發](disable-publishing-and-distribution.md)  
 [啟用用於複寫的資料庫 (SQL Server Management Studio)](enable-a-database-for-replication-sql-server-management-studio.md) 
