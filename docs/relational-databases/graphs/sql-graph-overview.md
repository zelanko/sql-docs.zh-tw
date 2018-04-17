---
title: 處理使用 SQL Server 和 Azure SQL Database 的圖形 |Microsoft 文件
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: graphs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: cc6951aa90bf71cb415770f30352120a529bcde1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>處理使用 SQL Server 和 Azure SQL Database 的圖形
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供圖形塑造多對多關聯性的資料庫功能。 圖形的關聯性已整合到[!INCLUDE[tsql-md](../../includes/tsql-md.md)]和使用的益處[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]為基礎的資料庫管理系統。


## <a name="what-is-a-graph-database"></a>什麼是圖形資料庫？  
圖形資料庫是節點 （或端點） 的集合和邊緣 （或關聯性）。 節點代表實體 （例如，個人或組織） 和邊緣表示連接 （適用於例如類似或朋友） 的兩個節點之間的關聯性。 節點和邊緣可能與其相關聯的屬性。 以下是一些功能，使圖表資料庫唯一：  
-   邊緣或關聯性是第一個類別的實體圖形資料庫中，可以有屬性與其相關聯。 
-   單一邊緣可以彈性地連接圖形資料庫中的多個節點。
-   您可以表示模式比對和多重躍點瀏覽查詢輕鬆。
-   輕鬆地可以表示遞移封閉和多型查詢。

## <a name="when-to-use-a-graph-database"></a>使用圖表資料庫的時機

沒有任何可以達到圖形資料庫，這不能利用關聯式資料庫來達成。 不過，圖表資料庫可以輕鬆來表示特定種類的查詢。 此外，特定的最佳化，某些查詢可能會更好。 若要選擇哪一個決策可以根據下列因素：  
-   您的應用程式具有階層式資料。 HierarchyID 資料類型可以用來實作的階層，但有一些限制。 例如，它不允許您將儲存多個節點的父代。
-   您的應用程式具有複雜的多對多關聯性;當應用程式的發展，就會加入新的關聯性。
-   您需要分析互連的資料和關聯性。

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>圖形中所引進的功能 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
我們已經開始圖形擴充功能加入 SQL Server，若要簡化儲存和查詢的圖形資料。 在第一個版本中推出了下列功能。 


### <a name="create-graph-objects"></a>建立圖形物件
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] 擴充功能可讓使用者建立節點或邊緣資料表。 節點和邊緣可以有與它們相關聯的屬性。 因為節點和邊緣會儲存為資料表中，節點或邊緣的資料表上都支援關聯式資料表才支援的所有作業。 範例如下：  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![人員的朋友資料表](../../relational-databases/graphs/media/person-friends-tables.png "/people/person 節點與朋友邊緣資料表")  
節點和邊緣儲存成資料表  

### <a name="query-language-extensions"></a>查詢語言擴充功能  
新`MATCH`子句已引入來支援模式比對和多重躍點瀏覽圖形。 `MATCH`函式會使用 ASCII 封面樣式語法進行模式比對。 例如：  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>完全整合在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]引擎 
Graph 延伸模組已完全整合在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]引擎。 我們使用相同的儲存引擎、 中繼資料，查詢處理器 」 等，來儲存和查詢圖形資料。 這可讓使用者透過其圖形和單一查詢中的關聯式資料查詢。 使用者也可以從圖形功能結合其他獲益[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]技術類似的資料行存放區，HA、 R 服務等。SQL 圖形資料庫也支援所有的安全性與相容性功能適用於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。
 
### <a name="tooling-and-ecosystem"></a>工具和生態系統  
使用者可從現有的工具和生態系統，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供。 工具，例如備份與還原、 匯入和匯出，請立即可用的 BCP 運作。 其他工具或 SSIS、 SSRS 等 PowerBI 服務將會使用圖形資料表只可使用關聯式資料表的方式。
 
 ## <a name="next-steps"></a>後續的步驟  
讀取[SQL 圖形 Database-架構](./sql-graph-architecture.md)
   

