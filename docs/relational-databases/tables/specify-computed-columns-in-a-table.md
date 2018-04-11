---
title: 指定資料表中的計算資料行 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- computed columns, define
ms.assetid: 731a4576-09c1-47f0-a8f6-edd0b55679f4
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 95980febab6a2801ca2f751a0cadd22f14991c59
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/10/2018
---
# <a name="specify-computed-columns-in-a-table"></a>指定資料表中的計算資料行
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  計算資料行是一個虛擬資料行，除非資料行標示了 PERSISTED，否則，並未實際儲存在資料表中。 計算資料行運算式可以使用來自其他資料行的資料來計算其所屬資料行的值。 您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中指定計算資料行的運算式。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Limitations)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來指定計算資料行：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Limitations"></a> 限制事項  
  
-   計算資料行不能用來做為 DEFAULT 或 FOREIGN KEY 條件約束定義，也不能搭配 NOT NULL 條件約束定義來使用。 不過，如果計算資料行值是由具決定性的運算式所定義，且索引資料行接受結果的資料類型，計算資料行便可用來做為索引中的索引鍵資料行，也可用在任何 PRIMARY KEY 或 UNIQUE 條件約束中。 例如，如果資料表有整數資料行 a 和 b，您可以建立計算資料行 a + b 的索引，但不能建立計算資料行 a +DATEPART(dd, GETDATE()) 的索引，因為在後續叫用時，值可能會改變。  
  
-   計算資料行不能是 INSERT 或 UPDATE 陳述式的目標。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
###  <a name="NewColumn"></a> 若要加入新的計算資料行  
  
1.  在 **[物件總管]**中，展開要在其中加入新的計算資料行的資料表。 以滑鼠右鍵按一下 [資料行]，然後選取 [新增資料行]。  
  
2.  輸入資料行名稱並接受預設資料類型 (**nchar**(10))。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會判斷計算資料行的資料類型，方法是將資料類型優先順序規則套用至公式中指定的運算式。 例如，如果公式參考 **money** 類型的資料行以及 **int**類型的資料行，則計算資料行會是 **money** 類型，因為該資料類型的優先順序較高。 如需詳細資訊，請參閱[資料類型優先順序 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
3.  在 **[資料行屬性]** 索引標籤中，展開 **[計算資料行規格]** 屬性。  
  
4.  在 [(Formula)] 子屬性右邊的方格資料格中，輸入此資料行的運算式。 例如，在 `SalesTotal` 資料行中，您輸入的公式可能是 `SubTotal+TaxAmt+Freight`，該公式會將資料表中每一個資料列的這些資料行中的值相加。  
  
    > [!IMPORTANT]  
    >  當一個公式結合兩個不同資料類型的運算式時，資料類型優先順序的規則，會指定將低優先順序的資料類型，轉換為高優先順序的資料類型。 如果轉換不是支援的隱含轉換，就會傳回錯誤 "`Error validating the formula for column column_name.`"。 使用 CAST 或 CONVERT 函數解決資料類型衝突。 例如，如果 **nvarchar** 類型的資料行與 **int**類型的資料行結合，則整數類型必須轉換為 **nvarchar** ，如 `('Prod'+CONVERT(nvarchar(23),ProductID))`這個公式所示。 如需詳細資訊，請參閱 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)。  
  
5.  藉由從 [Is Persisted] 子屬性的下拉式清單中選擇 [是] 或 [否]，指示資料是否為永續性。  
  
6.  在 [檔案]  功能表上，按一下 [儲存 <資料表名稱>]。  
  
#### <a name="to-add-a-computed-column-definition-to-an-existing-column"></a>若要將計算資料行定義新增至現有資料行  
  
1.  在物件總管中，以滑鼠右鍵按一下包含您要變更之資料行的資料表，然後展開 [資料行] 資料夾。  
  
2.  以滑鼠右鍵按一下要指定其計算資料行公式的資料行，然後按一下 [刪除]。 按一下 **[確定]**。  
  
3.  加入新的資料行，並依照上述程序加入新的計算料行，藉此指定計算資料行公式。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-add-a-computed-column-when-creating-a-table"></a>建立資料表時加入計算資料行  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例會建立包含計算資料行的資料表，該計算資料行會乘以 `QtyAvailable` 資料行的值乘 `UnitPrice` 資料行的值。  
  
    ```  
    CREATE TABLE dbo.Products   
    (  
        ProductID int IDENTITY (1,1) NOT NULL  
      , QtyAvailable smallint  
      , UnitPrice money  
      , InventoryValue AS QtyAvailable * UnitPrice  
    );  
  
    -- Insert values into the table.  
    INSERT INTO dbo.Products (QtyAvailable, UnitPrice)  
    VALUES (25, 2.00), (10, 1.5);  
  
    -- Display the rows in the table.  
    SELECT ProductID, QtyAvailable, UnitPrice, InventoryValue  
    FROM dbo.Products;  
  
    ```  
  
#### <a name="to-add-a-new-computed-column-to-an-existing-table"></a>若要將新的計算資料行加入至現有資料表  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 下列範例會將新的資料行加入至上一個範例中建立的資料表。  
  
    ```  
    ALTER TABLE dbo.Products ADD RetailValue AS (QtyAvailable * UnitPrice * 1.35);  
  
    ```  
  
#### <a name="to-change-an-existing-column-to-a-computed-column"></a>若要將現有的資料行變更為計算資料行  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  若要將現有的資料行變更為計算資料行，您必須卸除並重新建立計算資料行。 將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 下列範例會修改上一個範例中加入的資料行。  
  
    ```  
    ALTER TABLE dbo.Products DROP COLUMN RetailValue;  
    GO  
    ALTER TABLE dbo.Products ADD RetailValue AS (QtyAvailable * UnitPrice * 1.5);  
  
    ```  
  
     如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。  
  
###  <a name="TsqlExample"></a>  
