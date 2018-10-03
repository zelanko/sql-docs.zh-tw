---
title: 使用 EVENTDATA 函式 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- EVENTDATA function
- DDL triggers, EVENTDATA function
ms.assetid: 675b8320-9c73-4526-bd2f-91ba42c1b604
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 184e6a3354069ae5a1ed0d6b7557f4b0ac3fa716
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222648"
---
# <a name="use-the-eventdata-function"></a>使用 EVENTDATA 函數
  使用 EVENTDATA 函數擷取引發 DDL 觸發程序之事件的相關資訊。 此函數會傳回 `xml` 值。 XML 結構描述包括有關下列項目的資訊：  
  
-   事件的時間。  
  
-   執行觸發程序時連接的系統處理序識別碼 (SPID)。  
  
-   引發觸發程序的事件類型。  
  
 視事件類型而定，結構描述會包括其他資訊，例如發生事件的資料庫、發生事件的物件以及事件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 如需詳細資訊，請參閱 [DDL 觸發程序](ddl-triggers.md)。  
  
 例如，下列 DDL 觸發程序是在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫中建立：  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
```  
  
 接著會執行下列 `CREATE TABLE` 陳述式：  
  
 `CREATE TABLE NewTable (Column1 int);`  
  
 DDL 觸發程序中的 `EVENTDATA()` 陳述式，會擷取到不容許的 `CREATE TABLE` 陳述式文字。 做法是使用 XQuery 陳述`xml`產生的 EVENTDATA 和擷取資料\<CommandText > 項目。 如需詳細資訊，請參閱 [XQuery 語言參考 &#40;SQL Server&#41;](/sql/xquery/xquery-language-reference-sql-server)。  
  
> [!CAUTION]  
>  EVENTDATA 會擷取 CREATE_SCHEMA 事件的資料，以及對應之 CREATE SCHEMA 定義的 <schema_element> (如果有的話)。 此外，EVENTDATA 還會將 <schema_element> 定義識別為個別事件。 因此，在 CREATE_SCHEMA 事件和 CREATE SCHEMA 定義之 <schema_element> 代表的事件上建立的 DDL 觸發程序，可能會傳回相同的事件資料兩次，例如 `TSQLCommand` 資料。 例如，假設在 CREATE_SCHEMA 和 CREATE_TABLE 兩個事件上建立 DDL 觸發程序，並執行下列批次：  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  如果應用程式擷取 CREATE_TABLE 事件的 `TSQLCommand` 資料，請注意這項資料可能會出現兩次：一次是在發生 CREATE_SCHEMA 事件時，另一次則是在發生 CREATE_TABLE 事件時。 請避免同時在 CREATE_SCHEMA 事件和任何對應之 CREATE SCHEMA 定義的 <schema_element> 文字上建立 DDL 觸發程序，或在應用程式中建立邏輯，使應用程式不會重複處理相同的事件。  
  
## <a name="alter-table-and-alter-database-events"></a>ALTER TABLE 和 ALTER DATABASE 事件  
 ALTER_TABLE 和 ALTER_DATABASE 事件的事件資料也包含受到 DDL 陳述式所影響之其他物件的名稱和類型，以及在這些物件上執行的動作。 ALTER_TABLE 事件資料包含受到 ALTER TABLE 陳述式所影響之資料行、條件約束或觸發程序的名稱，以及在這些受影響物件上執行的動作 (建立、更改、卸除、啟用或停用)。 ALTER_DATABASE 事件資料包含受到 ALTER DATABASE 陳述式所影響之任何檔案或檔案群組的名稱，以及在這些受影響物件上執行的動作 (建立、更改或卸除)。  
  
 例如，您可以在 AdventureWorks 範例資料庫中建立下列 DDL 觸發程序：  
  
```  
CREATE TRIGGER ColumnChanges  
ON DATABASE   
FOR ALTER_TABLE  
AS  
-- Detect whether a column was created/altered/dropped.  
SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]', 'nvarchar(max)')  
RAISERROR ('Table schema cannot be modified in this database.', 16, 1);  
ROLLBACK;  
```  
  
 然後，執行下列違反條件約束的 ALTER TABLE 陳述式：  
  
```  
ALTER TABLE Person.Address ALTER COLUMN ModifiedDate date;   
```  
  
 DDL 觸發程序中的 EVENTDATA() 陳述式會擷取不允許的 `ALTER TABLE` 陳述式文字。  
  
## <a name="example"></a>範例  
 您可以使用 EVENTDATA 函數來建立事件的記錄。 在下列範例中，會建立儲存事件資訊的資料表。 每次發生資料庫層級 DDL 事件時，便會在使用下列資訊擴展資料表的目前資料庫上建立 DDL 觸發程序：  
  
-   事件時間 (使用 GETDATE 函數)。  
  
-   其工作階段上發生事件的資料庫使用者 (使用 CURRENT_USER 函數)。  
  
-   事件的類型。  
  
-   組成事件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
 同樣地，最後兩個項目會擷取使用 XQuery，以針對`xml`EVENTDATA 產生的資料。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE ddl_log (PostTime datetime, DB_User nvarchar(100), Event nvarchar(100), TSQL nvarchar(2000));  
GO  
CREATE TRIGGER log   
ON DATABASE   
FOR DDL_DATABASE_LEVEL_EVENTS   
AS  
DECLARE @data XML  
SET @data = EVENTDATA()  
INSERT ddl_log   
   (PostTime, DB_User, Event, TSQL)   
   VALUES   
   (GETDATE(),   
   CONVERT(nvarchar(100), CURRENT_USER),   
   @data.value('(/EVENT_INSTANCE/EventType)[1]', 'nvarchar(100)'),   
   @data.value('(/EVENT_INSTANCE/TSQLCommand)[1]', 'nvarchar(2000)') ) ;  
GO  
--Test the trigger  
CREATE TABLE TestTable (a int)  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
```  
  
> [!NOTE]  
>  若要傳回事件資料，我們建議您使用 XQuery `value()` 方法，而不要使用 `query()` 方法。 `query()`方法會傳回 XML 和 ampersand 逸出歸位字元和換行字元 (CRLF) 執行個體在輸出中，雖然`value()`方法呈現 CRLF 執行個體在輸出中不可見。  
  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫中則提供了相似的 DDL 觸發程序範例。 若要取得此範例，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來尋找 [Database Triggers] 資料夾。 這個資料夾位在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫的 [可程式性] 資料夾下。 以滑鼠右鍵按一下 [ddlDatabseTriggerLog]，然後選取 [編寫資料庫觸發程序的指令碼為]。 依預設，會停用 DDL 觸發程序 **ddlDatabseTriggerLog**。  
  
## <a name="see-also"></a>另請參閱  
 [DDL 事件](../triggers/ddl-events.md)   
 [DDL 事件群組](../triggers/ddl-event-groups.md)  
  
  
