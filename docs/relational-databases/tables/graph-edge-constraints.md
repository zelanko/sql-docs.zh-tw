---
title: 圖形邊緣條件約束 | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 86544dee5262a1d04c1ff1d8e59f8ddac5e9b5ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "64774652"
---
# <a name="edge-constraints"></a>邊緣條件約束
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  邊緣條件約束可以用來強制執行資料完整性以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 圖形資料庫之邊緣資料表上的特定語意。 
  
本文包含下列各節。  
  
[邊緣條件約束](../../relational-databases/tables/graph-edge-constraints.md#Connection)  

[邊緣條件約束](../../relational-databases/tables/graph-edge-constraints.md#Connection)  
  
[相關工作](../../relational-databases/tables/graph-edge-constraints.md#Tasks)  
  
##  <a name="Connection"></a> 邊緣條件約束
 在第一版的圖形功能中，邊緣資料表不會強制執行邊緣端點的任何項目。 亦即，圖形資料庫中的邊緣可以將任何節點連線至任何其他節點，不論類型為何。 

 此版本引進邊緣條件約束，讓使用者將條件約束新增至其邊緣資料表，藉此強制執行特定語意同時維護資料完整性。 使用邊緣條件約束將新的邊緣新增至邊緣資料表時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會強制邊緣所嘗試連線的節點存在於正確的節點資料表。 如果邊緣仍然參考節點，則也確保無法卸除節點。 

 ### <a name="edge-constraint-clauses"></a>邊緣條件約束子句
 每個邊緣條件約束都是由一或多個邊緣條件約束子句所組成。 邊緣條件約束子句是由一對 FROM 與指定邊緣可連線的 TO 節點所組成。 

 假設您的圖形中有 `Product` 和 `Customer` 節點，而且您使用 `Bought` 邊緣來連線這些節點。 邊緣條件約束子句指定 FROM 和 TO 節點配對以及邊緣方向。 在此情況下，邊緣條件約束子句會是 `Customer` TO `Product`。 亦即，允許插入從 `Customer` 流向 `Product` 的 `Bought`。 嘗試插入從 `Product` 流向 `Customer` 的邊緣失敗。 
  
- 邊緣條件約束子句包含強制執行邊緣條件約束的一對 FROM 與 TO 節點資料表。 
  
- 使用者可以為每個邊緣條件約束指定將套用為分離的多個邊緣條件約束子句。

- 如果在單一邊緣資料表上建立多個邊緣條件約束，則邊緣必須滿足允許的 ALL 條件約束。
  
### <a name="indexes-on-edge-constraints"></a>邊緣條件約束的索引
 建立邊緣條件約束並不會自動在邊緣資料表的 `$from_id` 和 `$to_id` 資料行上建立對應的索引。 如果您有點查閱查詢或 OLTP 工作負載，則建議在 `$from_id` 和 `$to_id` 配對上手動建立索引。 

##  <a name="Tasks"></a> 相關工作  
 下表列出與邊緣條件約束建立關聯的一般工作。  
  
|工作|發行項|  
|----------|-----------|  
|描述如何建立邊緣條件約束。|[建立邊緣條件約束](../../relational-databases/tables/create-edge-constraints.md)|  
|描述如何刪除邊緣條件約束。|[刪除邊緣條件約束](../../relational-databases/tables/delete-edge-constraint.md)|  
|描述如何修改邊緣條件約束。|[修改邊緣條件約束](../../relational-databases/tables/modify-edge-constraint.md)|  
|描述如何檢視邊緣條件約束屬性。|[檢視邊緣條件約束屬性](../../relational-databases/tables/view-edge-constraint-properties.md)|  
