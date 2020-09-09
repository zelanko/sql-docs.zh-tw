---
description: sp_changesubscriber (Transact-SQL)
title: sp_changesubscriber (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords:
- sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 96cce9a9d9a0b9bf74a1ac3b67d3089f4fcd23ed
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543665"
---
# <a name="sp_changesubscriber-transact-sql"></a>sp_changesubscriber (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  變更訂閱者的選項。 這個發行者之訂閱者的任何散發工作都會更新。 這個預存程式會寫入散發資料庫中的 **MSsubscriber_info** 資料表。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changesubscriber [ @subscriber= ] 'subscriber'  
    [ , [ @type= ] type ]  
    [ , [ @login= ] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @commit_batch_size= ] commit_batch_size ]  
    [ , [ @status_batch_size= ] status_batch_size ]  
    [ , [ @flush_frequency= ] flush_frequency ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @security_mode= ] security_mode ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @subscriber = ] 'subscriber'` 這是要變更選項之訂閱者的名稱。 *訂閱者* 是 **sysname**，沒有預設值。  
  
`[ @type = ] type` 這是訂閱者類型。 *類型* 是 **Tinyint**，預設值是 Null。 **0** 表示 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。 **1** 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或其他的 ODBC 資料來源伺服器訂閱者。  
  
`[ @login = ] 'login'` 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入識別碼。 *login* 是預設值為 NULL 的 **sysname**。  
  
`[ @password = ] 'password'` 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證密碼。 *password* 是 **sysname**，預設值是 **%** 。 **%** 指出 password 屬性沒有任何變更。  
  
`[ @commit_batch_size = ] commit_batch_size` 僅支援回溯相容性。  
  
`[ @status_batch_size = ] status_batch_size` 僅支援回溯相容性。  
  
`[ @flush_frequency = ] flush_frequency` 僅支援回溯相容性。  
  
`[ @frequency_type = ] frequency_type` 這是散發工作的排程頻率。 *frequency_type* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次性|  
|**2**|隨選|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64**|自動啟動|  
|**128**|重複執行|  
  
`[ @frequency_interval = ] frequency_interval` 這是 *frequency_type*的間隔。 *frequency_interval* 是 **int**，預設值是 Null。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 這是散發工作的日期。 當 *frequency_type* 設定為 **32** (每月相對) 時，就會使用這個參數。 *frequency_relative_interval* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|First|  
|**2**|Second|  
|**4**|Third|  
|**8**|第四個|  
|**16**|Last|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 這是散發工作在定義的 *frequency_type*期間應重複發生的頻率。 *frequency_recurrence_factor* 是 **int**，預設值是 Null。  
  
`[ @frequency_subday = ] frequency_subday` 在定義的期間內，重新排程的頻率。 *frequency_subday* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**2**|Second|  
|**4**|Minute|  
|**8**|小時|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 這是 *frequence_subday*的間隔。 *frequency_subday_interval* 是 **int**，預設值是 Null。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 這是第一次排程散發工作的當日時間，格式為 HHMMSS。 *active_start_time_of_day* 是 **int**，預設值是 Null。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 這是排程停止散發工作的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是 **int**，預設值是 Null。  
  
`[ @active_start_date = ] active_start_date` 這是第一次排程散發工作的日期，格式為 YYYYMMDD。 *active_start_date* 是 **int**，預設值是 Null。  
  
`[ @active_end_date = ] active_end_date` 這是排程停止散發工作的日期，格式為 YYYYMMDD。 *active_end_date*是 **int**，預設值是 Null。  
  
`[ @description = ] 'description'` 這是選擇性的文字描述。 *描述* 是 **Nvarchar (255) **，預設值是 Null。  
  
`[ @security_mode = ] security_mode` 是已執行的安全性模式。 *security_mode* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證|  
|**1**|Windows 驗證|  
  
`[ @publisher = ] 'publisher'` 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *publisher* 是 **sysname**，預設值是 Null。  
  
> [!NOTE]  
>  在發行者上變更發行項屬性時，不應使用「*發行者*」 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_changesubscriber** 用於所有類型的複寫中。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_changesubscriber**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addsubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
