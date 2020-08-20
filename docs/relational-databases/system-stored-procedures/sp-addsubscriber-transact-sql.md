---
description: sp_addsubscriber (Transact-SQL)
title: sp_addsubscriber (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber
- sp_addsubscriber_TSQL
helpviewer_keywords:
- sp_addsubscriber
ms.assetid: b8a584ea-2a26-4936-965b-b84f026e39c0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6e9c6ac18d6d7752baab05ea1d9fa9a65fc86b2c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474502"
---
# <a name="sp_addsubscriber-transact-sql"></a>sp_addsubscriber (Transact-SQL)
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]

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
`[ @subscriber = ] 'subscriber'` 這是要加入此伺服器上之發行集有效訂閱者的伺服器名稱。 *訂閱者* 是 **sysname**，沒有預設值。  
  
`[ @type = ] type` 這是訂閱者的類型。 *類型* 是 **Tinyint**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**0** (預設)|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者|  
|**1**|ODBC 資料來源伺服器|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet 資料庫|  
|**3**|OLE DB 提供者|  
  
`[ @login = ] 'login'` 這是驗證的登入識別碼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *login* 是預設值為 NULL 的 **sysname**。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @password = ] 'password'` 這是驗證的密碼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *密碼* 是 **Nvarchar (524) **，預設值是 Null。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @commit_batch_size = ] commit_batch_size` 此參數已被取代，並且為了腳本的回溯相容性而保留。  
  
> [!NOTE]  
>  指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @status_batch_size = ] status_batch_size` 此參數已被取代，並且為了腳本的回溯相容性而保留。  
  
> [!NOTE]  
>  指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @flush_frequency = ] flush_frequency` 此參數已被取代，並且為了腳本的回溯相容性而保留。  
  
> [!NOTE]  
>  指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @frequency_type = ] frequency_type` 這是用來排程複寫代理程式的頻率。 *frequency_type* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次性|  
|**2**|隨選|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64** (預設) |自動啟動|  
|**128**|重複執行|  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @frequency_interval = ] frequency_interval` 這是套用至 *frequency_type*所設定之頻率的值。 *frequency_interval* 是 **int**，預設值是1。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 這是複寫代理程式的日期。 當 *frequency_type* 設定為 **32** (每月相對) 時，就會使用這個參數。 *frequency_relative_interval* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1** (預設值)|First|  
|**2**|Second|  
|**4**|Third|  
|**8**|第四個|  
|**16**|Last|  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 這是 *frequency_type*所用的迴圈因數。 *frequency_recurrence_factor* 是 **int**，預設值是 **0**。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @frequency_subday = ] frequency_subday` 在定義的期間內，重新排程的頻率。 *frequency_subday* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**2**|Second|  
|**4** (預設) |Minute|  
|**8**|小時|  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 這是 *frequency_subday*的間隔。 *frequency_subday_interval* 是 **int**，預設值是 **5**。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 這是第一次排程複寫代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day* 是 **int**，預設值是 **0**。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 這是排程停止複寫代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是 **int**，預設值是235959，表示 11:59:59 P.M。 。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @active_start_date = ] active_start_date` 這是第一次排程複寫代理程式的日期，格式為 YYYYMMDD。 *active_start_date* 是 **int**，預設值是0。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @active_end_date = ] active_end_date` 這是排程停止複寫代理程式的日期，格式為 YYYYMMDD。 *active_end_date* 是 **int**，預設值是99991231，這表示9999年12月31日。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @description = ] 'description'` 這是訂閱者的文字描述。 *描述* 是 **Nvarchar (255) **，預設值是 Null。  
  
`[ @security_mode = ] security_mode` 是已執行的安全性模式。 *security_mode* 是 **int**，預設值是1。 **0** 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 **1** 指定 Windows 驗證。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 屬性現在會在執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)時，根據每個訂用帳戶來指定。 指定值之後，它會成為在這個訂閱者端建立訂閱時的預設值，且會傳回一則警告訊息。  
  
`[ @encrypted_password = ] encrypted_password` 此參數已被取代，而且是為了回溯相容性而提供，因此只會將 *Encrypted_password* 設定為任何值，但 **0** 會導致錯誤。  
  
`[ @publisher = ] 'publisher'` 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *publisher* 是 **sysname**，預設值是 Null。  
  
> [!NOTE]  
>  從發行者發行時，不應使用「*發行者*」 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_addsubscriber** 用於快照式複寫、異動複寫和合併式複寫中。  
  
 當訂閱者只會有合併式發行集的匿名訂閱時，不需要**sp_addsubscriber** 。  
  
 **sp_addsubscriber**寫入**散發**資料庫中的[MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md)資料表。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_addsubscriber**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [sp_changesubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
