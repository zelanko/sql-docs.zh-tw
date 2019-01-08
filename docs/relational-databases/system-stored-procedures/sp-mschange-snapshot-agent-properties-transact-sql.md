---
title: sp_MSchange_snapshot_agent_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_snapshot_agent_properties_TSQL
- sp_MSchange_snapshot_agent_properties
helpviewer_keywords:
- sp_MSchange_snapshot_agent_properties
ms.assetid: 7947a788-3fd7-469f-84db-b03ba89a153c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4a4c8eb45ad7864466ccedc3de5b034325279322
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2018
ms.locfileid: "53589752"
---
# <a name="spmschangesnapshotagentproperties-transact-sql"></a>sp_MSchange_snapshot_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更會在執行快照集代理程式作業的屬性[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更新版本散發者。 這個預存程序用來變更屬性，當 「 發行者 」 端執行的執行個體上[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。 這個預存程序執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_MSchange_snapshot_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @frequency_type= ] frequency_type  
        , [ @frequency_interval= ] frequency_interval  
        , [ @frequency_subday= ] frequency_subday  
        , [ @frequency_subday_interval= ] frequency_subday_interval  
        , [ @frequency_relative_interval= ] frequency_relative_interval  
        , [ @frequency_recurrence_factor= ] frequency_recurrence_factor  
        , [ @active_start_date= ] active_start_date  
        , [ @active_end_date= ] active_end_date  
        , [ @active_start_time_of_day= ] active_start_time_of_day  
        , [ @active_end_time_of_day= ] active_end_time_of_day  
        , [ @snapshot_job_name = ] 'snapshot_agent_name'  
        , [ @publisher_security_mode = ] publisher_security_mode  
        , [ @publisher_login = ] 'publisher_login'  
        , [ @publisher_password = ] 'publisher_password'   
        , [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
        , [ @publisher_type = ] 'publisher_type'  
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher** =] **'**_發行者_**'**  
 這是發行者的名稱。 *發行者*已**sysname**，沒有預設值。  
  
 [  **@publisher_db=** ] **'**_publisher_db_**'**  
 這是發行集資料庫的名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
 [  **@publication =** ] **'**_發行集_**'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@frequency_type =** ] *frequency_type*  
 這是快照集代理程式的執行頻率。 *frequency_type*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|視需要|  
|**4**|每日|  
|**8**|每週|  
|**10**|每月|  
|**20**|每月，相對於頻率間隔|  
|**40**|當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟動時|  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 要套用至所設定之頻率的值*frequency_type*。 *frequency_interval*已**int**，沒有預設值。  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 單位*freq_subday_interval*。 *frequency_subday*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 間隔*frequency_subday*。 *frequency_subday_interval*已**int**，沒有預設值。  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 這是快照集代理程式的執行日期。 *frequency_relative_interval*已**int**，沒有預設值。  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor&lt*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*已**int**，沒有預設值。  
  
 [ **@active_start_date =** ] *active_start_date*  
 這是第一次排程快照集代理程式的日期，格式為 YYYYMMDD。 *active_start_date*已**int**，沒有預設值。  
  
 [ **@active_end_date =** ] *active_end_date*  
 這是排程停止快照集代理程式的日期，格式為 YYYYMMDD。 *active_end_date*已**int**，沒有預設值。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 這是第一次排程快照集代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*已**int**，沒有預設值。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 這是排程停止快照集代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*已**int**，沒有預設值。  
  
 [  **@snapshot_job_name =** ] **'**_snapshot_agent_name_**'**  
 這是在使用現有作業時，現有快照集代理程式作業的名稱。 *snapshot_agent_name*已**nvarchar(100)**，沒有預設值。  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 這是當連接到發行者時使用的安全性模式。 *publisher_security_mode*已**int**，沒有預設值。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證，並**1**指定 Windows 驗證。 值為**0**您必須指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [ **@publisher_login**=] **'**_publisher_login_**'**  
 這是連接到發行者時所用的登入。 *publisher_login*已**sysname**，沒有預設值。 *publisher_login*時，必須指定*publisher_security_mode*是**0**。 如果*publisher_login*是 NULL，publisher *_ * * security_mode*會**1**，然後在指定的 Windows 帳戶*job_login*會連接到發行者時使用。  
  
 [ **@publisher_password**=] **'**_publisher_password_**'**  
 這是連接到發行者時所用的密碼。 *publisher_password*已**nvarchar(524)**，沒有預設值。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 若要改善安全性，我們建議您在執行階段提供登入名稱和密碼。  
  
 [ **@job_login**=] **'**_job_login_**'**  
 這是用來執行代理程式之 Windows 帳戶的登入。 *job_login*已**nvarchar(257)**，沒有預設值。 通往散發者的代理程式連接一律使用這個 Windows 帳戶。 您必須在建立新的快照集代理程式作業時，提供這個參數。 *無法變更為非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *發行者。*  
  
 [ **@job_password**=] **'**_job_password_**'**  
 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password*已**sysname**，沒有預設值。 您必須在建立新的快照集代理程式作業時，提供這個參數。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 若要改善安全性，我們建議您在執行階段提供登入名稱和密碼。  
  
 [ **@publisher_type**=] **'**_publisher_type_**'**  
 指定當發行者不是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中執行時的發行者類型。 *publisher_type*已**sysname**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。|  
|**ORACLE**|指定標準 Oracle 發行者。|  
|**ORACLE GATEWAY**|指定 Oracle Gateway 發行者。|  
  
 如需有關 Oracle 發行者 」 與 「 Oracle Gateway 發行者之間的差異的詳細資訊，請參閱 < [Oracle 發行概觀](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_MSchange_snapshot_agent_properties**用於快照式複寫、 異動複寫和合併式複寫。  
  
 執行時，您必須指定所有參數**sp_MSchange_snapshot_agent_properties**。 執行[sp_helppublication_snapshot](../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md)來傳回目前快照集代理程式作業的屬性。  
  
 當 「 發行者 」 端執行的執行個體上[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更新版本，您應該使用[sp_changepublication_snapshot](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)若要變更快照集代理程式作業的屬性。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**散發者端的固定的伺服器角色可以執行**sp_MSchange_snapshot_agent_properties**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
  
