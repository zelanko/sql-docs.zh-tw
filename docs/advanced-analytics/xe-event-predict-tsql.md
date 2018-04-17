---
title: 擴充事件監視預測陳述式 |Microsoft 文件
titleSuffix: SQL Server
ms.custom: ''
ms.date: 03/01/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: d517da44f989620003fef35d2e4721eead15d5d5
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
---
# <a name="extended-events-for-monitoring-predict-statements"></a>擴充的事件監視預測陳述式

這篇文章描述擴充的事件，提供 SQL Server 中可用來監視及分析作業使用[預測](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)執行 SQL Server 中的即時計分。

即時計分從的機器學習儲存在 SQL Server 中的模型產生分數。 PREDICT 函數不需要外部執行階段例如 R 或 Python，已使用特定的二進位格式建立的模型。 如需詳細資訊，請參閱[即時計分](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)。

## <a name="prerequisites"></a>필수 구성 요소

如需擴充的事件 （有時稱為 XEvents），以及如何追蹤的事件工作階段中的一般資訊，請參閱下列文章：

+ [擴充事件概念與架構](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [在 SSMS 中的事件擷取設定](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [管理 [物件總管] 中的事件工作階段](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>擴充事件列表

下列擴充的事件是適用於所有版本的 SQL Server 支援[T-SQL 預測](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)陳述式，包括 SQL Server on Linux 及 Azure SQL Database。 

SQL Server 2017 中引進了 T-SQL 的預測陳述式。 

|name |object_type|description| 
|----|----|----|
|predict_function_completed |event  |內建的執行時間細分|
|predict_model_cache_hit |event|從預測函數模型快取中擷取模型時，就會發生。 使用此事件及其他 predict_model_cache_ * 事件，對預測函式模型快取所造成的問題進行疑難排解。|
|predict_model_cache_insert |event  |   當模型是預測函式模型快取插入，就會發生。 使用此事件及其他 predict_model_cache_ * 事件，對預測函式模型快取所造成的問題進行疑難排解。    |
|predict_model_cache_miss   |event|預測函式模型快取中找不到模型時，就會發生。 如果經常發生此事件可能表示 SQL Server 需要更多記憶體。 使用此事件及其他 predict_model_cache_ * 事件，對預測函式模型快取所造成的問題進行疑難排解。|
|predict_model_cache_remove |event| 發生於從預測函式的模型快取中移除模型。 使用此事件及其他 predict_model_cache_ * 事件，對預測函式模型快取所造成的問題進行疑難排解。|

## <a name="query-for-related-events"></a>查詢的相關事件

若要檢視這些事件所傳回的所有資料行的清單，請在 SQL Server Management Studio 中執行下列查詢：

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>範例

若要擷取計分工作階段使用預測的效能相關資訊：

1. 建立新的擴充事件工作階段，使用 Management Studio 或其他支援[工具](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)。
2. 加入事件`predict_function_completed`和`predict_model_cache_hit`到工作階段。
3. 啟動擴充的事件工作階段。
4. 執行會使用預測查詢。

在結果中，檢閱這些資料行：

+ 值`predict_function_completed`顯示多少時間花在載入模型和計分的查詢。
+ 布林值`predict_model_cache_hit`指出查詢是否或不使用快取的模型。 

### <a name="native-scoring-model-cache"></a>原生計分模型快取

除了預測特定的事件，您可以使用下列查詢來取得快取的模型和快取使用量的詳細資訊：

檢視原生的計分模型快取：

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

