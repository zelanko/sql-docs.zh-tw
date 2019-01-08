---
title: sp_changepublication_snapshot & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changepublication_snapshot_TSQL
- sp_changepublication_snapshot
helpviewer_keywords:
- sp_changepublication_snapshot
ms.assetid: 518a4618-3592-4edc-8425-cbc33cdff891
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f1f001752ee67253297917746ff50eeb61a3ff1d
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53203627"
---
# <a name="spchangepublicationsnapshot-transact-sql"></a>sp_changepublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更指定發行集的快照集代理程式屬性。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!IMPORTANT]  
>  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changepublication_snapshot [ @publication= ] 'publication'  
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
 [  **@publication =**] **'***發行集***'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@frequency_type =**] *frequency_type*  
 這是代理程式的排程頻率。 *frequency_type*已**int**，而且可以是下列值之一。  
  
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
  
 [  **@frequency_interval =**] *frequency_interval*  
 指定代理程式執行的天數。 *frequency_interval*已**int**，而且可以是下列值之一。  
  
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
  
 [  **@frequency_subday =**] *frequency_subday*  
 單位*freq_subday_interval*。 *frequency_subday*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (預設值)||  
  
 [  **@frequency_subday_interval =**] *frequency_subday_interval*  
 間隔*frequency_subday*。 *frequency_subday_interval*已**int**，預設值是 NULL。  
  
 [  **@frequency_relative_interval =**] *frequency_relative_interval*  
 這是快照集代理程式的執行日期。 *frequency_relative_interval*已**int**，預設值是 NULL。  
  
 [  **@frequency_recurrence_factor =**] *frequency_recurrence_factor&lt*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*已**int**，預設值是 NULL。  
  
 [  **@active_start_date =**] *active_start_date*  
 這是第一次排程快照集代理程式的日期，格式為 YYYYMMDD。 *active_start_date*已**int**，預設值是 NULL。  
  
 [  **@active_end_date =**] *active_end_date*  
 這是排程停止快照集代理程式的日期，格式為 YYYYMMDD。 *active_end_date*已**int**，預設值是 NULL。  
  
 [  **@active_start_time_of_day =**] *active_start_time_of_day*  
 這是第一次排程快照集代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*已**int**，預設值是 NULL。  
  
 [  **@active_end_time_of_day =**] *active_end_time_of_day*  
 這是排程停止快照集代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*已**int**，預設值是 NULL。  
  
 [  **@snapshot_job_name =** ] **'***snapshot_agent_name***'**  
 這是在使用現有作業時，現有快照集代理程式作業的名稱。 *snapshot_agent_name*已**nvarchar(100)** 預設值是 NULL。  
  
 [  **@publisher_security_mode =** ] *publisher_security_mode*  
 這是當連接到發行者時使用的安全性模式。 *publisher_security_mode*已**smallint**，預設值是 NULL。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證，並**1**指定 Windows 驗證。 值為**0**您必須指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@publisher_login =** ] **'***publisher_login***'**  
 這是連接到發行者時所用的登入。 *publisher_login*已**sysname**，預設值是 NULL。 *publisher_login*時，必須指定*publisher_security_mode*是**0**。 如果*publisher_login*為 NULL 並*publisher_security_mode*是**1**，在指定的 Windows 帳戶*job_login*時使用連接到發行者。  
  
 [  **@publisher_password =** ] **'***publisher_password***'**  
 這是連接到發行者時所用的密碼。 *publisher_password*已**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
 [ **@job_login** =] **'***job_login***'**  
 這是用來執行代理程式之 Windows 帳戶的登入。 *job_login*已**nvarchar(257)**，預設值是 NULL。 通往散發者的代理程式連接一律使用這個 Windows 帳戶。 您必須在建立新的快照集代理程式作業時，提供這個參數。 無法變更非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
 [  **@job_password =** ] **'***job_password***'**  
 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password*已**sysname**，預設值是 NULL。 您必須在建立新的快照集代理程式作業時，提供這個參數。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
 [  **@publisher =** ] **'***發行者***'**  
 指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應建立在快照集代理程式時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changepublication_snapshot**用於快照式複寫、 異動複寫和合併式複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_changepublication_snapshot**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication_snapshot &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
