---
title: 建立外部索引鍵關聯性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], creating
ms.assetid: 867a54b8-5be4-46e6-9702-49ae6dabf67c
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: baf89a41a42a1ea84e37d103890c3c8ea1ed22db
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274554"
---
# <a name="create-foreign-key-relationships"></a>建立外部索引鍵關聯性
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立外部索引鍵關聯性。 當想要將一個資料表的資料列，與其他資料表的資料列建立相關時，可以建立兩者間的關聯性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要建立外部索引鍵關聯性使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   外部索引鍵條件約束不一定只能連結到另一個資料表中的主索引鍵條件約束；它也可以定義成參考另一個資料表中 UNIQUE 條件約束的資料行。  
  
-   在 FOREIGN KEY 條件約束的資料行中輸入 NULL 以外的值時，值必須在參考的資料行中；否則，系統會傳回外部索引鍵違規錯誤訊息。 若要確定會驗證複合外部索引鍵條件約束的所有值，請對所有參與的資料行指定 NOT NULL。  
  
-   FOREIGN KEY 條件約束只能參考在相同伺服器之相同資料庫內的資料表。 跨資料庫參考完整性必須利用觸發程序來實作。 如需詳細資訊，請參閱 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)。  
  
-   FOREIGN KEY 條件約束可以參考相同資料表中的另一個資料行。 這稱為自我參考。  
  
-   資料行層級上指定的 FOREIGN KEY 條件約束只能列出一個參考資料行。 這個資料行必須有定義了條件約束的資料行之相同資料類型。  
  
-   資料表層級上指定的 FOREIGN KEY 條件約束，必須有與條件約束資料行清單中資料行一樣多的參考資料行。 每個參考資料行的資料類型，也必須與資料行清單中的對應資料行相同。  
  
-   在資料表所能包含參考其他資料表的 FOREIGN KEY 條件約束數目，及其他資料表所擁有參考特定資料表的 FOREIGN KEY 條件約束數目上， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 並沒有預先定義的限制。 不過，FOREIGN KEY 條件約束的實際可用數目，會受到硬體組態及資料庫和應用程式設計的限制。 建議資料表所包含的 FOREIGN KEY 條件約束數目不要超出 253 個，參考資料表的 FOREIGN KEY 條件約束數目也不要超出 253 個。  
  
-   暫存資料表不會強制執行 FOREIGN KEY 條件約束。  
  
-   如果在 CLR 使用者定義的類型資料行上定義外部索引鍵，類型的實作必須支援二進位順序。 如需詳細資訊，請參閱 [CLR 使用者定義型別](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
-   只有在所參考的主索引鍵也定義成 `varchar(max)` 類型時，`varchar(max)` 類型的資料行才能夠參與 FOREIGN KEY 條件約束。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 建立具有外部索引鍵的新資料表，需要資料庫中的 CREATE TABLE 權限及建立資料表的結構描述之 ALTER 權限。  
  
 在現有資料表中建立外部索引鍵需要此資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-foreign-key-relationship-in-table-designer"></a>若要在資料表設計工具建立外部索引鍵關聯性  
  
1.  在物件總管中，以滑鼠右鍵按一下位於關聯性之外部索引鍵端上的資料表，然後按一下 [設計]。  
  
     資料表會在 **[資料表設計工具]** 中開啟。  
  
2.  從 **[資料表設計工具]** 功能表中，按一下 **[關聯性]**。  
  
3.  在 [外部索引鍵關聯性] 對話方塊中，按一下 [加入]。  
  
     關聯性會出現在 [選取的關聯性] 清單中，並顯示系統提供的名稱，格式為 FK_\<資料表名稱>>_\<資料表名稱>，其中<資料表名稱> 為外部索引鍵資料表的名稱。  
  
4.  在 [ **選取的關聯性** ] 清單中，按一下關聯性。  
  
5.  按一下方格右邊的 [資料表及資料行規格]，然後按一下屬性右邊的省略符號 (**…**)。  
  
6.  在 [資料表和資料行] 對話視窗的 [主索引鍵] 下拉式清單中，選擇將要成為關聯性主索引鍵端的資料表。  
  
7.  在方格的下方，選擇組成資料表主索引鍵的資料行。 在每個資料行左側的鄰近方格資料格，選擇對應到外部索引鍵資料表的外部索引鍵資料行。  
  
     **[資料表設計工具]** 會提供關聯性的建議名稱。 若要變更這個名稱，請編輯 **[關聯性名稱]** 文字方塊的內容。  
  
8.  選擇 **[確定]** 建立關聯性。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-foreign-key-in-a-new-table"></a>在新的資料表建立外部索引鍵  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例會建立資料表並在 `TempID` 資料行上定義外部索引鍵條件約束，而此資料行會參考 `SalesReasonID` 資料表中的 `Sales.SalesReason` 資料行。 ON DELETE CASCADE 和 ON UPDATE CASCADE 子句用來確定對 `Sales.SalesReason` 資料表所做的變更會自動傳播至 `Sales.TempSalesReason` 資料表。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Sales.TempSalesReason (TempID int NOT NULL, Name nvarchar(50),   
    CONSTRAINT PK_TempSales PRIMARY KEY NONCLUSTERED (TempID),   
    CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)   
        REFERENCES Sales.SalesReason (SalesReasonID)   
        ON DELETE CASCADE  
        ON UPDATE CASCADE  
    );GO  
  
    ```  
  
#### <a name="to-create-a-foreign-key-in-an-existing-table"></a>在現有的資料表建立外部索引鍵  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例會在 `TempID` 資料行上建立外部索引鍵，並參考 `SalesReasonID` 資料表中的 `Sales.SalesReason` 資料行。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Sales.TempSalesReason   
    ADD CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)   
        REFERENCES Sales.SalesReason (SalesReasonID)   
        ON DELETE CASCADE  
        ON UPDATE CASCADE  
    ;  
    GO  
  
    ```  
  
     如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)、[CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) 和 [table_constraint &#40;Transact-SQL&#41;](/sql/relational-databases/system-information-schema-views/table-constraints-transact-sql)。  
  
  
