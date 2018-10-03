---
title: sp_addmergepushsubscription_agent & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepushsubscription_agent_TSQL
- sp_addmergepushsubscription_agent
helpviewer_keywords:
- sp_addmergepushsubscription_agent
ms.assetid: 808a1925-be46-4999-8d69-b3a83010ec81
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e156b6912633e45ada9f1c26be40b85fd7db23d6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758056"
---
# <a name="spaddmergepushsubscriptionagent-transact-sql"></a>sp_addmergepushsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@publication =** ] **'***publication***'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@subscriber =** ] **'***訂閱者***'**  
 這是訂閱者的名稱。 *訂閱者*已**sysname**，預設值是 NULL。  
  
 [  **@subscriber_db =** ] **'***subscriber_db***'**  
 這是訂閱資料庫的名稱。 *subscriber_db*已**sysname**，預設值是 NULL。  
  
 [  **@subscriber_security_mode =** ] *subscriber_security_mode*  
 這是進行同步處理時，連接到訂閱者時使用的安全性模式。 *subscriber_security_mode*已**int**，預設值是 1。 如果**0**，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 如果**1**，指定 Windows 驗證。  
  
 [  **@subscriber_login =** ] **'***subscriber_login***'**  
 這是進行同步處理時，連接到訂閱者時使用的訂閱者登入。 *subscriber_login* ，便須*subscriber_security_mode*設定為**0**。 *subscriber_login*已**sysname**，預設值是 NULL。  
  
 [  **@subscriber_password =** ] **'***subscriber_password***'**  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的訂閱者密碼。 *subscriber_password* ，便須*subscriber_security_mode*設定為**0**。 *subscriber_password*已**sysname**，預設值是 NULL。 如果使用訂閱者密碼，它會自動加密。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
 [  **@publisher_security_mode =** ] *publisher_security_mode*  
 這是進行同步處理時，連接到發行者時使用的安全性模式。 *publisher_security_mode*已**int**，預設值是 1。 如果**0**，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 如果**1**，指定 Windows 驗證。  
  
 [  **@publisher_login =** ] **'***publisher_login***'**  
 這是在同步處理時，用來連接發行者的登入。 *publisher_login*已**sysname**，預設值是 NULL。  
  
 [  **@publisher_password =** ] **'***publisher_password***'**  
 這是連接到發行者時所用的密碼。 *publisher_password*已**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
 [  **@job_login =** ] **'***job_login***'**  
 這是用來執行代理程式之 Windows 帳戶的登入。 *job_login*已**nvarchar(257)**，預設值是 NULL。 代理程式連接到散發者時，一律使用這個 Windows 帳戶，當利用 Windows 整合式驗證來連接到訂閱者和發行者時，也一律使用這個 Windows 帳戶。  
  
 [  **@job_password =** ] **'***job_password***'**  
 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password*已**sysname**，沒有預設值。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
 [ **@job_name =** ] **'***job_name***'**  
 這是現有散發代理程式作業的名稱。 *job_name*已**sysname**，預設值是 NULL。 只有在利用現有的作業來建立同步處理訂閱，而不用新建立的作業 (預設值) 時，才指定這個參數。 如果您不屬於**sysadmin**固定伺服器角色，您必須指定*job_login*並*job_password*當您指定*job_name*.  
  
 [  **@frequency_type =** ] *frequency_type*  
 這是排程合併代理程式所採用的頻率。 *frequency_type*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|視需要|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64**|自動啟動|  
|**128**|重複執行|  
|NULL (預設值)||  
  
> [!NOTE]  
>  指定的值是**64**會導致合併代理程式以連續模式執行。 這對應於設定 **-連續**代理程式參數。 如需詳細資訊，請參閱 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 合併代理程式的執行天數。 *frequency_interval*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**3**|星期二|  
|**4**|星期三|  
|**5**|星期四|  
|**6**|星期五|  
|**7**|星期六|  
|**8**|Day|  
|**9**|工作日|  
|**10**|週末|  
|NULL (預設值)||  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 這是合併代理程式的日期。 使用這個參數時*frequency_type*設為**32** （每月相對）。 *frequency_relative_interval*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
|NULL (預設值)||  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor&lt*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*已**int**，預設值是 NULL。  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 這是在定義的期間內，重新排程的頻率。 *frequency_subday*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (預設值)||  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 間隔*frequency_subday*。 *frequency_subday_interval*已**int**，預設值是 NULL。  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 這是第一次排程合併代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*已**int**，預設值是 NULL。  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 這是排程停止合併代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*已**int**，預設值是 NULL。  
  
 [ **@active_start_date =** ] *active_start_date*  
 這是第一次排程合併代理程式的日期，格式為 YYYYMMDD。 *active_start_date*已**int**，預設值是 NULL。  
  
 [ **@active_end_date =** ] *active_end_date*  
 這是排程停止合併代理程式的日期，格式為 YYYYMMDD。 *active_end_date*已**int**，預設值是 NULL。  
  
 [  **@enabled_for_syncmgr =** ] **'***enabled_for_syncmgr***'**  
 指定是否能夠利用 Windows Synchronization Manager 來同步處理訂閱。 *enabled_for_syncmgr*已**nvarchar(5)**，預設值是 FALSE。 如果**false**，訂用帳戶未註冊使用 Synchronization Manager。 如果**真**，訂用帳戶使用 Synchronization Manager 註冊，並可以同步處理，而不啟動[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addmergepushsubscription_agent**用於合併式複寫中，並使用類似的功能[sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepushsubscript_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addmergepushsubscription_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergesubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
