---
description: sp_addmergepushsubscription_agent (Transact-SQL)
title: sp_addmergepushsubscription_agent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepushsubscription_agent_TSQL
- sp_addmergepushsubscription_agent
helpviewer_keywords:
- sp_addmergepushsubscription_agent
ms.assetid: 808a1925-be46-4999-8d69-b3a83010ec81
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 91131da8fe1102edf1c2d6f890ece76be440d1ff
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89529376"
---
# <a name="sp_addmergepushsubscription_agent-transact-sql"></a>sp_addmergepushsubscription_agent (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  新增一項新的代理程式作業，以便用來排程合併式發行集發送訂閱的同步處理。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!IMPORTANT]  
>  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmergepushsubscription_agent [ @publication =] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password = ] 'subscriber_password' ]   
    [ , [ @publisher_security_mode = ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
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
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @subscriber = ] 'subscriber'` 這是訂閱者的名稱。 *訂閱者* 是 **sysname**，預設值是 Null。  
  
`[ @subscriber_db = ] 'subscriber_db'` 這是訂閱資料庫的名稱。 *subscriber_db* 是 **sysname**，預設值是 Null。  
  
`[ @subscriber_security_mode = ] subscriber_security_mode` 這是在同步處理時，連接到訂閱者時所要使用的安全性模式。 *subscriber_security_mode* 是 **int**，預設值是1。 如果為 **0**，則指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 如果是 **1**，則指定 Windows 驗證。  
  
`[ @subscriber_login = ] 'subscriber_login'` 這是在同步處理時，連接到訂閱者時所使用的訂閱者登入。 如果*subscriber_security_mode*設定為**0**，則需要*subscriber_login* 。 *subscriber_login* 是 **sysname**，預設值是 Null。  
  
`[ @subscriber_password = ] 'subscriber_password'` 這是驗證的訂閱者密碼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果*subscriber_security_mode*設定為**0**，則需要*subscriber_password* 。 *subscriber_password* 是 **sysname**，預設值是 Null。 如果使用訂閱者密碼，它會自動加密。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @publisher_security_mode = ] publisher_security_mode` 這是在同步處理時，連接到發行者時所使用的安全性模式。 *publisher_security_mode* 是 **int**，預設值是1。 如果為 **0**，則指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 如果是 **1**，則指定 Windows 驗證。  
  
`[ @publisher_login = ] 'publisher_login'` 這是在同步處理時，用來連接發行者的登入。 *publisher_login* 是 **sysname**，預設值是 Null。  
  
`[ @publisher_password = ] 'publisher_password'` 這是連接到發行者時所使用的密碼。 *publisher_password* 是 **sysname**，預設值是 Null。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @job_login = ] 'job_login'` 這是用來執行代理程式之 Windows 帳戶的登入。 *job_login* 是 **Nvarchar (257) **，預設值是 Null。 代理程式連接到散發者時，一律使用這個 Windows 帳戶，當利用 Windows 整合式驗證來連接到訂閱者和發行者時，也一律使用這個 Windows 帳戶。  
  
`[ @job_password = ] 'job_password'` 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password* 是 **sysname**，沒有預設值。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @job_name = ] 'job_name'` 這是現有代理程式作業的名稱。 *job_name* 是 **sysname**，預設值是 Null。 只有在利用現有的作業來建立同步處理訂閱，而不用新建立的作業 (預設值) 時，才指定這個參數。 如果您不是**系統管理員（sysadmin** ）固定伺服器角色的成員，則必須在指定*job_name*時指定*job_login*和*job_password* 。  
  
`[ @frequency_type = ] frequency_type` 這是排程合併代理程式的頻率。 *frequency_type* 是 **int**，而且可以是下列其中一個值。  
  
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
|NULL (預設值)||  
  
> [!NOTE]  
>  指定 **64** 的值會導致合併代理程式在連續模式下執行。 這對應于設定代理程式的 **-連續** 參數。 如需詳細資訊，請參閱 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
`[ @frequency_interval = ] frequency_interval` 合併代理程式執行的天數。 *frequency_interval* 是 **int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**3**|Tuesday|  
|**4**|星期三|  
|**5**|Thursday|  
|**6**|星期五|  
|**7**|星期六|  
|**8**|天|  
|**9**|工作日|  
|**10**|週末|  
|NULL (預設值)||  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 這是合併代理程式的日期。 當 *frequency_type* 設定為 **32** (每月相對) 時，就會使用這個參數。 *frequency_relative_interval* 是 **int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|First|  
|**2**|Second|  
|**4**|Third|  
|**8**|第四個|  
|**16**|Last|  
|NULL (預設值)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 這是 *frequency_type*所用的迴圈因數。 *frequency_recurrence_factor* 是 **int**，預設值是 Null。  
  
`[ @frequency_subday = ] frequency_subday` 在定義的期間內，重新排程的頻率。 *frequency_subday* 是 **int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**2**|Second|  
|**4**|Minute|  
|**8**|小時|  
|NULL (預設值)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 這是 *frequency_subday*的間隔。 *frequency_subday_interval* 是 **int**，預設值是 Null。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 這是第一次排程合併代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day* 是 **int**，預設值是 Null。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 這是排程合併代理程式停止的當日時間，格式為 HHMMSS。 *active_end_time_of_day* 是 **int**，預設值是 Null。  
  
`[ @active_start_date = ] active_start_date` 這是第一次排程合併代理程式的日期，格式為 YYYYMMDD。 *active_start_date* 是 **int**，預設值是 Null。  
  
`[ @active_end_date = ] active_end_date` 這是排程停止合併代理程式的日期，格式為 YYYYMMDD。 *active_end_date* 是 **int**，預設值是 Null。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'` 指定訂閱是否可以透過 Windows 同步處理管理員進行同步處理。 *enabled_for_syncmgr* 是 **Nvarchar (5) **，預設值是 FALSE。 如果 **為 false**，則表示訂閱未向同步處理管理員註冊。 若 **為 true**，則會向同步處理管理員註冊訂閱，而且可以在不啟動的情況下同步處理 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addmergepushsubscription_agent** 用於合併式複寫中，並使用類似 [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)的功能。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepushsubscript_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_addmergepushsubscription_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
