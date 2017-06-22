---
title: "修改或重新命名 DML 觸發程序 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- renaming triggers
- modifying triggers
- DML triggers, modifying
ms.assetid: c7317eec-c0e9-479e-a4a7-83b6b6c58d59
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2ac7956829213d52669a3408a9a64c597cafa03d
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="modify-or-rename-dml-triggers"></a>修改或重新命名 DML 觸發程序
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 修改或重新命名 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的 DML 觸發程序。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法修改或重新命名 DML 觸發程序：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   當您重新命名觸發程序時，觸發程序必須位於目前資料庫中，而且新名稱必須遵照 [識別碼](../../relational-databases/databases/database-identifiers.md)的規則。  
  
###  <a name="Recommendations"></a> 建議  
  
-   我們建議您不要使用 [sp_rename](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md) 預存程序重新命名觸發程序。 變更物件名稱的任何部分，可能破壞指令碼和預存程序。 重新命名觸發程序並不會變更 [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 目錄檢視 definition 資料行中對應的物件名稱。 我們建議您先卸除，再重新建立觸發程序。  
  
-   如果您變更 DML 觸發程序所參考的物件名稱，就必須修改觸發程序以反映新的名稱。 因此，在您重新命名物件之前，請先顯示此物件的相依性，以判斷是否有任何觸發程序受到相關變更的影響。  
  
-   亦可將 DML 觸發程序的定義修改為加密的形態  
  
-   若要檢視觸發程序的相依性，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或下列函數和目錄檢視：  
  
    -   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
    -   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)  
  
    -   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 變更 DML 觸發程序需要定義觸發程序的資料表或檢視表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-a-dml-trigger"></a>若要修改 DML 觸發程序  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開您要的資料庫，展開 **[資料表]**，然後展開包含您要修改之觸發程序的資料表。  
  
3.  展開 **[觸發程序]**，以滑鼠右鍵按一下要修改的觸發程序，再按一下 **[修改]**。  
  
4.  修改觸發程序，然後按一下 **[執行]**。  
  
#### <a name="to-rename-a-dml-trigger"></a>若要重新命名 DML 觸發程序  
  
1.  [刪除觸發程序](../../relational-databases/triggers/delete-or-disable-dml-triggers.md) ，也就是要重新命名的觸發程序。  
  
2.  [重新建立觸發程序](../../relational-databases/triggers/create-dml-triggers.md)，並指定新名稱。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-modify-a-trigger-using-alter-trigger"></a>若要使用 ALTER TRIGGER 修改觸發程序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並貼入查詢中。 執行第一個範例，建立當使用者嘗試在 `SalesPersonQuotaHistory` 資料表中加入或變更資料時，將使用者定義訊息列印到用戶端的 DML 觸發程序。 執行 [ALTER TRIGGER](../../t-sql/statements/alter-trigger-transact-sql.md) 陳述式修改觸發程式，使它只在 `INSERT` 活動上引發。 這個觸發程序很有用，因為它會提醒使用者在這份資料表中更新或插入資料列，以便同時通知 `Compensation` 部門。  
  
```tsql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
```tsql  
USE AdventureWorks2012;  
GO  
ALTER TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
AFTER INSERT  
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
#### <a name="to-rename-a-trigger-using-drop-trigger-and-alter-trigger"></a>若要使用 DROP TRIGGER 和 ALTER TRIGGER 重新命名觸發程序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例會使用 [DROP TRIGGER](../../t-sql/statements/drop-trigger-transact-sql.md) 和 [ALTER TRIGGER](../../t-sql/statements/alter-trigger-transact-sql.md) 陳述式將 `Sales.bonus_reminder` 觸發程序重新命名為 `Sales.bonus_reminder_2`。  
  
```tsql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder_2  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [取得關於 DML 觸發程序的詳細資訊](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
  
