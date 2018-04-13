---
title: "教學課程： 使用 SQL Operations Studio （預覽） 的 TRANSACT-SQL 編輯器來建立資料庫物件 |Microsoft 文件"
description: "本教學課程示範簡化使用 T-SQL SQL Operations Studio （預覽） 中的主要功能。"
ms.custom: tools|sos
ms.date: 03/13/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db9cc8185742980b649f9fcc11eced5687201464
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2018
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>教學課程： 使用 TRANSACT-SQL 編輯器來建立資料庫物件， [!INCLUDE[name-sos](../includes/name-sos-short.md)]

建立和執行查詢、 預存程序、 指令碼等是資料庫專業人員的核心工作。 本教學課程示範如何在 T-SQL 編輯器來建立資料庫物件中的主要功能。

您可以在本教學課程，了解如何使用[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]：
> [!div class="checklist"]
> * 搜尋資料庫物件
> * 編輯資料表資料 
> * 使用程式碼片段快速地撰寫 T-SQL 
> * 使用*查看定義*和*移至定義*檢視資料庫物件的詳細資料


## <a name="prerequisites"></a>必要條件

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立 *TutorialDB* 資料庫，請完成下列其中一項快速入門教學：

- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連接及查詢 SQL Server ](quickstart-sql-server.md)
- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連接及查詢 Azure SQL Database ](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>快速找出資料庫物件和執行一般工作

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 提供的搜尋小工具，以快速找出資料庫物件。 結果清單中提供的內容功能表的一般工作與選取的物件，例如*編輯資料*資料表。

1. 開啟 [伺服器資訊看板] (**Ctrl + G**)，展開**資料庫**，然後選取**TutorialDB**。 

1. 滑鼠右鍵點選 **TutorialDB**，從內容功能表選取**管理**，開啟 *TutorialDB 儀表板*：

   ![操作功能表： 管理](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. 在儀表板上，滑鼠右鍵點選 **dbo.Customers**（在 [搜尋] 小工具中) 並選取**編輯資料**。
   
   > [!TIP]
   > 對於包含許多物件的資料庫，您可以透過搜尋小工具快速地找到想要的資料表、檢視表...等。

   ![快速搜尋 widget](./media/tutorial-sql-editor/quick-search-widget.png)

1. 編輯**電子郵件**欄位的第一筆資料，輸入 *orlando0@adventure-works.com*，然後按 **Enter** 鍵儲存變更。

   ![編輯資料](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>使用 T-SQL 程式碼片段建立預存程序

SQL Operations Studio 提供許多內建的 T-SQL 程式碼片段，可快速建立陳述式。


1. 按下 **Ctrl + N** 開啟新的查詢編輯器。

2. 在編輯器中輸入 **sql**，按向下鍵至 **sqlCreateStoredProcedure**，然後按 *Tab*鍵 (或*Enter*) 載入新增預存程序程式碼片段。

   ![snippet-list](./media/tutorial-sql-editor/snippet-list.png)

3. 建立預存程序程式碼片段有兩個欄位可以進行 [快速編輯]， *StoredProcedureName* 和 *SchemaName*。 選取 *StoredProcedureName* ，按一下滑鼠右鍵，然後選取**變更所有相符項目**。 鍵入 *getCustomer* 並將全部 *StoredProcedureName* 項目變更為 *getCustomer*。

   ![程式碼片段](./media/tutorial-sql-editor/snippet.png)

5. 同上一步操作，將所有 *SchemaName* 變更為 *dbo*。 
6. 程式碼片段包含許多參數預留位置與內容需要更新。 *EXECUTE* 陳述式也包含文字預留位置，因為不知道預存程序有多少參數。 本教學課程更新程式碼片段後，結果如下列程式碼所示：

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
    SELECT  c.CustomerId, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerId = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. 若要建立預存程序並測試執行，請按**F5**鍵。

預存程序現在已經建立，而**結果**窗格會顯示所回傳客戶資料(JSON 格式)。 若要查看已排版的 JSON ，請點選回傳資料。 


## <a name="use-peek-definition"></a>使用查看定義 

透過查看定義功能，SQL Operations Studio 提供檢視物件定義的能力。 本節會建立第二個預存程序，並使用查看定義查看資料表內有那些欄位，快速地建立預存程序主體。

1. 按下 **Ctrl + N** 開啟新的編輯器。 

2. 在編輯器中輸入 **sql**，按向下鍵至 **sqlCreateStoredProcedure**，然後按 *Tab*鍵 (或*Enter*) 載入新增預存程序程式碼片段。
3. 在編輯器中輸入 *setCustomer* 取代 *StoredProcedureName*、輸入 *dbo* 取代 *SchemaName*

3. 取代預設參數 @param 為下列的參數定義

   ```sql
   @json_val nvarchar(max)
   ```

4. 取代預存程序的主體為下列程式碼：
   ```sql
   INSERT INTO dbo.Customers
   ```

5. 以滑鼠右鍵按一下**dbo.Customers**選取**查看定義**。

   ![查看定義](./media/tutorial-sql-editor/peek-definition.png)

6. 資料表定義會出現，讓您可以快速查看資料表中的資料欄位。 參考資料欄位清單，輕鬆地完成您的預存程序的陳述式。 完成您先前所建立預存程序主體內的 Insert 陳述式，然後關閉 [查看定義] 視窗：

   ```sql
   INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
    )
   ```
7. 刪除 （或註解）查詢底下的 *EXECUTE* 命令。
8. 整個陳述式應該如下列程式碼所示：

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
       INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. 若要建立 *setCustomer* 預存程序，請按**F5**鍵。

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>使用將查詢結果儲存為 JSON，將測試 setCustomer 預存程序

*SetCustomer*前一節中所建立的預存程序需要 JSON 資料傳遞至*@json_val*參數。 本節示範如何取得正確格式的位元的 JSON 來將傳入參數，所以您可以測試預存程序。

1. 在**伺服器**[資訊看板] 上按一下滑鼠右鍵*dbo。客戶*資料表，並按一下**選取前 1000 個資料列**。

2. 在 [結果] 檢視中選取第一個資料列，請確定已選取整個資料列 （按一下最左邊資料行中的數字 1），然後選取**儲存為 JSON**。  
3. 變更資料夾位置，您應記得讓您可以刪除更新版本 （針對範例桌面） 檔案，然後按一下**儲存**。 JSON 格式化的檔案隨即開啟。

   ![將儲存為 JSON](./media/tutorial-sql-editor/save-as-json.png)

4. 在編輯器中選取 JSON 資料，並將它複製。
5. 按下開啟新的編輯器**Ctrl + N**。
6. 先前的步驟顯示如何輕鬆地取得正確格式的資料，才能完成呼叫*setCustomer*程序。 您可以查看下列程式碼會使用新的客戶詳細資料與相同的 JSON 格式讓我們可以測試*setCustomer*程序。 陳述式包含語法來宣告參數和執行新的 get 和設定程序。 您可以貼上複製的資料，從上一節和編輯它，讓它相當於下列範例中，或只是將下列陳述式貼到查詢編輯器。

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerId": 5,
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

## <a name="next-steps"></a>後續的步驟
在此教學課程中，您學會如何：
> [!div class="checklist"]
> * 快速搜尋結構描述物件
> * 編輯資料表資料 
> * 撰寫使用程式碼片段的 T-SQL 指令碼
> * 深入了解使用查看定義的資料庫物件詳細資料，並移至定義


若要了解如何啟用**5 名最慢的查詢** widget 中，完成下一個教學課程：

> [!div class="nextstepaction"]
> [啟用緩慢的查詢範例深入了解 widget](tutorial-qds-sql-server.md)
