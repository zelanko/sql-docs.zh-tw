---
title: "EVENTDATA (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EVENTDATA
- fn_event_data
- EVENTDATA_TSQL
- fn_event_data_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server instance event data [SQL Server]
- event notifications [SQL Server], event status
- events [SQL Server], status infromation
- EVENTDATA function
- status information [SQL Server], events
- DDL triggers, returning event data
ms.assetid: 03a80e63-6f37-4b49-bf13-dc35cfe46c44
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 45f9d434e5833180320dcb3184fdcceec56c715c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="eventdata-transact-sql"></a>EVENTDATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回伺服器或資料庫事件的相關資訊。 EVENTDATA 是在引發事件通知之時呼叫的，結果會傳回指定的 Service Broker。 EVENTDATA 也可以用在 DDL 或登入觸發程序主體內。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
EVENTDATA( )  
```  
  
## <a name="remarks"></a>備註  
 只有在 DDL 或登入觸發程序內直接參考時，EVENTDATA 才會傳回資料。 如果 EVENTDATA 是由其他常式所呼叫，它便會傳回 NULL，即使這些常式是由 DDL 或登入觸發程序所呼叫亦然。  
  
 在呼叫 EVENTDATA 的交易之後，EVENTDATA 傳回的資料便告無效，可能是明確或隱含地認可或回復。  
  
> [!CAUTION]  
>  EVENTDATA 會傳回 XML 資料。 這項資料會以 Unicode 的方式傳給用戶端，每個字元佔 2 個位元組。 下列 Unicode 字碼指標可以用 EVENTDATA 傳回的 XML 來表示：  
>   
>  `0x0009`  
>   
>  `0x000A`  
>   
>  `0x000D`  
>   
>  `>= 0x0020 && <= 0xD7FF`  
>   
>  `>= 0xE000 && <= 0xFFFD`  
>   
>  在 XML 中，無法表示或不允許使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 識別碼和資料所能使用的某些字元。 有上述清單所未顯示之字碼指標的字元或資料會對應至問號 (?)。  
  
 為了保護登入的安全性，在執行 CREATE LOGIN 或 ALTER LOGIN 陳述式時將不會顯示密碼。  
  
## <a name="schemas-returned"></a>傳回的結構描述  
 EVENTDATA 會傳回型別的值**xml**。 根據預設，所有事件的結構描述定義都會安裝在以下目錄：[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]Tools\Binn\schemas\sqlserver\2006\11\events\events.xsd。  
  
 或者，事件結構描述發行位置是在[Microsoft SQL Server XML 結構描述](http://go.microsoft.com/fwlink/?LinkID=31850)網頁。  
  
 若要針對任何特定的事件擷取結構描述，請搜尋複雜類型 `EVENT_INSTANCE_\<event_type>` 的結構描述。 例如，若要擷取 DROP_TABLE 事件的結構描述，請搜尋 `EVENT_INSTANCE_DROP_TABLE` 的結構描述。  
  
## <a name="examples"></a>範例  
  
### <a name="a-querying-event-data-in-a-ddl-trigger"></a>A. 查詢 DDL 觸發程序中的事件資料  
 下列範例會建立一個 DDL 觸發程序來防止在資料庫中建立新的資料表。 引發觸發程序的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式是利用 XQuery 針對 EVENTDATA 所產生的 XML 資料來擷取的。 如需詳細資訊，請參閱 [XQuery 語言參考 &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)。  
  
> [!NOTE]  
>  當您查詢`\<TSQLCommand>`所使用的項目**以方格顯示結果**中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，看不到指令文字中的分行符號。 使用**以文字顯示結果**改為。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER safety   
ON DATABASE   
FOR CREATE_TABLE   
AS   
    PRINT 'CREATE TABLE Issued.'  
    SELECT EVENTDATA().value  
        ('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
   RAISERROR ('New tables cannot be created in this database.', 16, 1)   
   ROLLBACK  
;  
GO  
--Test the trigger.  
CREATE TABLE NewTable (Column1 int);  
GO  
--Drop the trigger.  
DROP TRIGGER safety  
ON DATABASE;  
GO  
```  
  
> [!NOTE]  
>  當您想要傳回事件資料時，我們建議您使用 XQuery **value （)**方法，而非**query （)**方法。 **Query （)**方法會傳回 XML 和 ampersand 逸出歸位字元傳回而換行字元 (CR/LF) 執行個體在輸出中，雖然**value （)**方法呈現 CR/LF 執行個體在輸出中不可見。  
  
### <a name="b-creating-a-log-table-with-event-data-in-a-ddl-trigger"></a>B. 利用 DDL 觸發程序中的事件資料來建立記錄資料表  
 下列範例會建立一份資料表來儲存有關所有資料庫層級事件的資訊，且會以 DDL 觸發程序來擴展資料表。 事件類型和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式是利用 XQuery 針對 `EVENTDATA` 所產生的 XML 資料所擷取。  
  
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
--Test the trigger.  
CREATE TABLE TestTable (a int);  
DROP TABLE TestTable ;  
GO  
SELECT * FROM ddl_log ;  
GO  
--Drop the trigger.  
DROP TRIGGER log  
ON DATABASE;  
GO  
--Drop table ddl_log.  
DROP TABLE ddl_log;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [使用 EVENTDATA 函數](../../relational-databases/triggers/use-the-eventdata-function.md)   
 [DDL 觸發程序](../../relational-databases/triggers/ddl-triggers.md)   
 [事件通知](../../relational-databases/service-broker/event-notifications.md)   
 [登入觸發程序](../../relational-databases/triggers/logon-triggers.md)  
  
  
