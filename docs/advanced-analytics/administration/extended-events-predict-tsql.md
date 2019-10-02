---
title: 監視使用擴充事件來預測 T-sql
description: 瞭解如何使用擴充事件來監視和疑難排解 SQL Server Machine Learning 服務中的 SQL 語句。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 958ac3e24a9deec231e7fd4d5da14477d693f4de
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714302"
---
# <a name="monitor-predict-t-sql-statements-with-extended-events-in-sql-server-machine-learning-services"></a>使用 SQL Server Machine Learning 服務中的擴充事件來監視預測 T-sql 語句

瞭解如何使用擴充事件來監視[和疑難排解 SQL Server](../../t-sql/queries/predict-transact-sql.md) Machine Learning 服務中的 SQL 語句。

## <a name="table-of-extended-events"></a>擴充事件的資料表

下列擴充事件適用于所有支援[PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) t-sql 語句的 SQL Server 版本。 

|name |object_type|description| 
|----|----|----|
|predict_function_completed |event  |內建執行時間細目|
|predict_model_cache_hit |event|從 PREDICT 函數模型快取中抓取模型時發生。 使用此事件以及其他 predict_model_cache_ * 事件，針對 PREDICT 函數模型快取所造成的問題進行疑難排解。|
|predict_model_cache_insert |event  |   當模型插入預測函數模型快取中時發生。 使用此事件以及其他 predict_model_cache_ * 事件，針對 PREDICT 函數模型快取所造成的問題進行疑難排解。    |
|predict_model_cache_miss   |event|在 PREDICT 函數模型快取中找不到模型時發生。 經常發生此事件可能表示 SQL Server 需要更多記憶體。 使用此事件以及其他 predict_model_cache_ * 事件，針對 PREDICT 函數模型快取所造成的問題進行疑難排解。|
|predict_model_cache_remove |event| 從模型快取中移除模型以進行 PREDICT 函數時發生。 使用此事件以及其他 predict_model_cache_ * 事件，針對 PREDICT 函數模型快取所造成的問題進行疑難排解。|

## <a name="query-for-related-events"></a>查詢相關事件

若要查看針對這些事件傳回的所有資料行清單, 請在 SQL Server Management Studio 中執行下列查詢:

```sql
SELECT * 
FROM sys.dm_xe_object_columns 
WHERE object_name LIKE `predict%'
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

## <a name="next-steps"></a>後續步驟

如需擴充事件（有時稱為 XEvents）以及如何在會話中追蹤事件的詳細資訊，請參閱下列文章：

+ [使用 SQL Server Machine Learning Services 中的擴充事件來監視 Python 和 R 腳本](extended-events.md)
+ [擴充事件概念和架構](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [在 SSMS 中設定事件捕獲](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [管理物件總管中的事件會話](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)
