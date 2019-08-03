---
title: sp_addsubscriber_schedule (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 7baa7419620fd25be06a731894432862bfba2b96
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769048"
---
# <a name="spaddsubscriberschedule-transact-sql"></a>sp_addsubscriber_schedule (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @subscriber = ] 'subscriber'`這是訂閱者的名稱。 *訂閱者* **sysname**。 訂閱者的名稱在資料庫中必須是唯一的，絕不能已經存在，而且不能是 NULL。  
  
`[ @agent_type = ] agent_type`這是代理程式的類型。 *agent_type*是**Smallint**, 而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**0** (預設)|散發代理程式|  
|**1**|[合併代理程式]|  
  
`[ @frequency_type = ] frequency_type`這是用來排程散發代理程式的頻率。 *frequency_type*是**int**, 而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|視需要|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64** (預設值)|自動啟動|  
|**128**|重複執行|  
  
`[ @frequency_interval = ] frequency_interval`這是要套用至*frequency_type*所設定之頻率的值。 *frequency_interval*是**int**, 預設值是**1**。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`這是散發代理程式的日期。 當*frequency_type*設定為**32** (每月相對) 時, 會使用這個參數。 *frequency_relative_interval*是**int**, 而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1** (預設值)|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`這是*frequency_type*所使用的迴圈因數。 *frequency_recurrence_factor*是**int**, 預設值是**0**。  
  
`[ @frequency_subday = ] frequency_subday`這是在定義的期間內重新排定的頻率。 *frequency_subday*是**int**, 而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4** (預設值)|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`這是*frequency_subday*的間隔。 *frequency_subday_interval*是**int**, 預設值是**5**。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`這是第一次排程散發代理程式的當日時間, 格式為 HHMMSS。 *active_start_time_of_day*是**int**, 預設值是**0**。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`這是排程停止散發代理程式的當日時間, 格式為 HHMMSS。 *active_end_time_of_day*是**int**, 預設值是 235959, 表示 11:59:59 P.M。 。  
  
`[ @active_start_date = ] active_start_date`這是第一次排程散發代理程式的日期, 格式為 YYYYMMDD。 *active_start_date*是**int**, 預設值是**0**。  
  
`[ @active_end_date = ] active_end_date`這是排程停止散發代理程式的日期, 格式為 YYYYMMDD。 *active_end_date*是**int**, 預設值是 99991231, 這表示9999年12月31日。  
  
`[ @publisher = ] 'publisher'`指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *publisher*是**sysname**, 預設值是 Null。  
  
> [!NOTE]  
>  發行者不應指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或**1** (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addsubscriber_schedule**用於快照式複寫、異動複寫和合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有**系統管理員 (sysadmin** ) 固定伺服器角色的成員, 才能夠執行**sp_addsubscriber_schedule**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_changesubscriber_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-schedule-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
