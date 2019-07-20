---
title: 監視 PREDICT 陳述式的擴充事件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1c534681200abf056c8bc7dd3745d8098d59c146
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345660"
---
# <a name="extended-events-for-monitoring-predict-statements"></a>監視 PREDICT 陳述式的擴充事件

本文描述 SQL Server 中提供的擴充事件, 您可以用來監視和分析使用[PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)在 SQL Server 中執行即時評分的作業。

即時計分會從已儲存在 SQL Server 中的機器學習模型產生分數。 PREDICT 函數不需要外部執行時間 (例如 R 或 Python), 只有使用特定二進位格式建立的模型。 如需詳細資訊, 請參閱[即時評分](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)。

## <a name="prerequisites"></a>必要條件

如需擴充事件 (有時稱為 XEvents) 的一般資訊, 以及如何追蹤會話中的事件, 請參閱下列文章:

+ [擴充事件概念和架構](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [在 SSMS 中設定事件捕獲](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [管理物件總管中的事件會話](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>擴充事件的資料表

下列擴充事件適用于支援[T-SQL PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)語句的所有 SQL Server 版本, 包括 Linux 上的 SQL Server 和 Azure SQL Database。 

T-SQL PREDICT 語句是在 SQL Server 2017 中引進。 

|name |object_type|description| 
|----|----|----|
|predict_function_completed |event  |內建執行時間細目|
|predict_model_cache_hit |event|從 PREDICT 函數模型快取中抓取模型時發生。 使用此事件以及其他 predict_model_cache_ * 事件, 針對 PREDICT 函數模型快取所造成的問題進行疑難排解。|
|predict_model_cache_insert |event  |   當模型插入預測函數模型快取中時發生。 使用此事件以及其他 predict_model_cache_ * 事件, 針對 PREDICT 函數模型快取所造成的問題進行疑難排解。    |
|predict_model_cache_miss   |event|在 PREDICT 函數模型快取中找不到模型時發生。 經常發生此事件可能表示 SQL Server 需要更多記憶體。 使用此事件以及其他 predict_model_cache_ * 事件, 針對 PREDICT 函數模型快取所造成的問題進行疑難排解。|
|predict_model_cache_remove |event| 從模型快取中移除模型以進行 PREDICT 函數時發生。 使用此事件以及其他 predict_model_cache_ * 事件, 針對 PREDICT 函數模型快取所造成的問題進行疑難排解。|

## <a name="query-for-related-events"></a>查詢相關事件

若要查看針對這些事件傳回的所有資料行清單, 請在 SQL Server Management Studio 中執行下列查詢:

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>範例

若要使用 PREDICT 來捕捉評分會話效能的相關資訊:

1. 使用 Management Studio 或其他支援的[工具](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)來建立新的擴充事件會話。
2. 將事件`predict_function_completed`和`predict_model_cache_hit`新增至會話。
3. 啟動擴充的事件會話。
4. 執行使用 PREDICT 的查詢。

在結果中, 檢查下列資料行:

+ 的值`predict_function_completed`會顯示查詢載入模型和計分所花費的時間。
+ 的布林值`predict_model_cache_hit`表示查詢是否使用快取模型。 

### <a name="native-scoring-model-cache"></a>原生評分模型快取

除了預測的特定事件以外, 您還可以使用下列查詢來取得有關快取模型和快取使用量的詳細資訊:

查看原生評分模型快取:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

查看模型快取中的物件:

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

