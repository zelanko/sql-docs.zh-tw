---
Title: 'Tutorial: Connect and Query SQL Server using SQL Server Management Studio'
description: 使用 SQL Server Management Studio 連線到 SQL Server 並執行基本 T-SQL 查詢的教學課程。
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 7b389c5b58dc0afde077f70e2fd8bec7c6cac4d0
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2018
---
# <a name="tutorial-connect-and-query-sql-server-using-sql-server-management-studio"></a>教學程課：使用 SQL Server Management Studio 連線和查詢 SQL Server
本教學課程將教導您如何使用 SQL Server Management Studio (SSMS) 連線到 SQL Server 執行個體，並執行一些基本的 Transact-SQL (T-SQL) 命令。 本文會示範如何執行下列操作：
    - [連線到 SQL Server](#connect-to-a-sql-server)
    - [建立新的資料庫 (**TutorialDB**)](#create-a-database)
    - [在新資料庫中建立資料表 (**客戶**)](#create-a-table)
    - [將資料列插入新**客戶**資料表](#insert-rows)
    - [查詢**客戶**資料表和檢視結果](#view-query-results)
    - [使用查詢視窗資料表來驗證您的連線屬性](#verify-your-query-window-connection-properties)
    - [變更您查詢視窗所連線的伺服器](#change-server-connection-within-query-window)


## <a name="prerequisites"></a>Prerequisites
若要完成本教學課程，您需要 SQL Server Management Studio 和 SQL Server 存取權。 

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)。

如果您沒有 SQL Server 存取權，請從下列連結中選取平台 (如果您選擇 SQL 驗證，請確認您記住 SQL 登入名稱和密碼！)：
- [Windows - 下載 SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS - 下載 Docker 上的 SQL Server 2017](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker)


## <a name="connect-to-a-sql-server"></a>連線到 SQL Server

1. 啟動 SQL Server Management Studio (SSMS)。
1. 第一次執行 SSMS 時，[連線到伺服器] 對話方塊隨即開啟。 
      - 如果 [連線到伺服器] 對話方塊未開啟，可以在**物件總管** > [連線] (或其旁邊的圖示) > [資料庫引擎] 中手動開啟。

        ![在物件總管中連線](media/connect-query-sql-server/connectobjexp.png)

1. 在 [連線到伺服器] 對話方塊中，填寫您的連線選項： 

    - **伺服器類型**：資料庫引擎 (通常預設為已選取)
    - **驗證**：Windows 驗證 (本文使用 Windows 驗證，但支援 SQL 登入；如選取，將提示您輸入使用者名稱及密碼)

      ![連接](media/connect-query-sql-server/connection.png)

        您也可以透過點一下 [選項] 按鈕來修改其他連線選項 (例如您要連線的資料庫、連線逾時值和網路通訊協定)。 為了本文目的，所有內容都保留預設值。 

1. 一旦欄位填寫完畢，請按一下 [連線]。 

1. 您可以透過瀏覽**物件總管**中的物件來驗證您是否已成功連線到 SQL Server： 

   ![連線成功](media/connect-query-sql-server/successfulconnection.png)


## <a name="create-a-database"></a>建立資料庫
下列步驟會建立名為 TutorialDB 的新資料庫。 

1. 在**物件總管**中，以滑鼠右鍵按一下您的伺服器，然後選取 [新增查詢]：

   ![新增查詢](media/connect-query-sql-server/newquery.png)
   
1. 將下列 T-SQL 程式碼貼入查詢視窗中： 
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
   ```
2. 若要執行查詢，請按一下 [執行] (或在鍵盤上按 F5 鍵)。 

   ![執行查詢](media/connect-query-sql-server/execute.png)
  
 
查詢完成後，新的 **TutorialDB** 會出現在**物件總管**的資料庫清單中。 以滑鼠右鍵按一下資料庫節點，然後選取 [重新整理]。  


## <a name="create-a-table"></a>建立資料表
下列步驟現在會在新建立的資料表中建立 **TutorialDB** 資料庫。 但是，查詢編輯器仍然位於 *Master* 資料庫的內容中，並且您要在 *TutorialDB* 資料庫中建立一個資料表。 

1. 藉由從資料庫下拉式清單中選取所需的資料庫，將查詢的連線內容從 Master 資料庫變更為 **TutorialDB**。 

   ![變更資料庫](media/connect-query-sql-server/changedb.png)

1. 將下列 T-SQL 程式碼片段貼入查詢視窗中並反白顯示，然後按一下 [執行] (或按鍵盤上的 F5 鍵)： 
    - 您可以替換查詢視窗中的現有文字，或將其附加至結尾。 如果要在查詢視窗中執行所有事項，請按一下 [執行]。 如果您想要執行部分文字，請反白顯示該部分，然後按一下 [執行]。  
  
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
查詢完成後，新的**客戶**資料表會出現在**物件總管**的資料表清單中。 如果看不到資料表，請以滑鼠右鍵按一下**物件總管**中的 **TutorialDB > [資料表]** 節點，然後選取 [重新整理]。

## <a name="insert-rows"></a>插入資料列
下列步驟會將一些資料列插入先前建立的**客戶**資料表。 

將下列 T-SQL 程式碼貼入查詢視窗中，然後按一下 [執行]： 


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

## <a name="view-query-results"></a>檢視查詢結果
查詢結果在查詢文字視窗下方可見。 下列步驟可讓您查詢**客戶**資料表並查看先前插入的資料列。  

1. 將下列 T-SQL 程式碼貼入查詢視窗中，然後按一下 [執行]： 

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```
1. 查詢結果會顯示在輸入文字的區域下： 

   ![查詢結果](media/connect-query-sql-server/queryresults.png)


1.  您可以透過選取下列選項之一，來修改結果呈現的方式：

     ![結果](media/connect-query-sql-server/results.png)

    - 根據預設，結果將位於 [格線檢視] 中，這是中間按鈕，並會在資料表中顯示結果。 
    - 第一個按鈕將在 [文字檢視] 中顯示您的結果，如下一節中的影像所示。
    - 第三個按鈕可讓您將結果儲存至檔案中，預設情況下檔案以 *.rpt 結尾。

## <a name="verify-your-query-window-connection-properties"></a>驗證查詢視窗的連線屬性
您可以在查詢結果下找到連線屬性的相關資訊。 
- 在上一個步驟執行上述查詢之後，請檢閱查詢視窗底部的連線屬性。
    - 您可以判斷您連線的伺服器和資料庫，以及您登入的使用者。
    - 您也可以查看查詢持續時間，以及稍早執行的查詢所傳回之資料列數目。
    
    ![連線屬性](media/connect-query-sql-server/connectionproperties.png)  
    在此影像中，結果會顯示在 文字檢視} 中。  

## <a name="change-server-connection-within-query-window"></a>在 [查詢視窗] 中變更伺服器連線
您可以遵循下列步驟變更目前查詢視窗所連線的伺服器。
1. 在查詢視窗中按一下滑鼠右鍵 > [連線] > [變更連線]。
2. 這將再次開啟 [連線到伺服器] 對話方塊，可讓您變更查詢連線的伺服器。 
 
   ![變更連接](media/connect-query-sql-server/changeconnection.png)
   - 請注意，這不會變更**物件總管**所連線的伺服器，而只會變更目前的查詢視窗。 



