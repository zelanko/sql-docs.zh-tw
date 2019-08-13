---
title: 快速入門：連線及查詢 Azure SQL 資料倉儲
titleSuffix: Azure Data Studio
description: 本快速入門說明如何使用 Azure Data Studio 連線到 Azure SQL 資料倉儲並執行查詢
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.openlocfilehash: 810d03ab97fd584e1ddaab45e06a21377b81685d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959400"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>快速入門：使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 連線及查詢 Azure SQL 資料倉儲中的資料

本快速入門示範如何使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 連線到 Azure SQL 資料倉儲，然後使用 Transact-SQL 陳述式建立、插入和選取資料。 

## <a name="prerequisites"></a>Prerequisites
若要完成本快速入門，您需要 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 和 Azure SQL 資料倉儲。

- [安裝 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)。

如果您還沒有 SQL 資料倉儲，請參閱[建立 SQL 資料倉儲](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision)。

請記住伺服器名稱和登入認證！


## <a name="connect-to-your-data-warehouse"></a>連線到您的資料倉儲

使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)]建立與您 Azure SQL 資料倉儲伺服器的連線。

1. 第一次執行 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 時，應該會開啟 [連線]  頁面。 如果沒有看到 [連線]  頁面，請按一下 [伺服器]  提要欄位中的 [新增連線]  或**新增連線**圖示：
   
   ![新增連線圖示](media/quickstart-sql-dw/new-connection-icon.png)

2. 本文使用「SQL 登入」  ，但「Windows 驗證」  亦受支援。 使用「您的」  Azure SQL 伺服器的伺服器名稱、使用者名稱和密碼填入欄位如下：

   | 設定       | 建議值 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器名稱** | 完整伺服器名稱 | 名稱應如下所示：**sqldwsample.database.windows.net** |
   | **驗證** | SQL 登入| 本教學課程使用 SQL 驗證。 |
   | **User name** | 伺服器系統管理員帳戶 | 這是您在建立伺服器時指定的帳戶。 |
   | **密碼 (SQL 登入)** | 伺服器系統管理員帳戶的密碼 | 這是您在建立伺服器時指定的密碼。 |
   | **儲存密碼嗎？** | [是] 或 [否] | 如果您不想要每次都輸入密碼，請選取 [是]。 |
   | **資料庫名稱** | 保留空白  | 要連線之資料庫的名稱。 |
   | **伺服器群組** | 選取 <Default> | 如果您已建立伺服器群組，您可以設定為特定伺服器群組。 | 

   ![新增連線圖示](media/quickstart-sql-dw/new-connection-screen.png) 

3. 如果您伺服器的防火牆規則沒有允許 Azure Data Studio 進行連線，就會開啟 [建立新的防火牆規則]  表單。 完成表單，以便建立新的防火牆規則。 如需詳細資訊，請參閱[防火牆規則](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)。

   ![新增防火牆規則](media/quickstart-sql-dw/firewall.png)  

4. 成功連線之後，您的伺服器就會在 [伺服器]  提要欄位中開啟。

## <a name="create-the-tutorial-data-warehouse"></a>建立教學課程資料倉儲
1. 以滑鼠右鍵按一下您的伺服器，然後在物件總管中選取 [新增查詢]  。

1. 將下列程式碼片段貼到查詢編輯器，然後按一下 [執行]  ：

   ```sql
    IF NOT EXISTS (
       SELECT name
       FROM sys.databases
       WHERE name = N'TutorialDB'
    )
    CREATE DATABASE [TutorialDB] (EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');
    GO  
    
    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
   ```


## <a name="create-a-table"></a>建立資料表

查詢編輯器仍會連線到 *master* 資料庫，但我們想要在 *TutorialDB* 資料庫中建立資料表。 

1. 將連線內容變更為 **TutorialDB**：

   ![變更內容](media/quickstart-sql-database/change-context.png)


1. 將下列程式碼片段貼到查詢編輯器，然後按一下 [執行]  ：

   > [!NOTE]
   > 您可以在編輯器中將此項目附加至查詢，或覆寫先前的查詢。 請注意，按一下 [執行]  只會執行選取的查詢。 如果沒有選取任何項目，按一下 [執行]  會執行編輯器中的所有查詢。

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT     NOT NULL,
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows"></a>插入資料列

1. 將下列程式碼片段貼到查詢編輯器，然後按一下 [執行]  ：

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
      SELECT 1, N'Orlando',N'Australia', N'' UNION ALL
      SELECT 2, N'Keith', N'India', N'keith0@adventure-works.com' UNION ALL
      SELECT 3, N'Donna', N'Germany', N'donna0@adventure-works.com' UNION ALL
      SELECT 4, N'Janet', N'United States', N'janet1@adventure-works.com'
   ```


## <a name="view-the-result"></a>檢視結果
1. 將下列程式碼片段貼到查詢編輯器，然後按一下 [執行]  ：

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. 查詢的結果隨即顯示：

   ![選取結果](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>清除資源

此集合中的其他文章都是以本快速入門為基礎來建立。 如果您打算繼續進行後續的快速入門，請勿清除於本快速入門所建立的資源。 如果您不打算繼續進行，請使用下列步驟在 Azure 入口網站中刪除本快速入門所建立的資源。
藉由刪除您不再需要的資源群組，即可清除資源。 如需詳細資訊，請參閱[清除資源](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources)。


## <a name="next-steps"></a>後續步驟

現在您已成功連線到 Azure SQL 資料倉儲並執行查詢，請嘗試[程式碼編輯器教學課程](tutorial-sql-editor.md)。
