---
title: "快速入門： 連接及查詢 SQL Server 使用 SQL Operations Studio （預覽） |Microsoft 文件"
description: "本快速入門示範如何使用 SQL Operations Studio （預覽） 來連接到 SQL Server 和執行查詢"
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c0f78537429026583fe970a65426bc909a46557
ms.sourcegitcommit: 6c06267f3eeeb3f0d6fc4c57e1387621720ca8bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/09/2018
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>快速入門： 連接及查詢 SQL Server 使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)]
本快速入門示範如何使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]連接到 SQL Server，並再使用 TRANSACT-SQL (T-SQL) 陳述式來建立*TutorialDB*用於[!INCLUDE[name-sos](../includes/name-sos-short.md)]教學課程。

## <a name="prerequisites"></a> 必要條件

若要完成本快速入門，您需要[!INCLUDE[name-sos](../includes/name-sos-short.md)]，和 SQL Server 存取權。

- [安裝[!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md)。

如果您沒有 SQL Server 存取權，請從下列連結選取平台 （請確定您記得您的 SQL 登入和密碼 ！）：
- [Windows-下載 SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS-下載 SQL Server 2017 docker](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker)
- [Linux-下載 SQL Server 2017 Developer Edition](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-overview#install) -您只需要遵循的步驟，最多*建立及查詢資料*。


## <a name="connect-to-a-sql-server"></a>連接到 SQL Server

   
1. 啟動 **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** 。
1. 第一次執行 *[!INCLUDE[name-sos](../includes/name-sos-short.md)]*  **連接** 對話方塊隨即開啟。 如果**連接**未開啟的對話方塊中，按一下**新連線**中的圖示**伺服器**頁面：
   
   ![新的連線圖示](media/quickstart-sql-server/new-connection-icon.png)

1. 本文使用*SQL 登入*，但*Windows 驗證*支援。 填妥欄位，如下所示：
 
    - **伺服器名稱：** localhost
    - **驗證類型：** SQL 登入  
    - **使用者名稱：** for SQL Server 的使用者名稱  
    - **密碼：** for SQL Server 密碼  
    - **資料庫名稱：**這個欄位保留空白 
    - **伺服器群組：** \<預設\>  

   ![新的 [連接] 畫面](media/quickstart-sql-server/new-connection-screen.png)



## <a name="create-a-database"></a>建立資料庫

下列步驟會建立一個名為資料庫**TutorialDB**:

1. 您的伺服器，以滑鼠右鍵按一下**localhost**，然後選取**新查詢。**
1. [查詢] 視窗中貼入下列程式碼片段： 

   ```sql
   USE master
   GO
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
1. 若要執行查詢時，按一下**執行**。

查詢完成後，新**TutorialDB**會出現在資料庫清單。 如果您沒有看到它，以滑鼠右鍵按一下**資料庫**節點，然後選取**重新整理**。


## <a name="create-a-table"></a>建立資料表

查詢編輯器仍然會連線到*主要*資料庫，但我們想要建立的資料表中*TutorialDB*資料庫。 

1. 變更的連接內容**TutorialDB**:

   ![變更內容](media/quickstart-sql-server/change-context.png)



1. 下列程式碼片段貼到查詢視窗，然後按一下**執行**:

   > [!NOTE]
   > 您可以附加，或覆寫先前的查詢編輯器中。 請注意，按一下**執行**執行所選取的查詢。 如果未選取，按一下**執行**執行所有的查詢編輯器中。

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

查詢完成後，新**客戶**資料表會出現在資料表清單。 您可能需要以滑鼠右鍵按一下**TutorialDB > 資料表**節點，然後選取**重新整理**。

## <a name="insert-rows"></a>插入資料列

- 下列程式碼片段貼到查詢視窗，然後按一下**執行**:

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



## <a name="view-the-data-returned-by-a-query"></a>檢視查詢所傳回的資料
1. 下列程式碼片段貼到查詢視窗，然後按一下**執行**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. 查詢的結果會顯示：

   ![選取 [結果]](media/quickstart-sql-server/select-results.png)


## <a name="next-steps"></a>後續的步驟
現在您已成功連接到 SQL Server 和執行查詢，試試[教學課程中的程式碼編輯器](tutorial-sql-editor.md)。


