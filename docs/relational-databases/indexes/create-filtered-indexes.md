---
description: 建立篩選的索引
title: 建立篩選的索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- filtered indexes [SQL Server], about filtered indexes
- designing indexes [SQL Server], filtered
- filtered indexes [SQL Server]
- nonclustered indexes [SQL Server], filtered
- indexes [SQL Server], filtered
ms.assetid: 25e1fcc5-45d7-4c53-8c79-5493dfaa1c74
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3f67ff91e6f5270c3bec207223eb3f72a070eea3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460371"
---
# <a name="create-filtered-indexes"></a>建立篩選的索引
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立篩選索引。 篩選索引是最佳化的非叢集索引，特別適合涵蓋從妥善定義的資料子集選取而來的查詢。 篩選索引會使用篩選述詞對資料表中的部分資料列進行索引。 與完整資料表索引相較，設計良好的篩選索引可以提升查詢效能、降低索引維護成本和儲存成本。  
  
 篩選索引可以提供全資料表索引所不及的下列優勢：  
  
-   **提升的查詢效能和計畫品質**  
  
     設計良好的篩選索引可以提升查詢效能和執行計畫品質，因為它比全資料表的非叢集索引來得小，且具有篩選統計資料。 篩選統計資料比全資料表統計資料更為正確，因為僅涵蓋篩選索引中的資料列。  
  
-   **降低的索引維護成本**  
  
     只有在資料操作語言 (DML) 陳述式影響到索引中的資料時，才會對索引進行維護。 與完整資料表的非叢集索引相較，篩選索引可以降低維護成本，因為後者較小且僅會在索引中的資料已變更時才會進行維護。 篩選索引的數量可能很多，特別是當其包含不常變更的資料時。 同樣地，如果篩選索引僅包含經常修改的資料，則因為索引的大小較小，更新統計資料的成本就會下降。  
  
-   **降低的索引儲存成本**  
  
     在不需要全資料表索引時，建立篩選索引可以縮減非叢集索引的磁碟儲存量。 您可以使用多個篩選索引來取代全資料表的非叢集索引，而不會大幅增加儲存需求。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [設計考量](#Design)  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法建立篩選的索引：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="design-considerations"></a><a name="Design"></a> 設計考量  
  
-   當資料行僅具有少數的查詢相關值時，可以在值的子集上建立篩選索引。 例如，當資料行中的值大部分都是 NULL 且查詢只會從非 NULL 值進行選取時，您可以針對非 NULL 的資料列建立篩選索引。 所產生的索引比在相同的索引鍵資料行上定義的全資料表非叢集索引還小，維護成本也比較低。  
  
-   當資料表具有異質資料列時，您可以針對一或多個資料類別建立篩選索引。 這會將查詢焦點縮小為資料表的特定區域，改善這些資料列的查詢效能。 同樣地，所產生的索引比完整資料表非叢集索引還小，維護成本也比較低。  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   您無法在檢視上建立篩選索引； 不過，如果在檢視中參考的資料表上定義篩選索引，則可為查詢最佳化工具提供多項優點。 如果查詢結果會是正確的，則查詢最佳化工具會針對從檢視進行選取的查詢考慮篩選索引。

-   篩選運算式中存取的資料行為 CLR 資料類型時，您無法在資料表上建立篩選過的索引。
  
-   篩選索引具有索引檢視表所不及的下列優勢：  
  
    -   降低的索引維護成本。 例如，相較於索引檢視表而言，查詢處理器會使用較少的 CPU 資源來更新篩選索引。  
  
    -   改善的計畫品質。 例如，在查詢編譯期間，查詢最佳化工具考慮使用篩選索引的情況會比對等的索引檢視表更多。  
  
    -   線上索引重建。 您可以在篩選索引可用於查詢時，重建篩選索引。 線上索引重建不支援索引檢視表。 如需詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) 的 REBUILD 選項。  
  
    -   非唯一索引。 篩選索引可以是非唯一的，而索引檢視表則必須是唯一的。  
  
-   篩選索引定義於單一資料表，且僅支援簡單[比較運算子](../../t-sql/language-elements/comparison-operators-transact-sql.md)。 如果需要參考多個資料表或具有複雜邏輯的篩選運算式，則應該建立檢視。 篩選索引不支援 `LIKE` 運算子。 
  
-   如果篩選索引運算式相等於查詢述詞，且查詢並未以篩選索引運算式中的資料行傳回查詢結果，則篩選索引運算式中的資料行不需要是篩選索引定義中的索引鍵或內含資料行。  
  
-   如果查詢述詞在不等於篩選索引運算式的比較中使用篩選索引運算式中的資料行，則該資料行應該是篩選索引定義中的索引鍵或內含資料行。  
  
-   如果篩選索引運算式中的資料行在查詢結果集中，則該資料行應該是篩選索引定義中的索引鍵或內含資料行。  
  
-   資料表的叢集索引鍵並不需要是篩選索引定義中的索引鍵或內含資料行。 叢集索引鍵會自動包含在所有非叢集的索引中 (包含篩選索引在內)。  
  
-   如果在篩選索引的篩選索引運算式中指定的比較運算子產生隱含或明確的資料轉換，則如果該轉換是發生在比較運算子的左側，就會發生錯誤。 解決方案是以資料轉換運算子 (CAST 或 CONVERT) 在比較運算子的右側寫下篩選索引運算式。  

- 檢閱 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md) 語法中用於建立已篩選索引的必要 SET 選項
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料表或檢視表的 ALTER 權限。 使用者必須是 **系統管理員** 固定伺服器角色的成員，或是 **db_ddladmin** 和 **db_owner** 固定資料庫角色的成員。 若要修改篩選索引運算式，請使用 CREATE INDEX WITH DROP_EXISTING。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-filtered-index"></a>建立篩選的索引  
  
1.  在 [物件總管] 中，按一下加號展開資料庫，此資料庫包含您要建立篩選索引的資料表。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開要建立篩選索引的資料表。  
  
4.  以滑鼠右鍵按一下 [索引] 資料夾，指向 [新增索引]，然後選取 [非叢集索引…]。  
  
5.  在 **[新增索引]** 對話方塊，於 **[一般]** 頁面上的 **[索引名稱]** 方塊中輸入新索引的名稱。  
  
6.  按一下 [索引鍵資料行] 下的 [新增...]。  
  
7.  在 [從 _table\_name_ 選取資料行] 對話方塊中，選取要新增至唯一索引之一或多個資料表資料行的一或多個核取方塊。  
  
8.  按一下 [確定]。  
  
9. 在 [篩選] 頁面的 [篩選運算式]底下，輸入要用來建立篩選索引的 SQL 運算式。  
  
10. 按一下 [確定]。  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-filtered-index"></a>建立篩選的索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Looks for an existing filtered index named "FIBillOfMaterialsWithEndDate"  
    -- and deletes it from the table Production.BillOfMaterials if found.   
    IF EXISTS (SELECT name FROM sys.indexes  
        WHERE name = N'FIBillOfMaterialsWithEndDate'  
        AND object_id = OBJECT_ID (N'Production.BillOfMaterials'))  
    DROP INDEX FIBillOfMaterialsWithEndDate  
        ON Production.BillOfMaterials  
    GO  
    -- Creates a filtered index "FIBillOfMaterialsWithEndDate"  
    -- on the table Production.BillOfMaterials   
    -- using the columms ComponentID and StartDate.  
  
    CREATE NONCLUSTERED INDEX FIBillOfMaterialsWithEndDate  
        ON Production.BillOfMaterials (ComponentID, StartDate)  
        WHERE EndDate IS NOT NULL ;  
    GO  
    ```  
  
     以上的篩選索引對下列查詢有效。 您可以顯示查詢執行計畫，以判斷查詢最佳化工具是否使用了篩選索引。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT ProductAssemblyID, ComponentID, StartDate   
    FROM Production.BillOfMaterials  
    WHERE EndDate IS NOT NULL   
        AND ComponentID = 5   
        AND StartDate > '01/01/2008' ;  
    GO  
    ```  
  
#### <a name="to-ensure-that-a-filtered-index-is-used-in-a-sql-query"></a>確定在 SQL 查詢中使用篩選的索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT ComponentID, StartDate FROM Production.BillOfMaterials  
        WITH ( INDEX ( FIBillOfMaterialsWithEndDate ) )   
    WHERE EndDate IN ('20000825', '20000908', '20000918');   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)。  
  
  
