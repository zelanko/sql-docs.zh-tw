---
title: 使用擴充事件監視 T-SQL
description: 了解如何使用擴充事件來監視 SQL Server 機器學習服務中的 PREDICT T-SQL 陳述式及針對其進行疑難排解。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/24/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4d3be71d304cb17392fcc4ec5a8796588de9d884
ms.sourcegitcommit: 48d60fe6b6991303a88936fb32322c005dfca2d8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2020
ms.locfileid: "85352315"
---
# <a name="monitor-predict-t-sql-statements-with-extended-events-in-sql-server-machine-learning-services"></a>使用 SQL Server 機器學習服務中的擴充事件來監視預測 PREDICT T-SQL 陳述式

了解如何使用擴充事件來監視 SQL Server 機器學習服務中的 [PREDICT](../../t-sql/queries/predict-transact-sql.md) T-SQL 陳述式及針對其進行疑難排解。

## <a name="table-of-extended-events"></a>擴充事件表

下列擴充事件在支援 [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) T-SQL 陳述式的所有 SQL Server 版本上都可用。 

|NAME |object_type|description| 
|----|----|----|
|predict_function_completed |event  |內建執行時間明細|
|predict_model_cache_hit |event|從 PREDICT 函式模型快取中擷取模型時發生。 請搭配其他 predict_model_cache_* 事件使用此事件，以針對 PREDICT 函式模型快取所造成的問題進行疑難排解。|
|predict_model_cache_insert |event  |   當模型 插入到 PREDICT 函式模型快取時發生。 請搭配其他 predict_model_cache_* 事件使用此事件，以針對 PREDICT 函式模型快取所造成的問題進行疑難排解。    |
|predict_model_cache_miss   |event|在 PREDICT 函式模型快取中找不到模型時發生。 經常發生此事件可能表示 SQL Server 需要更多記憶體。 請搭配其他 predict_model_cache_* 事件使用此事件，以針對 PREDICT 函式模型快取所造成的問題進行疑難排解。|
|predict_model_cache_remove |event| 從 PREDICT 函式的模型快取移除模型時發生。 請搭配其他 predict_model_cache_* 事件使用此事件，以針對 PREDICT 函式模型快取所造成的問題進行疑難排解。|

## <a name="query-for-related-events"></a>查詢相關事件

若要查看針對這些事件傳回的所有資料行清單，請在 SQL Server Management Studio 中執行下列查詢：

```sql
SELECT * 
FROM sys.dm_xe_object_columns 
WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>範例

使用 PREDICT 來擷取評分工作階段效能的相關資訊：

1. 使用 Management Studio 或其他支援的[工具](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)來建立新的擴充事件工作階段。
2. 將事件 `predict_function_completed` 與 `predict_model_cache_hit` 新增到工作階段。
3. 啟動擴充事件工作階段。
4. 執行使用 PREDICT 的查詢。

在結果中，檢閱這些資料行：

+ `predict_function_completed` 的值會顯示查詢載入模型及評分所花的時間。
+ `predict_model_cache_hit` 的布林值會指出查詢是否使用快取模型。 

### <a name="native-scoring-model-cache"></a>原生評分模型快取

除了 PREDICT 的特定事件之外，您還可以使用下列查詢來取得有關快取模型與快取使用狀況的詳細資訊：

檢視原生評分模型快取：

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

檢視模型快取中的物件：

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

## <a name="next-steps"></a>後續步驟

如需擴充事件 (有時稱為 XEvents) 以及如何在工作階段中追蹤事件的詳細資訊，請參閱下列文章：

+ [使用 SQL Server 機器學習服務中的擴充事件來監視 Python 與 R 指令碼](extended-events.md)
+ [擴充事件概念與架構](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [在 SSMS 中設定事件擷取](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [在物件總管中管理事件工作階段](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)
