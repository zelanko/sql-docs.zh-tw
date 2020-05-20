---
title: sysmail_delete_log_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_log_sp_TSQL
- sysmail_delete_log_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_log_sp
ms.assetid: e94b37a1-70ad-46a5-86c0-721892156f7c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1aa837168c5aaff963a0b475596f4e6a4d3ff85f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82807529"
---
# <a name="sysmail_delete_log_sp-transact-sql"></a>sysmail_delete_log_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從 Database Mail 記錄中刪除事件。 刪除記錄中的所有事件或符合日期或類型條件的事件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_delete_log_sp  [ [ @logged_before = ] 'logged_before' ]  
    [, [ @event_type = ] 'event_type' ]  
  
```  
  
## <a name="arguments"></a>引數  
`[ @logged_before = ] 'logged_before'`刪除*logged_before*引數所指定的日期和時間為止的專案。 *logged_before*是具有 Null 做為預設值的**日期時間**。 NULL 表示所有日期。  
  
`[ @event_type = ] 'event_type'`刪除指定為*event_type*之類型的記錄專案。 *event_type*為**Varchar （15）** ，沒有預設值。 有效的專案包括**成功**、**警告**、**錯誤**和**資訊**。 NULL 表示所有事件類型。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 請使用**sysmail_delete_log_sp**預存程式，從 Database Mail 記錄檔中永久刪除專案。 一個選擇性引數可藉由提供日期和時間，讓您只刪除較舊的記錄。 比該引數舊的事件會被刪除。 選擇性引數可讓您只刪除特定類型的事件，指定為**event_type**引數。  
  
 刪除 Database Mail 記錄中的項目不會從 Database Mail 資料表中刪除電子郵件項目。 使用[sysmail_delete_mailitems_sp](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)從 Database Mail 資料表中刪除電子郵件。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠存取此程式。  
  
## <a name="examples"></a>範例  
  
### <a name="a-deleting-all-events"></a>A. 刪除所有事件  
 下列範例會刪除 Database Mail 記錄中的所有事件。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp ;  
GO  
```  
  
### <a name="b-deleting-the-oldest-events"></a>B. 刪除最舊的事件  
 下列範例會刪除 Database Mail 記錄中 2005 年 10 月 9 日以前的事件。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @logged_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-events-of-a-certain-type"></a>C. 刪除特定類型的所有事件  
 下列範例會刪除 Database Mail 記錄中的成功訊息。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @event_type = 'success' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sysmail_event_log &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_delete_mailitems_sp &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)   
 [建立 SQL Server Agent 作業以封存 Database Mail 訊息及事件記錄檔](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
