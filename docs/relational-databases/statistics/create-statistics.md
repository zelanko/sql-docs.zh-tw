---
title: "建立統計資料 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-statistics
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.stat.properties.f1
- sql13.swb.statistics.filter.f1
- sql13.swb.stat.columns.f1
- sql13.swb.statistics.propertis.f1
helpviewer_keywords:
- creating statistics
- statistics [SQL Server], creating
ms.assetid: 95a455fb-664d-4c95-851e-c6b62d7ebe04
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7e08b4318e4faa13aba2e242f0458db3572d7884
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="create-statistics"></a>建立統計資料
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中針對資料表或索引檢視表的一個或多個資料行建立查詢最佳化統計資料。 對於大部分查詢而言，查詢最佳化工具已經產生高品質查詢計畫的必要統計資料。不過，在少數情況下，您必須建立其他統計資料。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目建立統計資料：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   使用 CREATE STATISTICS 陳述式來建立統計資料之前，請確認 AUTO_CREATE_STATISTICS 選項是在資料庫層級設定。 這將確保查詢最佳化工具能夠繼續例行地針對查詢述詞資料行建立單一資料行統計資料。  
  
-   您最多可以針對每個統計資料物件列出 32 個資料行。  
  
-   您不能卸除、重新命名或變更在篩選統計資料述詞中定義的資料表資料行定義。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 使用者必須是資料表或索引檢視表擁有者，或是下列其中一個角色的成員： **系統管理員** 固定伺服器角色、 **db_owner** 固定資料庫角色或 **db_ddladmin** 固定資料庫角色。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-statistics"></a>若要建立統計資料  
  
1.  在 **[物件總管]**中，按一下加號展開要在其中建立新統計資料的資料庫。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開要在其中建立新統計資料的資料表。  
  
4.  以滑鼠右鍵按一下 [統計資料] 資料夾，然後選取 [新增統計資料…]。  
  
     下列屬性會在 [*資料表名稱* 資料表上的新統計資料] 對話方塊的 [一般] 頁面中顯示。  
  
     **資料表名稱**  
     顯示統計資料所描述的資料表名稱。  
  
     **統計資料名稱**  
     顯示儲存統計資料的資料庫物件名稱。  
  
     **統計資料行**  
     此方格會顯示此組統計資料所描述的資料行。 方格中所有的值均為唯讀。  
  
     **名稱**  
     顯示統計資料所描述的資料行名稱。 這可以是單一資料行，或單一資料表中的資料行組合。  
  
     **資料類型**  
     指出統計資料所描述之資料行的資料類型。  
  
     **大小**  
     顯示各個資料行的資料類型大小。  
  
     **識別**  
     勾選時表示為識別欄位。  
  
     **允許 Null**  
     指出資料行是否接受 NULL 值。  
  
     **加入**  
     將資料表的其他資料行加入統計資料方格。  
  
     **移除**  
     從統計資料方格中移除選取的資料行。  
  
     **上移**  
     將選取的資料行移動到統計資料方格中較前面的位置。 方格中的位置，會大幅影響統計資料的效益。  
  
     **下移**  
     將選取的資料行，移動到統計資料方格中較後面的位置。  
  
     **上次更新這些資料行的統計資料：**  
     指出統計資料有多舊。 愈新的統計資料愈有價值。 在資料大量變更後，或加入非典型資料後，更新統計資料。 資料的分佈較為一致的資料表統計資料，就不需要經常地更新。  
  
     **更新這些資料行的統計資料**  
     勾選即可在對話方塊關閉時更新統計資料。  
  
     下列屬性會在 [*資料表名稱* 資料表上的新統計資料] 對話方塊的 [篩選] 頁面中顯示。  
  
     **篩選運算式**  
     定義要在篩選統計資料中包含什麼資料列。 例如， `Production.ProductSubcategoryID IN ( 1,2,3 )`  
  
5.  在 [*資料表名稱* 資料表上的新統計資料] 對話方塊的 [一般] 頁面上，按一下 [加入]。  
  
     下列屬性會在 **[選取資料行]** 對話方塊中顯示。 此資訊是唯讀的。  
  
     **名稱**  
     顯示統計資料所描述的資料行名稱。 這可以是單一資料行，或單一資料表中的資料行組合。  
  
     **資料類型**  
     指出統計資料所描述之資料行的資料類型。  
  
     **大小**  
     顯示各個資料行的資料類型大小。  
  
     **識別**  
     勾選時表示為識別欄位。  
  
     **Allow NULLs**  
     指出資料行是否接受 NULL 值。  
  
6.  在 **[選取資料行]** 對話方塊中，選取要為其建立統計資料的每個資料行的核取方塊，然後按一下 **[確定]**。  
  
7.  在 [*資料表名稱* 資料表上的新統計資料] 對話方塊中，按一下 [確定]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-statistics"></a>若要建立統計資料  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Create new statistic object called ContactMail1  
    -- on the BusinessEntityID and EmailPromotion columns in the Person.Person table.   
  
    CREATE STATISTICS ContactMail1  
        ON Person.Person (BusinessEntityID, EmailPromotion);   
    GO  
    ```  
  
4.  以上建立的統計資訊可能會改進下列查詢的結果。  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    SELECT LastName, FirstName  
    FROM Person.Person  
    WHERE EmailPromotion = 2  
    ORDER BY LastName, FirstName;   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)。  
  
  

