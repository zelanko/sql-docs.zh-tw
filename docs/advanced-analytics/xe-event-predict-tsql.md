---
title: 監視 PREDICT 陳述式-SQL Server Machine Learning 服務的擴充的事件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fa0d9d4ed647a6616c525533e696960784d09290
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63142310"
---
# <a name="extended-events-for-monitoring-predict-statements"></a>監視 PREDICT 陳述式的擴充事件

這篇文章描述的擴充的事件，提供 SQL Server 中，您可以使用監視及分析作業使用[PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)執行 SQL Server 中的即時評分。

即時評分，則會從機器學習 SQL Server 中已儲存的模型產生分數。 PREDICT 函式不需要外部執行階段例如 R 或 Python，使用特定的二進位格式已建立的模型。 如需詳細資訊，請參閱 <<c0> [ 即時評分](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)。

## <a name="prerequisites"></a>先決條件

如需擴充的事件 （有時稱為 XEvents），以及如何追蹤的事件工作階段中的一般資訊，請參閱下列文章：

+ [擴充事件概念與架構](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [在 SSMS 中的事件擷取設定](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [管理事件工作階段，在 [物件總管]](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>擴充事件列表

適用於 SQL server 支援的所有版本的下列的擴充事件很[T-SQL 預測](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)陳述式，包括 Linux 和 Azure SQL Database 上的 SQL Server。 

在 SQL Server 2017 引進了 T-SQL 預測陳述式。 

|NAME |object_type|description| 
|----|----|----|
|predict_function_completed |event  |內建執行時間分解|
|predict_model_cache_hit |event|發生於從 PREDICT 函式模型快取中擷取模型。 使用這個事件及其他 predict_model_cache_ * 事件，PREDICT 函式模型快取所造成的問題進行疑難排解。|
|predict_model_cache_insert |event  |   當模型插入 PREDICT 函式模型快取時發生。 使用這個事件及其他 predict_model_cache_ * 事件，PREDICT 函式模型快取所造成的問題進行疑難排解。    |
|predict_model_cache_miss   |event|PREDICT 函式模型快取中找不到模型時，就會發生。 如果經常發生此事件可能表示 SQL Server 需要更多的記憶體。 使用這個事件及其他 predict_model_cache_ * 事件，PREDICT 函式模型快取所造成的問題進行疑難排解。|
|predict_model_cache_remove |event| 從 PREDICT 函式模型快取中移除模型時，就會發生。 使用這個事件及其他 predict_model_cache_ * 事件，PREDICT 函式模型快取所造成的問題進行疑難排解。|

## <a name="query-for-related-events"></a>查詢相關的事件

若要檢視這些事件所傳回的所有資料行的清單，請在 SQL Server Management Studio 中執行下列查詢：

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>範例

若要擷取效能，使用 PREDICT 評分工作階段的相關資訊：

1. 建立新的擴充事件工作階段，使用 Management Studio 或其他支援[工具](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)。
2. 加入的事件`predict_function_completed`和`predict_model_cache_hit`工作階段。
3. 啟動擴充的事件工作階段。
4. 執行使用預測查詢。

在結果中，檢閱這些資料行：

+ 值`predict_function_completed`顯示多少時間花在載入模型及評分的查詢。
+ 布林值，如`predict_model_cache_hit`指出查詢是否用快取的模型。 

### <a name="native-scoring-model-cache"></a>原生評分的模型快取

除了預測特定的事件，您可以使用下列查詢來取得快取的模型和快取使用量的詳細資訊：

檢視原生評分模型快取：

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

檢視中的物件模型快取：

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

