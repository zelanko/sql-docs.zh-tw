---
title: "sp_addsubscriber (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addsubscriber
- sp_addsubscriber_TSQL
helpviewer_keywords:
- sp_addsubscriber
ms.assetid: b8a584ea-2a26-4936-965b-b84f026e39c0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 48dba20940cff922fa3bdacd78471d57fbec7707
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spaddsubscriber-transact-sql"></a>sp_addsubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將訂閱者加入發行者中，使它能夠接收發行集。 針對快照集和交易式發行集，這個預存程序執行於發行集資料庫的發行者端；如果是使用遠端散發者的合併式發行集，這個預存程序便執行於散發者端。  
  
> [!IMPORTANT]  
>  這個預存程序已被取代。 您已不需要在發行者端明確登錄訂閱者。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addsubscriber [ @subscriber = ] 'subscriber'  
    [ , [ @type = ] type ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @commit_batch_size = ] commit_batch_size ]  
    [ , [ @status_batch_size = ] status_batch_size ]  
    [ , [ @flush_frequency = ] flush_frequency ]  
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
    [ , [ @description = ] 'description' ]  
    [ , [ @security_mode = ] security_mode ]  
    [ , [ @encrypted_password = ] encrypted_password ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@subscriber=**] **'***訂閱者***'**  
 這是要做為有效訂閱者加入這部伺服器的發行集之伺服器名稱。 *訂閱者*是**sysname**，沒有預設值。  
  
 [  **@type=**]*類型*  
 這是訂閱者的類型。 *型別*是**tinyint**，而且可以是下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**0** (預設)|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者|  
|**1**|ODBC 資料來源伺服器|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet 資料庫|  
|**3**|OLE DB 提供者|  
  
 [  **@login=**] **'***登入***'**  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼。 *登入*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@password=**] **'***密碼***'**  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼。 *密碼*是**nvarchar （524)**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@commit_batch_size=**] *commit_batch_size*  
 這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。  
  
> [!NOTE]  
>  指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@status_batch_size=**] *status_batch_size*  
 這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。  
  
> [!NOTE]  
>  指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@flush_frequency=**] *flush_frequency*  
 這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。  
  
> [!NOTE]  
>  指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@frequency_type=**] *frequency_type*  
 這是排程複寫代理程式所採用的頻率。 *frequency_type*是**int**，而且可以是下列值之一。  
  
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
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [**@frequency_interval=** ] *frequency_interval*  
 若要設定的頻率所套用的值*frequency_type*。 *frequency_interval*是**int**，預設值是 1。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 這是複寫代理程式的日期。 使用這個參數時*frequency_type*設**32** （每月相對）。 *frequency_relative_interval*是**int**，而且可以是下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**1** (預設值)|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*是**int**，預設值是**0**。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@frequency_subday=**] *frequency_subday*  
 這是在定義的期間內，重新排程的頻率。 *frequency_subday*是**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4** （預設值）|Minute|  
|**8**|Hour|  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 間隔*frequency_subday*。 *frequency_subday_interval*是**int**，預設值是**5**。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 這是第一次排程複寫代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，預設值是**0**。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 這是排程停止複寫代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，預設值是 235959，表示下午 11:59:59 。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@active_start_date=**] *active_start_date*  
 這是第一次排程複寫代理程式的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是 0。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@active_end_date=**] *active_end_date*  
 這是排程停止複寫代理程式的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是 99991231，表示年 12 月 31 日 9999。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@description=**] **'***描述***'**  
 這是訂閱者的文字描述。 *描述*是**nvarchar （255)**，預設值是 NULL。  
  
 [  **@security_mode=**] *security_mode*  
 這是實作的安全性模式。 *security_mode*是**int**，預設值是 1。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 **1**指定 Windows 驗證。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 執行時，每個訂用帳戶為基礎現在指定屬性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
 [  **@encrypted_password=**] *encrypted_password*  
 這個參數已被取代，並設定僅供回溯相容性*encrypted_password*為任何值，但**0**會導致錯誤。  
  
 [  **@publisher** =] **'***發行者***'**  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *發行者*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應從發行時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addsubscriber**用於快照式複寫、 異動複寫和合併式複寫。  
  
 **sp_addsubscriber**時 「 訂閱者 」 只會有合併式發行集的匿名訂閱不需要。  
  
 **sp_addsubscriber**寫入[MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md)資料表中**發佈**資料庫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_addsubscriber**。  
  
## <a name="see-also"></a>請參閱＜  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [sp_changesubscriber &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
