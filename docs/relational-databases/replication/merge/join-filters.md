---
title: "聯結篩選 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "篩選 [SQL Server 複寫], 聯結"
  - "發行集 [SQL Server 複寫], 聯結篩選"
  - "合併式複寫聯結篩選 [SQL Server 複寫]"
  - "聯結篩選"
ms.assetid: dd78fd8f-56e3-4582-9abd-6bc25c91e075
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 聯結篩選
  聯結篩選可讓您根據發行集內相關資料表的篩選方式來篩選資料表。 通常，父資料表會使用參數化篩選進行篩選，然後一或多個聯結篩選會以您在資料表之間定義聯結的相同方式進行定義。 聯結篩選可以擴充參數化篩選，以便僅當資料與聯結篩選子句相符時，才複寫相關資料表中的資料。  
  
 聯結篩選通常會遵循為套用到之資料表所定義的主索引鍵/外部索引鍵關聯性，但並非嚴格受限於主索引鍵/外部索引鍵關聯性。 聯結篩選可基於任何比較兩資料表中相關資料的邏輯。  
  
 請考慮使用 [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] 範本資料庫中的下列資料表，這些資料表透過主索引鍵到外部索引鍵的關聯性相關聯：  
  
-   **HumanResources.Employee**  
  
-   **Sales.SalesOrderHeader**  
  
-   **Sales.SalesOrderDetail**  
  
 這些資料表無法在應用程式中用來支援行動銷售團隊，但是它們必須如此，每個篩選中的銷售人員 **HumanResources.Employee** 資料表收到只有客戶的訂單與相關資料。  
  
 第一個步驟是在父資料表，即在此範例中定義參數化的篩選 **HumanResources.Employee** 資料表。 此資料表包含資料行 **LoginID**, ，其中包含登入表單中的每一位員工 *網域 \ 使用者名稱*。 若要篩選此資料表，以使各員工僅收到與其相關的資料，請指定參數化篩選子句：  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 此篩選器可確保每位員工的訂閱僅包含資料 **HumanResources.Employee** （這在此情況下是單一資料列） 該員工相關的資料表。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
 第二步要使用與指定兩資料表之間聯結類似的語法，將此篩選擴充到所有相關資料表。 第一個聯結篩選子句為：  
  
```  
Employee.EmployeeID = SalesOrderHeader.SalesPersonID  
```  
  
 此子句可確保訂閱中只包含與各業務員相關的訂單資料。 第二個聯結篩選子句為：  
  
```  
SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
```  
  
 此子句可確保訂閱中只包含與各業務員訂單資料相關的詳細資料。 此範例只顯示每個聯結點聯結一個資料表的情況，您還可在每個聯結點上聯結多個資料表。  
  
 聯結篩選可以加入一次透過新的發行集精靈 」 和 **發行集屬性** 對話方塊中，也可以以程式設計方式加入。 透過「新增發行集精靈」可自動產生聯結篩選：為資料表指定一個資料列篩選，然後聯結篩選會套用到所有相關的資料表。 如需詳細資訊，請參閱 [定義及修改聯結篩選之間合併發行項](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md), ，[自動產生設定聯結篩選之間合併發行項的 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md), ，和 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
## 最佳化聯結篩選效能  
 下列指導方針有助於最佳化聯結篩選效能：   
  
-   限制聯結篩選階層中資料表的數量。  
  
     聯結篩選可以包含無限數量的資料表，但如果篩選中的資料表數量過多，會嚴重影響合併處理過程中的效能。 若您正在產生五個以上資料表的聯結篩選，請考慮其他方案：不要篩選小型、無法變更或主要為查詢資料表的資料表。 聯結篩選只能用於必須在訂閱中分割的資料表之間。  
  
-   設定 **聯結唯一索引鍵** 選項 **True** 適當的位置。  
  
     如果父資料表中聯結資料行是唯一的，則合併處理可實現特殊效能最佳化。 如果聯結條件根據唯一資料行，設定 **聯結唯一索引鍵** 聯結篩選的選項。 如需設定此選項的詳細資訊，請參閱上一節列出的如何主題。  
  
-   確定聯結篩選中參考的資料行已進行索引。  
  
     如果篩選中參考的資料行已進行索引，則複寫能夠更有效地處理篩選。  
  
-   請勿建立模仿聯結篩選的資料列篩選。  
  
     在 WHERE 子句中使用子查詢可建立模仿聯結篩選的資料列篩選，例如：  
  
    ```  
    WHERE Customer.SalesPersonID IN (SELECT EmployeeID FROM Employee WHERE LoginID = SUSER_SNAME())   
    ```  
  
     強烈建議以聯結篩選而不是子查詢表示所有上述邏輯。 如果應用程式要求資料列篩選使用子查詢，請確定子查詢僅參考查閱資料 (不進行變更)。  
  
## 另請參閱  
 [篩選合併式複寫之發行的資料](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [參數化資料列篩選器](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  