---
title: 使用 SQL Database 受控執行個體複寫 | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Database replication
- replication, SQL Database
ms.assetid: e8484da7-495f-4dac-b38e-bcdc4691f9fa
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: d55aea5d50d9ea434aabb392d0c6b53573c0199e
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559568"
---
# <a name="replication-with-sql-database-managed-instance"></a>使用 SQL Database 受控執行個體複寫

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

Azure SQL Database 受控執行個體 (預覽) 支援異動複寫。 受控執行個體可以裝載發行者、散發者和訂閱者資料庫。

## <a name="common-configurations"></a>常用設定

一般而言，發行者和散發者必須同時在雲端或內部部署。 支援下列設定：

- **在受控執行個體上擁有本機散發者的發行者**

   ![Replication-with-azure-sql-db-single-managed-instance-publisher-distributor](./media/replication-with-sql-database-managed-instance/01-single-instance-asdbmi-pubdist.png)

   發行者和散發者資料庫都是在單一受控執行個體上設定的。

- **在受控執行個體上擁有遠端散發者的發行者**

   ![Replication-with-azure-sql-db-separate-managed-instances-publisher-distributor](./media/replication-with-sql-database-managed-instance/02-separate-instances-asdbmi-pubdist.png)

   發行者和散發者是在兩個受控執行個體上設定的。 在此設定中：

  - 兩個受控執行個體都位於相同的 vNet 中。

  - 兩個受控執行個體都位於相同的位置。

- **在受控執行個體上擁有訂閱者的發行者和散發者內部部署**

   ![Replication-from-on-premises-to-azure-sql-db-subscriber](./media/replication-with-sql-database-managed-instance/03-azure-sql-db-subscriber.png)

   在此設定中，Azure SQL Database 就是訂閱者。 此設定支援從內部部署移轉至 Azure。 在訂閱者角色中，SQL 資料庫不需要受控執行個體，但是您可以使用 SQL Database 受控執行個體作為從內部部署移轉至 Azure 的步驟。 如需有關 Azure SQL Database 訂閱者的詳細資訊，請參閱[複寫至 SQL Database](replication-to-sql-database.md)。

## <a name="requirements"></a>需求

Azure SQL Database 上的發行者和散發者需要：

- Azure SQL Database 受控執行個體。

   >[!NOTE]
   >未使用受控執行個體設定的 Azure SQL Database 只能是訂閱者。

- 所有 SQL Server 執行個體都必須位於相同的 vNet 上。

- 連線會在複寫參與者之間使用 SQL 驗證。

- 複寫工作目錄的 Azure 儲存體帳戶共用。

## <a name="features"></a>功能

支援：

- 內部部署和 Azure SQL Database 受控執行個體的執行個體混用異動與快照式複寫。

- 訂閱者在 Azure SQL Database 或彈性集區中可以是內部部署的。

- 單向或雙向複寫

## <a name="configure-publishing-and-distribution-example"></a>設定發行和散發範例

1. 在入口網站中，[建立 Azure SQL Database 受控執行個體](http://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-tutorial-portal)。

1. 針對工作目錄，[建立 Azure 儲存體帳戶](http://docs.microsoft.com/azure/storage/common/storage-create-storage-account#create-a-storage-account)。 請務必複製儲存體金鑰。 請參閱[檢視和複製儲存體存取金鑰](http://docs.microsoft.com/azure/storage/common/storage-create-storage-account#manage-your-storage-access-keys)。

1. 建立發行者的資料庫。

   在以下的範例指令碼中，將 `<Publishing_DB>` 取代為此資料庫的名稱。

1. 使用 SQL 驗證，為散發者建立資料庫使用者。 請參閱[建立資料庫使用者](http://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial#creating-database-users)。 使用安全的密碼。

   在以下的範例指令碼中，使用 `<SQL_USER>` 和 `<PASSWORD>` 搭配此 SQL Server 帳戶資料庫使用者和密碼。

1. [連線至 Azure SQL Database 受控執行個體](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ssms)。

1. 執行下列查詢，以新增散發者和散發資料庫。

   ```sql
   USE [master]
   GO
   EXEC sp_adddistributor @distributor = @@ServerName;
   EXEC sp_adddistributiondb @database = N'distribution';
   ```

1. 若要將發行者設定為使用指定的散發資料庫，請更新並執行下列查詢。

   將 `<SQL_USER>` 和 `<PASSWORD>` 取代為 SQL Server 帳戶和密碼。

   將 `\\<STORAGE_ACCOUNT>.file.core.windows.net\<SHARE>` 取代為您儲存體帳戶的值。 

   將 `<STORAGE_CONNECTION_STRING>` 取代為您存取金鑰的值。

   更新下列查詢後，執行該查詢。 

   ```sql
   USE [master]
   EXEC sp_adddistpublisher @publisher = @@ServerName,
                @distribution_db = N'distribution',
                @security_mode = 0,
                @login = N'<SQL_USER>',
                @password = N'<PASSWORD>',
                @working_directory = N'\\<STORAGE_ACCOUNT>.file.core.windows.net\<SHARE>',
                @storage_connection_string = N'<STORAGE_CONNECTION_STRING>';
   GO
   ```

1. 設定發行者以進行複寫。 

    在下列查詢中，將 `<Publishing_DB>` 取代為發行者資料庫的名稱。

    將 `<Publication_Name>` 取代為發行集的名稱。

    將 `<SQL_USER>` 和 `<PASSWORD>` 取代為 SQL Server 帳戶和密碼。

    更新查詢之後，執行該查詢以建立發行集。

   ```sql
   USE [<Publishing_DB>]
   EXEC sp_replicationdboption @dbname = N'<Publishing_DB>',
                @optname = N'publish',
                @value = N'true';

   EXEC sp_addpublication @publication = N'<Publication_Name>',
                @status = N'active';

   EXEC sp_changelogreader_agent @publisher_security_mode = 0,
                @publisher_login = N'<SQL_USER>',
                @publisher_password = N'<PASSWORD>',
                @job_login = N'<SQL_USER>',
                @job_password = N'<PASSWORD>';

   EXEC sp_addpublication_snapshot @publication = N'<Publication_Name>',
                @frequency_type = 1,
                @publisher_security_mode = 0,
                @publisher_login = N'<SQL_USER>',
                @publisher_password = N'<PASSWORD>',
                @job_login = N'<SQL_USER>',
                @job_password = N'<PASSWORD>'
   ```

1. 新增發行項、訂閱和發送訂閱代理程式。 

   若要新增這些物件，請更新下列指令碼。

   將 `<Object_Name>` 取代為發行集物件的名稱。

   將 `<Object_Schema>` 取代為來源結構描述的名稱。 

   取代角括弧括住的其他參數 `<>` 以符合先前指令碼中的值。 

   ```sql
   EXEC sp_addarticle @publication = N'<Publication_Name>',
                @type = N'logbased',
                @article = N'<Object_Name>',
                @source_object = N'<Object_Name>',
                @source_owner = N'<Object_Schema>'

   EXEC sp_addsubscription @publication = N'<Publication_Name>',
                @subscriber = @@ServerName,
                @destination_db = N'<Subscribing_DB>',
                @subscription_type = N'Push'

   EXEC sp_addpushsubscription_agent @publication = N'<Publication_Name>',
                @subscriber = @@ServerName,
                @subscriber_db = N'<Subscribing_DB>',
                @subscriber_security_mode = 0,
                @subscriber_login = N'<SQL_USER>',
                @subscriber_password = N'<PASSWORD>',
                @job_login = N'<SQL_USER>', 
                @job_password = N'<PASSWORD>'
   GO
   ```

## <a name="limitations"></a>限制

不支援下列功能：

- 可更新的訂閱

- 作用中的異地備援

## <a name="see-also"></a>另請參閱

- [什麼是受控執行個體 (預覽)？](http://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)
