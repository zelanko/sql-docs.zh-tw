---
title: 圖表處理
titleSuffix: SQL Server and Azure SQL Database
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: ''
author: shkale-msft
ms.author: shkale
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2b0934562f2f0ff1a2dd3ec8df1ed15f10d955ee
ms.sourcegitcommit: 6e7696a169876eb914f79706d022451a1213eb6b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428149"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>SQL Server 和 Azure SQL Database 的圖表處理
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供圖形資料庫功能來建立多對多關聯性的模型。 圖形關聯性會整合到[!INCLUDE[tsql-md](../../includes/tsql-md.md)]中，並獲得使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]做為基礎資料庫管理系統的優點。


## <a name="what-is-a-graph-database"></a>什麼是圖形資料庫？  
圖表資料庫是節點 (或頂點) 與邊線 (或關聯性) 的集合。 節點代表實體 (例如，個人或組織)，而邊緣代表其所連接的兩個節點之間的關聯性 (例如，按讚數或朋友)。 節點和邊緣可能會有相關聯的屬性。 以下是讓圖表資料庫變成唯一的一些功能：  
-    邊緣或關聯性是圖形資料庫中的第一級實體，可以有與其相關聯的屬性。 
-    單一邊緣可以彈性地連接圖形資料庫中的多個節點。
-    您可以輕鬆地表達模式比對和多躍點導覽查詢。
-    您可以輕鬆地表達遞移閉包和多型查詢。

## <a name="when-to-use-a-graph-database"></a>使用圖形資料庫的時機

關係資料庫可以達到圖形資料庫的任何目標。 不過，圖表資料庫可讓您更輕鬆地表達特定種類的查詢。 此外，使用特定的優化功能，某些查詢的效能可能較佳。 您決定選擇關聯式或圖形資料庫的方式，取決於下列因素：  
-    您的應用程式有階層式資料。 HierarchyID 資料類型可以用來執行階層，但有一些限制。 例如，它不允許您儲存節點的多個父代。
-    您的應用程式具有複雜的多對多關聯性;隨著應用程式發展，會加入新的關聯性。
-    您需要分析互連的資料和關聯性。

## <a name="graph-features-introduced-in-sssqlv14"></a>中引進的圖形功能[!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
我們即將開始將圖形擴充功能新增至 SQL Server，讓您更輕鬆地儲存和查詢圖形資料。 第一版引進了下列功能。 


### <a name="create-graph-objects"></a>建立繪圖物件
[!INCLUDE[tsql-md](../../includes/tsql-md.md)]擴充功能可讓使用者建立節點或邊緣資料表。 節點和邊緣都可以有相關聯的屬性。 因為節點和邊緣會儲存為數據表，所以在節點或邊緣資料表上支援關係資料表所支援的所有作業。 下列是一個範例：  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![人員-朋友-資料表](../../relational-databases/graphs/media/person-friends-tables.png "Person 節點和朋友邊緣資料表")  
節點和邊緣會儲存為數據表  

### <a name="query-language-extensions"></a>查詢語言延伸模組  
引進`MATCH` New 子句來支援模式比對，以及透過圖形的多重躍點導覽。 `MATCH`函式會使用 ASCII 藝術樣式語法來進行模式比對。 例如：  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-ssnoversion-engine"></a>在引擎中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]完全整合 
圖表延伸模組已完全整合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到引擎中。 使用相同的儲存引擎、中繼資料、查詢處理器等來儲存和查詢圖形資料。 在單一查詢中跨圖表和關聯式資料進行查詢。 結合圖形功能與其他[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]技術（例如資料行存放區、HA、R 服務等）。SQL graph 資料庫也支援所提供的所有安全性和合規性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]功能。
 
### <a name="tooling-and-ecosystem"></a>工具和生態系統

受益于提供的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]現有工具和生態系統。 「備份與還原」、「匯入和匯出」之類的工具，BCP 只是現成可用的。 其他工具或服務（如 SSIS、SSRS 或 Power BI）將會使用圖表資料表，就像使用關聯式資料表一樣。

## <a name="edge-constraints"></a>邊緣條件約束
邊緣條件約束是在圖形邊緣資料表上定義，而且是指定的邊緣類型可以連接的一對節點資料表。 這可讓使用者更有效地控制其圖形架構。 透過 edge 條件約束的協助，使用者可以限制指定邊緣允許連接的節點類型。 

若要深入瞭解如何建立和使用邊緣條件約束，請參閱[邊緣條件約束](../../relational-databases/tables/graph-edge-constraints.md)

## <a name="merge-dml"></a>合併 DML 
[MERGE](../../t-sql/statements/merge-transact-sql.md)語句會根據與來源資料表聯結的結果，在目標資料表上執行插入、更新或刪除作業。 例如，您可以根據目標資料表與來源資料表之間的差異，在目標資料表中插入、更新或刪除資料列，以同步處理兩個數據表。 Azure SQL Database 和 SQL Server vNext 現在支援在 MERGE 語句中使用 MATCH 述詞。 也就是說，現在可以使用 MATCH 述詞，將目前的圖形資料（節點或邊緣資料表）與新資料合併，以在單一語句中指定圖形關聯性，而不是個別的 INSERT/UPDATE/DELETE 子句。

若要深入瞭解如何在 merge DML 中使用 match，請參閱[Merge 語句](../../t-sql/statements/merge-transact-sql.md)

## <a name="shortest-path"></a>最短路徑
[SHORTEST_PATH](./sql-graph-shortest-path.md)函式會尋找圖形中任何2個節點之間的最短路徑，或從指定節點開始到圖形中的所有其他節點。 最短路徑也可以用來尋找可轉移的關閉或圖形中的任意長度周遊。 

 ## <a name="next-steps"></a>後續步驟  
讀取[SQL Graph 資料庫-架構](./sql-graph-architecture.md)
   

