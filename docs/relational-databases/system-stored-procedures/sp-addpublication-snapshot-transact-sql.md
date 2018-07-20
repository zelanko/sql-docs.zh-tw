---
title: sp_addpublication_snapshot (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
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
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9ea774a66ea2e89eba185197d07630a6a2edc6ab
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39088030"
---
# <a name="spaddpublicationsnapshot-transact-sql"></a>sp_addpublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  建立指定發行集的快照集代理程式。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!IMPORTANT]  
>  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addpublication_snapshot [ @publication= ] 'publication'  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @snapshot_job_name = ] 'snapshot_agent_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@frequency_type=**] *frequency_type*  
 這是快照集代理程式的執行頻率。 *frequency_type*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次。|  
|**4** （預設值）|每天。|  
|**8**|每週。|  
|**16**|每月。|  
|**32**|每月，相對於頻率間隔。|  
|**64**|當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟動時。|  
|**128**|在電腦閒置之時執行|  
  
 [  **@frequency_interval=**] *frequency_interval*  
 要套用至所設定之頻率的值*frequency_type*。 *frequency_interval*已**int**，而且可以是下列值之一。  
  
|frequency_type 的值|對 frequency_interval 的作用|  
|------------------------------|-----------------------------------|  
|**1**|*frequency_interval*未使用。|  
|**4** （預設值）|每隔*frequency_interval*天，預設值是每日。|  
|**8**|*frequency_interval*是一或多個項目 (結合[ &#124; (Bitwise OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)邏輯運算子):<br /><br /> **1** = 星期日&#124;<br /><br /> **2** = 星期一&#124;<br /><br /> **4** = 星期二&#124;<br /><br /> **8** = 星期三&#124;<br /><br /> **16** = 星期四&#124;<br /><br /> **32** = 星期五&#124;<br /><br /> **64** = 星期六|  
|**16**|在  *frequency_interval*天的月份。|  
|**32**|*frequency_interval*是下列其中之一：<br /><br /> **1** = 星期日&#124;<br /><br /> **2** = 星期一&#124;<br /><br /> **3** = 星期二&#124;<br /><br /> **4** = 星期三&#124;<br /><br /> **5** = 星期四&#124;<br /><br /> **6** = 星期五&#124;<br /><br /> **7** = 星期六&#124;<br /><br /> **8** = 日&#124;<br /><br /> **9** = 工作日&#124;<br /><br /> **10** = 週末|  
|**64**|*frequency_interval*未使用。|  
|**128**|*frequency_interval*未使用。|  
  
 [  **@frequency_subday=**] *frequency_subday*  
 單位*freq_subday_interval*。 *frequency_subday*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4** （預設值）|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 間隔*frequency_subday*。 *frequency_subday_interval*已**int**，預設值是 5，這表示每隔 5 分鐘。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 這是快照集代理程式的執行日期。 *frequency_relative_interval*已**int**，預設值是 1。  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor&lt*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*已**int**，預設值是 0。  
  
 [  **@active_start_date=**] *active_start_date*  
 這是第一次排程快照集代理程式的日期，格式為 YYYYMMDD。 *active_start_date*已**int**，預設值是 0。  
  
 [  **@active_end_date=**] *active_end_date*  
 這是排程停止快照集代理程式的日期，格式為 YYYYMMDD。 *active_end_date*已**int**，預設值是 99991231，表示年 12 月 31 日至 9999。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 這是第一次排程快照集代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*已**int**，預設值是 0。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 這是排程停止快照集代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*已**int**，預設值是 235959，表示下午 11:59:59 。  
  
 [  **@snapshot_job_name =** ] **'***snapshot_agent_name***'**  
 這是在使用現有作業時，現有快照集代理程式作業的名稱。 *snapshot_agent_name*已**nvarchar(100)** 預設值是 NULL。 這個參數供內部使用，當建立新的發行集時，不應指定。 如果*snapshot_agent_name*指定*job_login*並*job_password*必須是 NULL。  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 這是當連接到發行者時使用的安全性模式。 *publisher_security_mode*已**smallint**，預設值是 1。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證，並**1**指定 Windows 驗證。 值為**0**您必須指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [ **@publisher_login**=] **'***publisher_login***'**  
 這是連接到發行者時所用的登入。 *publisher_login*已**sysname**，預設值是 NULL。 *publisher_login*時，必須指定*publisher_security_mode*是**0**。 如果*publisher_login*為 NULL 並*publisher_security_mode*是**1**，在指定的帳戶*job_login*將時使用連接到發行者。  
  
 [ **@publisher_password**=] **'***publisher_password***'**  
 這是連接到發行者時所用的密碼。 *publisher_password*已**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 若要改善安全性，我們建議您在執行階段提供登入名稱和密碼。  
  
 [ **@job_login**=] **'***job_login***'**  
 是執行代理程式帳戶的登入。 Azure SQL Database 受控執行個體，使用 SQL Server 帳戶。 *job_login*已**nvarchar(257)**，預設值是 NULL。 代理程式連接到 「 散發者 」 一律使用此帳戶。 您必須在建立新的快照集代理程式作業時，提供這個參數。  
  
> [!NOTE]  
>  針對非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者，這必須是指定的相同登入[sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)。  
  
 [ **@job_password**=] **'***job_password***'**  
 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password*已**sysname**，沒有預設值。 您必須在建立新的快照集代理程式作業時，提供這個參數。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 若要改善安全性，我們建議您在執行階段提供登入名稱和密碼。  
  
 [ **@publisher**=] **'***發行者***'**  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應建立在快照集代理程式時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addpublication_snapshot**用於快照式複寫、 異動複寫和合併式複寫。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>[權限]  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addpublication_snapshot**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [建立並套用快照集](../../relational-databases/replication/create-and-apply-the-snapshot.md)   
 [sp_addpublication &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication_snapshot &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_startpublication_snapshot &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
