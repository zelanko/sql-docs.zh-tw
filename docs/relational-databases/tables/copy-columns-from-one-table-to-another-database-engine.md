---
title: "將資料行從一個資料表複製至另一個資料表 (Database Engine) | Microsoft 文件"
ms.custom: 
ms.date: 09/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- copying columns
- columns [SQL Server], copying
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: ab6c5c510e8f1d13c5212f316d27dabcdedd1009
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="copy-columns-from-one-table-to-another-database-engine"></a>將資料行從一個資料表複製至另一個資料表 (Database Engine)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中將資料行從某個資料表複製到另一個資料表，但只複製資料行定義，或複製定義和資料。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **使用下列方式複製資料行：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 當您在資料庫之間複製擁有別名資料類型的資料行時，別名資料類型可能無法在目的地資料庫中使用。 在這種狀況下，將指派資料庫中可用而最符合的基本資料類型給該資料行。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>若要將資料行定義從一個資料表複製到另一個資料表  
  
1.  以滑鼠右鍵按一下含有要複製之資料行的資料表，以及您要複製到其中的目標資料表，再按一下 [設計]，加以開啟。  
  
2.  按一下您要複製資料行的資料表索引標籤，並選取這些資料行。  
  
3.  從 [ **編輯** ] 功能表中，按一下 [ **複製**]。  
  
4.  按一下資料行複製目的地的資料表之索引標籤。  
  
5.  選取要在其前面插入資料行的資料行，並從 **[編輯]** 功能表中，按一下 **[貼上]**。  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>若要將資料從一個資料表複製到另一個資料表  
  
1.  依照前述的指示複製資料行定義。  
  
    > [!NOTE]  
    >  在開始將資料從一個資料表複製到另一個資料表之前，請確定目的資料行中的資料類型與來源資料行的資料類型是否相容。  
  
2.  開啟新的 [查詢編輯器] 視窗。 

3.  以滑鼠右鍵按一下 [查詢編輯器]，然後按一下 [在編輯器中設計查詢]。 

4.  在 [新增資料表] 對話方塊中，選取來源和目的地資料表，並按一下 [新增]，然後關閉 [新增資料表] 對話方塊。 

5.  以滑鼠右鍵按一下 [查詢編輯器] 的已開啟區域，並指向 [變更類型]，然後按一下 [插入結果]。  

6.  在 [選擇插入結果的目標資料表] 對話方塊中，選取目的地資料表。 

7.  在 [查詢設計工具] 的上方部分，按一下來源資料表中的來源資料行。

8. [查詢設計工具] 現在已建立 INSERT 查詢。 按一下 [確定]，將查詢放入原始 [查詢編輯器] 視窗。  

9.  執行查詢，將資料從來源資料表插入目的地資料表中。

  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>若要將資料行定義從一個資料表複製到另一個資料表  
  
1.  您無法透過使用 Transact-SQL 陳述式將個別資料行從一個資料表複製到另一個現有資料表。 不過，可透過 SELECT INTO，在預設的檔案群組中建立新的資料表，然後將查詢的結果資料列插入其中。 如需詳細資訊，請參閱 [INTO 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-into-clause-transact-sql.md)。  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>若要將資料從一個資料表複製到另一個資料表  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.EmployeeSales  
    ( BusinessEntityID   varchar(11) NOT NULL,  
      SalesYTD money NOT NULL  
    );  
    GO  
    INSERT INTO dbo.EmployeeSales  
        SELECT BusinessEntityID, SalesYTD   
        FROM Sales.SalesPerson;  
    GO  
    ```  
  
  
