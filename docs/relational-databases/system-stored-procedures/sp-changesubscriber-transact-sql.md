---
title: sp_changesubscriber (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords:
- sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c2cb0047dd66b0c3fd96d399e404b801401d202a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32993125"
---
# <a name="spchangesubscriber-transact-sql"></a>sp_changesubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更訂閱者的選項。 這個發行者之訂閱者的任何散發工作都會更新。 這個預存程序會寫入**MSsubscriber_info**散發資料庫中的資料表。 這個預存程序執行於發行集資料庫的發行者端。  
  
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
 [  **@subscriber=**] **'***訂閱者***'**  
 這是要變更選項之訂閱者的名稱。 *訂閱者*是**sysname**，沒有預設值。  
  
 [  **@type=**]*類型*  
 這是訂閱者類型。 *型別*是**tinyint**，預設值是 NULL。 **0**指出[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者。 **1**指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或其他 ODBC 資料來源伺服器訂閱者。  
  
 [  **@login=**] **'***登入***'**  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼。 *login* 是預設值為 NULL 的 **sysname**。  
  
 [  **@password=**] **'***密碼***'**  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼。 *密碼*是**sysname**，預設值是**%**。 **%** 表示 password 屬性沒有變更。  
  
 [  **@commit_batch_size=**] *commit_batch_size*  
 支援這個項目的目的，只是為了與舊版相容。  
  
 [  **@status_batch_size=**] *status_batch_size*  
 支援這個項目的目的，只是為了與舊版相容。  
  
 [  **@flush_frequency=**] *flush_frequency*  
 支援這個項目的目的，只是為了與舊版相容。  
  
 [  **@frequency_type=**] *frequency_type*  
 這是散發工作的排程頻率。 *frequency_type*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|視需要|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64**|自動啟動|  
|**128**|重複執行|  
  
 [  **@frequency_interval=**] *frequency_interval*  
 間隔*frequency_type*。 *frequency_interval*是**int**，預設值是 NULL。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 這是散發工作的日期。 使用這個參數時*frequency_type*設**32** （每月相對）。 *frequency_relative_interval*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 是散發工作應該循環執行頻率期間定義*frequency_type*。 *frequency_recurrence_factor*是**int**，預設值是 NULL。  
  
 [  **@frequency_subday=**] *frequency_subday*  
 這是在定義的期間內，重新排程的頻率。 *frequency_subday*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 間隔*frequence_subday*。 *frequency_subday_interval*是**int**，預設值是 NULL。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 這是第一次排程散發工作的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，預設值是 NULL。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 這是排程停止散發工作的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，預設值是 NULL。  
  
 [  **@active_start_date=**] *active_start_date*  
 這是第一次排程散發工作的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是 NULL。  
  
 [  **@active_end_date=**] *active_end_date*  
 這是排程停止散發工作的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是 NULL。  
  
 [  **@description=**] **'***描述***'**  
 這是選擇性的文字描述。 *描述*是**nvarchar （255)**，預設值是 NULL。  
  
 [  **@security_mode=**] *security_mode*  
 這是實作的安全性模式。 *security_mode*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證|  
|**1**|Windows 驗證|  
  
 [ **@publisher**=] **'***發行者***'**  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *發行者*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*應該不在上變更發行項屬性時才使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changesubscriber**用於所有複寫類型。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_changesubscriber**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addsubscriber &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpserver & #40;TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
