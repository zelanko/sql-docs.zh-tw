---
title: 快速入門：連線與查詢 Azure SQL 資料庫
titleSuffix: Azure Data Studio
description: 本快速入門說明如何使用 Azure Data Studio 連線到 SQL 資料庫並執行查詢
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.openlocfilehash: bdb1a9c8efb8ebdf5d2e35c1da00c12578ade7d6
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959430"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>快速入門：使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 連線與查詢 Azure SQL 資料庫

在本快速入門中，您將使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 連線到 Azure SQL Database 伺服器。 接著，您會執行 Transact-SQL (T-SQL) 陳述式來建立和查詢 TutorialDB d資料庫，而此資料庫會在其他 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 教學課程中使用。

## <a name="prerequisites"></a>Prerequisites

若要完成本快速入門，您需要 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 和 Azure SQL Database 伺服器。

- [安裝 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)

如果您沒有 Azure SQL 伺服器，請完成下列其中一個 Azure SQL Database 快速入門。 請記住完整伺服器名稱和登入認證，以供後續步驟執行：

- [建立 DB - 入口網站](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [建立 DB - CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [建立 DB - PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>連接到 Azure SQL Database 伺服器

使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 來建立與您 Azure SQL Database 伺服器的連線。

1. 第一次執行 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 時，應該會開啟 [歡迎使用]  頁面。 如果您沒有看到 [歡迎使用]  頁面，請選取 [說明]   > [歡迎使用]  。 選取 [新增連線]  以開啟 [連線]  窗格：
   
   ![新增連線圖示](media/quickstart-sql-database/new-connection-icon.png)

2. 此文章使用 SQL 登入，但也支援 Windows 驗證。 使用 Azure SQL 伺服器的伺服器名稱、使用者名稱和密碼填入下列欄位：

   | 設定       | 建議值 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器名稱** | 完整伺服器名稱 | 如下所示：**servername.database.windows.net**。 |
   | **驗證** | SQL 登入| 本教學課程使用 SQL 驗證。 |
   | **User name** | 伺服器系統管理員帳戶使用者名稱 | 用來建立伺服器之帳戶的使用者名稱。 |
   | **密碼 (SQL 登入)** | 伺服器系統管理員帳戶密碼 | 用來建立伺服器之帳戶的密碼。 |
   | **儲存密碼嗎？** | [是] 或 [否] | 如果您不想要每次都輸入密碼，請選取 [是]  。 |
   | **資料庫名稱** | *保留空白* | 您在這裡只會連線至伺服器。 |
   | **伺服器群組** | 選取 <Default> | 您可以將此欄位設定為您所建立的特定伺服器群組。 | 

   ![新增連線圖示](media/quickstart-sql-database/new-connection-screen.png)  

3. 選取 [連接]  。

4. 如果您的伺服器沒有允許 Azure Data Studio 進行連線的防火牆規則，就會開啟 [建立新的防火牆規則]  表單。 完成表單以建立新的防火牆規則。 如需詳細資訊，請參閱[防火牆規則](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) \(部分機器翻譯\)。

   ![新增防火牆規則](media/quickstart-sql-database/firewall.png)  

成功連線之後，您的伺服器就會在 [伺服器]  提要欄位中開啟。

## <a name="create-the-tutorial-database"></a>建立教學課程資料庫

下一節會建立其他 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 教學課程中所使用的 TutorialDB 資料庫。

1. 在 [伺服器]  提要欄位中，以滑鼠右鍵按一下您的 Azure SQL 伺服器，然後選取 [新增查詢]  。

1. 將此 SQL 貼到查詢編輯器中。

   ```sql
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```

1. 從工具列中，選取 [執行]  。 通知會出現在顯示查詢進度的 [訊息]  窗格中。

## <a name="create-a-table"></a>建立資料表

查詢編輯器會連線至 **Master** 資料庫，並且我們希望在 **TutorialDB** 資料庫中建立一個資料表。 

1. 連線至 **TutorialDB** 資料庫。

   ![變更內容](media/quickstart-sql-database/change-context2.png)



1. 建立 `Customers` 資料表。 

   在查詢編輯器中將先前的查詢取代為此項，然後選取 [執行]  。

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows-into-the-table"></a>在資料表中插入資料列

將先前的查詢取代為此項，然後選取 [執行]  。

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

## <a name="view-the-result"></a>檢視結果

將先前的查詢取代為此項，然後選取 [執行]  。

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

查詢結果會顯示：

   ![選取結果](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>清除資源

稍後的快速入門文章是根據此處所建立的資源來建置。 如果您打算完成這些文章，請務必不要刪除這些資源。 否則，請在 Azure 入口網站中刪除您不再需要的資源。 如需詳細資訊，請參閱[清除資源](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources)。

## <a name="next-steps"></a>後續步驟

既然您已成功連線到 Azure SQL 資料庫並執行查詢，請嘗試[程式碼編輯器教學課程](tutorial-sql-editor.md)。
