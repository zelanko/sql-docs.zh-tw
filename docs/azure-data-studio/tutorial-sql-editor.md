---
title: 使用 Transact-SQL 編輯器建立資料庫物件
description: 本教學課程示範 Azure Data Studio 中簡化 T-SQL 使用的主要功能。
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: b8e5bd6cb986601baf97a02a3f167432e0c29b95
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726744"
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---azure-data-studio"></a>教學課程：使用 Transact-SQL 編輯器建立資料庫物件 - Azure Data Studio

建立和執行查詢、預存程序、指令碼等是資料庫專業人員的核心工作。 本教學課程示範 T-SQL 編輯器中用來建立資料庫物件的主要功能。

在本教學課程中，您將了解如何使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 執行下列動作：
> [!div class="checklist"]
> * 搜尋資料庫物件
> * 編輯資料表資料 
> * 使用程式碼片段快速撰寫 T-SQL
> * 使用 [查看定義] 和 [移至定義]，檢視資料庫物件詳細資料


## <a name="prerequisites"></a>必要條件

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立 *TutorialDB* 資料庫，請完成下列任一項快速入門：

- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連線及查詢 SQL Server](quickstart-sql-server.md)
- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連線及查詢 Azure SQL Database](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>快速尋找資料庫物件並執行常見工作

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 提供搜尋小工具，快速尋找資料庫物件。 結果清單提供與所選物件相關的常見工作操作功能表，例如對資料表 [編輯資料]。

1. 開啟 [伺服器] 提要欄位 (**Ctrl+G**)，展開 [資料庫]，然後選取 [TutorialDB]。 

1. 以滑鼠右鍵按一下 [TutorialDB]，然後從操作功能表選取 [管理]，開啟 [TutorialDB 儀表板]：

   ![操作功能表 - 管理](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. 在儀表板上，以滑鼠右鍵按一下 [dbo.Customers] (在搜尋小工具中)，然後選取 [編輯資料]。
   
   > [!TIP]
   > 對於具有許多物件的資料庫，使用搜尋小工具可快速找出您要尋找的資料表、檢視等。

   ![快速搜尋小工具](./media/tutorial-sql-editor/quick-search-widget.png)

1. 編輯第一個資料列中的 [電子郵件] 資料行，輸入 *orlando0\@adventure-works.com*，然後按 **Enter** 儲存變更。

   ![編輯資料](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>使用 T-SQL 程式碼片段建立預存程序

Azure Data Studio 提供許多內建的 T-SQL 程式碼片段，其用來快速建立陳述式。


1. 按 **Ctrl+N** 開啟新的查詢編輯器。

2. 在編輯器中鍵入 **sql**，按向下鍵到 **sqlCreateStoredProcedure**，然後按 *Tab* 鍵 (或 *Enter*) 載入建立預存程序程式碼片段。

   ![程式碼片段清單](./media/tutorial-sql-editor/snippet-list.png)

3. 建立預存程序程式碼片段已設定兩個可快速編輯的欄位：[StoredProcedureName] 和 [SchemaName]。 選取 [StoredProcedureName]，按一下滑鼠右鍵並選取 [變更所有發生次數]。 現在鍵入 *getCustomer*，所有的 *StoredProcedureName* 項目都會變更為 *getCustomer*。

   ![程式碼片段](./media/tutorial-sql-editor/snippet.png)

5. 將所有出現的 *SchemaName* 變更為 *dbo*。 
6. 此程式碼片段會包含需要更新的預留位置參數和本文。 *EXECUTE* 陳述式也會包含預留位置文字，因為它不知道程序將擁有多少參數。 在本教學課程中，請更新程式碼片段，使其看起來像下列程式碼：

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
    
5. 若要建立預存程序並進行測試回合，請按 **F5**。

現在已建立預存程序，且 [結果] 窗格會以 JSON 顯示傳回的客戶。 若要查看格式化的 JSON，請按一下傳回的記錄。 


## <a name="use-peek-definition"></a>使用查看定義 

Azure Data Studio 可供使用查看定義功能來檢視物件定義。 此區段會建立第二個預存程序，並使用 [查看定義] 查看資料表中有哪些資料行，以便快速建立預存程序的主體。

1. 按 **Ctrl+N** 開啟新的編輯器。 

2. 在編輯器中鍵入 *sql*，按向下鍵到 *sqlCreateStoredProcedure*，然後按 *Tab* 鍵 (或 *Enter*) 載入建立預存程序程式碼片段。
3. 在 [StoredProcedureName] 鍵入 *setCustomer*，並在 [SchemaName] 鍵入 *dbo*

3. 將 @param 預留位置取代為下列參數定義：

   ```sql
   @json_val nvarchar(max)
   ```

4. 將預存程序的主體取代為下列程式碼：
   ```sql
   INSERT INTO dbo.Customers
   ```

5. 在您剛才新增的 *INSERT* 行中，以滑鼠右鍵按一下 [dbo.Customers]，然後選取 [查看定義]。

   ![查看定義](./media/tutorial-sql-editor/peek-definition.png)

6. 資料表定義隨即出現，讓您可以快速查看資料表中有哪些資料行。 請參閱資料行清單，輕鬆地完成預存程序的陳述式。 完成建立您先前新增的 INSERT 陳述式，以完成預存程序的主體，然後關閉 [查看定義] 視窗：

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
7. 刪除 (或取消註解) 查詢底部的 *EXECUTE* 命令。
8. 整個陳述式看起來應該像下列程式碼：

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

8. 若要建立 *setCustomer* 預存程序，請按 **F5**。

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>使用將查詢結果另存為 JSON，測試 setCustomer 預存程序

在上一節中建立的 *setCustomer* 預存程序需要將 JSON 資料傳遞至 tion requires JSON data be passed into the *\@json_val* 參數。 本節說明如何取得一些格式正確的 JSON 並傳遞至參數，讓我們可以測試預存程序。

1. 在 [伺服器] 提要欄位中，以滑鼠右鍵按一下 [dbo.Customers] 資料表，然後按一下 [SELECT TOP 1000 Rows] \(選取前 1000 個資料列\)。

2. 選取結果檢視中的第一個資料列，確認已選取整個資料列 (按一下最左方資料行中的數字 1)，然後選取 [另存為 JSON]。  
3. 將資料夾變更為您記得的位置，讓您可以在稍後刪除檔案 (例如桌面)，然後按一下 [儲存]。 JSON 格式的檔案隨即開啟。

   ![另存為 JSON](./media/tutorial-sql-editor/save-as-json.png)

4. 在編輯器中選取 JSON 資料並予以複製。
5. 按 **Ctrl+N** 開啟新的編輯器。
6. 先前的步驟示範如何輕鬆地取得格式正確的資料，完成對 *setCustomer* 程序的呼叫。 您可以看到下列程式碼使用與新客戶詳細資料相同的 JSON 格式，讓我們可以測試 *setCustomer* 程序。 此陳述式包含宣告參數並執行新 get 和 set 程序的語法。 您可以貼上從上一節複製的資料，並加以編輯使其與下列範例相同，或直接將下列陳述式貼到查詢編輯器。

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

7. 按 **F5** 執行指令碼。 此指令碼會插入新的客戶，並以 JSON 格式傳回新客戶的資訊。 按一下結果，即可開啟格式化的檢視。

   ![測試結果](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已了解如何：
> [!div class="checklist"]
> * 快速搜尋結構描述物件
> * 編輯資料表資料 
> * 使用程式碼片段撰寫 T-SQL 指令碼
> * 使用 [查看定義] 和 [移至定義]，了解資料庫物件詳細資料


若要了解如何啟用**五個最慢速查詢**小工具，請完成下一個教學課程：

> [!div class="nextstepaction"]
> [啟用慢速查詢範例深入解析小工具](tutorial-qds-sql-server.md)
