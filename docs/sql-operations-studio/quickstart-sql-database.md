---
title: "快速入門： 使用 SQL Operations Studio （預覽) 連接及查詢 Azure SQL database |Microsoft 文件"
description: "本快速入門示範如何使用連接到 SQL 資料庫並執行查詢的 SQL Operations Studio （預覽）"
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82fbe7376d762940815c7739311e69672b7fbff6
ms.sourcegitcommit: 6c06267f3eeeb3f0d6fc4c57e1387621720ca8bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/09/2018
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>快速入門： 使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]連接並查詢 Azure SQL database

本快速入門示範如何使用 *[!INCLUDE[name-sos](../includes/name-sos-short.md)]* 連接到 Azure SQL database，然後使用 TRANSACT-SQL (T-SQL) 陳述式來建立 *TutorialDB* ，並用於 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 教學課程。

## <a name="prerequisites"></a>必要條件

若要完成本快速入門，您需要[!INCLUDE[name-sos](../includes/name-sos-short.md)]，和 Azure SQL 伺服器。

- [安裝[!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md)。

如果您還沒有 Azure SQL 伺服器，請完成下列 Azure SQL Database 快速入門 (請記住伺服器名稱和登入認證！)：

- [建立資料庫-入口網站](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [建立資料庫-CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [建立資料庫-PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>連接到 Azure SQL Database 伺服器

使用[!INCLUDE[name-sos](../includes/name-sos-short.md)] 連接 Azure SQL Database 伺服器。

1. 第一次執行[!INCLUDE[name-sos](../includes/name-sos-short.md)]時應該會開啟**連接**頁面。 如果您沒有看到**連接**頁面，請按一下**加入連接**或**伺服器**資訊看板中的**新增連線**圖示：
   
   ![新的連線圖示](media/quickstart-sql-database/new-connection-icon.png)

2. 本文使用 *SQL 登入*，但也支援 *Windows 驗證*。如下表所示，填入您的 Azure SQL server 所使用的伺服器名稱、使用者名稱和密碼：

   | 設定       | 建議值 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器名稱** | 完整伺服器名稱 | 此名稱應該像這樣： **servername.database.windows.net** |
   | **驗證** | SQL 登入| 本教學課程中使用 SQL 驗證。 |
   | **使用者名稱** | 伺服器系統管理員帳戶 | 這是您在建立伺服器時指定的帳戶。 |
   | **密碼 (SQL 登入)** | 伺服器系統管理員帳戶的密碼 | 這是您在建立伺服器時指定的密碼。 |
   | **儲存密碼嗎？** | [是] 或 [否] | 如果您不想每次輸入密碼，請選取 [是]。 |
   | **資料庫名稱** | *保留空白* | 您想要連接到資料庫的名稱。 |
   | **伺服器群組** | 選取 <Default> | 如果您建立伺服器群組，您可以設定為特定的伺服器群組。 | 

   ![新的連線圖示](media/quickstart-sql-database/new-connection-screen.png)  

3. 如果您的伺服器沒有允許 SQL Operations Studio 連線的防火牆規則，**建立新的防火牆規則**表單將會開啟。請完成表單，以建立新的防火牆規則。如需詳細資訊，請參閱[防火牆規則](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)。

   ![新的防火牆規則](media/quickstart-sql-database/firewall.png)  

4. 成功連接後，您的伺服器會在*伺服器*資訊看板中開啟。

## <a name="create-the-tutorial-database"></a>建立教學課程的資料庫

下列章節將建立*TutorialDB*資料庫，可用於各個[!INCLUDE[name-sos](../includes/name-sos-short.md)]教學課程。

1. 在伺服器資訊看板上以滑鼠右鍵按一下您的 Azure SQL 伺服器，然後選取**新增查詢。**

1. 下列程式碼片段貼到查詢編輯器，然後按一下**執行**:

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



## <a name="create-a-table"></a>建立資料表

查詢編輯器仍然會連線到*master*資料庫，但我們想要在*TutorialDB*資料庫中建立資料表。 

1. 變更連接內容為**TutorialDB**:

   ![變更內容](media/quickstart-sql-database/change-context.png)



1. 下列程式碼片段貼到查詢編輯器，然後按一下**執行**:

   > [!NOTE]
   > 您可以將程式碼片段附加或覆寫先前編輯器中的查詢。請注意，按一下**執行**只會執行已選取的查詢。如果未選取，按一下**執行**將執行編輯器中所有的查詢。

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


## <a name="insert-rows"></a>插入資料列

- 下列程式碼片段貼到查詢編輯器，然後按一下**執行**:

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
1. 下列程式碼片段貼到查詢編輯器，然後按一下**執行**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. 查詢的結果會顯示：

   ![選取 [結果]](media/quickstart-sql-database/select-results.png)


## <a name="clean-up-resources"></a>清除資源

在此系列文章中其他的文章建立在本快速入門之上。 如果您打算繼續實作後續的快速入門，請勿清除本快速入門中建立的資源。 如果您不打算繼續，請使用下列步驟刪除本快速入門在 Azure 入口網站所建立的資源。
刪除您不再需要的資源群組來清除資源。 如需詳細資訊，請參閱[清除資源](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-portal#clean-up-resources)。

## <a name="next-steps"></a>後續的步驟

現在您已成功連接到 Azure SQL database，並執行查詢，試試[教學課程中的程式碼編輯器](tutorial-sql-editor.md)。
