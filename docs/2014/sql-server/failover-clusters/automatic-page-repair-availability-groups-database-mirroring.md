---
title: 自動頁面修復 （適用於可用性群組和資料庫鏡像） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- automatic page repair
- Availability Groups [SQL Server], automatic page repair
- database mirroring [SQL Server], automatic page repair
- suspect pages [SQL Server]
ms.assetid: cf2e3650-5fac-4f34-b50e-d17765578a8e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f4f39024817d3d0aa35c015ed815eb8f412f1c8e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63137509"
---
# <a name="automatic-page-repair-for-availability-groups-and-database-mirroring"></a>自動修復頁面 (適用於可用性群組和資料庫鏡像)
  資料庫鏡像與 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 都支援自動修復頁面。 在頁面因為某些錯誤類型而損毀、無法讀取之後，資料庫鏡像夥伴 (主體或鏡像) 或可用性複本 (主要或次要) 會嘗試自動復原頁面。 無法讀取頁面的夥伴/複本會向其夥伴或另一個複本要求一個全新頁面副本。 如果這個要求成功，無法讀取的頁面就會被可讀取的副本取代，而這通常會解決錯誤。  
  
 一般來說，資料庫鏡像和 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 會以相等方式處理 I/O 錯誤。 幾個差異會在這裡明確標註。  
  
> [!NOTE]  
>  自動修復頁面不同於 DBCC 修復。 自動修復頁面會保留所有資料。 相反地，利用 DBCC REPAIR_ALLOW_DATA_LOSS 選項來更正錯誤，可能需要刪除某些頁面，因而也需要刪除某些資料。  
  
  
  
##  <a name="ErrorTypes"></a> 造成嘗試自動修復頁面的錯誤類型  
 資料庫鏡像的自動修復頁面僅會嘗試修復在操作資料檔案時，因為下表列出的其中一個錯誤而失敗的頁面。  
  
|錯誤號碼|描述|造成嘗試自動修復頁面的執行個體|  
|------------------|-----------------|---------------------------------------------------------|  
|[823](../../relational-databases/errors-events/mssqlserver-823-database-engine-error.md)|只有當作業系統在資料上執行循環冗餘檢查 (CRC) 失敗時，才會採取動作。|ERROR_CRC。 這項錯誤的作業系統值為 23。|  
|[824](../../relational-databases/errors-events/mssqlserver-824-database-engine-error.md)|邏輯錯誤。|邏輯資料錯誤，例如，分次寫入或頁面總和檢查碼錯誤。|  
|829|頁面已標示為還原暫止。|全部。|  
  
 若要檢視最近的 823 CRC 錯誤和 824 錯誤，請參閱 [msdb](/sql/relational-databases/system-tables/suspect-pages-transact-sql) 資料庫中的 [suspect_pages](../../relational-databases/databases/msdb-database.md) 資料表。  
  
  
  
##  <a name="UnrepairablePageTypes"></a> 無法自動修復的頁面類型  
 自動修復頁面無法修復下列控制頁類型：  
  
-   檔案標頭頁面 (頁面識別碼 0)。  
  
-   第 9 頁 (資料庫啟動頁面)。  
  
-   配置頁面：全域配置對應 (GAM) 頁面、 共用全域配置對應 (SGAM) 頁面，以及頁面可用空間 (PFS) 頁面。  
  

  
##  <a name="PrimaryIOErrors"></a> 處理主體/主要資料庫的 I/O 錯誤  
 在主體/主要資料庫上，只有當資料庫處於 SYNCHRONIZED 狀態，而且主體/主要資料庫仍在將資料庫的記錄檔記錄傳送到鏡像/次要資料庫時，才會嘗試自動修復頁面。 自動修復頁面的基本動作順序如下所示：  
  
1.  在主體/主要資料庫的資料頁面上發生讀取錯誤時，主體/主要資料庫會在 [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) 資料表中插入一個資料列，列出適當的錯誤狀態。 如果是資料庫鏡像，主體資料庫接著就會向鏡像資料庫要求頁面的副本。 如果是 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]，主要資料庫會向所有次要資料庫廣播要求，並從第一個回應的次要資料庫取得頁面。 此要求會指定目前在已排清記錄檔結尾的頁面識別碼和 LSN。 該頁面會標示為 *還原暫止*。 這樣就無法在嘗試進行自動修復頁面期間存取該頁面。 在嘗試修復期間存取此頁面的嘗試將會失敗，其錯誤為 829 (還原暫止)。  
  
2.  收到頁面要求後，鏡像/次要資料庫會等到已經將記錄重做到要求中指定的 LSN 為止。 然後，鏡像/次要資料庫就會嘗試存取其資料庫副本中的頁面。 如果可以存取頁面，鏡像/次要資料庫就會將該頁面的副本傳送到主體/主要資料庫。 否則，鏡像/次要資料庫會將錯誤傳回主體/主要資料庫，而且自動修復頁面嘗試會失敗。  
  
3.  主體/主要資料庫會處理包含全新頁面副本的回應。  
  
4.  自動修復頁面修復可疑頁面之後，該頁面在 **suspect_pages** 資料表中會標示為已還原 (**event_type** = 5)。  
  
5.  如果頁面 I/O 錯誤造成任何 [延遲的交易](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)，修復該頁面後，主體/主要資料庫會嘗試解決那些交易。  
  

  
##  <a name="SecondaryIOErrors"></a> 處理鏡像/次要資料庫的 I/O 錯誤  
 資料庫鏡像與 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]通常會以相同方式處理鏡像/次要資料庫上發生的資料頁面 I/O 錯誤。  
  
1.  對於資料庫鏡像，如果鏡像資料庫在重做記錄檔記錄時遇到一個或多個頁面 I/O 錯誤，鏡像工作階段會進入 SUSPENDED 狀態。 對於 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]，如果次要複本在重做記錄檔記錄時遇到一個或多個頁面 I/O 錯誤，次要資料庫會進入 SUSPENDED 狀態。 此時，鏡像/次要資料庫會在 **suspect_pages** 資料表中插入一個資料列，列出適當的錯誤狀態。 鏡像/次要資料庫接著就會向主體/主要資料庫要求頁面的副本。  
  
2.  主體/主要資料庫會嘗試存取其資料庫副本中的頁面。 如果可以存取頁面，主體/主要資料庫就會將該頁面的副本傳送到鏡像/次要資料庫。  
  
3.  如果鏡像/次要資料庫收到所要求之每個頁面的副本，鏡像/次要資料庫會嘗試繼續鏡像工作階段。 如果自動修復頁面修復可疑頁面，該頁面在 **suspect_pages** 資料表中會標示為已還原 (**event_type** = 4)。  
  
     如果鏡像/次要資料庫沒有收到向主體/主要資料庫要求的頁面，自動修復頁面嘗試會失敗。 對於資料庫鏡像，鏡像工作階段保持暫停。 對於 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]，次要資料庫也會保持暫停。 如果手動繼續鏡像工作階段或次要資料庫，在同步處理階段期間，將會再次叫用損毀的頁面。  

  
##  <a name="DevBP"></a> Developer Best Practice  
 自動修復頁面是在背景中執行的非同步程序。 因此，要求無法讀取之頁面的資料庫作業也會失敗，而且會針對造成失敗的情況，傳回錯誤碼。 開發鏡像資料庫或可用性資料庫的應用程式時，您應該攔截失敗作業的例外狀況。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤碼為 823、824 或 829，您應該稍後重試該作業。  
  

  
##  <a name="ViewAPRattempts"></a> 操作說明：檢視自動修復頁面嘗試  
 下列動態管理檢視會針對給定可用性資料庫或鏡像資料庫上進行的最新自動修復頁面嘗試行為傳回資料列，每個資料庫最多 100 個資料列。  
  
-   **AlwaysOn 可用性群組：**  
  
     [sys.dm_hadr_auto_page_repair &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql)  
  
     針對可用性複本上的任何可用性資料庫進行的每個自動修復頁面嘗試行為，各傳回一個資料列，該可用性複本是針對伺服器執行個體的任何可用性群組所裝載。  
  
-   **資料庫鏡像：**  
  
     [sys.dm_db_mirroring_auto_page_repair &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-auto-page-repair)  
  
     針對在伺服器執行個體之任何鏡像資料庫上進行的每個自動修復頁面嘗試行為，各傳回一個資料列。  
  
 
  
## <a name="see-also"></a>另請參閱  
 [管理 suspect_pages 資料表 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)   
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
