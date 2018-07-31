---
title: Microsoft SQL 資料庫中的智慧查詢處理 | Microsoft Docs
description: 可改善 SQL Server 和 Azure SQL Database 查詢效能的智慧查詢處理功能。
ms.custom: ''
ms.date: 07/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6f1b215e95b7cc911cd2815493eabbbd53a47424
ms.sourcegitcommit: a162a8f02d66c13b32d0b6255b0b52fc80e2187e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2018
ms.locfileid: "39250446"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 資料庫中的智慧查詢處理
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

**智慧查詢處理**功能系列都包含具有廣泛影響的功能，能夠以最少的實作投入量改善現有工作負載的效能。

![智慧查詢處理功能](./media/1_IQPFeatureFamily.png)

## <a name="adaptive-query-processing"></a>彈性查詢處理
彈性查詢處理功能系列包括查詢處理改良功能，可調整最佳化策略以符合您應用程式工作負載的執行階段條件。 包含以下改良功能：批次模式自適性聯結、記憶體授與意見反應，以及交錯執行多重陳述式資料表值函式。

### <a name="batch-mode-adaptive-joins"></a>批次模式自適性聯結
這項功能可讓您的計劃在使用單一快取計畫的執行期間，以動態方式切換到較好的聯結策略。

### <a name="row-and-batch-mode-memory-grant-feedback"></a>資料列和批次模式記憶體授與意見反應
這項功能將會重新計算查詢所需的實際記憶體，然後更新快取計劃的授與值，減少影響並行存取的過多記憶體授與，並修正導致佔用大量磁碟資源的低估記憶體授與。

### <a name="interleaved-execution-for-multi-statement-table-valued-functions-mstvfs"></a>交錯執行多重陳述式資料表值函式 (MSTVF)
利用交錯執行，我們可以使用函式的實際資料列計數制定更明智的下游查詢計劃決策。 

如需詳細資訊，請參閱 [SQL 資料庫中的彈性查詢處理](../../relational-databases/performance/adaptive-query-processing.md)。

## <a name="table-variable-deferred-compilation"></a>資料表變數延遲編譯
資料表變數延遲編譯可針對參考資料表變數的查詢，提升計劃品質和整體效能。 在最佳化和初始編譯期間，此功能將會根據實際資料表變數的資料列計數，傳播基數估計值。  這個精確的資料列計數資訊將用於最佳化下游計劃作業。

使用資料表變數延遲編譯時，會延遲編譯參考資料表變數的陳述式，直到第一次實際執行陳述式為止。 這個延遲編譯行為與暫存資料表的行為完全相同，而且此變更會導致使用實際基數，而不是原始的單一資料列猜測。 若要在 Azure SQL Database 中啟用資料表變數延遲編譯的公開預覽功能，請在執行查詢時，針對您所連線的資料庫，啟用資料庫相容性層級 150。

如需詳細資訊，請參閱[資料表變數延遲編譯](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation ).

## <a name="approximate-query-processing"></a>近似查詢處理
近似查詢處理是一個新的功能系列，其設計目的在於提供大型資料集之間的彙總，在此情況下回應性比絕對精確度更重要。  例如，針對 10 億個資料列計算 COUNT(DISTINCT())，以顯示在儀表板上。  在此情況下，絕對精確度並不重要，但回應性很重要。 新的 APPROX_COUNT_DISTINCT 彙總函式會傳回群組中非 Null 的唯一值的近似數目。

如需詳細資訊，請參閱 [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md)。

## <a name="see-also"></a>另請參閱
[SQL Server 資料庫引擎和 Azure SQL Database 的效能中心](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[查詢處理架構指南](../../relational-databases/query-processing-architecture-guide.md)    
[執行程序邏輯和實體運算子參考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[聯結](../../relational-databases/performance/joins.md)    
[示範彈性查詢處理](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)        
