---
title: sp_MSchange_snapshot_agent_properties （T-sql）
description: 描述用來變更用於 SQL Server 複寫之快照集代理程式屬性的 sp_MSchange_snapshot_agent_properties 預存程式。
ms.custom: seo-lt-2019
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
ms.openlocfilehash: 6c5c3c2573465072de0d1f0a7c08d47df5d387b6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "75321796"
---
# <a name="sp_mschange_snapshot_agent_properties-transact-sql"></a>sp_MSchange_snapshot_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更新版本散發者上執行之快照集代理程式作業的屬性。 當發行者執行於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的執行個體時，系統會利用這個預存程序來變更屬性。 這個預存程序執行於散發資料庫的散發者端。  
  
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
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'`這是發行集資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @frequency_type = ] frequency_type`這是執行快照集代理程式的頻率。 *frequency_type*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**2**|隨選|  
|**4**|每日|  
|**8**|每週|  
|**10**|每月|  
|**20**|每月，相對於頻率間隔|  
|**40**|當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟動時|  
  
`[ @frequency_interval = ] frequency_interval`這是要套用至*frequency_type*所設定之頻率的值。 *frequency_interval*是**int**，沒有預設值。  
  
`[ @frequency_subday = ] frequency_subday`這是*freq_subday_interval*的單位。 *frequency_subday*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`這是*frequency_subday*的間隔。 *frequency_subday_interval*是**int**，沒有預設值。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`這是快照集代理程式執行的日期。 *frequency_relative_interval*是**int**，沒有預設值。  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`這是*frequency_type*所使用的迴圈因數。 *frequency_recurrence_factor*是**int**，沒有預設值。  
  
`[ @active_start_date = ] active_start_date`這是第一次排程快照集代理程式的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，沒有預設值。  
  
`[ @active_end_date = ] active_end_date`這是排程停止快照集代理程式的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，沒有預設值。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`這是第一次排程快照集代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，沒有預設值。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`這是排程停止快照集代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，沒有預設值。  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'`如果正在使用現有的作業，則為現有快照集代理程式作業名稱的名稱。 *snapshot_agent_name*是**Nvarchar （100）**，沒有預設值。  
  
`[ @publisher_security_mode = ] publisher_security_mode`這是連接到發行者時，代理程式所使用的安全性模式。 *publisher_security_mode*是**int**，沒有預設值。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證， **1**指定 Windows 驗證。 非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者必須指定**0**的值。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`這是連接到發行者時所使用的登入。 *publisher_login*是**sysname**，沒有預設值。 當*publisher_security_mode*為**0**時，必須指定*publisher_login* 。 如果*publisher_login*是 Null，而發行者 *_ * * security_mode*是**1**，則連接到發行者時，將會使用*job_login*中指定的 Windows 帳戶。  
  
`[ @publisher_password = ] 'publisher_password'`這是連接到發行者時所使用的密碼。 *publisher_password*是**Nvarchar （524）**，沒有預設值。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 若要改善安全性，我們建議您在執行階段提供登入名稱和密碼。  
  
`[ @job_login = ] 'job_login'`這是用來執行代理程式之 Windows 帳戶的登入。 *job_login*是**Nvarchar （257）**，沒有預設值。 通往散發者的代理程式連接一律使用這個 Windows 帳戶。 您必須在建立新的快照集代理程式作業時，提供這個參數。 *這無法針對非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *發行者*進行變更。  
  
`[ @job_password = ] 'job_password'`這是執行代理程式之 Windows 帳戶的密碼。 *job_password*是**sysname**，沒有預設值。 您必須在建立新的快照集代理程式作業時，提供這個參數。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 若要改善安全性，我們建議您在執行階段提供登入名稱和密碼。  
  
`[ @publisher_type = ] 'publisher_type'`當發行者不是在實例中執行時，指定發行者類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 *publisher_type*是**sysname**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。|  
|**ORACLE**|指定標準 Oracle 發行者。|  
|**ORACLE GATEWAY**|指定 Oracle Gateway 發行者。|  
  
 如需有關「Oracle 發行者」與「Oracle 閘道發行者」之間差異的詳細資訊，請參閱[Oracle 發行總覽](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_MSchange_snapshot_agent_properties**用於快照式複寫、異動複寫和合併式複寫中。  
  
 執行**sp_MSchange_snapshot_agent_properties**時，您必須指定所有參數。 執行[sp_helppublication_snapshot](../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md)以傳回快照集代理程式作業的目前屬性。  
  
 當發行者在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更新版本的實例上執行時，您應該使用[sp_changepublication_snapshot](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)來變更快照集代理程式作業的屬性。  
  
## <a name="permissions"></a>權限  
 只有在散發者端的**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_MSchange_snapshot_agent_properties**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
  
