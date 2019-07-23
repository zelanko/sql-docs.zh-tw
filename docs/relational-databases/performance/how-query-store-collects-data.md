---
title: 查詢存放區如何收集資料 | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, data collection
ms.assetid: 8d5eec36-0013-480a-9c11-183e162e4c8e
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83fbc6c183216cedcbb664a0c3a2e3a9337e1513
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946776"
---
# <a name="how-query-store-collects-data"></a>查詢存放區如何收集資料
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  查詢存放區可當作 **飛行資料記錄器** 來使用，不斷地收集與查詢和計畫相關的編譯和執行階段資訊。 查詢相關的資料會保存於內部資料表，並透過一組檢視呈現給使用者。  
  
## <a name="views"></a>檢視  
 下圖顯示查詢存放區檢視及其邏輯關聯性，以及顯示為藍色實體的編譯時間資訊︰  
  
 ![query-store-process-2views](../../relational-databases/performance/media/query-store-process-2views.png "query-store-process-2views")  
**檢視描述**  
  
|檢視|Description|  
|----------|-----------------|  
|**sys.query_store_query_text**|顯示針對資料庫執行的唯一查詢文字。 查詢文字前後的註解和空格會被忽略。 不會忽略文字內的註解和空格。 批次中的每個陳述式都會產生個別的查詢文字項目。|  
|**sys.query_context_settings**|顯示會影響執行查詢之設定的獨特計畫組合。 使用影響設定的不同計畫來執行的相同查詢文字，會在查詢存放區中產生不同的查詢項目，因為 `context_settings_id` 是查詢索引鍵的一部分。|  
|**sys.query_store_query**|在查詢存放區中個別追蹤和強制執行的查詢項目。 如果單一查詢文字會在不同的內容設定下執行或在不同的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 模組 (預存程序、觸發程序等) 內部與外部執行，則它可以產生多個查詢項目。|  
|**sys.query_store_plan**|顯示查詢的估計計畫以及編譯時間統計資料。 預存的計畫相當於您使用 `SET SHOWPLAN_XML ON`所得到的計畫。|  
|**sys.query_store_runtime_stats_interval**|查詢存放區會將時間細分為自動產生的時間範圍 (間隔)，並在每個執行計畫的該間隔中儲存彙總統計資料。 間隔的大小是透過組態選項 「統計資料收集間隔」 (在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中) 或使用 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) 的 `INTERVAL_LENGTH_MINUTES` 來控制。|  
|**sys.query_store_runtime_stats**|針對執行計畫彙總的執行階段統計資料。 所有擷取的計量均會以 4 個統計函式形式來表示：平均值、最小值、最大值及標準差。|  
  
 如需查詢存放區檢視的詳細資訊，請參閱[使用查詢存放區監視效能](monitoring-performance-by-using-the-query-store.md)中的**相關檢視、函數與程序**一節。  
  
## <a name="query-processing"></a>查詢處理  
 查詢存放區會在下列關鍵時刻，與查詢處理管線互動︰  
  
1.  當查詢第一次進行編譯時，會將查詢文字和初始計畫傳送至查詢存放區  
  
2.  當查詢重新編譯時，會在查詢存放區中更新計畫。 如果建立了新計畫，查詢存放區就會為查詢加入新的計畫項目，並保留先前的項目以及它們的執行統計資料。  
  
3.  當查詢執行之後，會立即將執行階段統計資料傳送至查詢存放區。 針對已在目前有效間隔內執行的每個計畫，查詢存放區會維持其彙總統計資料的準確性。  
  
4.  在編譯和檢查以進行重新編譯階段期間， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會判斷查詢存放區中是否有計畫應該針對目前執行的查詢加以套用。 如果有強制執行的計畫且程序快取中的計畫與強制執行的計畫不同，則查詢會重新編譯，實際上這個方式就像將 PLAN HINT 套用到該查詢一樣。 此程序會明確地發生於使用者應用程式中。  
  
 下圖說明上述的整合時機︰  
  
 ![query-store-process-2processor](../../relational-databases/performance/media/query-store-process-2processor.png "query-store-process-2processor")  
  
 為了減少 I/O 額外負荷，會從記憶體內部擷取新資料。 寫入作業會排入佇列，隨後排清至磁碟。 查詢和計畫資訊 (見下圖的計劃存放區) 會以最快速度排清。 執行階段統計資料 (執行階段統計資料) 會保留在記憶體中，時間長短依 `SET QUERY_STORE` 陳述式 `DATA_FLUSH_INTERVAL_SECONDS` 選項所定義的期限。 SSMS 的 [查詢存放區] 對話方塊讓您輸入 [資料排清間隔 (分鐘)]  ，其可轉換為秒。  
  
 ![query-store-process-3plan](../../relational-databases/performance/media/query-store-process-3.png "query-store-process-3plan")  
  
 如果系統損毀，查詢存放區就會遺失執行階段資料，最多遺失使用 `DATA_FLUSH_INTERVAL_SECONDS` 所定義的數量。 預設值 900 秒 (15 分鐘) 是查詢擷取效能與資料可用性之間的最佳平衡。  
如果有記憶體壓力，執行階段統計資料就能在使用 `DATA_FLUSH_INTERVAL_SECONDS` 所定義的時間之前排清至磁碟。  
讀取查詢存放區期間，記憶體內部資料和磁碟上的資料會完全一樣。
如果工作階段終止，或者用戶端應用程式重新啟動或當機，將不會記錄查詢統計資料。  
  
 ![query-store-process-4planinfo](../../relational-databases/performance/media/query-store-process-4planinfo.png "query-store-process-4planinfo")    

  
## <a name="see-also"></a>另請參閱  
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [使用查詢存放區的最佳作法](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [查詢存放區目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
