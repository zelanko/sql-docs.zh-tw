---
description: 還原已啟用 Stretch 的資料庫 (Stretch Database)
title: 還原已啟用 Stretch 的資料庫
ms.date: 07/06/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cebc1f6d-d5ea-460d-ae60-d047d29c2723
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 8cef37be62e91b608852a4b5867d5917e72e8742
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492598"
---
# <a name="restore-stretch-enabled-databases-stretch-database"></a>還原已啟用 Stretch 的資料庫 (Stretch Database)
[!INCLUDE [sqlserver2016-windows-only](../../includes/applies-to-version/sqlserver2016-windows-only.md)]


  有必要復原許多類型的失敗、錯誤和嚴重損壞時，請還原備份的資料庫。
  
  如需備份的詳細資訊，請參閱 [備份已啟用延展功能的資料庫](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)。

> [!TIP]
> 備份只是完整高可用性和商務持續性解決方案的一部分。 如需高可用性的詳細資訊，請參閱 [高可用性解決方案](../../database-engine/sql-server-business-continuity-dr.md)。

## <a name="restore-your-sql-server-data"></a>還原 SQL Server 資料
從硬體故障或損毀復原，請從備份還原已啟用 Stretch 的 SQL Server 資料庫。 您可以繼續使用目前所用的 SQL Server 還原方法。 如需詳細資訊，請參閱 [還原和復原概觀](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)。

還原 SQL Server 資料庫之後，您必須執行預存程序 **sys.sp_rda_reauthorize_db** ，重新建立已啟用 Stretch 的 SQL Server 資料庫和遠端 Azure 資料庫之間的連線。 如需詳細資訊，請參閱 [還原 SQL Server 資料庫與遠端 Azure 資料庫之間的連線](#reconnect)。

## <a name="restore-your-remote-azure-data"></a>還原遠端的 Azure 資料

### <a name="recover-a-live-azure-database"></a>復原即時的 Azure 資料庫
Azure 的 SQL Server Stretch Database 服務使用 Azure 儲存體快照集至少每隔 8 小時快照所有的即時資料。 這些快照集會保留 7 天。 這可讓您將資料還原到過去 7 天內擷取最後一個快照集時，至少 21 個時間點中的其中之一。

若要使用 Azure 入口網站將即時的 Azure 資料庫還原到較早的時間點，請執行下列作業。

1. 登入 [Azure 入口網站][]。
2. 在畫面左側選取 [瀏覽]****，然後選取 [SQL 資料庫]****。
3. 瀏覽並選取您的資料庫。
4. 在 [資料庫] 刀鋒視窗頂端，按一下 [還原]****。
5. 指定新的**資料庫名稱**，選取 [還原點]**** 然後按一下 [建立]****。
6. 資料庫還原程序就會開始，您可以使用 **NOTIFICATIONS**監視。

### <a name="recover-a-deleted-azure-database"></a>復原刪除的 Azure 資料庫
Azure 的 SQL Server Stretch Database 服務，會在卸除資料庫前擷取資料庫快照集，並保留 7 天。 此後即不再保留即時資料庫的快照集。 這可讓您將已刪除的資料庫還原到刪除的時點。

若要使用 Azure 入口網站將刪除的 Azure 資料庫還原到刪除的時點，請執行下列作業。

1. 登入 [Azure 入口網站][]。
2. 在畫面左側選取 [瀏覽]，然後選取 [SQL Server]。
3. 瀏覽並選取您的伺服器。
4. 向下捲動到伺服器的 [作業] 刀鋒視窗，按一下 [已刪除的資料庫]**** 圖格。
5. 選取您要還原的已刪除資料庫。
5. 指定新的**資料庫名稱**，然後按一下 [建立]****。
6. 資料庫還原程序就會開始，您可以使用 **NOTIFICATIONS**監視。

## <a name="restore-the-connection-between-the-sql-server-database-and-the-remote-azure-database"></a><a name="reconnect"></a>還原 SQL Server 資料庫與遠端 Azure 資料庫之間的連線

1.  如果您打算使用不同的名稱或在不同的區域連接到還原的 Azure 資料庫，請執行預存程序 [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) 中斷與前一個 Azure 資料庫的連線。  
  
2.  執行預存程序 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 將本機已啟用 Stretch 的資料庫重新連接到 Azure 資料庫。  
  
    -   提供以 sysname 或 varchar(128) 值為認證範圍的現有資料庫。 (請勿使用 varchar(max)。)您可以在 **sys.database_scoped_credentials**檢視中查詢認證名稱。  
  
    -   指定是否要複製一份遠端資料，並連接到複本 (建議選項)。  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    EXEC sp_rda_reauthorize_db
        @credential = N'<existing_database_scoped_credential_name>',
        @with_copy = 1 ;  
    GO  
    ```  
    
  ## <a name="see-also"></a>另請參閱  
 [備份已啟用 Stretch 的資料庫](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
 [管理 Stretch Database 並對其進行疑難排解](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)   
 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 
 [sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)  
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
 
 [Azure 入口網站]: https://portal.azure.com/
 
