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
ms.openlocfilehash: f60ded18e88d57c5a2975b567fa246923ece7ebe
ms.sourcegitcommit: f6bfe4a0647ce7efebaca11d95412d6a9a92cd98
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2019
ms.locfileid: "71974365"
---
# <a name="how-query-store-collects-data"></a>查詢存放區如何收集資料
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SQL Server 查詢存放區可當作飛行資料記錄器來使用，不斷地收集與查詢和計劃相關的編譯和執行階段資訊。 查詢相關的資料會保存於內部資料表，並透過一組檢視呈現給使用者。
  
## <a name="views"></a>檢視 
 下圖顯示查詢存放區檢視及其邏輯關聯性，以及顯示為藍色實體的編譯時間資訊︰
  
 ![查詢存放區程序檢視](../../relational-databases/performance/media/query-store-process-2views.png "query-store-process-2views")  
**檢視描述**  
  
|檢視|Description|  
|----------|-----------------|  
|**sys.query_store_query_text**|顯示針對資料庫執行的唯一查詢文字。 查詢文字前後的註解和空格會被忽略。 不會忽略文字內的註解和空格。 批次中的每個陳述式都會產生個別的查詢文字項目。|  
|**sys.query_context_settings**|顯示在其下執行查詢之影響計劃設定的唯一組合。 使用不同影響計劃設定來執行的相同查詢文字，會在查詢存放區中產生不同的查詢項目，因為 `context_settings_id` 是查詢索引鍵的一部分。|  
|**sys.query_store_query**|在查詢存放區中個別追蹤和強制執行的查詢項目。 如果單一查詢文字會在不同的內容設定下執行，或在不同的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 模組 (預存程序、觸發程序等) 內部與外部執行，則可以產生多個查詢項目。|  
|**sys.query_store_plan**|顯示查詢的估計計畫以及編譯時間統計資料。 預存計劃相當於您使用 `SET SHOWPLAN_XML ON` 所得到的計劃。|  
|**sys.query_store_runtime_stats_interval**|查詢存放區會將時間細分為自動產生的時間範圍 (間隔)，並在每個執行計畫的該間隔中儲存彙總統計資料。 間隔的大小，是透過設定選項 [統計資料收集間隔]  (在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中) 或使用 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) 的 `INTERVAL_LENGTH_MINUTES` 來控制。|  
|**sys.query_store_runtime_stats**|針對執行計畫彙總的執行階段統計資料。 所有擷取的計量均會以四個統計函式形式來表示：平均值、最小值、最大值及標準差。|  
  
 如需查詢存放區檢視的詳細資訊，請參閱[使用查詢存放區監視效能](monitoring-performance-by-using-the-query-store.md)中的＜相關檢視、函式與程序＞一節。 
  
## <a name="query-processing"></a>查詢處理
 查詢存放區會在下列關鍵點，與查詢處理管線互動︰
  
1.  當查詢第一次進行編譯時，會將查詢文字和初始計劃傳送至查詢存放區。
  
2.  當查詢重新編譯時，會在查詢存放區中更新計劃。 如果建立了新計劃，查詢存放區就會為查詢新增新計劃項目，並保留先前項目以及它們的執行統計資料。
  
3.  當查詢執行之後，會立即將執行階段統計資料傳送至查詢存放區。 針對已在目前有效間隔內執行的每個計畫，查詢存放區會維持其彙總統計資料的準確性。 
  
4.  在編譯和檢查以進行重新編譯階段期間，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會判斷查詢存放區中是否有計劃應該針對目前執行的查詢加以套用。 如果有強制執行的計劃且程序快取中計劃與所強制執行計劃不同，則查詢會重新編譯。 實際上這個方式就像將 PLAN HINT 套用到該查詢一樣。 此程序會明確地發生於使用者應用程式中。 
  
 下圖說明先前步驟所述的整合時機︰
  
 ![查詢存放區程序](../../relational-databases/performance/media/query-store-process-2processor.png "query-store-process-2processor") 

## <a name="remarks"></a>Remarks
 為了減少 I/O 額外負荷，會從記憶體內部擷取新資料。 寫入作業會排入佇列，並隨後排清至磁碟。 查詢和計劃資訊 (在下圖中顯示為計劃存放區) 會以最快速度排清。 執行階段統計資料 (顯示為執行階段統計資料) 會保留在記憶體中，時間長短依 `SET QUERY_STORE` 陳述式 `DATA_FLUSH_INTERVAL_SECONDS` 選項所定義的期限。 您可以使用 [[!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 查詢存放區] 對話方塊輸入 [資料排清間隔 (分鐘)]  的值，這會在內部轉換為秒。 
  
 ![查詢存放區程序計劃](../../relational-databases/performance/media/query-store-process-3.png "query-store-process-3plan") 
  
 如果在使用[追蹤旗標 7745](../../relational-databases/performance/best-practice-with-the-query-store.md#Recovery) 時發生系統當機或關機，則查詢存放區可能會遺失已收集但尚未保存的執行時間資料，最多至 `DATA_FLUSH_INTERVAL_SECONDS` 所定義的時間範圍。 我們建議使用預設值 900 秒 (15 分鐘) 作為查詢擷取效能與資料可用性之間的平衡。
 
 > [!IMPORTANT] 
 > 系統不會嚴格強制執行 [大小上限 (MB)]  的限制。 只有當查詢存放區將資料寫入磁碟時，系統才會檢查儲存體大小。 此間隔是由 [資料排清間隔]  值所設定。 如果查詢存放區違反儲存體大小檢查之間的大小上限，即會轉換為唯讀模式。 如果啟用 [大小基礎的清除模式]  ，也會觸發強制執行大小上限的清除機制。
 
 > [!NOTE]
 > 如果有記憶體壓力，執行階段統計資料就能在使用 `DATA_FLUSH_INTERVAL_SECONDS` 所定義的時間之前排清至磁碟。
 
 讀取查詢存放區期間，記憶體內部資料和磁碟上的資料會明顯地一致。 
 
 如果工作階段終止，或者用戶端應用程式重新啟動或當機，將不會記錄查詢統計資料。 
  
 ![查詢存放區程序計劃資訊](../../relational-databases/performance/media/query-store-process-4planinfo.png "query-store-process-4planinfo")    

## <a name="see-also"></a>另請參閱
 [使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [查詢存放區的最佳做法](../../relational-databases/performance/best-practice-with-the-query-store.md)  
 [查詢存放區目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md) 
  
  
