---
title: Microsoft SQL 資料庫中的智慧查詢處理 | Microsoft Docs
description: 可改善 SQL Server 和 Azure SQL Database 查詢效能的智慧查詢處理功能。
ms.custom: ''
ms.date: 05/22/2018
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
ms.openlocfilehash: 7786fd048f1698c90f379450b31e0bac3457706e
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
ms.locfileid: "34455762"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 資料庫中的智慧查詢處理
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

**智慧查詢處理**功能系列都包含具有廣泛影響的功能，能夠以最少的實作投入量改善現有工作負載的效能。   這包括改善既有的建構，同時引進彈性的方法和功能。  

## <a name="adaptive-query-processing"></a>彈性查詢處理
在智慧查詢處理功能系列中是 SQL Server 2017 和 Azure SQL Database 中引進的彈性查詢處理功能系列，其新增整體的新查詢處理功能，可根據應用程式工作負載的執行階段條件來調整最佳化策略：
- **批次模式自適性聯結**。 這項功能可讓您的計劃在使用單一快取計畫的執行期間，以動態方式切換到較好的聯結策略。
- **批次模式記憶體授與意見反應**。 這項功能將會重新計算查詢所需的實際記憶體，然後更新快取計劃的授與值，減少影響並行存取的過多記憶體授與，並修正導致佔用大量磁碟資源的低估記憶體授與。
- **交錯執行多重陳述式資料表值函式 (MSTVF)**. 利用交錯執行，我們可以使用函式的實際資料列計數制定更明智的下游查詢計劃決策。 

如需彈性查詢處理的詳細資訊，請參閱 [SQL 資料庫中的彈性查詢處理](../../relational-databases/performance/adaptive-query-processing.md)。

## <a name="see-also"></a>另請參閱
[SQL Server 資料庫引擎和 Azure SQL Database 的效能中心](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[查詢處理架構指南](../../relational-databases/query-processing-architecture-guide.md)    
[執行程序邏輯和實體運算子參考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[聯結](../../relational-databases/performance/joins.md)    
[示範彈性查詢處理](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)        
