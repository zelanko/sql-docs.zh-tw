---
title: 建立資料表 (教學課程) | Microsoft Docs
ms.custom: ''
ms.date: 04/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- creating tables
ms.assetid: 653f2dd3-36a2-4bd5-8703-71a57d244661
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8a835c6da700059a15b782a9dd08cf6beabb37cd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-1-2---creating-a-table"></a>課程 1-2 - 建立資料表
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

若要建立資料表，您必須提供資料表的名稱，以及資料表中各資料行的名稱和資料類型， 最好也能指出各資料行中是否允許有 Null 值。 若要建立資料表，您必須擁有 `CREATE TABLE` 權限，以及將包含資料表之結構描述的 `ALTER SCHEMA` 權限。 `db_ddladmin` 固定資料庫角色擁有這些權限。  
  
大多數資料表都具有由資料表中一或多個資料行組成的主索引鍵。 主索引鍵一定是唯一的。 [!INCLUDE[ssDE](../includes/ssde-md.md)] 會強制限制資料表中的所有主索引鍵值都不能重複。  
  
如需資料類型以及各資料類型之描述連結的清單，請參閱[資料類型 &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md)。  
  
> [!NOTE]  
> [!INCLUDE[ssDE](../includes/ssde-md.md)] 可以安裝為區分大小寫或不區分大小寫。 如果將 [!INCLUDE[ssDE](../includes/ssde-md.md)] 安裝為區分大小寫，則物件名稱的大小寫一定要完全相同。 例如，名稱為 OrderData 的資料表與名稱為 ORDERDATA 的資料表會代表不同的資料表。 如果將 [!INCLUDE[ssDE](../includes/ssde-md.md)] 安裝為不區分大小寫，則會將這兩個資料表名稱視為代表同一個資料表，而且該名稱只能使用一次。  
  
### <a name="to-create-a-database-to-contain-the-new-table"></a>若要建立包含新資料表的資料庫  
  
-   將下列程式碼輸入 [查詢編輯器] 視窗中。  
  
    ```  
    USE master;  
    GO  
  
    --Delete the TestData database if it exists.  
    IF EXISTS(SELECT * from sys.databases WHERE name='TestData')  
    BEGIN  
        DROP DATABASE TestData;  
    END  
  
    --Create a new database called TestData.  
    CREATE DATABASE TestData;  
    Press the F5 key to execute the code and create the database.  
    ```  
  
### <a name="switch-the-query-editor-connection-to-the-testdata-database"></a>將查詢編輯器連接切換到 TestData 資料庫  
  
-   在 [查詢編輯器] 視窗中，輸入並執行下列程式碼，將連接變更為 `TestData` 資料庫。  
  
    ```  
    USE TestData  
    GO  
    ```  
  
### <a name="to-create-a-table"></a>若要建立資料表  
  
-   在 [查詢編輯器] 視窗中，輸入並執行下列程式碼，建立名稱為 `Products`的簡單資料表。 此資料表中的資料行名稱分別為 `ProductID`、 `ProductName`、 `Price`和 `ProductDescription`。 `ProductID` 資料行是此資料表的主索引鍵。 `int`、 `varchar(25)`、 `money`和 `text` 全部都是資料類型。 在插入或變更資料列時，只有 `Price` 和 `ProductionDescription` 資料行可以不含任何資料。 這個陳述式包含一個選擇性的元素 (`dbo.`)，稱為「結構描述」。 結構描述就是擁有資料表的資料庫物件。 如果您是系統管理員，則 `dbo` 是預設的結構描述。 `dbo` 代表資料庫擁有者。  
  
    ```  
    CREATE TABLE dbo.Products  
       (ProductID int PRIMARY KEY NOT NULL,  
        ProductName varchar(25) NOT NULL,  
        Price money NULL,  
        ProductDescription text NULL)  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[在資料表中插入及更新資料 &#40;教學課程&#41;](../t-sql/lesson-1-3-inserting-and-updating-data-in-a-table.md)  
  
## <a name="see-also"></a>另請參閱  
[CREATE TABLE &#40;Transact-SQL&#41;](../t-sql/statements/create-table-transact-sql.md)  
  
  
  

