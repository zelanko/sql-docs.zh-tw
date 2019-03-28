---
title: 刪除或停用 DML 觸發程序 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DML triggers, disabling
- removing DML triggers
- disabling DML triggers
- dropping DML triggers
- deleting DML triggers
- DML triggers, removing
ms.assetid: 0f97f953-33c5-4b26-afeb-db2a26ce38b4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1195d1b15ed845728cd254032fc7187b3f355f8f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536790"
---
# <a name="delete-or-disable-dml-triggers"></a>刪除或停用 DML 觸發程序
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 刪除或停用 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的 DML 觸發程序。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **若要刪除或停用 DML 觸發程序，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   刪除觸發程序時，會從目前的資料庫卸除它。 其所依據的資料表和資料不受影響。 刪除資料表時會自動刪除資料表上的所有觸發程序。  
  
-   觸發程序預設為在建立時啟用。  
  
-   即使停用觸發程序，也不會卸除它。 該觸發程序仍然會以物件形式存在於目前的資料庫中。 不過，當設計此觸發程序的 INSERT、UPDATE 或 DELETE 陳述式執行時，不會引發觸發程序。 已停用的觸發程序可重新啟用。 啟用觸發程序並不會重新建立它。 觸發程序會以當初建立的相同方式引發。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 刪除 DML 觸發程序需要定義觸發程序所在資料表或檢視表的 ALTER 權限。  
  
 若要停用或啟用 DML 觸發程序，使用者至少要對建立該觸發程序的資料表或檢視，具備 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-dml-trigger"></a>刪除 DML 觸發程序  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開您要的資料庫，展開 **[資料表]**，然後展開包含您要刪除之觸發程序的資料表。  
  
3.  展開 **[觸發程序]**，以滑鼠右鍵按一下要刪除的觸發程序，然後按一下 **[刪除]**。  
  
4.  在 **[刪除物件]** 對話方塊中，確認要刪除的觸發程序，然後按一下 **[確定]**。  
  
#### <a name="to-disable-and-enable-a-dml-trigger"></a>若要停用和啟用 DML 觸發程序  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開您要的資料庫，展開 **[資料表]**，然後展開包含您要停用之觸發程序的資料表。  
  
3.  展開 **[觸發程序]**，以滑鼠右鍵按一下要停用的觸發程序，然後按一下 **[停用]**。  
  
4.  若要啟用觸發程序，請按一下 **[啟用]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-dml-trigger"></a>刪除 DML 觸發程序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中。 執行 [CREATE TRIGGER](/sql/t-sql/statements/create-trigger-transact-sql) 陳述式即可建立 `Sales.bonus_reminder` 觸發程序。 若要刪除觸發程序，請執行 [DROP TRIGGER](/sql/t-sql/statements/drop-trigger-transact-sql) 陳述式。  
  
```sql  
--Create the trigger.  
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
  
```sql  
--Delete the trigger.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('Sales.bonus_reminder', 'TR') IS NOT NULL  
   DROP TRIGGER Sales.bonus_reminder;  
GO  
  
```  
  
#### <a name="to-disable-and-enable-a-dml-trigger"></a>若要停用和啟用 DML 觸發程序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中。 執行 [CREATE TRIGGER](/sql/t-sql/statements/create-trigger-transact-sql) 陳述式即可建立 `Sales.bonus_reminder` 觸發程序。 若要停用和啟用觸發程序，請分別執行 [DISABLE TRIGGER](/sql/t-sql/statements/disable-trigger-transact-sql) 和 [ENABLE TRIGGER](/sql/t-sql/statements/enable-trigger-transact-sql) 陳述式。  
  
```sql  
--Create the trigger.  
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
  
```sql  
--Disable the trigger.  
USE AdventureWorks2012;  
GO  
DISABLE TRIGGER Sales.bonus_reminder ON Sales.SalesPersonQuotaHistory;  
GO  
  
```  
  
```sql  
--Enable the trigger.  
USE AdventureWorks2012;  
GO  
ENABLE TRIGGER Sales.bonus_reminder ON Sales.SalesPersonQuotaHistory;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/enable-trigger-transact-sql)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/disable-trigger-transact-sql)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)   
 [取得關於 DML 觸發程序的詳細資訊](dml-triggers.md)   
 [sp_help &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-transact-sql)   
 [sp_helptrigger &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptrigger-transact-sql)   
 [sys.triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql)   
 [sys.trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-trigger-events-transact-sql)   
 [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)   
 [sys.server_triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)  
  
  
