---
title: 快速入門：連線及查詢 Azure SQL database
titleSuffix: Azure Data Studio
description: 本快速入門示範如何使用 Azure Data Studio 來連接到 SQL database，然後執行查詢
ms.custom: seodec18
ms.date: 12/21/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: d368f38589530f27db98c3c61b9cec4610818ae4
ms.sourcegitcommit: a11e733bd417905150567dfebc46a137df85a2fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991811"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>快速入門：使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]連線及查詢 Azure SQL database

在此快速入門中，您將使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]連接到 Azure SQL Database 伺服器。 然後，您就會執行 TRANSACT-SQL (T-SQL) 陳述式來建立及查詢用在其他的 TutorialDB 資料庫[!INCLUDE[name-sos](../includes/name-sos-short.md)]教學課程。

## <a name="prerequisites"></a>先決條件

若要完成本快速入門中，您需要[!INCLUDE[name-sos](../includes/name-sos-short.md)]，和 Azure SQL Database 伺服器。

- [安裝 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)

如果您沒有 Azure SQL 伺服器，請完成下列的 Azure SQL Database 快速入門的其中一個。 請記住完整的伺服器名稱並登入認證，供後續步驟：

- [建立 DB-入口網站](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [建立 DB-CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [建立 DB-PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>連接到 Azure SQL Database 伺服器

使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]連接 Azure SQL Database 伺服器。

1. 第一次執行[!INCLUDE[name-sos](../includes/name-sos-short.md)]時應該會開啟**連接**頁面。 如果您沒有看到**連接**頁面上，選取**加入連接**，或**新連線**中的圖示**伺服器**提要欄位：
   
   ![新的 [連線] 圖示](media/quickstart-sql-database/new-connection-icon.png)

2. 這篇文章會使用 SQL 登入，但也支援 Windows 驗證。 填寫用於您的 Azure SQL server 的伺服器名稱、 使用者名稱和密碼的下列欄位：

   | 設定       | 建議值 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器名稱** | 完整伺服器名稱 | 如下所示： **servername.database.windows.net**。 |
   | **驗證** | SQL 登入| 本教學課程使用 SQL 驗證。 |
   | **使用者名稱** | 伺服器系統管理員帳戶的使用者名稱 | 從用來建立伺服器的帳戶使用者名稱。 |
   | **密碼 (SQL 登入)** | 伺服器系統管理員帳戶密碼 | 從用來建立伺服器的帳戶密碼。 |
   | **儲存密碼嗎？** | [是] 或 [否] | 選取 **是**若不想每次輸入密碼。 |
   | **資料庫名稱** | *保留空白* | 您只能連接到的伺服器。 |
   | **伺服器群組** | 選取 <Default> | 您可以將此欄位設定您所建立的特定伺服器群組。 | 

   ![新的 [連線] 圖示](media/quickstart-sql-database/new-connection-screen.png)  

3. 選取 [連接]。

4. 如果您的伺服器沒有防火牆規則來允許連線，Azure Data Studio**建立新的防火牆規則**表單隨即開啟。 請完成表單，以建立新的防火牆規則。 如需詳細資訊，請參閱[防火牆規則](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)。

   ![新的防火牆規則](media/quickstart-sql-database/firewall.png)  

成功連線之後，您的伺服器會在中開啟**伺服器**資訊看板。

## <a name="create-the-tutorial-database"></a>建立教學課程的資料庫

下一節中建立所使用的 TutorialDB 資料庫中其他[!INCLUDE[name-sos](../includes/name-sos-short.md)]教學課程。

1. 以滑鼠右鍵按一下您的 Azure SQL 伺服器**伺服器**資訊看板，然後選取**新的查詢**。

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

1. 從工具列中，選取**執行**。 通知會出現在**訊息**窗格顯示查詢進度。

## <a name="create-a-table"></a>建立資料表

查詢編輯器連接至**主要**資料庫中，但我們想要建立的資料表中**TutorialDB**資料庫。 

1. 連接到**TutorialDB**資料庫。

   ![變更內容](media/quickstart-sql-database/change-context2.png)



1. 建立`Customers`資料表。 

   與這個取代上一個查詢，查詢編輯器中的，然後選取**執行**。

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


## <a name="insert-rows-into-the-table"></a>資料列插入資料表

與這個取代先前的查詢，然後選取**執行**。

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

與這個取代先前的查詢，然後選取**執行**。

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

顯示查詢結果：

   ![選取 [結果]](media/quickstart-sql-database/select-results2.png)


## <a name="clean-up-resources"></a>清除資源

在這裡建立的資源時，建置更新的快速入門文章。 如果您計畫在這些文章，務必未先刪除這些資源。 否則，請在 Azure 入口網站中，刪除您不再需要的資源。 如需詳細資訊，請參閱 <<c0> [ 清除資源](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources)。

## <a name="next-steps"></a>後續步驟

現在您已成功連線至 Azure SQL database 並執行查詢，請嘗試[教學課程中的程式碼編輯器](tutorial-sql-editor.md)。
