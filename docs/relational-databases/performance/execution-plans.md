---
title: 執行計劃 | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- query execution plans
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753f
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 9bf75c2d176c4ea2c596f29f1ddda910e794ae12
ms.sourcegitcommit: ba7fb4b9b4f0dbfe77a7c6906a1fde574e5a8e1e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303231"
---
# <a name="execution-plans"></a>執行計劃
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

為了能夠執行查詢，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 必須分析陳述式來判斷存取必要資料最有效率的方式。 這項分析會由稱為「查詢最佳化工具」的元件處理。 查詢最佳化工具的輸入是由查詢、資料庫結構描述 (資料表和索引定義) 以及資料庫統計資料所組成。 查詢最佳化工具的輸出即是查詢執行計劃，有時稱為查詢計劃或執行計劃。   

查詢執行計畫是用以定義下列項目： 

* 存取來源資料表的順序。  
  一般而言，資料庫伺服器存取基底資料表以建立結果集的順序有很多種。 例如，如果 `SELECT` 陳述式參考三個資料表，則資料庫伺服器可能會先存取 `TableA`、使用 `TableA` 中的資料來擷取 `TableB` 中相符資料列，然後使用 `TableB` 中的資料來擷取 `TableC` 中資料。 資料庫伺服器可以存取資料表的其他順序如下：  
  `TableC`、 `TableB`、 `TableA`或  
  `TableB`、 `TableA`、 `TableC`或  
  `TableB`、 `TableC`、 `TableA`或  
  `TableC`、 `TableA`、 `TableB`  

* 從各資料表取得資料所用的方法。  
  一般而言，有各種不同的方式可存取每個資料表中的資料。 如果僅需要特定索引鍵值的一些資料列，則資料庫伺服器可以使用索引。 如果需要資料表中的所有資料列，則資料庫伺服器可以忽略索引，並執行資料表掃描。 如果需要資料表中的所有資料列，但其中有一個索引的索引鍵資料行是在 `ORDER BY`中，那麼，執行索引掃描來替代資料表掃描，就能儲存不同排序的結果集。 如果資料表非常小，則資料表掃描可能是所有資料表存取中最有效率的方式。

> [!TIP]
> 如需查詢處理和查詢執行計劃的詳細資訊，請參閱[查詢處理架構指南](../../relational-databases/query-processing-architecture-guide.md)。

## <a name="in-this-section"></a>本節內容  
  
-   [查詢分析基礎結構](../../relational-databases/performance/query-profiling-infrastructure.md)  
  
-   [顯示並儲存執行計畫](../../relational-databases/performance/display-and-save-execution-plans.md)  
  
-   [比較及分析執行計劃](../../relational-databases/performance/compare-and-analyze-execution-plans.md)  

-   [計畫指南](../../relational-databases/performance/plan-guides.md)  

## <a name="see-also"></a>另請參閱  
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [效能監視及微調工具](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [查詢處理架構指南](../../relational-databases/query-processing-architecture-guide.md)    
 [即時查詢統計資料](../../relational-databases/performance/live-query-statistics.md)     
 [活動監視器](../../relational-databases/performance-monitor/activity-monitor.md)     
 [使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [執行程序邏輯和實體運算子參考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)
