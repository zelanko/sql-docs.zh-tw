---
title: sysmail_delete_mailitems_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_mailitems_sp_TSQL
- sysmail_delete_mailitems_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_mailitems_sp
ms.assetid: f87c9f4a-bda1-4bce-84b2-a055a3229ecd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ee0298a714394bdf90009657c3d5b7a4daafebcd
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814260"
---
# <a name="sysmail_delete_mailitems_sp-transact-sql"></a>sysmail_delete_mailitems_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從 Database Mail 內部資料表中永久刪除電子郵件訊息。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_delete_mailitems_sp  [ [ @sent_before = ] 'sent_before' ]  
    [ , [ @sent_status = ] 'sent_status' ]  
```  
  
## <a name="arguments"></a>引數  
`[ \@sent_before = ] 'sent_before'`刪除以*sent_before*引數提供的日期和時間為止的電子郵件。 *sent_before*是具有 Null 做為預設值的**日期時間**。 NULL 表示所有日期。  
  
`[ \@sent_status = ] 'sent_status'`刪除*sent_status*所指定之類型的電子郵件。 *sent_status*為**Varchar （8）** ，沒有預設值。 有效的專案會傳送 **、未****傳送**、**重試**，以及**失敗**。 NULL 表示所有狀態。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 Database Mail 訊息及其附件會儲存在**msdb**資料庫中。 應定期刪除訊息，以防止**msdb**成長超過預期，並符合您組織的檔保留計畫。 您可以使用**sysmail_delete_mailitems_sp**預存程式，從 Database Mail 資料表中永久刪除電子郵件訊息。 一個選擇性引數可藉由提供日期和時間，讓您只刪除較舊的電子郵件。 比該引數舊的電子郵件會被刪除。 另一個選擇性引數可讓您只刪除特定類型的電子郵件，指定為**sent_status**引數。 您必須為** \@ sent_before**或** \@ sent_status**提供引數。 若要刪除所有訊息，請使用** \@ sent_before = getdate （）**。  
  
 刪除電子郵件也會刪除這些訊息的相關附加檔案。 刪除電子郵件並不會刪除**sysmail_event_log**中的對應專案。 使用[sysmail_delete_log_sp](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)從記錄中刪除專案。  
  
## <a name="permissions"></a>權限  
 根據預設，這個預存程式會被授與**系統管理員（sysadmin** ）固定伺服器角色和**DatabaseMailUserRole**的成員執行。 **系統管理員（sysadmin** ）固定伺服器角色的成員可以執行此程式，以刪除所有使用者所傳送的電子郵件。 **DatabaseMailUserRole**的成員只能刪除該使用者所傳送的電子郵件。  
  
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
 [sysmail_allitems &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_mailattachments &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)   
 [建立 SQL Server Agent 作業以封存 Database Mail 訊息及事件記錄檔](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
