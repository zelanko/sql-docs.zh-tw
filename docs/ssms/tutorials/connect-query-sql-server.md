---
Title: 'Tutorial: Connect to and query a SQL Server instance by using SQL Server Management Studio'
description: 透過使用 SQL Server Management Studio 並執行基本 T-SQL 查詢，來連線至 SQL Server 執行個體的教學課程。
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.prod: sql
ms.technology: ssms
ms.openlocfilehash: e487537bd5051d396e5f24243a33ded4aa38daf7
ms.sourcegitcommit: f9d4f9c1815cff1689a68debdccff5e7ff97ccaf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/31/2018
ms.locfileid: "39367660"
---
# <a name="tutorial-connect-to-and-query-a-sql-server-instance-by-using-sql-server-management-studio"></a>教學課程：透過使用 SQL Server Management Studio 來連線至及查詢 SQL Server 執行個體
本教學課程將教導您如何使用 SQL Server Management Studio (SSMS) 連線到 SQL Server 執行個體，並執行一些基本的 Transact-SQL (T-SQL) 命令。 本文會示範如何執行下列操作：

> [!div class="checklist"]  
> * 連接到 SQL Server 執行個體    
> * 建立資料庫 ("TutorialDB")    
> * 在新的資料庫中建立資料表 ("Customers")   
> * 在新的資料表內插入資料列 
> * 查詢新的資料表並檢視結果    
> * 使用查詢視窗資料表來驗證您的連線屬性 
> * 變更您查詢視窗所連線的伺服器

## <a name="prerequisites"></a>Prerequisites
若要完成本教學課程，您需要 SQL Server Management Studio 和 SQL Server 執行個體存取權。 

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

若您沒有 SQL Server 執行個體存取權，請從下列連結選取您的平台。 若您選擇 SQL 驗證，請使用您的 SQL Server 登入認證。
- **Windows**: [下載 SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- **macOS**: [下載 Docker 上的 SQL Server 2017](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker).


## <a name="connect-to-a-sql-server-instance"></a>連接到 SQL Server 執行個體

1. 啟動 SQL Server Management Studio。 首次執行 SSMS 時，會開啟 [連線至伺服器] 視窗。 若該視窗未開啟，您可透過選取 [物件總管] > [連線] > [資料庫引擎] 手動加以開啟。

    ![物件總管中的連線連結](media/connect-query-sql-server/connectobjexp.png)

2. 在 [連線至伺服器] 視窗中，執行下列動作： 

    - 針對**伺服器類型**，選取 [資料庫引擎] \(通常為預設選項)。
    - 針對**伺服器名稱**，輸入您 SQL Server 執行個體的名稱。 (本文使用了主機名稱 NODE5 [NODE5\SQL2016ST] 上的執行個體名稱 SQL2016ST)。若您不確定如何判斷 SQL Server 執行個體名稱，請參閱[使用 SSMS 的其他提示與祕訣](ssms-tricks.md#determine-sql-server-name)。  

    ![[伺服器名稱] 欄位與使用 SQL Server 執行個體的選項](media/connect-query-sql-server/connection2.png)

    - 針對**驗證**，請選取 [Windows 驗證]。 本文使用 Windows 驗證，但 SQL Server 登入亦受支援。 若您選取 [SQL 登入]，系統會提示您提供使用者名稱與密碼。 如需有關驗證類型的詳細資訊，請參閱[連線至伺服器 (資料庫引擎)](https://docs.microsoft.com/sql/ssms/f1-help/connect-to-server-database-engine)。

    您也可透過選取 [選項] 修改其他連線設定。 連線選項的範例為您所連線的資料庫、連線逾時值以及網路通訊協定。 本文會為所有選項使用預設值。 

3. 當您填完所有欄位後，請選取 [連線]。 

### <a name="examples-of-successful-connections"></a>成功連線的範例
若要驗證您的 SQL Server 連線成功，請展開並瀏覽 [物件總管] 中的物件。 這些物件會根據您所連線的伺服器類型而有所不同。 

- 連線到內部部署 SQL Server - 在此案例中為 NODE5\SQL2016ST：![連線到內部部署伺服器](media/connect-query-sql-server/connect-on-prem.png)

- 連線到 SQL Azure 資料庫 - 在此案例中為 msftestserver.database.windows.net：![連線到 SQL Azure 資料庫](media/connect-query-sql-server/connect-sql-azure.png)

  >[!NOTE]
  > 在本教學課程中，您之前使用「Windows 驗證」連線到您的內部部署 SQL Server，但 SQL Azure 資料庫不支援這個方法。 因此，此影像顯示使用 SQL 驗證連線到 SQL Azure 資料庫。 如需詳細資訊，請參閱 [SQL 內部部署驗證](../../relational-databases/security/choose-an-authentication-mode.md)和 [SQL Azure 驗證](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview#control-access)。 

## <a name="create-a-database"></a>建立資料庫
請執行下列動作來建立名為 TutorialDB 的資料庫： 

1. 在物件總管中以滑鼠右鍵按一下您的伺服器執行個體，然後選取 [新增查詢]：

   ![新增查詢連結](media/connect-query-sql-server/newquery.png)
   
2. 在查詢視窗中，貼上以下 T-SQL 程式碼片段： 
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
2. 若要執行查詢，請選取 [執行] (或在鍵盤上選取 F5)。 

   ![執行命令](media/connect-query-sql-server/execute.png)
  
    查詢完成後，新的 TutorialDB 資料庫會顯示在物件總管的資料庫清單中。 若其未顯示，請以滑鼠右鍵按一下 [資料庫] 節點，然後選取 [重新整理]。  


## <a name="create-a-table-in-the-new-database"></a>在新的資料庫中建立資料表
在本節中，您會在新建立的 TutorialDB 資料庫中建立資料表。 因為查詢編輯器仍在主要資料庫的內容中，請執行下列步驟將連線內容切換至 *TutorialDB*： 

1. 在資料庫下拉式清單中，選取您想要的資料庫，如此處所示： 

   ![變更資料庫](media/connect-query-sql-server/changedb.png)

2. 在查詢視窗中貼上以下 T-SQL 程式碼片段，然後選取 [執行] (或選取鍵盤上的 F5)。  
   您可以替換查詢視窗中的現有文字，或將其附加至結尾。 若要在查詢視窗中執行所有項目，請選取 [執行]。 若要執行部分文字，請將該部分反白，並選取 [執行]。  
  
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

查詢完成後，新的 [客戶] 資料表會顯示在物件總管的資料表清單中。 若資料表未顯示，請在物件總管中以滑鼠右鍵按一下 [TutorialDB] > [資料表] 節點，然後選取 [重新整理]。

## <a name="insert-rows-into-the-new-table"></a>在新的資料表插入資料列
在您先前建立的 [客戶] 資料表插入一些資料列。 若要這麼做，請在查詢視窗貼上以下 T-SQL 程式碼片段，然後選取 [執行]： 


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

## <a name="query-the-table-and-view-the-results"></a>查詢資料表並檢視結果
查詢結果會顯示在查詢文字視窗下方。 若要查詢 [客戶] 資料表並檢視先前插入的資料列，請執行下列步驟：  

1. 在查詢視窗中貼上以下 T-SQL 程式碼片段，然後選取 [執行]： 

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

    查詢結果會顯示在輸入文字的區域下： 

   ![結果清單](media/connect-query-sql-server/queryresults.png)

2. 您可透過選取下列其中一個選項來修改結果的呈現方式：

     ![三個顯示查詢結果的選項](media/connect-query-sql-server/results.png)

    - 中間的按鈕會在 [格線檢視] 中顯示結果，這是預設選項。 
    - 第一個按鈕會在 [文字檢視] 中顯示結果，如下一節中的影像所示。
    - 第三個按鈕可讓您將結果儲存至檔案，其副檔名預設為 .rpt。

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>您可透過使用查詢視窗資料表來驗證連線屬性
您可以在查詢結果下找到連線屬性的相關資訊。 當您執行在上一個步驟提到的查詢後，請檢閱查詢視窗底部的連線屬性。

- 您可以判斷您所連線的伺服器與資料庫，以及您用來登入的使用者名稱。
- 您也可以檢視上一個執行之查詢所傳回的查詢持續時間與資料列數。

    ![連線內容](media/connect-query-sql-server/connectionproperties.png)
    
    在此影像中，請注意結果會顯示在 [文字檢視] 中。 

## <a name="change-the-server-that-the-query-window-is-connected-to"></a>變更查詢視窗所連線的伺服器
您可以透過執行下列步驟，變更目前查詢視窗所連線的伺服器：

1. 以滑鼠右鍵按一下查詢視窗，然後選取 [連線] > [變更連線]。 [連線至伺服器] 視窗會再次開啟。
2. 變更您查詢所連線的伺服器。 
 
   ![變更連線命令](media/connect-query-sql-server/changeconnection.png)

    > [!NOTE]
    > 此動作只會變更查詢視窗所連線的伺服器，而不會變更物件總管所連線的伺服器。 

## <a name="next-steps"></a>後續步驟
下一篇文章會教您如何在 SQL Server Management Studio 中，撰寫不同物件的指令碼。 

請前往下一篇文章以深入了解：
> [!div class="nextstepaction"]
> [後續步驟](scripting-ssms.md)


