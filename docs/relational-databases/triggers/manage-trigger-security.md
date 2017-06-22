---
title: "管理觸發程序安全性 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- triggers [SQL Server], security
ms.assetid: e94720a8-a3a2-4364-b0a3-bbe86e3ce4d5
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d86813b142cbd85527fb1e4e1c11d87884258ecf
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="manage-trigger-security"></a>管理觸發程序安全性
  依預設，DML 與 DDL 觸發程序會在呼叫觸發程序的該使用者之環境下執行。 觸發程序的呼叫者是執行陳述式而引發觸發程序執行的使用者。 例如，如果使用者 **Mary** 執行 DELETE 陳述式而引發 DML 觸發程序 **DML_trigMary** 執行，就會在 **Mary** 使用者權限的環境下執行 **DML_trigMary**內的程式碼。 此預設行為有可能遭到居心不良的使用者加以利用，成為在資料庫或伺服器執行個體中導入惡意程式碼的漏洞。 例如，下列 DDL 觸發程序是由使用者 `JohnDoe`建立的：  
  
 `CREATE TRIGGER DDL_trigJohnDoe`  
  
 `ON DATABASE`  
  
 `FOR ALTER_TABLE`  
  
 `AS`  
  
 `GRANT CONTROL SERVER TO JohnDoe ;`  
  
 `GO`  
  
 這個觸發程序所代表的意義是，只要有權執行 `GRANT CONTROL SERVER` 陳述式的使用者 (例如 **sysadmin** 固定伺服器角色的成員) 執行 `ALTER TABLE` 陳述式，就會授與 `JohnDoe` `CONTROL SERVER` 權限。 換句話說，雖然 `JohnDoe` 無法授與 `CONTROL SERVER` 權限給自己，不過他可以啟用觸發程序程式碼，以便授與自己在提升權限的情況下執行的權限。 DML 與 DDL 觸發程序都曝露於此種安全性威脅下。  
  
## <a name="trigger-security-best-practices"></a>觸發程序安全性最佳作法  
 您可以採用下列措施來防止觸發程序的程式碼在提升權限的情況下執行：  
  
-   請透過查詢 [sys.triggers](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) 與 [sys.server_triggers](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md) 目錄檢視來了解資料庫與伺服器執行個體上所存在的 DML 與 DDL 觸發程序。 下列查詢會傳回目前資料庫中所有的 DML 與資料庫層級的 DDL 觸發程序，以及在伺服器執行個體上的所有伺服器層級的 DDL 觸發程序：  
  
    ```  
    SELECT type, name, parent_class_desc FROM sys.triggers  
    UNION  
    SELECT type, name, parent_class_desc FROM sys.server_triggers ;  
    ```  
  
-   如果觸發程序是在提升權限的情況下執行，使用 [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md) 停用觸發程序有可能會傷害資料庫或伺服器的完整性。 下列陳述式會停用目前資料庫中所有資料庫層級的 DDL 觸發程序：  
  
    ```  
    DISABLE TRIGGER ALL ON DATABASE  
    ```  
  
     下列陳述式會停用在伺服器執行個體上所有伺服器層級的 DDL 觸發程序：  
  
    ```  
    DISABLE TRIGGER ALL ON ALL SERVER  
    ```  
  
     此陳述式停用了目前資料庫中所有的 DML 觸發程序：  
  
    ```  
    DECLARE @schema_name sysname, @trigger_name sysname, @object_name sysname ;  
    DECLARE @sql nvarchar(max) ;  
    DECLARE trig_cur CURSOR FORWARD_ONLY READ_ONLY FOR  
        SELECT SCHEMA_NAME(schema_id) AS schema_name,  
            name AS trigger_name,  
            OBJECT_NAME(parent_object_id) as object_name  
        FROM sys.objects WHERE type in ('TR', 'TA') ;  
  
    OPEN trig_cur ;  
    FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name ;  
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        SELECT @sql = 'DISABLE TRIGGER ' + QUOTENAME(@schema_name) + '.'  
            + QUOTENAME(@trigger_name) +  
            ' ON ' + QUOTENAME(@schema_name) + '.'   
            + QUOTENAME(@object_name) + ' ; ' ;  
        EXEC (@sql) ;  
        FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name ;  
    END  
    GO  
  
    -- Verify triggers are disabled. Should return an empty result set.  
    SELECT * FROM sys.triggers WHERE is_disabled = 0 ;  
    GO  
  
    CLOSE trig_cur ;  
    DEALLOCATE trig_cur;  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DML 觸發程序](../../relational-databases/triggers/dml-triggers.md)   
 [DDL 觸發程序](../../relational-databases/triggers/ddl-triggers.md)  
  
  
