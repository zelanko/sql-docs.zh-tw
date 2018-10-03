---
title: 圖形處理與 SQL Server 和 Azure SQL Database |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4d6e3a5e26fd40fc4f2fca093a41048aa7e3c5b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695897"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>SQL Server 和 Azure SQL Database 的圖表處理
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供圖形資料庫功能來塑造多對多關聯性。 圖形的關聯性已整合到[!INCLUDE[tsql-md](../../includes/tsql-md.md)]接收使用的優點和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]做為基礎的資料庫管理系統。


## <a name="what-is-a-graph-database"></a>什麼是一種圖表資料庫？  
圖表資料庫是節點 （或端點） 的集合和邊緣 （或關聯性）。 節點表示 （例如，個人或組織） 的實體，邊緣表示連接 （適用於範例中，按讚數或朋友） 的兩個節點之間的關聯性。 節點和邊緣都可能有與其相關聯的屬性。 以下是一些功能，使圖表資料庫的唯一：  
-   邊緣或關聯性是第一級實體中的圖表資料庫，可以有屬性與其相關聯。 
-   單一邊緣可以彈性地連接圖形資料庫中的多個節點。
-   您可以表示模式比對和多重躍點瀏覽查詢輕鬆。
-   輕鬆地可以表示遞移封閉和多型查詢。

## <a name="when-to-use-a-graph-database"></a>使用圖表資料庫的時機

沒有可以達成圖形資料庫，它不能使用關聯式資料庫來達成。 不過，圖表資料庫可以輕鬆地表達某些類型的查詢。 此外，使用特定的最佳化，某些查詢可能會更好。 您決定来選擇哪一個可以根據下列因素：  
-   您的應用程式具有階層式資料。 HierarchyID 資料類型可以用來實作的階層，但有一些限制。 比方說，它不允許您儲存多個節點的父代。
-   您的應用程式具有複雜的多對多關聯性;當應用程式的發展，會加入新的關聯性。
-   您要分析相互連接的資料和關聯性。

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>圖形中所引進的功能 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
我們將開始加入 SQL Server，以便於儲存和查詢的圖形資料的圖表延伸模組。 第一版中引進下列功能。 


### <a name="create-graph-objects"></a>建立圖形物件
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] 擴充功能可讓使用者建立節點或邊緣資料表。 節點和邊緣都可以有與其相關聯的屬性。 因為節點和邊緣會儲存為資料表中，節點或 edge 資料表上都支援關聯式資料表才支援的所有作業。 範例如下：  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![人員朋友表格](../../relational-databases/graphs/media/person-friends-tables.png "/people/person 節點和 friend 邊緣資料表")  
節點和邊緣會儲存為資料表  

### <a name="query-language-extensions"></a>查詢語言擴充功能  
新`MATCH`子句為了要支援模式比對和多重躍點瀏覽圖形。 `MATCH`函式會使用 ASCII 作品樣式語法進行模式比對。 例如：  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>完全整合在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]引擎 
圖表延伸模組已完全整合在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]引擎。 使用相同的儲存體引擎、 中繼資料，查詢處理器等，來儲存和查詢圖形資料。 跨圖，並在單一查詢中的關聯式資料的查詢。 圖形功能結合其他[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]等資料行存放區，HA，R services，技術等等。SQL graph database 也支援所有的安全性和合規性功能適用於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。
 
### <a name="tooling-and-ecosystem"></a>工具和生態系統

受益於現有的工具和生態系統，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供。 工具，例如備份與還原、 匯入和匯出，請立即可用的 BCP 都可運作。 其他工具或服務，例如 SSIS、 SSRS、 或 Power BI 會使用圖形資料表的關聯式表格運作方式。

## <a name="edge-constraints"></a>邊緣條件約束
邊緣條件約束圖形邊緣資料表上定義，而且是一組指定的邊緣類型可連接的節點資料表。 這可讓使用者透過其圖形結構描述更佳控制。 透過邊緣條件約束的協助，使用者可以限制允許連接指定的邊緣節點的類型。 

若要深入了解如何建立和使用邊緣條件約束，請參閱[邊緣條件約束](../../relational-databases/tables/graph-edge-constraints.md)

## <a name="merge-dml"></a>合併 DML 
[合併](../../t-sql/statements/merge-transact-sql.md)陳述式會執行插入、 更新或刪除與來源資料表聯結的結果為基礎的目標資料表上的作業。 例如，您可以同步處理兩個資料表插入、 更新或刪除根據目標資料表與來源資料表之間的差異在目標資料表中的資料列。 Azure SQL Database 和 SQL Server vNext 現在支援使用 MERGE 陳述式中的相符項目述詞。 也就是說，現可使用符合述詞來指定在單一陳述式，而不是個別的 INSERT/UPDATE/DELETE 陳述式中的圖形關聯性的新資料與合併您目前的圖表資料 （節點或邊緣資料表）。

若要了解如何使用相符項目，在合併 DML 參閱[MERGE 陳述式](../../t-sql/statements/merge-transact-sql.md)

 ## <a name="next-steps"></a>後續步驟  
讀取[SQL 圖形資料庫架構](./sql-graph-architecture.md)
   

