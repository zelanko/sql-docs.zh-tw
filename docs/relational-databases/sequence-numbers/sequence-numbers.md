---
title: 序號 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- sequence number object, overview
- sequence [Database Engine]
- autonumbers, sequences
- sequence numbers [SQL Server]
- sequence number object
ms.assetid: c900e30d-2fd3-4d5f-98ee-7832f37e79d1
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b5198b8919fb41c754d5d94ac45c895dda852e2e
ms.sourcegitcommit: 630f7cacdc16368735ec1d955b76d6d030091097
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2019
ms.locfileid: "67343843"
---
# <a name="sequence-numbers"></a>序號
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  序列是使用者定義的結構描述繫結物件，該物件會根據建立順序所使用的規格產生數值序列。 數值序列是在定義的間隔依照遞增或遞減順序來產生，而且可依照要求循環 (重複)。 與識別欄位不同的是，順序不會與資料表產生關聯。 應用程式會參考順序物件，以擷取它的下一個值。 順序與資料表之間的關聯性是由應用程式所控制。 使用者應用程式可以參考順序物件，並協調跨越多個資料列和資料表的值索引鍵。  
  
 順序是使用 **CREATE SEQUENCE** 陳述式所建立，與資料表無關。 有一些選項可讓您控制遞增、最大和最小值、起點、自動重新啟動功能與快取以改善效能。 如需有關這些選項的詳細資訊，請參閱 [CREATE SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md)。  
  
 不同於插入資料列時產生的識別欄位值，應用程式可以藉由呼叫 [NEXT VALUE FOR](../../t-sql/functions/next-value-for-transact-sql.md) 函數，在插入資料列之前取得下一個序號。 此序號是在呼叫 NEXT VALUE FOR 時配置的，即使該編號從未插入資料表也一樣。 NEXT VALUE FOR 函數可當做資料表定義中資料行的預設值使用。 您可以使用 [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) 一次取得多個序號範圍。  
  
 順序可以定義為任何整數資料類型。 如果沒有指定資料類型，順序就會預設為 **bigint**。  
  
## <a name="using-sequences"></a>使用順序  
 在下列案例中，您可以使用順序來取代識別欄位：  
  
-   進行插入資料表的作業之前，應用程式需要一個編號。  
  
-   應用程式需要在多個資料表或資料表中多個資料行之間共用單一編號序列。  
  
-   達到指定的編號時，應用程式必須重新啟動編號序列。 例如，指派 1 到 10 的值之後，應用程式就會再次開始指派 1 到 10 的值。  
  
-   應用程式要求依照另一個欄位排序順序值。 NEXT VALUE FOR 函數可以將 OVER 子句套用至函數呼叫。 OVER 子句會確保傳回的值都按照 OVER 子句之 ORDER BY 子句的順序來產生。  
  
-   應用程式要求同時指派多個編號。 例如，應用程式需要保留五個序號。 如果同時針對其他處理序發出編號，要求識別值可能會在序列中產生間距。 呼叫 sp_sequence_get_range 可以一次擷取順序中的許多編號。  
  
-   您必須變更順序的規格，例如遞增值。  
  
## <a name="limitations"></a>限制  
 不同於無法變更其值的識別欄位，當順序值插入資料表之後，並不會自動受保護。 若要防止順序值變更，請在資料表上使用更新觸發程序來回復變更。  
  
 系統不會針對順序值自動強制執行唯一性。 重複使用順序值的能力是依照設計提供的。 如果資料表中的順序值都必須是唯一的，請針對資料行建立唯一索引。 如果資料表中的順序值在整個資料表群組中必須是唯一的，請建立觸發程序來防止更新陳述式或序號循環所導致的重複項目。  
  
 雖然順序物件會根據其定義產生編號，不過順序物件不會控制編號的使用方式。 當您回復交易時、當多個資料表共用順序物件時，或者當您配置序號而沒有將它們用於資料表時，插入資料表中的序號可能會產生間距。 以 CACHE 選項建立時，非預期關閉 (例如停電) 可能會失去快取中的序號。  
  
 如果單一 **陳述式具有多個指定相同順序產生器的** NEXT VALUE FOR [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數執行個體，所有執行個體都會針對該 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式所處理的給定資料列傳回相同的值。 這種行為與 ANSI 標準一致。  
 
 序號是在目前交易範圍之外產生的。 無論使用序號的交易被認可或回復交易，都會耗用序號。 只有在填完記錄之後才會出現重複驗證。 這會導致在某些情況下，同一個數字會在建立期間用於多筆記錄，但會識別為重複項目。 如果發生這種情況，而且已將其他自動編號值套用至後續記錄，這會導致自動編號值之間出現間距。
  
## <a name="typical-use"></a>一般用法  
 若要建立從 -2,147,483,648 到 2,147,483,647 且遞增量為 1 的整數序號，請使用下列陳述式。  
  
```  
CREATE SEQUENCE Schema.SequenceName  
    AS int  
    INCREMENT BY 1 ;  
```  
  
 若要建立從 1 到 2,147,483,647 且遞增量為 1 的整數序號 (類似於識別欄位)，請使用下列陳述式。  
  
```  
CREATE SEQUENCE Schema.SequenceName  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
  
```  
  
## <a name="managing-sequences"></a>管理順序  
 如需有關順序的詳細資訊，請查詢 [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)、[NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md) 和 [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) 主題中有其他範例。  
  
### <a name="a-using-a-sequence-number-in-a-single-table"></a>A. 在單一資料表中使用序號  
 下列範例會建立名為 Test 的結構描述、名為 Orders 的資料表，以及名為 CountBy1 的順序，然後使用 NEXT VALUE FOR 函數，將資料列插入資料表。  
  
```  
--Create the Test schema  
CREATE SCHEMA Test ;  
GO  
  
-- Create a table  
CREATE TABLE Test.Orders  
    (OrderID int PRIMARY KEY,  
    Name varchar(20) NOT NULL,  
    Qty int NOT NULL);  
GO  
  
-- Create a sequence  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
-- Insert three records  
INSERT Test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Tire', 2) ;  
INSERT test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Seat', 1) ;  
INSERT test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Brake', 1) ;  
GO  
  
-- View the table  
SELECT * FROM Test.Orders ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `OrderID  Name    Qty`  
  
 `1        Tire    2`  
  
 `2        Seat    1`  
  
 `3        Brake   1`  
  
### <a name="b-calling-next-value-for-before-inserting-a-row"></a>B. 在插入資料列之前呼叫 NEXT VALUE FOR  
 下列範例會使用在範例 A 中建立的 `Orders` 資料表來宣告名為 `@nextID`的變數，然後使用 NEXT VALUE FOR 函數，將此變數設定為下一個可用的序號。 應用程式應該會針對訂單進行一些處理，例如為客戶提供其潛在訂單的 `OrderID` 編號，然後驗證訂單。 不論這項處理可能需要多少時間，或者在處理期間加入其他多少訂單，原始的編號都會保留給這個連接使用。 最後， `INSERT` 陳述式會將訂單加入至 `Orders` 資料表。  
  
```  
DECLARE @NextID int ;  
SET @NextID = NEXT VALUE FOR Test.CountBy1;  
-- Some work happens  
INSERT Test.Orders (OrderID, Name, Qty)  
    VALUES (@NextID, 'Rim', 2) ;  
GO  
  
```  
  
### <a name="c-using-a-sequence-number-in-multiple-tables"></a>C. 在多個資料表中使用序號  
 這個範例會假設生產線監視處理序接收整個工廠所發生之事件的通知。 每個事件都會接收唯一且單純遞增的 `EventID` 編號。 所有事件都會使用相同的 `EventID` 序號，讓結合所有事件的報表能夠唯一識別每個事件。 不過，事件資料會根據事件的類型儲存在三個不同的資料表中。 此程式碼範例會建立名為 `Audit`的結構描述、名為 `EventCounter`的順序，以及三個資料表，而且每個資料表都使用 `EventCounter` 順序作為預設值。 然後，此範例會將資料列加入至三個資料表並查詢結果。  
  
```  
CREATE SCHEMA Audit ;  
GO  
CREATE SEQUENCE Audit.EventCounter  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
CREATE TABLE Audit.ProcessEvents  
(  
    EventID int PRIMARY KEY CLUSTERED   
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EventCode nvarchar(5) NOT NULL,  
    Description nvarchar(300) NULL  
) ;  
GO  
  
CREATE TABLE Audit.ErrorEvents  
(  
    EventID int PRIMARY KEY CLUSTERED  
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EquipmentID int NULL,  
    ErrorNumber int NOT NULL,  
    EventDesc nvarchar(256) NULL  
) ;  
GO  
  
CREATE TABLE Audit.StartStopEvents  
(  
    EventID int PRIMARY KEY CLUSTERED  
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EquipmentID int NOT NULL,  
    StartOrStop bit NOT NULL  
) ;  
GO  
  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (248, 0) ;  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (72, 0) ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (2735,   
    'Clean room temperature 18 degrees C.') ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (18, 'Spin rate threashold exceeded.') ;  
INSERT Audit.ErrorEvents (EquipmentID, ErrorNumber, EventDesc)   
    VALUES (248, 82, 'Feeder jam') ;  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (248, 1) ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (1841, 'Central feed in bypass mode.') ;  
-- The following statement combines all events, though not all fields.  
SELECT EventID, EventTime, Description FROM Audit.ProcessEvents   
UNION SELECT EventID, EventTime, EventDesc FROM Audit.ErrorEvents   
UNION SELECT EventID, EventTime,   
CASE StartOrStop   
    WHEN 0 THEN 'Start'   
    ELSE 'Stop'  
END   
FROM Audit.StartStopEvents  
ORDER BY EventID ;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `EventID  EventTime                Description`  
  
 `1        2009-11-02 15:00:51.157  Start`  
  
 `2        2009-11-02 15:00:51.160  Start`  
  
 `3        2009-11-02 15:00:51.167  Clean room temperature 18 degrees C.`  
  
 `4        2009-11-02 15:00:51.167  Spin rate threshold exceeded.`  
  
 `5        2009-11-02 15:00:51.173  Feeder jam`  
  
 `6        2009-11-02 15:00:51.177  Stop`  
  
 `7        2009-11-02 15:00:51.180  Central feed in bypass mode.`  
  
### <a name="d-generating-repeating-sequence-numbers-in-a-result-set"></a>D. 在結果集中產生重複的序號  
 下列範例會示範序號的兩種功能：循環以及在 SELECT 陳述式中使用 `NEXT VALUE FOR` 。  
  
```  
CREATE SEQUENCE CountBy5  
   AS tinyint  
    START WITH 1  
    INCREMENT BY 1  
    MINVALUE 1  
    MAXVALUE 5  
    CYCLE ;  
GO  
  
SELECT NEXT VALUE FOR CountBy5 AS SurveyGroup, Name FROM sys.objects ;  
GO  
```  
  
### <a name="e-generating-sequence-numbers-for-a-result-set-by-using-the-over-clause"></a>E. 使用 OVER 子句來產生結果集的序號  
 下列範例會使用 `OVER` 子句並依照 `Name` 排序結果集，然後再加入序號資料行。  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Samples ;  
GO  
  
CREATE SEQUENCE Samples.IDLabel  
    AS tinyint  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
### <a name="f-resetting-the-sequence-number"></a>F. 重設序號  
 範例 E 取用了前 79 個 `Samples.IDLabel` 序號 (您的 `AdventureWorks2012` 版本可能會傳回不同的結果數目)。請執行下列陳述式來取用後續 79 個序號 (80 到 158)。  
  
```  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
 請執行下列陳述式來重新啟動 `Samples.IDLabel` 順序。  
  
```  
ALTER SEQUENCE Samples.IDLabel  
RESTART WITH 1 ;  
```  
  
 請再次執行 SELECT 陳述式，以便確認 `Samples.IDLabel` 順序從編號 1 重新啟動。  
  
```  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
### <a name="g-changing-a-table-from-identity-to-sequence"></a>G. 將資料表從識別變更為順序  
 下列範例會建立結構描述以及包含範例中三個資料列的資料表。 然後，此範例會加入新的資料行並卸除舊的資料行。  
  
```  
-- Create a schema  
CREATE SCHEMA Test ;  
GO  
  
-- Create a table  
CREATE TABLE Test.Department  
    (  
        DepartmentID smallint IDENTITY(1,1) NOT NULL,  
        Name nvarchar(100) NOT NULL,  
        GroupName nvarchar(100) NOT NULL  
    CONSTRAINT PK_Department_DepartmentID PRIMARY KEY CLUSTERED   
         (DepartmentID ASC)   
    ) ;  
GO  
  
-- Insert three rows into the table  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Engineering', 'Research and Development');  
GO  
  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Tool Design', 'Research and Development');  
GO  
  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Sales', 'Sales and Marketing');  
GO  
  
-- View the table that will be changed  
SELECT * FROM Test.Department ;  
GO  
  
-- End of portion creating a sample table  
--------------------------------------------------------  
-- Add the new column that does not have the IDENTITY property  
ALTER TABLE Test.Department   
    ADD DepartmentIDNew smallint NULL  
GO  
  
-- Copy values from the old column to the new column  
UPDATE Test.Department  
    SET DepartmentIDNew = DepartmentID ;  
GO  
  
-- Drop the primary key constraint on the old column  
ALTER TABLE Test.Department  
    DROP CONSTRAINT [PK_Department_DepartmentID];  
-- Drop the old column  
ALTER TABLE Test.Department  
    DROP COLUMN DepartmentID ;  
GO  
  
-- Rename the new column to the old columns name  
EXEC sp_rename 'Test.Department.DepartmentIDNew',   
    'DepartmentID', 'COLUMN';  
GO  
  
-- Change the new column to NOT NULL  
ALTER TABLE Test.Department  
    ALTER COLUMN DepartmentID smallint NOT NULL ;  
-- Add the unique primary key constraint  
ALTER TABLE Test.Department  
    ADD CONSTRAINT PK_Department_DepartmentID PRIMARY KEY CLUSTERED   
         (DepartmentID ASC) ;  
-- Get the highest current value from the DepartmentID column   
-- and create a sequence to use with the column. (Returns 3.)  
SELECT MAX(DepartmentID) FROM Test.Department ;  
-- Use the next desired value (4) as the START WITH VALUE;  
CREATE SEQUENCE Test.DeptSeq  
    AS smallint  
    START WITH 4  
    INCREMENT BY 1 ;  
GO  
  
-- Add a default value for the DepartmentID column  
ALTER TABLE Test.Department  
    ADD CONSTRAINT DefSequence DEFAULT (NEXT VALUE FOR Test.DeptSeq)   
        FOR DepartmentID;  
GO  
  
-- View the result  
SELECT DepartmentID, Name, GroupName  
FROM Test.Department ;   
-- Test insert  
INSERT Test.Department (Name, GroupName)  
    VALUES ('Audit', 'Quality Assurance') ;  
GO  
  
-- View the result  
SELECT DepartmentID, Name, GroupName  
FROM Test.Department ;  
GO  
  
```  
  
 使用 `SELECT *` 的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式將收到新的資料行做為最後一個資料行，而非第一個資料行。 如果這是無法接受的資料行，您就必須建立全新的資料表、將資料移入其中，然後重新建立新資料表的權限。  
  
## <a name="related-content"></a>相關內容  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)  
  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)  
  
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)  
  
 [IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
  
  
