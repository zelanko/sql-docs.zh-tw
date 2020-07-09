---
title: 刪除或停用 DML 觸發程序 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 56af23085e590c5c9d63b6b3da6626b4c2edb601
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757584"
---
# <a name="delete-or-disable-dml-triggers"></a>刪除或停用 DML 觸發程序
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 刪除或停用 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的 DML 觸發程序。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要刪除或停用 DML 觸發程序，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   刪除觸發程序時，會從目前的資料庫卸除它。 其所依據的資料表和資料不受影響。 刪除資料表時會自動刪除資料表上的所有觸發程序。  
  
-   觸發程序預設為在建立時啟用。  
  
-   即使停用觸發程序，也不會卸除它。 該觸發程序仍然會以物件形式存在於目前的資料庫中。 不過，當設計此觸發程序的 INSERT、UPDATE 或 DELETE 陳述式執行時，不會引發觸發程序。 已停用的觸發程序可重新啟用。 啟用觸發程序並不會重新建立它。 觸發程序會以當初建立的相同方式引發。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 刪除 DML 觸發程序需要定義觸發程序所在資料表或檢視表的 ALTER 權限。  
  
 若要停用或啟用 DML 觸發程序，使用者至少要對建立該觸發程序的資料表或檢視，具備 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-dml-trigger"></a>刪除 DML 觸發程序  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開您要的資料庫，展開 **[資料表]** ，然後展開包含您要刪除之觸發程序的資料表。  
  
3.  展開 **[觸發程序]** ，以滑鼠右鍵按一下要刪除的觸發程序，然後按一下 **[刪除]** 。  
  
4.  在 **[刪除物件]** 對話方塊中，確認要刪除的觸發程序，然後按一下 **[確定]** 。  
  
#### <a name="to-disable-and-enable-a-dml-trigger"></a>若要停用和啟用 DML 觸發程序  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開您要的資料庫，展開 **[資料表]** ，然後展開包含您要停用之觸發程序的資料表。  
  
3.  展開 **[觸發程序]** ，以滑鼠右鍵按一下要停用的觸發程序，然後按一下 **[停用]** 。  
  
4.  若要啟用觸發程序，請按一下 **[啟用]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-dml-trigger"></a>刪除 DML 觸發程序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中。 執行 [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) 陳述式即可建立 `Sales.bonus_reminder` 觸發程序。 若要刪除觸發程序，請執行 [DROP TRIGGER](../../t-sql/statements/drop-trigger-transact-sql.md) 陳述式。  
  
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
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中。 執行 [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) 陳述式即可建立 `Sales.bonus_reminder` 觸發程序。 若要停用和啟用觸發程序，請分別執行 [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md) 和 [ENABLE TRIGGER](../../t-sql/statements/enable-trigger-transact-sql.md) 陳述式。  
  
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
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
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
  
  
