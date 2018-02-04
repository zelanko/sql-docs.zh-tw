---
title: "sysmail_delete_mailitems_sp (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_delete_mailitems_sp_TSQL
- sysmail_delete_mailitems_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_mailitems_sp
ms.assetid: f87c9f4a-bda1-4bce-84b2-a055a3229ecd
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6a7843e44e42de868c3748dbf31794d4c69e361e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysmaildeletemailitemssp-transact-sql"></a>sysmail_delete_mailitems_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從 Database Mail 內部資料表中永久刪除電子郵件訊息。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_delete_mailitems_sp  [ [ @sent_before = ] 'sent_before' ]  
    [ , [ @sent_status = ] 'sent_status' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@sent_before=** ] **'***sent_before***'**  
 刪除以前的日期和時間做為提供的電子郵件*sent_before*引數。 *sent_before*是**datetime**但做為預設值是 NULL。 NULL 表示所有日期。  
  
 [ **@sent_status=** ] **'***sent_status***'**  
 刪除所指定之類型的電子郵件*sent_status*。 *sent_status*是**varchar(8)**沒有預設值。 有效的項目是**傳送**，**未傳送**，**重試**，和**失敗**。 NULL 表示所有狀態。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 Database Mail 訊息及其附件會儲存在**msdb**資料庫。 訊息應定期刪除，以防止**msdb**成長大於預期，並符合您組織的文件保留計畫。 使用**sysmail_delete_mailitems_sp**預存程序，從 Database Mail 資料表中永久刪除電子郵件訊息。 一個選擇性引數可藉由提供日期和時間，讓您只刪除較舊的電子郵件。 比該引數舊的電子郵件會被刪除。 另一個選擇性引數可讓您刪除特定類型，做為指定的電子郵件**sent_status**引數。 您必須提供引數的 **@sent_before** 或 **@sent_status** 。 若要刪除所有訊息，請使用 **@sent_before = getdate （）**。  
  
 刪除電子郵件也會刪除這些訊息的相關附加檔案。 刪除電子郵件並不會刪除對應的項目中**sysmail_event_log**。 使用[sysmail_delete_log_sp](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)從記錄檔刪除項目。  
  
## <a name="permissions"></a>Permissions  
 根據預設，此預存程序會授與執行成員關閉**sysadmin**固定的伺服器角色和**DatabaseMailUserRole**。 成員**sysadmin**固定的伺服器角色可以執行此程序來刪除所有使用者都傳送的電子郵件。 成員**DatabaseMailUserRole**只能刪除該使用者所傳送的電子郵件。  
  
## <a name="examples"></a>範例  
  
### <a name="a-deleting-all-e-mails"></a>A. 刪除所有電子郵件  
 下列範例會刪除 Database Mail 系統中的所有電子郵件。  
  
```  
DECLARE @GETDATE datetime  
SET @GETDATE = GETDATE();  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @GETDATE;  
GO  
```  
  
### <a name="b-deleting-the-oldest-e-mails"></a>B. 刪除最舊的電子郵件  
 下列範例會刪除 Database Mail 記錄中 `October 9, 2005` 以前的電子郵件。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-e-mails-of-a-certain-type"></a>C. 刪除特定類型的所有電子郵件  
 下列範例會刪除 Database Mail 記錄中所有失敗的電子郵件。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_status = 'failed' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sysmail_allitems &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_mailattachments &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)   
 [建立 SQL Server Agent 作業以封存 Database Mail 訊息及事件記錄檔](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
