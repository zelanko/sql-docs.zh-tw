---
title: 系統版本設定時態表與記憶體最佳化資料表 | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 23274522-e5cf-4095-bed8-bf986d6342e0
caps.latest.revision: 16
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 6b06f92184a4adc301ba29e9422f357f09394cc9
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39546318"
---
# <a name="system-versioned-temporal-tables-with-memory-optimized-tables"></a>系統版本設定時態表與記憶體最佳化資料表
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [記憶體最佳化資料表](../../relational-databases/in-memory-oltp/memory-optimized-tables.md) 之系統版本設定時態表的設計，是為了在利用記憶體內部 OLTP 工作負載所收集的最上層資料需要 [資料稽核與時間點分析](http://msdn.microsoft.com/library/mt631669.aspx) 時，提供符合成本效益的解決方案。 它們提供高交易處理能力、無鎖定同時並行處理，儲存大量歷程記錄資料並可輕鬆查詢的功能。  
  
## <a name="overview"></a>概觀  
 系統版本設定時態表會自動保留資料變更的完整歷程記錄，並公開便利的 Transact-SQL 延伸模組以進行時間點分析。 在一般案例中，即使沒有經常查詢資料記錄，資料記錄仍會保留很長一段時間 (數個月甚至是數年)。  
  
 資料稽核及以時間為基礎的分析可能在不同環境中要求，特別是在處理極大量要求數目以及使用記憶體內部 OLTP 技術的 OLTP 系統中。 不過，在時態表案例中使用記憶體最佳化資料表很困難，因為大量產生的歷程記錄資料通常會超過可用 RAM 記憶體的限制。 同時，使用 RAM 來儲存隨著越舊而越少存取的唯讀歷程記錄資料並非最佳的解決方案。  
  
 記憶體最佳化資料表的系統版本設定時態表提供高交易處理能力，無鎖定同時並行處理，使用記憶體中資料表儲存目前資料 (時態表)，並使用磁碟資料表儲存歷程記錄資料，提供儲存大量歷程記錄資料的功能。 透過使用內部、自動產生的記憶體最佳化暫存資料表 (其中儲存最近歷程記錄) 並使 DML 可以從原生編譯的程式碼執行，對於 DML 作業的影響會最小化。  
  
 下圖說明此架構。![暫時的記憶體內部架構](../../relational-databases/tables/media/temporal-in-memory-architecture.png "暫時的記憶體內部架構")  
  
## <a name="implementation-details"></a>實作細節  
 下列關於系統版本設定時態表與記憶體最佳化表格的事實，是當您建立系統建立版本記憶體最佳化資料表時，必須注意的考量。 如需語法選項及範例，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)。  
  
-   只有持久的記憶體最佳化資料表可以是系統建立版本 (**DURABILITY = SCHEMA_AND_DATA**)。  
  
-   記憶體最佳化系統建立版本資料表的歷程記錄資料表，必須是以磁碟為基礎，無論它是由使用者或系統建立。  
  
-   只有影響目前資料表 (記憶體內部) 的查詢可用於 [原生編譯的 T-SQL 模組](https://msdn.microsoft.com/en-us/library/dn133184.aspx)。 原生編譯的模組不支援使用 FOR SYSTEM TIME 子句的暫時查詢。 支援在特定查詢和非原生模組中搭配使用 FOR SYSTEM TIME 子句和記憶體最佳化資料表。  
  
-   當 **SYSTEM_VERSIONING = ON**時，內部記憶體最佳化暫存資料表會自動建立，以接受最近的系統控制版本變更，該變更是在記憶體最佳化目前資料表上更新與刪除作業的結果。  
  
-   內部記憶體最佳化暫存資料表的資料，會透過非同步資料排清工作定期移動至磁碟歷程記錄資料表。 此資料排清機制的目標，是將它們父物件的內部記憶體緩衝區耗用量維持低於 10%。 您可以藉由查詢 [sys.dm_db_xtp_memory_consumers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md) 並從內部記憶體最佳化暫存資料表和目前時態表摘要資料，追蹤記憶體最佳化系統版本設定時態表的總記憶體耗用量。  
  
-   您可以叫用 [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md) 來強制執行資料排清。  
  
-   當 **SYSTEM_VERSIONING = OFF** 或系統版本設定資料表的結構描述因為新增、卸除或改變資料行而修改時，整個內部暫存緩衝區的內容會移至磁碟記錄資料表。  
  
-   歷程記錄資料的查詢實際上位於快照隔離等級下，且一律會傳回記憶體內部暫存緩衝區與磁碟資料表的聯集而不會重複。   
  
-   在內部變更資料表結構描述的**ALTER TABLE** 作業必須執行資料排清，這可能會延長作業的期間。  
  
## <a name="the-internal-memory-optimized-staging-table"></a>內部記憶體最佳化暫存資料表  
 內部記憶體最佳化暫存資料表是由系統建立的內部物件，用來最佳化 DML 作業。  
  
-   資料表名稱會以下列格式產生：**Memory_Optimized_History_Table_<物件識別碼>**，其中 <物件識別碼> 是目前時態表的識別碼。  
  
-   資料表會複寫目前時態表的結構描述，加上一個 BIGINT 資料行。 這個額外的資料行可保證移動到內部歷程記錄緩衝區之資料列的唯一性。  
  
-   額外的資料行具有下列名稱格式：**Change_ID[_<後置詞>]**，其中 *_\<後置詞>* 是在資料表已經有 *Change_ID* 資料行時選擇性加入。  
  
-   因為暫存資料表中額外的 BIGINT 資料行，系統建立版本記憶體最佳化資料表的資料列大小上限減少 8 個位元組。 現在新的最大值為 8052 位元組。  
  
-   內部記憶體最佳化暫存資料表不會出現在 SQL Server Management Studio 的「物件總管」中。  
  
-   關於此資料表的中繼資料與其目前時態表的連線，可在 [sys.internal_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md) 中找到。  
  
## <a name="the-data-flush-task"></a>資料排清工作  
 資料排清是定期啟動的工作，檢查是否有任何記憶體最佳化資料表符合資料移動的記憶體大小條件。 當內部暫存資料表的記憶體耗用量到達目前時態表記憶體耗用量的 8% 時，就會開始移動資料。  
  
 資料排清工作會依排程 (視現有的工作負載而定) 定期啟動。 較重的工作負載時，頻率為每 5 秒，較輕的工作負載時，頻率為每 1 分鐘。 針對每個需要清除的內部記憶體最佳化暫存資料表會產生一個執行序。  
  
 資料排清會刪除比目前執行之最舊的交易還舊的記憶體內部內部緩衝區記錄，將這些記錄移動到磁碟歷程記錄資料表。  
  
 您可以叫用 [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md) 並指定結構描述和資料表名稱來強制執行資料排清：   
**sys.sp_xtp_flush_temporal_history @schema_name，@object_name**。 利用這個使用者執行的命令，當資料排清工作由系統依據內部排程叫用時，會叫用相同的資料移動程序。  
  
## <a name="see-also"></a>另請參閱  
 [時態表](../../relational-databases/tables/temporal-tables.md)   
 [開始使用系統建立版本的時態表](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [時態表使用案例](../../relational-databases/tables/temporal-table-usage-scenarios.md)   
 [時態表系統一致性檢查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [對時態表進行資料分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [時態表考量與限制](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [時態表安全性](../../relational-databases/tables/temporal-table-security.md)   
 [管理系統設定版本之時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [暫存資料表中繼資料檢視和函數](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
