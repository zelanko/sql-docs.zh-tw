---
title: DDL 觸發程序 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: triggers
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-ddl
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- DDL triggers, about DDL triggers
ms.assetid: 1a4a6564-9820-4a14-9305-2c0e9ea37454
caps.latest.revision: 35
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 724ca9b1262b66cb232108d7de6115b8293c7142
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="ddl-triggers"></a>DDL 觸發程序
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  DDL 觸發程序則是為了回應各種資料定義語言 (DDL) 事件而引發的。 這些事件主要對應至以 CREATE、ALTER、DROP、GRANT、DENY、REVOKE 或 UPDATE STATISTICS 關鍵字開頭的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 執行類似 DDL 作業的某些系統預存程序也可能引發 DDL 觸發程序。  
  
 當您要執行下列作業時，可使用 DDL 觸發程序：  
  
-   防止對資料庫結構描述進行特定變更。  
  
-   在資料庫中發生特定動作以回應資料庫結構描述的變更。  
  
-   記錄資料庫結構描述的變更或事件。  
  
> [!IMPORTANT]  
>  請測試 DDL 觸發程序，以判斷它們對執行之系統預存程序的回應。 例如，CREATE TYPE 陳述式與 **sp_addtype** 預存程序，都會引發在 CREATE_TYPE 事件上建立的 DDL 觸發程序。  
  
## <a name="types-of-ddl-triggers"></a>DDL 觸發程序的類型  
 Transact-SQL DDL 觸發程序  
 特殊類型的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序，可執行一個或多個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式以回應伺服器範圍或資料庫範圍事件。 例如，如果執行陳述式 (例如 ALTER SERVER CONFIGURATION) 或使用 DROP TABLE 刪除資料表，則可能會引發 DDL 觸發程序。  
  
 CLR DDL 觸發程序  
 CLR 觸發程序不執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序，而是執行以 Managed 程式碼撰寫的一個或多個方法，這些方法是在 .NET Framework 中建立並在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中上傳的組件成員。  
  
 在執行會觸發 DDL 觸發程序的 DDL 陳述式之後，才會引發 DDL 觸發程序。 DDL 觸發程序不能使用為 INSTEAD OF 觸發程序。 對於影響區域或全域暫存資料表與預存程序的事件，DDL 觸發程序不會為了回應它而引發。  
  
 DDL 觸發程序不會建立特殊 **inserted** 和 **deleted** 資料表。  
  
 使用 EVENTDATA 函數將可擷取引發 DLL 觸發程序的事件資訊，以及觸發程序所造成的後續變更之資訊。  
  
 要針對每個 DDL 事件建立的多個觸發程序。  
  
 DDL 觸發程序不像 DML 觸發程序，並不以結構描述為範圍。 因此，OBJECT_ID、OBJECT_NAME、OBJECTPROPERTY 和 OBJECTPROPERTYEX 等函數無法用來查詢有關 DDL 觸發程序的中繼資料。 請改用目錄檢視。  
  
 伺服器範圍的 DDL 觸發程序會出現在 SQL Server Management Studio 物件總管的 [觸發程序] 資料夾中。 這個資料夾在 **[伺服器物件]** 資料夾之下。 資料庫範圍的 DDL 觸發程序則是出現在 [資料庫觸發程序] 資料夾。 這個資料夾在對應資料庫的 **[可程式性]** 資料夾之下。  
  
> [!IMPORTANT]  
>  觸發程序內的惡意程式碼可能在擴大的權限下執行。 如需如何協助降低此威脅的詳細資訊，請參閱 [管理觸發程序安全性](../../relational-databases/triggers/manage-trigger-security.md)。  
  
## <a name="ddl-trigger-scope"></a>DDL 觸發程序範圍  
 DDL 觸發程序可以引發以回應目前資料庫中 (或目前伺服器上) 處理的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 事件。 觸發程序的範圍需視事件而定。 例如，每當資料庫或伺服器執行個體上發生 CREATE_TABLE 事件時，為了回應 CREATE_TABLE 事件而建立來引發的 DDL 觸發程序可以進行此處理。 只有當伺服器執行個體上發生 CREATE_LOGIN 事件時，為了回應 CREATE_LOGIN 事件而建立來引發的 DDL 觸發程序才可以進行此處理。  
  
 在下列範例中，每當資料庫中發生 `safety` 或 `DROP_TABLE` 事件時，就會引發 DDL 觸發程序 `ALTER_TABLE` 。  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
```  
  
 在下列範例中，如果目前伺服器執行個體上發生了任何 `CREATE_DATABASE` 事件，DDL 觸發程序就會列印訊息。 這個範例使用 `EVENTDATA` 函數擷取對應 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的文字。 如需如何搭配 DDL 觸發程序使用 EVENTDATA 的詳細資訊，請參閱 [使用 EVENTDATA 函數](../../relational-databases/triggers/use-the-eventdata-function.md)。  
  
```  
IF EXISTS (SELECT * FROM sys.server_triggers  
    WHERE name = 'ddl_trig_database')  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
CREATE TRIGGER ddl_trig_database   
ON ALL SERVER   
FOR CREATE_DATABASE   
AS   
    PRINT 'Database Created.'  
    SELECT EVENTDATA().value('(/EVENT_INSTANCE/TSQLCommand/CommandText)[1]','nvarchar(max)')  
GO  
DROP TRIGGER ddl_trig_database  
ON ALL SERVER;  
GO  
  
```  
  
 您可以在本主題後面「選取特定的 DDL 陳述式以引發 DDL 觸發程序」一節所提供的連結中，找到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式與其可指定之範圍的對應清單。  
  
 以資料庫限定範圍的 DDL 觸發程序是以物件形式儲存在它們所建立的資料庫中。 DDL 觸發程序可以在 **master** 資料庫中建立，其運作方式與使用者指定的資料庫中所建立者相似。 您可以查詢 **sys.triggers** 目錄檢視，以取得有關 DDL 觸發程序的資訊。 您可以在觸發程序建立所在的資料庫環境中查詢 **sys.triggers** ，或是藉由將資料庫名稱指定為識別碼，例如 **master.sys.triggers**。  
  
 伺服器範圍的 DDL 觸發程序是以物件的形式儲存在 **master** 資料庫中。 然而，您可以藉由查詢任何資料庫環境中的 **sys.server_triggers** 目錄檢視，以取得有關伺服器範圍之 DDL 觸發程序的資訊。  
  
## <a name="specifying-a-transact-sql-statement-or-group-of-statements"></a>指定 Transact-SQL 陳述式或陳述式群組  
  
### <a name="selecting-a-particular-ddl-statement-to-fire-a-ddl-trigger"></a>選取特定的 DDL 陳述式以引發 DDL 觸發程序  
 DDL 觸發程序可以設計成在執行一個或多個特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式之後才引發。 在前面的範例中，觸發程序 `safety` 會在任何 `DROP_TABLE` 或 `ALTER_TABLE` 事件之後引發。 如需可指定來引發 DDL 觸發程序的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式清單以及此觸發程序可以引發的範圍，請參閱 [DDL 事件](../../relational-databases/triggers/ddl-events.md)。  
  
### <a name="selecting-a-predefined-group-of-ddl-statements-to-fire-a-ddl-trigger"></a>選取預先定義的 DDL 陳述式群組以引發 DDL 觸發程序  
 DDL 觸發程序可以在執行任何屬於預先定義之相似事件群組的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 事件之後引發。 例如，如果您想要在執行 CREATE TABLE、ALTER TABLE 或 DROP TABLE 陳述式後引發 DDL 觸發程序，可以在 CREATE TRIGGER 陳述式中指定 FOR DDL_TABLE_EVENTS。 在執行 CREATE TRIGGER 後，事件群組所涵蓋的事件將加入 **sys.trigger_events** 目錄檢視中。  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中，如果在事件群組上建立觸發程序，則 **sys.trigger_events** 不會包含有關此事件群組的資訊，而 **sys.trigger_events** 則只會包含有關該群組涵蓋之個別事件的資訊。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中， **sys.trigger_events** 會保存有關觸發程序建立所在之事件群組的中繼資料，也會保存有關此事件群組涵蓋之個別事件的中繼資料。 因此，對 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中事件群組所涵蓋之事件的變更，不會套用到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中的這些事件群組上所建立的 DDL 觸發程序。  
  
 如需可供 DDL 觸發程序使用之預先定義的 DDL 陳述式群組清單、事件群組所涵蓋的特定陳述式，以及可以為這些事件群組編寫程式的範圍，請參閱＜ [DDL Event Groups](../../relational-databases/triggers/ddl-event-groups.md)＞。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作|主題|  
|----------|-----------|  
|描述如何建立、修改、刪除或停用 DDL 觸發程序。|[實作 DDL 觸發程序](../../relational-databases/triggers/implement-ddl-triggers.md)|  
|描述如何建立 CLR DDL 觸發程序。|[建立 CLR 觸發程序](../../relational-databases/triggers/create-clr-triggers.md)|  
|描述如何傳回有關 DDL 觸發程序的詳細資訊。|[取得 DDL 觸發程序的詳細資訊](../../relational-databases/triggers/get-information-about-ddl-triggers.md)|  
|描述如何傳回有關使用 EVENTDATA 函數引發 DDL 觸發程序之事件的詳細資訊。|[使用 EVENTDATA 函數](../../relational-databases/triggers/use-the-eventdata-function.md)|  
|描述如何管理觸發程序安全性。|[管理觸發程序安全性](../../relational-databases/triggers/manage-trigger-security.md)|  
  
## <a name="see-also"></a>另請參閱  
 [DML 觸發程序](../../relational-databases/triggers/dml-triggers.md)   
 [登入觸發程序](../../relational-databases/triggers/logon-triggers.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
