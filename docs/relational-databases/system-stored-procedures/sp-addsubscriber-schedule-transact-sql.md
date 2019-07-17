---
title: sp_addsubscriber_schedule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber_schedule_TSQL
- sp_addsubscriber_schedule
helpviewer_keywords:
- sp_addsubscriber_schedule
ms.assetid: a6225033-5c3b-452f-ae52-79890a3590ed
author: stevestein
ms.author: sstein
ms.openlocfilehash: 49bf433969d72e253afed2a87837ad2ca03fb94a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022407"
---
# <a name="spaddsubscriberschedule-transact-sql"></a>sp_addsubscriber_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  新增散發代理程式和合併代理程式的排程。 這個預存程序執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addsubscriber_schedule [ @subscriber = ] 'subscriber'  
    [ , [ @agent_type = ] agent_type ]  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @subscriber = ] 'subscriber'` 是訂閱者的名稱。 *訂閱者*已**sysname**。 訂閱者的名稱在資料庫中必須是唯一的，絕不能已經存在，而且不能是 NULL。  
  
`[ @agent_type = ] agent_type` 是代理程式的類型。 *agent_type*已**smallint**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0** (預設)|散發代理程式|  
|**1**|[合併代理程式]|  
  
`[ @frequency_type = ] frequency_type` 是用來排程散發代理程式的頻率。 *frequency_type*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|視需要|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64** （預設值）|自動啟動|  
|**128**|重複執行|  
  
`[ @frequency_interval = ] frequency_interval` 要套用至所設定之頻率的值*frequency_type*。 *frequency_interval*已**int**，預設值是**1**。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 這是散發代理程式的日期。 使用這個參數時*frequency_type*設為**32** （每月相對）。 *frequency_relative_interval*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1** (預設值)|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*已**int**，預設值是**0**。  
  
`[ @frequency_subday = ] frequency_subday` 已定義的期間重新排程的頻率。 *frequency_subday*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4** （預設值）|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 間隔*frequency_subday*。 *frequency_subday_interval*已**int**，預設值是**5**。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 散發代理程式時第一天的排程時間，格式為 HHMMSS。 *active_start_time_of_day*已**int**，預設值是**0**。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 是 「 散發代理程式停止的當日時間排程，格式為 HHMMSS。 *active_end_time_of_day*已**int**，預設值是 235959，表示下午 11:59:59 。  
  
`[ @active_start_date = ] active_start_date` 是 「 散發代理程式時第一個排程的日期，格式為 YYYYMMDD。 *active_start_date*已**int**，預設值是**0**。  
  
`[ @active_end_date = ] active_end_date` 是 「 散發代理程式停止的日期排程，格式為 YYYYMMDD。 *active_end_date*已**int**，預設值是 99991231，表示年 12 月 31 日至 9999。  
  
`[ @publisher = ] 'publisher'` 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應指定為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addsubscriber_schedule**用於快照式複寫、 異動複寫和合併式複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_addsubscriber_schedule**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_changesubscriber_schedule &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-schedule-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
