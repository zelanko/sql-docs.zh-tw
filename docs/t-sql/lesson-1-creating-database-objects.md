---
title: T-SQL 教學課程：建立及查詢資料庫物件 | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 9fb8656b-0e4e-4ada-b404-4db4d3eea995
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aa027f58bd673539dd09f118ea1b9433c42c7990
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000270"
---
# <a name="lesson-1-create-and-query-database-objects"></a>第 1 課：建立及查詢資料庫物件
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

這一課會示範如何建立資料庫、在資料庫中建立資料表，然後在資料表中存取和變更資料。 因為這一課是使用 [!INCLUDE[tsql](../includes/tsql-md.md)]的簡介，所以並不會使用或描述這些陳述式所能使用的許多選項。  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] 撰寫陳述式並且提交給 [!INCLUDE[ssDE](../includes/ssde-md.md)] 可以採用下列方式：  
  
-   使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。 這個教學課程會假設您使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]，但是您也可以使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] Express，這個版本可以從 [Microsoft 下載中心](https://go.microsoft.com/fwlink/?linkid=67359)免費下載。  
  
-   使用 [sqlcmd 公用程式](../tools/sqlcmd-utility.md)。  
  
-   從您建立的應用程式連接。  
  
不論您提交程式碼陳述式的方式為何，這個程式碼在 [!INCLUDE[ssDE](../includes/ssde-md.md)] 上都會以相同的方式和相同的權限來執行。  
  
若要在 [!INCLUDE[tsql](../includes/tsql-md.md)] 中執行 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]陳述式，請開啟 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 並且連接到 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]的執行個體。  

## <a name="prerequisites"></a>Prerequisites
若要完成本教學課程，您需要 SQL Server Management Studio 和 SQL Server 執行個體存取權。 

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

若您沒有 SQL Server 執行個體存取權，請從下列連結選取您的平台。 若您選擇 SQL 驗證，請使用您的 SQL Server 登入認證。
- **Windows**：[下載 SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- **macOS**：[下載 Docker 上的 SQL Server 2017](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)。

## <a name="create-a-database"></a>建立資料庫
和許多 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式一樣，CREATE DATABASE 陳述式也有一個必要參數，那就是資料庫的名稱。 CREATE DATABASE 另外還有許多選擇性參數，例如，要用來放置資料庫檔案的磁碟位置。 當您執行 CREATE DATABASE 但未指定任何選擇性參數時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 多半會使用這些參數的預設值。 這個教學課程使用的選擇性語法參數非常少。   

1.  在 [查詢編輯器] 視窗中，輸入下列程式碼 (但不要執行)：  
  
    ```sql  
    CREATE DATABASE TestData  
    GO  
    ```  
  
2.  使用指標選取 `CREATE DATABASE`這兩個字，然後按 **F1**鍵。 這時應該會開啟《SQL Server 線上叢書》中的＜CREATE DATABASE＞主題。 您可以利用這種方式找到 CREATE DATABASE 以及在這個教學課程中所使用之其他陳述式的完整語法。  
  
3.  在 [查詢編輯器] 中按 **F5** ，執行陳述式並建立名為 `TestData`的資料庫。  
  
當您建立資料庫時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會建立 **model** 資料庫的複本，並且將此複本重新命名為資料庫的名稱。 除非您在選擇性參數中指定了非常大的資料庫初始大小，否則這項作業應該只需要幾秒鐘的時間。  
  
> [!NOTE]  
> 如果在單一批次中提交了一個以上的陳述式，可用關鍵字 GO 來分隔陳述式； 如果批次中只包含一個陳述式，則 GO 可有可無。  

## <a name="create-a-table"></a>建立資料表
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

若要建立資料表，您必須提供資料表的名稱，以及資料表中各資料行的名稱和資料類型， 最好也能指出各資料行中是否允許有 Null 值。 若要建立資料表，您必須擁有 `CREATE TABLE` 權限，以及將包含資料表之結構描述的 `ALTER SCHEMA` 權限。 [`db_ddladmin`](../relational-databases/security/authentication-access/database-level-roles.md) 固定資料庫角色擁有這些權限。  
  
大多數資料表都具有由資料表中一或多個資料行組成的主索引鍵。 主索引鍵一定是唯一的。 [!INCLUDE[ssDE](../includes/ssde-md.md)] 會強制限制資料表中的所有主索引鍵值都不能重複。  
  
如需資料類型以及各資料類型之描述連結的清單，請參閱[資料類型 &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md)。  
  
> [!NOTE]  
> [!INCLUDE[ssDE](../includes/ssde-md.md)] 可以安裝為區分大小寫或不區分大小寫。 如果將 [!INCLUDE[ssDE](../includes/ssde-md.md)] 安裝為區分大小寫，則物件名稱的大小寫一定要完全相同。 例如，名稱為 OrderData 的資料表與名稱為 ORDERDATA 的資料表會代表不同的資料表。 如果將 [!INCLUDE[ssDE](../includes/ssde-md.md)] 安裝為不區分大小寫，則會將這兩個資料表名稱視為代表同一個資料表，而且該名稱只能使用一次。  
  
  
### <a name="switch-the-query-editor-connection-to-the-testdata-database"></a>將查詢編輯器連接切換到 TestData 資料庫  
在 [查詢編輯器] 視窗中，輸入並執行下列程式碼，將連接變更為 `TestData` 資料庫。  
  
  ```sql  
  USE TestData  
  GO  
  ```  
  
### <a name="create-the-table"></a>建立資料表
在 [查詢編輯器] 視窗中，輸入並執行下列程式碼，建立名稱為 `Products`的簡單資料表。 此資料表中的資料行名稱分別為 `ProductID`、 `ProductName`、 `Price`和 `ProductDescription`。 `ProductID` 資料行是此資料表的主索引鍵。 `int`、 `varchar(25)`、 `money`和 `text` 全部都是資料類型。 在插入或變更資料列時，只有 `Price` 和 `ProductionDescription` 資料行可以不含任何資料。 這個陳述式包含一個選擇性的元素 (`dbo.`)，稱為「結構描述」。 結構描述就是擁有資料表的資料庫物件。 如果您是系統管理員，則 `dbo` 是預設的結構描述。 `dbo` 代表資料庫擁有者。  
  
  ```sql  
  CREATE TABLE dbo.Products  
     (ProductID int PRIMARY KEY NOT NULL,  
     ProductName varchar(25) NOT NULL,  
     Price money NULL,  
     ProductDescription text NULL)  
  GO  
 ```  

## <a name="insert-and-update-data-in-a-table"></a>在資料表中插入及更新資料
既然您現在建立好 **Products** 資料表，就可以準備使用 INSERT 陳述式，將資料插入資料表。 在插入資料後，您將使用 UPDATE 陳述式來變更資料列的內容。 您將使用 UPDATE 陳述式的 WHERE 子句，限制對單一資料列進行更新。 接下來所述的四個陳述式將輸入下面資料。  
  
|ProductID|ProductName|Price|ProductDescription|  
|-------------|---------------|---------|----------------------|  
|1|Clamp|12.48|Workbench clamp|  
|50|Screwdriver|3.17|Flat head|  
|75|Tire Bar||Tool for changing tires.|  
|3000|3mm Bracket|.52||  
  
基本語法如下：INSERT、資料表、資料行清單、VALUES，以及要插入的值清單。 程式行前面的兩個連字號表示該程式行是註解，而編譯器會忽略這行文字。 在本案例中，註解說明所允許的語法變化。  
  
### <a name="insert-data-into-a-table"></a>將資料插入資料表中  
  
1.  執行下列陳述式，將資料列插入上一項工作中建立的 `Products` 資料表。 以下是基本語法。  
  
   ```sql 
   -- Standard syntax  
   INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
       VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
   GO   
   ```  
  
2.  下列陳述式示範如何可以在透過切換欄位清單 (括號內) 和值清單內 `ProductID` 和 `ProductName` 的位置所提供的參數中變更順序。  
  
   ```sql  
   -- Changing the order of the columns  
   INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
       VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
   GO    
   ```  
  
3.  下列陳述式示範只要依照正確的順序列出值，就可以省略資料行的名稱。 這是常見的語法，但不建議您使用，因為其他使用者可能會很難了解您的程式碼。 `NULL` 已針對 `Price` 資料行指定，這是因為此產品的價格不明。  
  
   ```sql  
   -- Skipping the column list, but keeping the values in order  
   INSERT dbo.Products  
       VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
   GO  
  ```  
  
4.  只要是在預設的結構描述中存取及變更資料表，就可以省略結構描述名稱。 因為 `ProductDescription` 資料行可以接受 Null 值及無值，所以在陳述式中便可以完全省略 `ProductDescription` 資料行名稱和值。  
  
   ```sql  
   -- Dropping the optional dbo and dropping the ProductDescription column  
   INSERT Products (ProductID, ProductName, Price)  
       VALUES (3000, '3mm Bracket', .52)  
   GO  
   ```  
  
### <a name="update-the-products-table"></a>更新產品資料表  
輸入並執行下列 `UPDATE` 陳述式，將第二個產品的 `ProductName` 從 `Screwdriver`變更為 `Flat Head Screwdriver`。  
  
  ```sql  
  UPDATE dbo.Products  
      SET ProductName = 'Flat Head Screwdriver'  
      WHERE ProductID = 50  
  GO  
  ```  

## <a name="read-data-from-a-table"></a>從資料表讀取資料
使用 SELECT 陳述式來讀取資料表的資料。 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式中最重要的其中一個陳述式就是 SELECT 陳述式，而其中有很多的語法變化。 在本教學課程中，您將使用五種簡單的變化樣式。  
  
### <a name="read-the-data-in-a-table"></a>讀取資料表的資料  
  
1.  輸入並執行下列陳述式，以讀取 `Products` 資料表的資料。  
  
  ```sql 
  -- The basic syntax for reading data from a single table  
  SELECT ProductID, ProductName, Price, ProductDescription  
      FROM dbo.Products  
  GO  
  ```  
  
2.  您可以使用星號，選取資料表中的所有資料行。 這個方法常在隨選查詢中使用。 您應該在固定程式碼中提供資料行清單，使陳述式會傳回預期的資料行，即使以後加入新資料行還是一樣。  
  
  ```sql  
  -- Returns all columns in the table  
  -- Does not use the optional schema, dbo  
  SELECT * FROM Products  
  GO   
  ```  
  
3.  您可以省略不要傳回的資料行。 而且會以資料行所列出的順序來傳回資料行。  
  
  ```sql  
  -- Returns only two of the columns from the table  
  SELECT ProductName, Price  
      FROM dbo.Products  
  GO    
  ```  
  
4.  使用 `WHERE` 子句，限制要傳回給使用者的資料列。  
  
  ``` sql 
  -- Returns only two of the records in the table  
  SELECT ProductID, ProductName, Price, ProductDescription  
      FROM dbo.Products  
      WHERE ProductID < 60  
  GO    
  ```  
  
5.  您可以處理資料行中所傳回的值。 下列範例會在 `Price` 資料行上進行數學運算。 除非使用 `AS` 關鍵字提供名稱，否則以這種方式變更的資料行將不會有名稱。  
  
  ```sql  
  -- Returns ProductName and the Price including a 7% tax  
  -- Provides the name CustomerPays for the calculated column  
  SELECT ProductName, Price * 1.07 AS CustomerPays  
      FROM dbo.Products  
  GO  
  ```  
  
### <a name="useful-functions-in-a-select-statement"></a>SELECT 陳述式中的實用函數  
如需有關某些可在 SELECT 陳述式中用來處理資料之函數的詳細資訊，請參閱下列主題：  
  
|||  
|-|-|  
|[字串函數 &#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md)|[日期和時間資料類型與函數 &#40;Transact-SQL&#41;](../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)|  
|[數學函數 &#40;Transact-SQL&#41;](../t-sql/functions/mathematical-functions-transact-sql.md)|[Text 和 Image 函數 &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|  

## <a name="create-views-and-stored-procedures"></a>建立檢視和預存程序
檢視是預存的 SELECT 陳述式，而預存程序是一個或多個批次執行的 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式。  
  
檢視的查詢方式就跟資料表一樣，而且不接受參數。 預存程序就比檢視還要複雜。 預存程序能有輸出和輸入參數，而且還能包含控制程式碼流程的陳述式，如 IF 和 WHILE 陳述式。 對於所有在資料庫中的重複動作，使用預存程序是一個不錯的程式設計方法。  
  
例如，您將使用 CREATE VIEW 建立檢視，其中只選取 **Products** 資料表中的兩個資料行。 接著，您將使用 CREATE PROCEDURE 建立預存程序，其中接受 price 參數並只傳回成本小於指定參數值的產品。  
  
### <a name="create-a-view"></a>建立檢視  
  
執行下列陳述式建立簡單的檢視，其中會執行 SELECT 陳述式並將產品名稱及價格傳回給使用者。  
  
  ```sql  
  CREATE VIEW vw_Names  
     AS  
     SELECT ProductName, Price FROM Products;  
  GO    
  ```  
  
### <a name="test-the-view"></a>測試檢視  
  
檢視的處理方式和資料表一樣。 使用 `SELECT` 陳述式存取檢視。  
  
  ```sql  
  SELECT * FROM vw_Names;  
  GO   
  ```  
  
### <a name="create-a-stored-procedure"></a>建立預存程序  
  
下列陳述式會建立預存程序名稱 `pr_Names`，接受資料類型為 `@VarPrice` 的輸入參數 (名稱是 `money`)。 預存程序會列印與輸出參數串連的 `Products less than` 陳述式，而這個輸出參數會從 `money` 資料類型變更為 `varchar(10)` 字元資料類型。 然後，預存程序會執行檢視上的 `SELECT` 陳述式，將輸出參數當做 `WHERE` 子句的一部分進行傳遞。 這樣會傳回成本小於輸出參數值的所有產品。  
  
  ```sql  
  CREATE PROCEDURE pr_Names @VarPrice money  
     AS  
     BEGIN  
        -- The print statement returns text to the user  
        PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
        -- A second statement starts here  
        SELECT ProductName, Price FROM vw_Names  
              WHERE Price < @varPrice;  
     END  
  GO    
  ```  
  
### <a name="test-the-stored-procedure"></a>測試預存程序  
  
若要測試預存程序，請輸入並執行下列陳述式。 這個程序應該傳回兩個成本小於 `Products` 的產品名稱，這兩個產品是在第 1 課輸入 `10.00`資料表而來的。  
  
  ```sql  
  EXECUTE pr_Names 10.00;  
  GO  
  ```  

## <a name="next-steps"></a>後續步驟
下一篇文章會教您如何設定資料庫物件的權限。 在課程 1 中建立的物件也會用於課程 2。 

請前往下一篇文章以深入了解：
> [!div class="nextstepaction"]
> [後續步驟](../t-sql/lesson-2-configuring-permissions-on-database-objects.md)
  
  
  
