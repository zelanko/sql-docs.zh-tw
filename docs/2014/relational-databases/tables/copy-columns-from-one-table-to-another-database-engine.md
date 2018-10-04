---
title: 將資料行從一個資料表複製至另一個資料表 (Database Engine) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- copying columns
- columns [SQL Server], copying
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3d2654485acdebdf3e7e79b23dadd533617ea937
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137518"
---
# <a name="copy-columns-from-one-table-to-another-database-engine"></a>將資料行從一個資料表複製至另一個資料表 (Database Engine)
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
  
2.  在物件總管 中，以滑鼠右鍵按一下 [檢視] 節點，然後按一下 [新檢視]。  
  
3.  在 [ **查詢設計工具** ] 功能表中指向 [ **變更類型**]，再按 [ **插入結果**]。  
  
4.  在 [ **選擇插入結果的目標資料表** ] 對話方塊中，選取要將資料複製到其中的資料表，再按 [ **確定**]。  
  
     如果您是在資料表中複製資料列，您可以加入來源資料表做為目的資料表。  
  
    > [!NOTE]  
    >  [**查詢設計工具** ] 無法預先判斷您可以更新哪些資料表和檢視。 因此，[ **選擇插入結果的目標資料表** ] 對話方塊中的資料表清單會顯示正在查詢之資料連接中的所有可用資料表和檢視，甚至包括您可能無法將資料列複製到其中的資料表和檢視。  
  
5.  在 [圖表] 窗格的主體中按一下滑鼠右鍵，再從快速鍵功能表中按一下 [Add Table to Diagram (將資料表加入圖表)]。  
  
6.  在 [ **加入資料表** ] 對話方塊中，選取要從中複製資料的每一個資料表，再按一下 [ **加入**]，再按 [ **關閉**]。  
  
     這些資料表會以縮寫格式顯示在 [圖表] 窗格中。  
  
7.  在縮寫的資料表中，核取要從中複製資料的每一個資料行的方塊。  
  
8.  在 [準則] 窗格的 [ **附加** ] 欄中，為每一個目標資料行選擇您要從中複製資料的資料行。  
  
9. 在 [準則] 窗格中輸入搜尋條件，以指定要複製的資料列。 如需詳細資訊，請參閱[指定搜尋條件 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)。  
  
     如果沒有指定搜尋條件，便會將來源資料表的所有資料列複製到目的資料表中。  
  
10. 若要複製摘要資訊，請指定 [ **群組依據** ] 選項。 如需詳細資訊，請參閱[摘要或彙總資料表中所有資料列的值 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools.md)。  
  
11. 按一下 [ **執行 SQL** ] 按鈕 以執行查詢。  
  
     在執行插入結果查詢時， [結果窗格](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)中不會報告結果， 而是出現訊息指出已經複製了多少資料列。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>若要將資料行定義從一個資料表複製到另一個資料表  
  
1.  您無法透過使用 Transact-SQL 陳述式將個別資料行從一個資料表複製到另一個現有資料表。 不過，可透過 SELECT INTO，在預設的檔案群組中建立新的資料表，然後將查詢的結果資料列插入其中。 如需詳細資訊，請參閱 [INTO 子句 &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-into-clause-transact-sql)。  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>若要將資料從一個資料表複製到另一個資料表  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
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
  
  
