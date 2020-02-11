---
title: sp_changesubscriber_schedule （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber_schedule
- sp_changesubscriber_schedule_TSQL
helpviewer_keywords:
- sp_changesubscriber_schedule
ms.assetid: ff84e8e2-d496-482c-b23e-38a6626596e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 22ecb1601108562607d1fdc550daaa945fe72910
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68770728"
---
# <a name="sp_changesubscriber_schedule-transact-sql"></a>sp_changesubscriber_schedule (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  變更訂閱者的散發代理程式或合併代理程式排程。 這個預存程序執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changesubscriber_schedule [ @subscriber = ] 'subscriber', [ @agent_type = ] type  
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
  
`[ @agent_type = ] type`這是代理程式的類型。 *類型*是**Smallint**，預設值是**0**。 **0**表示散發代理程式。 **1**表示合併代理程式。  
  
`[ @frequency_type = ] frequency_type`這是散發工作的排程頻率。 *frequency_type*是**int**，預設值是**64**。 共有 10 個排程資料行。  
  
`[ @frequency_interval = ] frequency_interval`這是*frequency_type*所設定的頻率所套用的值。 *frequency_interval*是**int**，預設值是**1**。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`這是散發工作的日期。 *frequency_relative_interval*是**int**，預設值是**1**。  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`這是*frequency_type*所使用的迴圈因數。 *frequency_recurrence_factor*是**int**，預設值是**0**。  
  
`[ @frequency_subday = ] frequency_subday`這是在定義的期間內，重新排程的頻率（以分鐘為單位）。 *frequency_subday*是**int**，預設值是**4**。  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`這是*frequency_subday*的間隔。 *frequency_subday_interval*是**int**，預設值是**5**。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`這是第一次排程散發工作的當日時間。 *active_start_time_of_day*是**int**，預設值是**0**。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`這是排程停止散發工作的當日時間。 *active_end_time_of_day*是**int**，預設值是**235959**，表示 11:59:59 P.M。 。  
  
`[ @active_start_date = ] active_start_date`這是第一次排程散發工作的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是**0**。  
  
`[ @active_end_date = ] active_end_date`這是排程停止散發工作的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是**99991231**，這表示9999年12月31日。  
  
`[ @publisher = ] 'publisher'`指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *publisher*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  ** 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者上變更發行項屬性時，不應使用「發行者」。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changesubscriber_schedule**用於所有類型的複寫中。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_changesubscriber_schedule**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addsubscriber_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-schedule-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
