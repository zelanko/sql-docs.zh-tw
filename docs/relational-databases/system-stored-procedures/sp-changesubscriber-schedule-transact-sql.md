---
title: sp_changesubscriber_schedule (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 83edeb0c94276e10528b05bc5a1cd8d9474d07aa
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127908"
---
# <a name="spchangesubscriberschedule-transact-sql"></a>sp_changesubscriber_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [  **@subscriber=**] **'**_訂閱者_**'**  
 這是訂閱者的名稱。 *訂閱者*已**sysname**。 訂閱者的名稱在資料庫中必須是唯一的，絕不能已經存在，而且不能是 NULL。  
  
 [  **@agent_type=**]*類型*  
 這是代理程式的類型。 *型別*已**smallint**，預設值是**0**。 **0**表示散發代理程式。 **1**表示合併代理程式。  
  
 [  **@frequency_type=**] *frequency_type*  
 這是散發工作的排程頻率。 *frequency_type*已**int**，預設值是**64**。 共有 10 個排程資料行。  
  
 [  **@frequency_interval=**] *frequency_interval*  
 若要設定的頻率所套用的值*frequency_type*。 *frequency_interval*已**int**，預設值是**1**。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 這是散發工作的日期。 *frequency_relative_interval*已**int**，預設值是**1**。  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor&lt*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*已**int**，預設值是**0**。  
  
 [  **@frequency_subday=**] *frequency_subday*  
 這是在定義的期間內，重新排程的頻率 (以分鐘為單位)。 *frequency_subday*已**int**，預設值是**4**。  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 間隔*frequency_subday*。 *frequency_subday_interval*已**int**，預設值是**5**。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 這是第一次排程散發工作的當日時間。 *active_start_time_of_day*已**int**，預設值是**0**。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 這是排程停止散發工作的當日時間。 *active_end_time_of_day*已**int**，預設值是**235959**，這表示下午 11:59:59 。  
  
 [  **@active_start_date=**] *active_start_date*  
 這是第一次排程散發工作的日期，格式為 YYYYMMDD。 *active_start_date*已**int**，預設值是**0**。  
  
 [  **@active_end_date=**] *active_end_date*  
 這是排程停止散發工作的日期，格式為 YYYYMMDD。 *active_end_date*已**int**，預設值是**99991231**，這表示年 12 月 31 日至 9999。  
  
 [ **@publisher**=] **'**_發行者_**'**  
 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*應該不在上變更發行項屬性時才使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changesubscriber_schedule**用於所有類型的複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_changesubscriber_schedule**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addsubscriber_schedule &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-schedule-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
