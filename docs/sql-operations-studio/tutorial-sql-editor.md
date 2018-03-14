---
title: "教學課程： 使用 SQL Operations Studio （預覽） 的 TRANSACT-SQL 編輯器來建立資料庫物件 |Microsoft 文件"
description: "本教學課程示範簡化使用 T-SQL SQL Operations Studio （預覽） 中的主要功能。"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2754a998963be5a25d00aa58dcb9b4105bb8f37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>教學課程： 使用 TRANSACT-SQL 編輯器來建立資料庫物件，[!INCLUDE[name-sos](../includes/name-sos-short.md)]

建立和執行查詢、 預存程序、 指令碼等是資料庫專業人員的核心工作。 本教學課程示範如何在 T-SQL 編輯器來建立資料庫物件中的主要功能。

您可以在本教學課程，了解如何使用[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]至：
> [!div class="checklist"]
> * 搜尋資料庫物件
> * 編輯資料表資料 
> * 使用快速撰寫 T-SQL 程式碼片段
> * 檢視資料庫物件的詳細資料使用*查看定義*和*移至定義*


## <a name="prerequisites"></a>必要條件

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立*TutorialDB*資料庫，請完成下列快速入門的其中一個：

- [連接及查詢 SQL Server 使用[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [連接及查詢使用 Azure SQL Database[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>快速找出資料庫物件和執行一般工作

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]提供的搜尋小工具，以快速找出資料庫物件。 結果清單中提供的內容功能表的一般工作與選取的物件，例如*編輯資料*資料表。

1. 開啟 [伺服器資訊看板] (**Ctrl + G**)，依序展開**資料庫**，然後選取**TutorialDB**。 

1. 開啟*TutorialDB 儀表板*選取**管理**從內容功能表。

   ![操作功能表： 管理](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. 找出*客戶*資料表輸入*自訂*搜尋 widget 中。
1. 以滑鼠右鍵按一下**dbo.Customers**選取**編輯資料**。

   ![快速搜尋 widget](./media/tutorial-sql-editor/quick-search-widget.png)

1. 編輯**電子郵件**第一個資料列型別中的資料行 *orlando0@adventure-works.com* ，然後按**Enter**以儲存變更。

   ![編輯資料](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-a-stored-procedure"></a>若要建立預存程序使用 T-SQL 程式碼片段

### <a name="use-snippets-in-includename-sos-shortincludesname-sos-shortmd"></a>使用中的程式碼片段[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]

1. 按下開啟新的查詢編輯器**Ctrl + N**。

2. 型別**sql**在編輯器中，向下箭號**sqlCreateStoredProcedure**，然後按 *索引標籤*載入新的預存程序程式碼片段的索引鍵。

   ![程式碼片段清單](./media/tutorial-sql-editor/snippet-list.png)

3. 將型別 *getCustomer* 和 全部 *StoredProcedureName* 項目變更為 *getCustomer*。 

   ![程式碼片段](./media/tutorial-sql-editor/snippet.png)

4. 預存程序的其餘部分取代 T-SQL 下方：

    ```sql
    -- Create a new stored procedure called 'getCustomer' in schema 'dbo'
    -- Drop the stored procedure if it already exists
    IF EXISTS (
    SELECT *
    FROM INFORMATION_SCHEMA.ROUTINES
    WHERE SPECIFIC_SCHEMA = N'dbo'
    AND SPECIFIC_NAME = N'getCustomer'
    )
    DROP PROCEDURE dbo.getCustomer
    GO
    -- Create the stored procedure in the specified schema
    CREATE PROCEDURE dbo.getCustomer
    @ID int
    -- add more stored procedure parameters here
    AS
    -- body of the stored procedure
    SELECT  c.CustomerID, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerID = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. 若要建立預存程序，並為它提供的測試回合，請按**F5**。

## <a name="use-peek-definition-and-go-to-definition"></a>使用查看定義並移至定義 

1. 按下開啟新的編輯器**Ctrl + N**。 

2. 輸入，然後選取**sqlCreateStoredProcedure**從程式碼片段的建議清單。 在中輸入**setCustomer**如**StoredProcedureName**和**dbo**如**SchemaName**

3. 取代@param具有下列的參數定義行：

   ```sql
       @json_val nvarchar(max)
   ```

4. 以下列內容取代預存程序的主體：
   ```sql
   -- body of the stored procedure
   INSERT INTO dbo.Customers
   ```

5. 以滑鼠右鍵按一下**dbo.Customers**選取**查看定義**。

   ![查看定義](./media/tutorial-sql-editor/peek-definition.png)

6. 使用來完成下列資料表定義 insert 陳述式：

   ```sql
   INSERT INTO dbo.Customers (CustomerID, Name, Location, Email)
       SELECT CustomerID, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerID int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
   ```
7. 最後一個陳述式應該是：

   ```sql
   -- Create a new stored procedure called 'setCustomer' in schema 'dbo'
   -- Drop the stored procedure if it already exists
   IF EXISTS (
   SELECT *
       FROM INFORMATION_SCHEMA.ROUTINES
       WHERE SPECIFIC_SCHEMA = N'dbo'
       AND SPECIFIC_NAME = N'setCustomer'
   )
   DROP PROCEDURE dbo.setCustomer
   GO
   -- Create the stored procedure in the specified schema
   CREATE PROCEDURE dbo.setCustomer
       @json_val nvarchar(max) 
   AS
       -- body of the stored procedure
       INSERT INTO dbo.Customers (CustomerID, Name, Location, Email)
       SELECT CustomerID, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerID int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. 若要執行指令碼，請按**F5**。

## <a name="use-save-query-results-as-json-to-test-our-stored-procedure"></a>使用將查詢結果儲存為 JSON，將測試我們預存程序

1. **選取前 1000 個資料列**從*dbo.Customers*資料表。

2. 選取第一個資料列在結果 檢視，然後按一下**儲存為 JSON**。  
3. 按一下**儲存**，並以 JSON 格式開啟反白顯示的資料列。

   ![將儲存為 JSON](./media/tutorial-sql-editor/save-as-json.png)

4. 選取的 JSON 資料，並將它複製。

5. 開啟新查詢*TutorialDB*並完成下列使用 JSON 資料做為範本，從上一個步驟的測試指令碼。 修改的值*CustomerID*，*名稱*，*位置*，和*電子郵件*。

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerID": 5,
           "Name": "Lucy",
           "Location": "Canada",
           "Email": "lucy0@adventure-works.com"
       }
   ]'

   EXECUTE dbo.setCustomer @json_val = @json
   GO

   EXECUTE dbo.getCustomer @ID = 5
   ```

7. 按下執行指令碼**F5**。 指令碼插入新客戶，並以 JSON 格式傳回新的客戶資訊。 按一下要開啟的格式化的檢視的結果。

   ![測試結果](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>後續步驟
在此教學課程中，您學會如何：
> [!div class="checklist"]
> * 快速搜尋結構描述物件
> * 編輯資料表資料 
> * 撰寫使用程式碼片段的 T-SQL 指令碼
> * 深入了解使用查看定義的資料庫物件詳細資料，並移至定義


若要了解如何啟用**5 名最慢的查詢**範例深入資訊，請完成下一個教學課程：

> [!div class="nextstepaction"]
> [啟用緩慢的查詢範例深入了解 widget](tutorial-qds-sql-server.md)
