---
title: "取得 DML 觸發程序的資訊 | Microsoft Docs"
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
- metadata [SQL Server], triggers
- viewing DML triggers
- DML triggers, metadata
- displaying DML triggers
- status information [SQL Server], triggers
- DML triggers, viewing
ms.assetid: 37574aac-181d-4aca-a2cc-8abff64237dc
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a8583bd2597f5107398a65df65dbe7f7eef53f4d
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="get-information-about-dml-triggers"></a>取得關於 DML 觸發程序的詳細資訊
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 取得有關 [!INCLUDE[tsql](../../includes/tsql-md.md)]中 DML 觸發程序的資訊。 這項資訊可能包括資料表上觸發程序的類型、觸發程序的名稱、其擁有者，以及建立或修改的日期。 如果觸發程序建立時並未加密，則您會取得觸發程序的定義。 定義可幫助您了解觸發程序如何影響本身定義所在的資料表。 另外，您可以找出特定觸發程序所使用的物件。 有了這項資訊，您就可以識別影響觸發程序的物件 (如果已在資料庫中變更或刪除這些物件)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要取得 DML 觸發程序的相關資訊，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 **sys.sql.modules**、 **sys.object**、 **sys.triggers**、 **sys.events**、 **sys.trigger_events**  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
 OBJECT_DEFINITION、OBJECTPROPERTY、 **sp_helptext**  
 需要 **public** 角色中的成員資格。 凡具有 ALTER、CONTROL、TAKE OWNERSHIP 或 VIEW DEFINITION 任一權限的物件擁有者或被授與者，都看得到使用者物件的定義。 **db_owner**、 **db_ddladmin**和 **db_securityadmin** 固定資料庫角色的成員隱含地擁有這些權限。  
  
 **sys.sql_expression_dependencies**  
 需要資料庫的 VIEW DEFINITION 權限和資料庫之 **sys.sql_expression_dependencies** 的 SELECT 權限。 依預設，SELECT 權限只授與 **db_owner** 固定資料庫角色的成員。 當 SELECT 和 VIEW DEFINITION 權限授與其他使用者時，被授與者就可以檢視資料庫中的所有相依性。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-definition-of-a-dml-trigger"></a>若要檢視 DML 觸發程序的定義  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開您要的資料庫，展開 **[資料表]**，然後展開包含您要檢視其定義之觸發程序的資料表。  
  
3.  展開 [觸發程序]，以滑鼠右鍵按一下您要的觸發程序，然後按一下 [修改]。 DML 觸發程序的定義會出現在查詢視窗中。  
  
#### <a name="to-view-the-dependencies-of-a-dml-trigger"></a>若要檢視 DML 觸發程序的相依性  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開您要的資料庫，展開 **[資料表]**，然後展開包含您要檢視的觸發程序及其相依性的資料表。  
  
3.  展開 [觸發程序]，以滑鼠右鍵按一下您要的觸發程序，然後按一下 [檢視相依性]。  
  
4.  在 [物件相依性] 視窗中，若要檢視相依於 DML 觸發程序的物件，請選取 [相依於 \<DML 觸發程序名稱> 的物件]。 物件會出現在 **[相依性]** 區域中。  
  
     若要檢視 DML 所相依的物件，請選取 [\<DML 觸發程序名稱> 所相依的物件]。 物件會出現在 **[相依性]** 區域中。 展開每個節點，查看所有物件。  
  
5.  若要取得出現在 **[相依性]** 區域中之物件的相關資訊，請按一下該物件。 **[選取的物件]** 欄位的 **[名稱]**、 **[類型]**和 **[相依性類型]** 方塊中會提供資訊。  
  
6.  若要關閉 **[物件相依性]** 視窗，請按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-definition-of-a-dml-trigger"></a>若要檢視 DML 觸發程序的定義  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列其中一個範例複製並貼到查詢視窗中，然後按一下 **[執行]**。 每個範例都會說明如何檢視 `iuPerson` 觸發程序的定義。  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT definition   
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID(N'Person.iuPerson');   
GO  
```  
  
```tsql  
USE AdventureWorks2012;   
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID(N'Person.iuPerson')) AS ObjectDefinition;   
GO  
  
```  
  
```tsql  
USE AdventureWorks2012;   
GO  
EXEC sp_helptext 'Person.iuPerson'  
GO  
  
```  
  
#### <a name="to-view-the-dependencies-of-a-dml-trigger"></a>若要檢視 DML 觸發程序的相依性  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列其中一個範例複製並貼到查詢視窗中，然後按一下 **[執行]**。 每個範例都會說明如何檢視 `iuPerson` 觸發程序的相依性。  
  
```  
USE AdventureWorks2012;   
GO  
SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
    o.type_desc AS referencing_desciption,   
    COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
    referencing_class_desc, referenced_class_desc,   
    referenced_server_name, referenced_database_name, referenced_schema_name,   
    referenced_entity_name,   
    COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,   
    is_caller_dependent, is_ambiguous  
FROM sys.sql_expression_dependencies AS sed  
INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
WHERE referencing_id = OBJECT_ID(N'Person.iuPerson');   
GO  
  
```  
  
#### <a name="to-view-information-about-dml-triggers-in-the-database"></a>若要檢視有關資料庫中 DML 觸發程序的資訊  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列其中一個範例複製並貼到查詢視窗中，然後按一下 **[執行]**。 每個範例都會說明如何檢視資料庫中有關 DML 觸發程序 (`TR`) 的資訊。  
  
```  
USE AdventureWorks2012;   
GO  
SELECT  name, parent_id, create_date, modify_date, is_instead_of_trigger  
FROM sys.triggers  
WHERE type = 'TR';   
GO  
  
```  
  
```tsql  
USE AdventureWorks2012;   
GO  
SELECT  name, object_id, schema_id, parent_object_id, type_desc, create_date, modify_date, is_published  
FROM sys.objects  
WHERE type = 'TR';   
GO  
  
```  
  
```tsql  
USE AdventureWorks2012;   
GO  
SELECT OBJECTPROPERTY(OBJECT_ID(N'Person.iuPerson'), 'ExecIsInsteadOfTrigger');   
GO  
  
```  
  
#### <a name="to-view-information-about-events-that-fire-a-dml-trigger"></a>若要檢視有關引發 DML 觸發程序之事件的資訊  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列其中一個範例複製並貼到查詢視窗中，然後按一下 **[執行]**。 每個範例都會說明如何檢視引發 `iuPerson` 觸發程序的事件。  
  
```tsql  
USE AdventureWorks2012;   
GO  
SELECT object_id, type, type_desc, is_trigger_event, event_group_type, event_group_type_desc   
FROM sys.events  
WHERE object_id = OBJECT_ID('Person.iuPerson');   
GO  
```  
  
```tsql  
USE AdventureWorks2012;   
GO   
SELECT object_id, type,is_first, is_last  
FROM sys.trigger_events  
WHERE object_id = OBJECT_ID('Person.iuPerson');   
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
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)  
  
  
