---
title: 逐步解說：建立及執行 SQL Server 單元測試 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 992c1d8e-3729-438b-9ef4-cd103e28f145
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a8eb48a0c3147b61eb57b6a8035765ed73850efa
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143588"
---
# <a name="walkthrough-creating-and-running-a-sql-server-unit-test"></a>逐步解說：建立及執行 SQL Server 單元測試
在這個逐步解說中，您要建立 SQL Server 單元測試，以確認數個預存程序的行為。 您可以建立 SQL Server 單元測試，協助識別可能會導致不正確之應用程式行為的程式碼缺失。 您可以執行 SQL Server 單元測試和應用程式測試，作為自動化測試套件的一部分。  
  
在本逐步解說中，您將會執行下列工作：  
  
-   [建立包含資料庫結構描述的指令碼](#CreateScript)  
  
-   [建立資料庫專案並匯入該結構描述](#CreateProjectAndImport)  
  
-   [將資料庫專案部署至隔離式開發環境](#DeployDBProj)  
  
-   [建立 SQL Server 單元測試](#CreateDBUnitTests)  
  
-   [定義測試邏輯](#DefineTestLogic)  
  
-   [執行 SQL Server 單元測試](#RunTests)  
  
-   [加入負面單元測試](#NegativeTest)  
  
在其中一個單元測試偵測到預存程序錯誤之後，您更正該錯誤並重新執行測試。  
  
## <a name="prerequisites"></a>Prerequisites  
若要完成此逐步解說，您必須能夠連接到您有權建立及部署資料庫的資料庫伺服器 (或 LocalDB 資料庫)。 如需詳細資訊，請參閱 [Visual Studio 資料庫功能的必要權限](https://msdn.microsoft.com/library/aa833413(VS.100).aspx)。  
  
## <a name="CreateScript"></a>建立包含資料庫結構描述的指令碼  
  
#### <a name="to-create-a-script-from-which-you-can-import-a-schema"></a>若要建立可從中匯入結構描述的指令碼  
  
1.  在 [ **檔案** ] 功能表上，指向 [ **新增**]，然後按一下 [ **檔案**]。  
  
    [ **新增檔案** ] 對話方塊隨即出現。  
  
2.  在 [ **類別目錄** ] 清單中，按一下 [ **一般** ] (若尚未反白顯示)。  
  
3.  在 [ **範本** ] 清單中，按一下 [ **SQL 檔案**]，然後按一下 [ **開啟**]。  
  
    Transact\-SQL 編輯器隨即開啟。  
  
4.  複製下列 Transact\-SQL 程式碼，並將它貼到 Transact\-SQL 編輯器中。  
  
    ```  
    PRINT N'Creating Sales...';  
    GO  
    CREATE SCHEMA [Sales]  
        AUTHORIZATION [dbo];  
    GO  
    PRINT N'Creating Sales.Customer...';  
    GO  
    CREATE TABLE [Sales].[Customer] (  
        [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
        [CustomerName] NVARCHAR (40) NOT NULL,  
        [YTDOrders]    INT           NOT NULL,  
        [YTDSales]     INT           NOT NULL  
    );  
    GO  
    PRINT N'Creating Sales.Orders...';  
    GO  
    CREATE TABLE [Sales].[Orders] (  
        [CustomerID] INT      NOT NULL,  
        [OrderID]    INT      IDENTITY (1, 1) NOT NULL,  
        [OrderDate]  DATETIME NOT NULL,  
        [FilledDate] DATETIME NULL,  
        [Status]     CHAR (1) NOT NULL,  
        [Amount]     INT      NOT NULL  
    );  
    GO  
    PRINT N'Creating Sales.Def_Customer_YTDOrders...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [Def_Customer_YTDOrders] DEFAULT 0 FOR [YTDOrders];  
    GO  
    PRINT N'Creating Sales.Def_Customer_YTDSales...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [Def_Customer_YTDSales] DEFAULT 0 FOR [YTDSales];  
    GO  
    PRINT N'Creating Sales.Def_Orders_OrderDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [Def_Orders_OrderDate] DEFAULT GetDate() FOR [OrderDate];  
    GO  
    PRINT N'Creating Sales.Def_Orders_Status...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [Def_Orders_Status] DEFAULT 'O' FOR [Status];  
    GO  
    PRINT N'Creating Sales.PK_Customer_CustID...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [PK_Customer_CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);  
    GO  
    PRINT N'Creating Sales.PK_Orders_OrderID...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [PK_Orders_OrderID] PRIMARY KEY CLUSTERED ([OrderID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);  
    GO  
    PRINT N'Creating Sales.FK_Orders_Customer_CustID...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [FK_Orders_Customer_CustID] FOREIGN KEY ([CustomerID]) REFERENCES [Sales].[Customer] ([CustomerID]) ON DELETE NO ACTION ON UPDATE NO ACTION;  
    GO  
    PRINT N'Creating Sales.CK_Orders_FilledDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [CK_Orders_FilledDate] CHECK ((FilledDate >= OrderDate) AND (FilledDate < '01/01/2020'));  
    GO  
    PRINT N'Creating Sales.CK_Orders_OrderDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [CK_Orders_OrderDate] CHECK ((OrderDate > '01/01/2005') and (OrderDate < '01/01/2020'));  
    GO  
    PRINT N'Creating Sales.uspCancelOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspCancelOrder]  
    @OrderID INT  
    AS  
    BEGIN  
    DECLARE @Delta INT, @CustomerID INT  
    BEGIN TRANSACTION  
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]  
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Orders]  
       SET [Status] = 'X'  
    WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Customer]  
       SET  
       YTDOrders = YTDOrders - @Delta  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    END  
    GO  
    PRINT N'Creating Sales.uspFillOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspFillOrder]  
    @OrderID INT, @FilledDate DATETIME  
    AS  
    BEGIN  
    DECLARE @Delta INT, @CustomerID INT  
    BEGIN TRANSACTION  
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]  
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Orders]  
       SET [Status] = 'F',  
           [FilledDate] = @FilledDate  
    WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales - @Delta  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    END  
    GO  
    PRINT N'Creating Sales.uspNewCustomer...';  
    GO  
    CREATE PROCEDURE [Sales].[uspNewCustomer]  
    @CustomerName NVARCHAR (40)  
    AS  
    BEGIN  
    INSERT INTO [Sales].[Customer] (CustomerName) VALUES (@CustomerName);  
    SELECT SCOPE_IDENTITY()  
    END  
    GO  
    PRINT N'Creating Sales.uspPlaceNewOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspPlaceNewOrder]  
    @CustomerID INT, @Amount INT, @OrderDate DATETIME, @Status CHAR (1)='O'  
    AS  
    BEGIN  
    DECLARE @RC INT  
    BEGIN TRANSACTION  
    INSERT INTO [Sales].[Orders] (CustomerID, OrderDate, FilledDate, Status, Amount)   
         VALUES (@CustomerID, @OrderDate, NULL, @Status, @Amount)  
    SELECT @RC = SCOPE_IDENTITY();  
    UPDATE [Sales].[Customer]  
       SET  
       YTDOrders = YTDOrders + @Amount  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    RETURN @RC  
    END  
    GO  
    CREATE PROCEDURE [Sales].[uspShowOrderDetails]  
    @CustomerID INT=0  
    AS  
    BEGIN  
    SELECT [C].[CustomerName], CONVERT(date, [O].[OrderDate]), CONVERT(date, [O].[FilledDate]), [O].[Status], [O].[Amount]  
      FROM [Sales].[Customer] AS C  
      INNER JOIN [Sales].[Orders] AS O  
         ON [O].[CustomerID] = [C].[CustomerID]  
      WHERE [C].[CustomerID] = @CustomerID  
    END  
    GO  
    ```  
  
5.  儲存檔案。 因為您在下一個程序必須使用這個指令碼，請記下位置。  
  
6.  按一下 [ **檔案** ] 功能表上的 [ **關閉方案**]。  
  
    接下來，您建立資料庫專案並從已建立的指令碼匯入結構描述。  
  
## <a name="CreateProjectAndImport"></a>建立資料庫專案並匯入結構描述  
  
#### <a name="to-create-a-database-project"></a>建立資料庫專案  
  
1.  在 [ **檔案** ] 功能表中，指向 [ **新增**]，然後按一下 [ **專案**]。  
  
    [新增專案]  對話方塊隨即出現。  
  
2.  在 [已安裝的範本] 底下，選取 [SQL Server] 節點，然後選取 [SQL Server 資料庫專案]。  
  
3.  在 [ **名稱**] 中輸入 **SimpleUnitTestDB**。  
  
4.  選取 [ **為方案建立目錄** ] 核取方塊 (若尚未選取)。  
  
5.  清除 [ **加入至原始檔控制** ] 核取方塊 (若尚未清除)，然後按一下 [ **確定**]。  
  
    資料庫專案就會在 [ **方案總管**] 中建立並出現。 接下來，您從指令碼匯入資料庫結構描述。  
  
#### <a name="to-import-a-database-schema-from-a-script"></a>若要從指令碼匯入資料庫結構描述  
  
1.  在 [專案] 功能表上，按一下 [匯入]，然後按一下 [指令碼 (\*.sql)]。  
  
2.  在閱讀過歡迎頁面之後，按 [ **下一步** ]。  
  
3.  按一下 [ **瀏覽**]，然後移至您儲存 .sql 檔案的目錄。  
  
4.  按兩下 .sql 檔案，然後按一下 [完成]。  
  
    指令碼會匯入，而且該指令碼中定義的物件會加入至資料庫專案。  
  
5.  檢閱摘要，然後按一下 [ **完成** ] 完成作業。  
  
    > [!NOTE]  
    > Sales.uspFillOrder 程序包含刻意設計的程式碼錯誤，這個程序稍後將探索並更正此錯誤。  
  
#### <a name="to-examine-the-resulting-project"></a>若要檢查結果專案  
  
1.  在 [ **方案總管**] 中，檢查匯入至專案的指令碼檔案。  
  
2.  在 [SQL Server 物件總管] 中，查看 [專案] 節點中的資料庫。  
  
## <a name="DeployDBProj"></a>部署至 LocalDB  
根據預設，當您按 F5 時，會將資料庫部署 (發行) 至 LocalDB 資料庫。 您可以移至專案屬性頁的 [偵錯] 索引標籤，然後變更連接字串，來變更資料庫位置。  
  
## <a name="CreateDBUnitTests"></a>建立 SQL Server 單元測試  
  
#### <a name="to-create-a-sql-server-unit-test-for-the-stored-procedures"></a>建立預存程序的 SQL Server 單元測試  
  
1.  在 [SQL Server 物件總管] 中，展開 **SimpleUnitTestDB** 的專案節點，然後依序展開 [可程式性] 和 [預存程序] 節點。  
  
2.  以滑鼠右鍵按一下其中一個預存程序，然後按一下 [建立單元測試] 以顯示 [建立單元測試] 對話方塊。  
  
3.  選取所有五個預存程序的核取方塊：**Sales.uspCancelOrder**、**Sales.uspFillOrder**、**Sales.uspNewCustomer**、**Sales.uspPlaceNewOrder** 及 **Sales.uspShowOrderDetails**。  
  
4.  在 [專案] 下拉式清單中，選取 [建立新的 Visual C# 測試專案]。  
  
5.  接受專案名稱和類別名稱的預設名稱，然後按一下 [ **確定**]。  
  
6.  在測試組態對話方塊中的 [ **使用下列資料連接來執行單元測試**]，指定連接到您稍早在此逐步解說部署的資料庫。 例如，如果使用預設部署位置 (即 LocalDB)，則按一下 [新增連接] 以指定 **(LocalDB)\Projects**。 然後，選擇資料庫的名稱。 再按一下 [確定] 關閉 [ **連接屬性** ] 對話方塊。  
  
    > [!NOTE]  
    > 如果您必須測試權限受限制的檢視表或預存程序，通常會在這個步驟中指定該連接。 然後您會指定具有更廣泛之權限的次要連接，驗證此測試。 如果您有次要連接，您應該將該使用者加入至資料庫專案，並在預先部署指令碼中建立該使用者的登入。  
  
7.  在測試組態對話方塊中的 [ **部署** ] 區段，選取 [ **執行單元測試前自動部署資料庫專案** ] 核取方塊。  
  
8.  在 [ **資料庫專案**]，按一下 **SimpleUnitTestDB.sqlproj**。  
  
9. 在 [ **部署組態**]，按一下 [ **偵錯**]。  
  
    您也可以產生測試資料，作為 SQL Server 單元測試的一部分。 針對這個逐步解說，因為測試會建立自己的資料，您會略過該步驟。  
  
10. 按一下 [確定] 。  
  
    測試專案就會建置而且 SQL Server 單元測試設計工具隨即出現。 接下來，您將更新單元測試 Transact\-SQL 指令碼中的測試邏輯。  
  
## <a name="DefineTestLogic"></a>定義測試邏輯  
這個非常簡單的資料庫有兩個資料表：Customer 和 Order。 使用下列預存程序來更新資料庫：  
  
-   uspNewCustomer - 這個預存程序將記錄加入至 Customer 資料表，因而將客戶的 YTDOrders 和 YTDSales 資料行設為零。  
  
-   uspPlaceNewOrder - 這個預存程序將記錄加入至指定之客戶的 Orders 資料表，並更新 Customer 資料表中對應記錄的 YTDOrders 值。  
  
-   uspFillOrder - 這個預存程序在 Orders 資料表中更新一筆記錄 (從狀態 'O' 變更為 'F')，並遞增 Customer 資料表中對應記錄的 YTDSales 金額。  
  
-   uspCancelOrder - 這個預存程序在 Orders 資料表中更新一筆記錄 (從狀態 'O' 變更為 'X") 並遞減 Customer 資料表中對應記錄的 YTDOrders 金額。  
  
-   uspShowOrderDetails - 這個預存程序聯結 Orders 資料表與 Customer 資料表，並顯示特定客戶的記錄。  
  
> [!NOTE]  
> 此範例說明如何建立簡單的 SQL Server 單元測試。 在真實資料庫，您可以針對特定客戶加總狀態為 'O' 或 'F' 的所有訂單總金額。 在這個逐步解說的程序也未包含錯誤處理。 例如，它們不會防止您針對已完成之訂單呼叫 uspFillOrder。  
  
測試假設資料庫在乾淨狀態下啟動。 您將建立確認下列條件的測試：  
  
-   uspNewCustomer - 確認 Customer 資料表在執行預存程序之後包含一個資料行。  
  
-   uspPlaceNewOrder - 針對 CustomerID 為 1 的客戶，下 $100 的訂單。 確認該客戶的 YTDOrders 金額為 100，而 YTDSales 金額是零。  
  
-   uspFillOrder - 針對 CustomerID 為 1 的客戶，下 $50 的訂單。 完成該訂單。 確認 YTDOrders 和 YTDSales 金額都是 50。  
  
-   uspShowOrderDetails - 針對 CustomerID 為 1 的客戶，分別下 $100、$50 和 $5 的訂單。 確認 uspShowOrderDetails 傳回正確的資料行數目，而且結果集有預期的總和檢查碼。  
  
> [!NOTE]  
> 針對一組完整的 SQL Server 單元測試，您通常會確認是否已正確設定其他資料行。 為了讓這個逐步解說的大小容易管理，它不會描述如何確認 uspCancelOrder 行為。  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspnewcustomer"></a>撰寫 uspNewCustomer 的 SQL Server 單元測試  
  
1.  在 SQL Server 單元測試設計工具的巡覽列中，按一下 **Sales_uspNewCustomerTest**，並確定在相鄰清單中的 [測試] 已反白顯示。  
  
    在您執行上述步驟之後，您可以在單元測試中建立測試動作的測試指令碼。  
  
2.  在 Transact\-SQL 編輯器中更新 Transact\-SQL 陳述式，以符合下列陳述式：  
  
    ```  
    -- ssNoVersion unit test for Sales.uspNewCustomer  
    DECLARE @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @CustomerName = 'Fictitious Customer';  
  
    EXECUTE @RC = [Sales].[uspNewCustomer] @CustomerName;  
  
    SELECT * FROM [Sales].[Customer];  
    ```  
  
3.  在 [測試條件] 窗格中，按一下 [結果不明] 測試條件，然後按一下 [刪除測試條件] 圖示 (紅色 X)。  
  
4.  在 [測試條件] 窗格中，按一下清單中的 [資料列計數]，然後按一下 [加入測試條件] 圖示 (綠色 +)。  
  
5.  開啟 [屬性] 視窗 (選取測試條件並按 F4)，然後將 [資料列計數] 屬性設定為 1。  
  
6.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
    接下來，您定義 uspPlaceNewOrder 的單元測試邏輯。  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspplaceneworder"></a>撰寫 uspPlaceNewOrder 的 SQL Server 單元測試  
  
1.  在 SQL Server 單元測試設計工具的巡覽列中，按一下 **Sales_uspPlaceNewOrderTest**，並確定在相鄰清單中的 [測試] 已反白顯示。  
  
    在您執行這個步驟之後，您可以在單元測試中建立測試動作的測試指令碼。  
  
2.  在 Transact\-SQL 編輯器中更新 Transact\-SQL 陳述式，以符合下列陳述式：  
  
    ```  
    -- ssNoVersion unit test for Sales.uspPlaceNewOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- place an order for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, @Amount, @OrderDate, @Status;  
  
    -- verify that the YTDOrders value is correct.  
    SELECT @RC = [YTDOrders] FROM [Sales].[Customer] WHERE [CustomerID] = @CustomerID  
  
    SELECT @RC AS RC  
    ```  
  
3.  在 [ **測試條件** ] 窗格，按一下結果不明的測試條件，然後按一下 [ **刪除測試條件**]。  
  
4.  在 [ **測試條件** ] 窗格，按一下清單中的 [ **純量值** ]，然後按一下 [ **加入測試條件**]。  
  
5.  在 [ **屬性** ] 視窗中，將 [ **需要的值** ] 屬性設為 100。  
  
6.  在 SQL Server 單元測試設計工具的巡覽列中，按一下 **Sales_uspPlaceNewOrderTest**，並確定在相鄰清單中的 [測試前] 已反白顯示。  
  
    執行此步驟之後，您可以指定陳述式，讓資料處於執行測試所需的狀態。 在此範例中，您必須先建立 Customer 記錄才能下訂單。  
  
7.  按一下 [按一下此處以建立]，建立測試前指令碼。  
  
8.  在 Transact\-SQL 編輯器中更新 Transact\-SQL 陳述式，以符合下列陳述式：  
  
    ```  
    /*  
    Add Transact-SQL statements here that you want to run before  
    the test script is run.  
    */  
    -- Add a customer for this test with the name 'Fictitious Customer'  
    DECLARE @NewCustomerID AS INT, @CustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
       @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
    ```  
  
9. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
    接下來，您建立 uspFillOrder 的單元測試。  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspfillorder"></a>撰寫 uspFillOrder 的 SQL Server 單元測試  
  
1.  在 SQL Server 單元測試設計工具的巡覽列中，按一下 **Sales_uspFillOrderTest**，並確定在相鄰清單中的 [測試] 已反白顯示。  
  
    在您執行這個步驟之後，您可以在單元測試中建立測試動作的測試指令碼。  
  
2.  在 Transact\-SQL 編輯器中更新 Transact\-SQL 陳述式，以符合下列陳述式：  
  
    ```  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @FilledDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
    -- Get the most recently added order.  
    SELECT @OrderID = MAX([OrderID]) FROM [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
  
    -- fill an order for that customer  
    EXECUTE @RC = [Sales].[uspFillOrder] @OrderID, @FilledDate;  
  
    -- verify that the YTDOrders value is correct.  
    SELECT @RC = [YTDSales] FROM [Sales].[Customer] WHERE [CustomerID] = @CustomerID  
  
    SELECT @RC AS RC;  
    ```  
  
3.  在 [ **測試條件** ] 窗格，按一下結果不明的測試條件，然後按一下 [ **刪除測試條件**]。  
  
4.  在 [ **測試條件** ] 窗格，按一下清單中的 [ **純量值** ]，然後按一下 [ **加入測試條件**]。  
  
5.  在 [ **屬性** ] 視窗中，將 [ **需要的值** ] 屬性設為 100。  
  
6.  在 SQL Server 單元測試設計工具的巡覽列中，按一下 **Sales_uspFillOrderTest**，並確定在相鄰清單中的 [測試前] 已反白顯示。 執行此步驟之後，您可以指定陳述式，讓資料處於執行測試所需的狀態。 在此範例中，您必須先建立 Customer 記錄才能下訂單。  
  
7.  按一下 [按一下此處以建立]，建立測試前指令碼。  
  
8.  在 Transact\-SQL 編輯器中更新 Transact\-SQL 陳述式，以符合下列陳述式：  
  
    ```  
    /*  
    Add Transact-SQL statements here that you want to run before  
    the test script is run.  
    */  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'CustomerB'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place an order for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, @Amount, @OrderDate, @Status;  
  
    COMMIT TRANSACTION  
    ```  
  
9. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspshoworderdetails"></a>撰寫 uspShowOrderDetails 的 SQL Server 單元測試  
  
1.  在 SQL Server 單元測試設計工具的巡覽列中，按一下 **Sales_uspShowOrderDetailsTest**，並確定在相鄰清單中的 [測試] 已反白顯示。  
  
    在您執行這個步驟之後，您可以在單元測試中建立測試動作的測試指令碼。  
  
2.  在 Transact\-SQL 編輯器中更新 Transact\-SQL 陳述式，以符合下列陳述式：  
  
    ```  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @FilledDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- fill an order for that customer  
    EXECUTE @RC = [Sales].[uspShowOrderDetails] @CustomerID;  
  
    SELECT @RC AS RC;  
    ```  
  
3.  在 [ **測試條件** ] 窗格，按一下結果不明的測試條件，然後按一下 [ **刪除測試條件**]。  
  
4.  在 [ **測試條件** ] 窗格，按一下清單中的 [ **預期的結構描述** ]，然後按一下 [ **加入測試條件**]。  
  
5.  在 [屬性] 視窗中，按一下 [組態] 屬性中的瀏覽按鈕 ([...])。  
  
6.  在 [ **expectedSchemaCondition1 的組態** ] 對話方塊中，指定資料庫連接。 例如，如果使用預設部署位置 (即 LocalDB)，則按一下 [新增連接] 以指定 **(LocalDB)\Projects**。 然後，選擇資料庫的名稱。  
  
7.  按一下 [ **擷取**]。 (如有需要，重複按一下 [擷取]，直到看見資料為止)。  
  
    單元測試的 Transact\-SQL 主體就會執行，而且產生的結構描述會出現在對話方塊中。 由於沒有執行測試前程式碼，所以不會傳回資料。 因為您只確認結構描述而非資料，這是正常的。  
  
8.  按一下 [確定] 。  
  
    預期的結構描述與測試條件一起儲存。  
  
9. 在 SQL Server 單元測試設計工具的巡覽列中，按一下 **Sales_uspShowOrderDetailsTest**，並確定在相鄰清單中的 [測試前] 已反白顯示。 執行此步驟之後，您可以指定陳述式，讓資料處於執行測試所需的狀態。 在此範例中，您必須先建立 Customer 記錄才能下訂單。  
  
10. 按一下 [按一下此處以建立]，建立測試前指令碼。  
  
11. 在 Transact\-SQL 編輯器中更新 Transact\-SQL 陳述式，以符合下列陳述式：  
  
    ```  
    /*  
    Add Transact-SQL statements here to run before the test script is run.  
    */  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'FictitiousCustomer'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place 3 orders for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 100, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 50, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 5, @OrderDate, @Status;  
  
    COMMIT TRANSACTION  
    ```  
  
12. 在 SQL Server 單元測試設計工具的巡覽列中，按一下 **Sales_uspShowOrderDetailsTest**，然後按一下相鄰清單中的 [測試]。  
  
    您必須這樣做，因為您要將總和檢查碼條件套用至測試，而不套用至測試前指令碼。  
  
13. 在 [ **測試條件** ] 窗格，按一下清單中的 [ **資料總和檢查碼** ]，然後按一下 [ **加入測試條件**]。  
  
14. 在 [屬性] 視窗中，按一下 [組態] 屬性中的瀏覽按鈕 ([...])。  
  
15. 在 [ **checksumCondition1 的組態** ] 對話方塊中，指定資料庫連接。  
  
16. 以下列程式碼取代對話方塊中的 Transact\-SQL (位於 [編輯連接] 按鈕底下)：  
  
    ```  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'CustomerB'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @Status AS CHAR (1);  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @OrderDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place 3 orders for that customer  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 100, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 50, @OrderDate, @Status;  
    EXECUTE @RC = [Sales].[uspPlaceNewOrder] @CustomerID, 5, @OrderDate, @Status;  
  
    COMMIT TRANSACTION  
  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @FilledDate AS DATETIME;  
    DECLARE @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- fill an order for that customer  
    EXECUTE @RC = [Sales].[uspShowOrderDetails] @CustomerID;  
  
    SELECT @RC AS RC;  
    ```  
  
    此程式碼會將測試前指令碼的 Transact\-SQL 程式碼與測試本身的 Transact\-SQL 程式碼結合。 您需要這兩個程式碼，以在執行測試時傳回相同的結果。  
  
17. 按一下 [ **擷取**]。 (如有需要，重複按一下 [擷取]，直到看見資料為止)。  
  
    您指定的 Transact\-SQL 就會執行，而且會計算所傳回資料的總和檢查碼。  
  
18. 按一下 [確定] 。  
  
    計算的總和檢查碼與測試條件一起儲存。 預期的總和檢查碼會出現在資料總和檢查碼測試條件的 [值] 資料行。  
  
19. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
    此時，您已經準備好執行測試。  
  
## <a name="RunTests"></a>執行 SQL Server 單元測試  
  
#### <a name="to-run-the-sql-server-unit-tests"></a>執行 SQL Server 單元測試  
  
1.  在 [測試] 功能表上，指向 [Windows]，然後按一下 [測試檢視] (Visual Studio 2010) 或 [測試總管] (Visual Studio 2012)。  
  
2.  在 [測試檢視] 視窗 (Visual Studio 2010) 中，按一下工具列上的 [重新整理] 以更新測試清單。 若要查看 [測試總管] (Visual Studio 2012) 中的測試清單，請建置方案。  
  
    [測試檢視] 或 [測試總管] 視窗會列出您稍早在此逐步解說中建立並已加入 Transact\-SQL 陳述式和測試條件的測試。 名為 TestMethod1 的測試為空白，而且不用於這個逐步解說。  
  
3.  以滑鼠右鍵按一下 **Sales_uspNewCustomerTest**，然後按一下 [執行選取範圍]。  
  
    Visual Studio 會使用您所指定的有權限的內容來連線到資料庫並套用資料產生計劃。 接著，Visual Studio 會切換至執行內容，然後在測試中執行 Transact\-SQL 指令碼。 最後，Visual Studio 會針對您在測試條件中指定的內容來評估 Transact\-SQL 指令碼的結果，而且成功或失敗結果會出現在 [測試結果] 視窗中。  
  
4.  檢視 [ **測試結果** ] 視窗中的結果。  
  
    測試成功，表示 **SELECT** 陳述式會在執行時傳回一個資料列。  
  
5.  針對 Sales_uspPlaceNewOrderTest、Sales_uspFillOrderTest 和 Sales_uspShowOrderDetailsTest 測試重複步驟 3。 結果應該如下所示：  
  
    |測試|預期的結果|  
    |--------|-------------------|  
    |Sales_uspPlaceNewOrderTest|成功|  
    |Sales_uspShowOrderDetailsTest|成功|  
    |Sales_uspFillOrderTest|失敗會顯示下列錯誤：「ScalarValueCondition 條件 (scalarValueCondition2) 失敗: ResultSet 1 資料列 1 資料行 1: 值不相符，實際為 '-100'，預期為 '100'」。發生這個錯誤的原因是預存程序的定義包含次要錯誤。|  
  
    接下來，您將更正錯誤並重新執行測試。  
  
#### <a name="to-correct-the-error-in-salesuspfillorder"></a>若要更正 Sales.uspFillOrder 的錯誤  
  
1.  在 [SQL Server 物件總管] 中，展開資料庫的 [專案] 節點，按兩下 **uspFillOrder** 預存程序，以便在 Transact\-SQL 編輯器中開啟其定義。  
  
2.  在定義中，尋找下列 Transact\-SQL 陳述式：  
  
    ```  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales - @Delta  
        WHERE [CustomerID] = @CustomerID  
    ```  
  
3.  變更陳述式中的 SET 子句，以符合下列陳述式：  
  
    ```  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales + @Delta  
        WHERE [CustomerID] = @CustomerID  
    ```  
  
4.  按一下 [ **檔案** ] 功能表上的 [ **儲存 uspFillOrder.sql**]。  
  
5.  在 [測試檢視] 中，以滑鼠右鍵按一下 **Sales_uspFillOrderTest**，然後按一下 [執行選取範圍]。  
  
    測試會成功。  
  
## <a name="NegativeTest"></a>加入負面單元測試  
您可以建立負面測試，確認測試會在應該失敗時失敗。 例如，如果您嘗試取消已完成的訂單，該測試應該會失敗。 在這個部分的逐步解說中，您建立 Sales.uspCancelOrder 預存程序的負面單元測試。  
  
若要建立並確認負面測試，您必須執行下列工作：  
  
-   更新預存程序以測試失敗條件  
  
-   定義新的單元測試  
  
-   修改單元測試的程式碼，以指出預期會失敗  
  
-   執行單元測試  
  
#### <a name="to-update-the-stored-procedure"></a>若要更新預存程序  
  
1.  在 [SQL Server 物件總管] 中，展開 SimpleUnitTestDB 資料庫的 [專案] 節點，依序展開 [可程式性] 節點、[預存程序] 節點，然後按兩下 [uspCancelOrder]。  
  
2.  在 Transact\-SQL 編輯器中，更新程序定義以符合下列程式碼：  
  
    ```  
    CREATE PROCEDURE [Sales].[uspCancelOrder]  
    @OrderID INT  
    AS  
    BEGIN  
        DECLARE @Delta INT, @CustomerID INT, @PriorStatus CHAR(1)  
        BEGIN TRANSACTION  
            BEGIN TRY  
                IF (NOT EXISTS(SELECT [CustomerID] from [Sales].[Orders] WHERE [OrderID] = @OrderID))  
                BEGIN  
                    -- Specify WITH LOG option so that the error is  
                    -- written to the application log.  
                    RAISERROR( 'That order does not exist.', -- Message text  
                               16, -- severity  
                                1 -- state  
                            ) WITH LOG;  
                END  
  
                SELECT @Delta = [Amount], @CustomerID = [CustomerID], @PriorStatus = [Status]  
                 FROM [Sales].[Orders] WHERE [OrderID] = @OrderID  
  
                IF @PriorStatus <> 'O'   
                BEGIN  
                    -- Specify WITH LOG option so that the error is  
                    -- written to the application log.  
                    RAISERROR ( 'You can only cancel open orders.', -- Message text  
                                16, -- Severity  
                                1 -- State  
                                ) WITH LOG;  
                END  
                ELSE  
                BEGIN  
                    -- If we make it to here, then we can cancel the order. Update the status to 'X' first...  
                    UPDATE [Sales].[Orders]  
                       SET [Status] = 'X'  
                    WHERE [OrderID] = @OrderID  
                    -- and then remove the amount from the YTDOrders for the customer  
                    UPDATE [Sales].[Customer]  
                           SET  
                               YTDOrders = YTDOrders - @Delta  
                    WHERE [CustomerID] = @CustomerID  
                    COMMIT TRANSACTION  
                    RETURN 1; -- indicate success  
                END  
            END TRY  
            BEGIN CATCH  
                DECLARE @ErrorMessage NVARCHAR(4000);  
                DECLARE @ErrorSeverity INT;  
                DECLARE @ErrorState INT;  
  
                SELECT @ErrorMessage = ERROR_MESSAGE(),  
                       @ErrorSeverity = ERROR_SEVERITY(),  
                       @ErrorState = ERROR_STATE();  
  
                ROLLBACK TRANSACTION  
                -- Use RAISERROR inside the CATCH block to return  
                -- error information about the original error that  
                -- caused execution to jump to the CATCH block.  
                RAISERROR (@ErrorMessage, -- Mesasge text  
                           @ErrorSeverity, -- Severity  
                           @ErrorState -- State  
                          );  
                RETURN 0; -- indicate failure  
            END CATCH;  
    END  
    ```  
  
3.  按一下 [ **檔案** ] 功能表上的 [ **儲存 uspCancelOrder.sql**]。  
  
4.  按 F5 部署 **SimpleUnitTestDB**。  
  
    您將更新部署至 uspCancelOrder 預存程序。 您未變更其他物件，因此只更新該預存程序。  
  
    接下來，您定義與這個程序相關聯的單元測試。  
  
#### <a name="to-write-the-sql-server-unit-test-for-uspcancelorder"></a>撰寫 uspCancelOrder 的 SQL Server 單元測試  
  
1.  在 SQL Server 單元測試設計工具的巡覽列中，按一下 **Sales_uspCancelOrderTest**，並確定在相鄰清單中的 [測試] 反白顯示。  
  
    在您執行這個步驟之後，您可以在單元測試中建立測試動作的測試指令碼。  
  
2.  在 Transact\-SQL 編輯器中更新 Transact\-SQL 陳述式，以符合下列陳述式：  
  
    ```  
    -- ssNoVersion unit test for Sales.uspFillOrder  
    DECLARE @RC AS INT, @CustomerID AS INT, @Amount AS INT, @FilledDate AS DATETIME, @Status AS CHAR (1);  
    DECLARE @CustomerName AS NVARCHAR(40), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
           @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
    -- Get the most recently added order.  
    SELECT @OrderID = MAX([OrderID]) FROM [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
  
    -- try to cancel an order for that customer that has already been filled  
    EXECUTE @RC = [Sales].[uspCancelOrder] @OrderID;  
  
    SELECT @RC AS RC;  
    ```  
  
3.  在 [ **測試條件** ] 窗格，按一下結果不明的測試條件，然後按一下 [ **刪除測試條件** ] 圖示。  
  
4.  在 [ **測試條件** ] 窗格，按一下清單中的 [ **純量值** ]，然後按一下 [ **加入測試條件** ] 圖示。  
  
5.  在 [ **屬性** ] 視窗中，將 [ **需要的值** ] 屬性設為 0。  
  
6.  在 SQL Server 單元測試設計工具的巡覽列中，按一下 **Sales_uspCancelOrderTest**，並確定在相鄰清單中的 [測試前] 已反白顯示。 執行此步驟之後，您可以指定陳述式，讓資料處於執行測試所需的狀態。 在此範例中，您必須先建立 Customer 記錄才能下訂單。  
  
7.  按一下 [按一下此處以建立]，建立測試前指令碼。  
  
8.  在 Transact\-SQL 編輯器中更新 Transact\-SQL 陳述式，以符合下列陳述式：  
  
    ```  
    /*  
    Add Transact-SQL statements here to run before the test script is run.  
    */  
    BEGIN TRANSACTION  
  
    -- Add a customer for this test with the name 'CustomerB'  
    DECLARE @NewCustomerID AS INT, @RC AS INT, @CustomerName AS NVARCHAR (40);  
  
    SELECT @RC = 0,  
           @NewCustomerID = 0,  
           @CustomerName = N'Fictitious Customer';  
  
    IF NOT EXISTS(SELECT * FROM [Sales].[Customer] WHERE CustomerName = @CustomerName)  
    BEGIN  
    EXECUTE @NewCustomerID = [Sales].[uspNewCustomer] @CustomerName;  
    END  
  
    DECLARE @CustomerID AS INT, @Amount AS INT, @OrderDate AS DATETIME, @FilledDate AS DATETIME, @Status AS CHAR (1), @OrderID AS INT;  
  
    SELECT @RC = 0,  
           @CustomerID = 0,  
       @OrderID = 0,  
           @CustomerName = N'Fictitious Customer',  
           @Amount = 100,  
           @OrderDate = getdate(),  
       @FilledDate = getdate(),  
           @Status = 'O';  
  
    -- NOTE: Assumes that you inserted a Customer record with CustomerName='Fictitious Customer' in the pre-test script.  
    SELECT @CustomerID = [CustomerID] FROM [Sales].[Customer] WHERE [CustomerName] = @CustomerName;  
  
    -- delete any old records in the Orders table and clear out the YTD Sales/Orders fields  
    DELETE from [Sales].[Orders] WHERE [CustomerID] = @CustomerID;  
    UPDATE [Sales].[Customer] SET YTDOrders = 0, YTDSales = 0 WHERE [CustomerID] = @CustomerID;  
  
    -- place an order for that customer  
    EXECUTE @OrderID = [Sales].[uspPlaceNewOrder] @CustomerID, @Amount, @OrderDate, @Status;  
  
    -- fill the order for that customer  
    EXECUTE @RC = [Sales].[uspFillOrder] @OrderID, @FilledDate;  
  
    COMMIT TRANSACTION  
    ```  
  
9. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
    此時，您已經準備好執行測試。  
  
#### <a name="to-run-the-sql-server-unit-tests"></a>執行 SQL Server 單元測試  
  
1.  在 [測試檢視] 中，以滑鼠右鍵按一下 [Sales_uspCancelOrderTest]，然後按一下 [執行選取範圍]。  
  
2.  檢視 [ **測試結果** ] 視窗中的結果。  
  
    測試失敗，而且會出現下列錯誤：  
  
    **測試方法 TestProject1.SqlServerUnitTests1.Sales_uspCancelOrderTest 擲回例外狀況:System.Data.SqlClient.SqlException:您只能取消待處理訂單。**  
  
    接下來，您修改程式碼，以指出預期會發生例外狀況。  
  
#### <a name="to-modify-the-code-for-the-unit-test"></a>若要修改單元測試的程式碼  
  
1.  在 [方案總管] 中，展開 [TestProject1]，以滑鼠右鍵按一下 [SqlServerUnitTests1.cs]，然後按一下 [檢視程式碼]。  
  
2.  在程式碼編輯器，巡覽至 Sales_uspCancelOrderTest 方法。 修改方法的屬性以符合下列程式碼：  
  
    ```  
    [TestMethod(), ExpectedSqlException(Severity=16, MatchFirstError=false, State=1)]  
    public void Sales_uspCancelOrderTest()  
    ```  
  
    您指定預期會發生特定例外狀況。 您可以選擇性地指定特定的錯誤號碼。 如果您沒有加入此屬性，單元測試會失敗，而且 [測試結果] 視窗會出現訊息。  
  
    > [!IMPORTANT]  
    > 目前 Visual Studio 2012 不支援 ExpectedSqlException 屬性。 如需解決此問題的詳細資訊，請參閱 [無法執行「預期的失敗」資料庫單元測試](https://social.msdn.microsoft.com/Forums/ssdt/thread/e74e06ad-e3c9-4cb0-97ad-a6f235a52345)。  
  
3.  在 [檔案] 功能表中，按一下 [儲存 SqlServerUnitTests1.cs]。  
  
    接下來，您重新執行單元測試以驗證它如預期失敗。  
  
#### <a name="to-re-run-the-sql-server-unit-tests"></a>重新執行 SQL Server 單元測試  
  
1.  在 [測試檢視] 中，以滑鼠右鍵按一下 [Sales_uspCancelOrderTest]，然後按一下 [執行選取範圍]。  
  
2.  檢視 [ **測試結果** ] 視窗中的結果。  
  
    測試成功，表示程序會在應該失敗時失敗。  
  
## <a name="next-steps"></a>Next Steps  
在典型的專案，您會定義其他單元測試，以確認所有重要資料庫物件都會正常運作。 當測試集合完成後，您會將這些測試簽入「版本控制」(Version Control)，與小組成員共用。  
  
在建立基準之後，您可以建立及修改資料庫物件，然後建立關聯的測試，以確認變更是否會中斷預期行為。  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[使用 SQL Server 單元測試驗證資料庫程式碼](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)  
[操作說明：建立空白 SQL Server 單元測試](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
[操作說明：設定 SQL Server 單元測試執行](../ssdt/how-to-configure-sql-server-unit-test-execution.md)  
  
