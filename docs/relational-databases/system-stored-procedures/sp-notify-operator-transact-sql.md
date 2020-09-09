---
description: sp_notify_operator (Transact-SQL)
title: sp_notify_operator (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_notify_operator_TSQL
- sp_notify_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_notify_operator
ms.assetid: c440f5c9-9884-4196-b07c-55d87afb17c3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 946a2adf54435499ae72d12ed10e984892295533
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541616"
---
# <a name="sp_notify_operator-transact-sql"></a>sp_notify_operator (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  利用 Database Mail 將電子郵件訊息傳送給操作員。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_notify_operator  
    [ @profile_name = ] 'profilename' ,  
    [ @id = ] id ,  
    [ @name = ] 'name' ,  
    [ @subject = ] 'subject' ,  
    [ @body = ] 'message' ,  
    [ @file_attachments = ] 'attachment'  
    [ @mail_database = ] 'mail_host_database'  
```  
  
## <a name="arguments"></a>引數  
`[ @profile_name = ] 'profilename'` 用來傳送訊息之 Database Mail 設定檔的名稱。 *profilename* 是 **Nvarchar (128) **。 如果未指定 *profilename* ，則會使用預設的 Database Mail 設定檔。  
  
`[ @id = ] id` 要傳送訊息之操作員的識別碼。 *id* 是 **int**，預設值是 Null。 必須指定其中一個 *識別碼* 或 *名稱* 。  
  
`[ @name = ] 'name'` 要傳送訊息的操作員名稱。 *名稱* 是 **Nvarchar (128) **，預設值是 Null。 必須指定其中一個 *識別碼* 或 *名稱* 。  
  
> **注意：** 必須先為操作員定義電子郵件地址，才能接收訊息。  
  
`[ @subject = ] 'subject'` 電子郵件訊息的主旨。 [*主體*] 是**Nvarchar (256) ** ，沒有預設值。  
  
`[ @body = ] 'message'` 電子郵件訊息的主體。 *訊息* 是 **Nvarchar (max) ** ，沒有預設值。  
  
`[ @file_attachments = ] 'attachment'` 要附加至電子郵件訊息的檔案名。 *附件* 是 **Nvarchar (512) **，沒有預設值。  
  
`[ @mail_database = ] 'mail_host_database'` 指定郵件主機資料庫的名稱。 *mail_host_database* 是 **Nvarchar (128) **。 如果未指定任何 *mail_host_database* ，預設會使用 **msdb** 資料庫。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 將指定的訊息傳送給指定操作員的電子郵件地址。 如果未設定操作員的電子郵件地址，就會傳回錯誤。  
  
 您必須先設定 Database Mail 和郵件主機資料庫，才能將通知傳給操作員。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
## <a name="examples"></a>範例  
 下列範例會利用 `François Ajenstat` Database Mail 設定檔，將通知電子郵件傳給 `AdventureWorks Administrator` 操作員。 電子郵件的主旨是 `Test Notification`。 電子郵件訊息包含 "This is a test of notification via e-mail." 這個句子。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_notify_operator  
   @profile_name = N'AdventureWorks Administrator',  
   @name = N'François Ajenstat',  
   @subject = N'Test Notification',  
   @body = N'This is a test of notification via e-mail.' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的 SQL Server Agent 預存程式 ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)  
  
  
