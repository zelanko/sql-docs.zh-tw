---
description: Stretch Database 的管理和疑難排解
title: 管理及疑難排解
ms.date: 06/27/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, managing
- Stretch Database, troubleshooting
- managing Stretch Database
- troubleshooting Stretch Database
ms.assetid: 6334db3e-9297-44df-8d53-211187a95520
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: efe0b68c605c96423dae5206693ff733430aff63
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454330"
---
# <a name="manage-and-troubleshoot-stretch-database"></a>Stretch Database 的管理和疑難排解
[!INCLUDE [sqlserver2016-windows-only](../../includes/applies-to-version/sqlserver2016-windows-only.md)]


  若要管理 Stretch Database 並對其進行疑難排解，請使用本文所述的工具和方法。  
## <a name="manage-local-data"></a>管理本機資料  
  
###  <a name="get-info-about-local-databases-and-tables-enabled-for-stretch-database"></a><a name="LocalInfo"></a> 取得針對 Stretch Database 啟用之本機資料庫和資料表的相關資訊  
 開啟 **sys.databases** 和 **sys.tables** 目錄檢視，即可查看已啟用延展功能之 SQL Server 資料庫和資料表的相關資訊。 如需詳細資訊，請參閱 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 和 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)。  
 
 若要查看 SQL Server 中啟用延展功能的資料表使用了多少空間，請執行下列陳述式。
 
 ```sql
USE <Stretch-enabled database name>;
GO
EXEC sp_spaceused '<Stretch-enabled table name>', 'true', 'LOCAL_ONLY';
GO
 ```
   
## <a name="manage-data-migration"></a>管理資料移轉  
  
### <a name="check-the-filter-function-applied-to-a-table"></a>檢查篩選函數是否已套用至資料表  
 開啟 **sys.remote_data_archive_tables** 目錄檢視，並檢查 **filter_predicate** 資料行的值，以識別 Stretch Database 用什麼函數來選取要移轉的資料列。 如果值為 Null，便代表整個資料表皆符合移轉資格。 如需詳細資訊，請參閱 [sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md) 和[使用篩選函數選取要移轉的資料列](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)。  
  
###  <a name="check-the-status-of-data-migration"></a><a name="Migration"></a> 檢查資料移轉狀態  
 若要在 Stretch Database 監視器中監視資料移轉，請針對 SQL Server Management Studio 中的資料庫，選取 [工作 | 延展 | 監視]****。 如需詳細資訊，請參閱 [監視和疑難排解資料移轉 &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)。  
  
 或者，開啟 **sys.dm_db_rda_migration_status** 動態管理檢視，查看已移轉的批次和資料列數目。  
  
###  <a name="troubleshoot-data-migration"></a><a name="Firewall"></a> 對資料移轉進行疑難排解  
 如需疑難排解建議，請參閱 [監視和疑難排解資料移轉 &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)。  
  
## <a name="manage-remote-data"></a>管理遠端資料  
  
###  <a name="get-info-about-remote-databases-and-tables-used-by-stretch-database"></a><a name="RemoteInfo"></a> 取得 Stretch Database 所使用之遠端資料庫和資料表的相關資訊  
 開啟 **sys.remote_data_archive_databases** 和 **sys.remote_data_archive_tables** 目錄檢視，即可查看已移轉資料儲存所在之遠端資料庫和資料表的相關資訊。 如需詳細資訊，請參閱 [sys.remote_data_archive_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-databases.md) 和 [sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md)。  
 
若要查看 Azure 中啟用延展功能的資料表使用了多少空間，請執行下列陳述式。
 
 ```sql
USE <Stretch-enabled database name>;
GO
EXEC sp_spaceused '<Stretch-enabled table name>', 'true', 'REMOTE_ONLY';
GO
 ```

### <a name="delete-migrated-data"></a>刪除已移轉的資料  
如果您想要刪除已移轉至 Azure 的資料，請遵循 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)中所述的步驟。  
  
## <a name="manage-table-schema"></a>管理資料表結構描述

### <a name="dont-change-the-schema-of-the-remote-table"></a>請不要變更遠端資料表的結構描述  
 請不要變更針對 Stretch Database 設定且已與 SQL Server 資料表建立關聯之遠端 Azure 資料表的結構描述。 尤其不要修改資料行的名稱或資料類型。 針對 SQL Server 資料表的結構描述與遠端資料表的結構描述，Stretch Database 功能可在兩者的相對關係方面進行各種假設。 如果您變更遠端結構描述，Stretch Database 針對已變更資料表將會停止運作。  

### <a name="reconcile-table-columns"></a>協調資料表資料行  
如果您不小心刪除遠端資料表中的資料行，可執行 **sp_rda_reconcile_columns** ，將存在於已啟用延展功能的 SQL Server 資料表中，但遠端資料表卻沒有的資料行加入遠端資料表中。 如需詳細資訊，請參閱 [sys.sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md)。  
  
  > [!IMPORTANT]
  > 當 **sp_rda_reconcile_columns** 重新建立您不小心從遠端資料表中刪除的資料行時，它不會還原先前存在於已刪除資料行中的資料。
  
**sp_rda_reconcile_columns** 不會從遠端資料表中刪除存在於遠端資料表中，但未存在於已啟用延展功能之 SQL Server 資料表中的資料行。 如果遠端 Azure 資料表中有些資料行已不再存在於已啟用延展功能的 SQL Server 資料表中，這些額外的資料行並不會影響 Stretch Database 的正常運作。 您也可以手動移除額外的資料行。  
 
## <a name="manage-performance-and-costs"></a>管理效能和成本  
  
### <a name="troubleshoot-query-performance"></a>針對查詢效能進行疑難排解  
  如果查詢包含啟用 Stretch 功能的資料表，預期的執行速度會比之前未啟用 Stretch 功能時更慢。 如果查詢效能大幅降低，請檢閱下列可能的問題。  
  
-   您的 Azure 伺服器與 SQL Server 是否位於不同的地理區域？ 請將 Azure 伺服器設為與 SQL Server 相同的地理區域，以縮短網路延遲。  
  
-   您的網路狀況可能已降級。 如需最新問題或中斷情形的資訊，請連絡網路系統管理員。  
  
### <a name="increase-azure-performance-level-for-resource-intensive-operations-such-as-indexing"></a>針對資源密集作業 (例如編製索引)，增加 Azure 效能等級  
 如果您在針對 Stretch Database 設定的大型資料表上建置、重建或重新組織索引，且預期會在 Azure 中同時進行已移轉資料的密集查詢，請考慮增加作業期間相對應的遠端 Azure 資料庫的效能等級。 如需效能層級和定價的詳細資訊，請參閱 [SQL Server Stretch Database 定價](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)。  
  
### <a name="you-cant-pause-the-sql-server-stretch-database-service-on-azure"></a>您無法暫停 Azure 上的 SQL Server Stretch Database 服務  
 請務必選取適當的效能和定價層級。 如果您暫時提高需要大量資源之作業的效能層級，請在作業完成之後，將它還原至先前的層級。 如需效能層級和定價的詳細資訊，請參閱 [SQL Server Stretch Database 定價](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)。  
   
 ## <a name="change-the-scope-of-queries"></a>變更查詢的範圍  
 查詢已啟用延展功能的資料表時，預設會傳回本機和遠端資料。 您可以針對所有使用者進行的一切查詢，或系統管理員進行的單一查詢來變更查詢範圍。  
   
 ### <a name="change-the-scope-of-queries-for-all-queries-by-all-users"></a>針對所有使用者進行的一切查詢來變更查詢範圍  
 若要針對所有使用者進行的一切查詢來變更查詢範圍，請執行 **sys.sp_rda_set_query_mode**預存程序。 您可以將範圍縮小為僅查詢本機資料、停用所有查詢，或還原預設範圍。 如需詳細資訊，請參閱 [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)。  
   
 ### <a name="change-the-scope-of-queries-for-a-single-query-by-an-administrator"></a><a name="queryHints"></a>針對系統管理員進行的單一查詢來變更查詢範圍  
 若要變更 db_owner 角色成員進行的單一查詢範圍，請將 **WITH ( REMOTE_DATA_ARCHIVE_OVERRIDE = *value* )** 查詢提示加入 SELECT 陳述式中。 REMOTE_DATA_ARCHIVE_OVERRIDE 查詢提示可以為下列值。  
 -   **LOCAL_ONLY**。 僅查詢本機資料。  
   
 -   **REMOTE_ONLY**。 僅查詢遠端資料。  
   
 -   **STAGE_ONLY**。 僅查詢下列資料表中的資料：Stretch Database 會在該資料表中暫存可進行移轉的資料列，並在移轉後的指定期間內保留已移轉的資料列。 這個查詢提示是查詢暫存資料表的唯一方法。  
  
例如，下列查詢僅會傳回本機結果。  
  
 ```sql  
USE <Stretch-enabled database name>;
GO
SELECT * FROM <Stretch_enabled table name> WITH (REMOTE_DATA_ARCHIVE_OVERRIDE = LOCAL_ONLY) WHERE ... ;
GO
```  
   
 ## <a name="make-administrative-updates-and-deletes"></a><a name="adminHints"></a>進行管理更新和刪除  
 在已啟用延展功能的資料表中，依預設無法 UPDATE (更新) 或 DELETE (刪除) 可進行移轉的資料列或已移轉的資料列。 當您必須修正問題時，db_owner 角色的成員可將 **WITH ( REMOTE_DATA_ARCHIVE_OVERRIDE = *value* )** 查詢提示加入陳述式中，以執行 UPDATE 或 DELETE 作業。 REMOTE_DATA_ARCHIVE_OVERRIDE 查詢提示可以為下列值。  
 -   **LOCAL_ONLY**。 僅更新或刪除本機資料。  
   
 -   **REMOTE_ONLY**。 僅更新或刪除遠端資料。  
   
 -   **STAGE_ONLY**。 僅更新或刪除下列資料表中的資料：Stretch Database 會在該資料表中暫存可進行移轉的資料列，並在移轉後的指定期間內保留已移轉的資料列。  
  
## <a name="see-also"></a>另請參閱  
 [監視和疑難排解資料移轉 &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)   
[備份已啟用延展功能的資料庫 &#40;Stretch Database&#41;](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
[還原已啟用延展功能的資料庫 &#40;Stretch Database&#41;](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
  
