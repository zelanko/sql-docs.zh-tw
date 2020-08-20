---
description: sp_addpublication_snapshot (Transact-SQL)
title: sp_addpublication_snapshot (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 764147434455852ef09fa70768b3b71d68cc913c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489614"
---
# <a name="sp_addpublication_snapshot-transact-sql"></a>sp_addpublication_snapshot (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

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
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @frequency_type = ] frequency_type` 這是執行快照集代理程式的頻率。 *frequency_type* 是 **int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次。|  
|**4** (預設) |每天。|  
|**8**|每週。|  
|**16**|每月。|  
|**32**|每月，相對於頻率間隔。|  
|**64**|當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟動時。|  
|**128**|在電腦閒置之時執行|  
  
`[ @frequency_interval = ] frequency_interval` 這是要套用至 *frequency_type*所設定之頻率的值。 *frequency_interval* 是 **int**，而且可以是下列其中一個值。  
  
|frequency_type 的值|對 frequency_interval 的作用|  
|------------------------------|-----------------------------------|  
|**1**|*frequency_interval* 未使用。|  
|**4** (預設) |每 *frequency_interval* 天，預設值為 [每日]。|  
|**8**|*frequency_interval* 是下列一或多個 (與 [&#124; (位或) ](../../t-sql/language-elements/bitwise-or-transact-sql.md) 邏輯運算子) 結合：<br /><br /> **1** = 星期日 &#124;<br /><br /> **2** = 星期一 &#124;<br /><br /> **4** = 星期二 &#124;<br /><br /> **8** = 星期三 &#124;<br /><br /> **16** = 星期四 &#124;<br /><br /> **32** = 星期五 &#124;<br /><br /> **64** = 星期六|  
|**16**|在當月的 *frequency_interval* 日。|  
|**32**|*frequency_interval* 是下列其中一項：<br /><br /> **1** = 星期日 &#124;<br /><br /> **2** = 星期一 &#124;<br /><br /> **3** = 星期二 &#124;<br /><br /> **4** = 星期三 &#124;<br /><br /> **5** = 星期四 &#124;<br /><br /> **6** = 星期五 &#124;<br /><br /> **7** = 星期六 &#124;<br /><br /> **8** = 天 &#124;<br /><br /> **9** = 工作日 &#124;<br /><br /> **10** = 週末日|  
|**64**|*frequency_interval* 未使用。|  
|**128**|*frequency_interval* 未使用。|  
  
`[ @frequency_subday = ] frequency_subday` 這是 *freq_subday_interval*的單位。 *frequency_subday* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**2**|Second|  
|**4** (預設) |Minute|  
|**8**|小時|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 這是 *frequency_subday*的間隔。 *frequency_subday_interval* 是 **int**，預設值是5，表示每5分鐘一次。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 這是快照集代理程式執行的日期。 *frequency_relative_interval* 是 **int**，預設值是1。  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 這是 *frequency_type*所用的迴圈因數。 *frequency_recurrence_factor* 是 **int**，預設值是0。  
  
`[ @active_start_date = ] active_start_date` 這是第一次排程快照集代理程式的日期，格式為 YYYYMMDD。 *active_start_date* 是 **int**，預設值是0。  
  
`[ @active_end_date = ] active_end_date` 這是排程停止快照集代理程式的日期，格式為 YYYYMMDD。 *active_end_date* 是 **int**，預設值是99991231，這表示9999年12月31日。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 這是第一次排程快照集代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day* 是 **int**，預設值是0。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 這是排程快照集代理程式停止的當日時間，格式為 HHMMSS。 *active_end_time_of_day* 是 **int**，預設值是235959，表示 11:59:59 P.M。 。  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'` 如果正在使用現有的作業，這是現有快照集代理程式作業名稱的名稱。 *snapshot_agent_name* 是 **Nvarchar (100) ** 預設值為 Null。 這個參數供內部使用，當建立新的發行集時，不應指定。 如果指定 *snapshot_agent_name* ，則 *job_login* 和 *job_password* 必須是 Null。  
  
`[ @publisher_security_mode = ] publisher_security_mode` 這是連接到發行者時，代理程式所使用的安全性模式。 *publisher_security_mode* 是 **Smallint**，預設值是1。 **0** 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證， **1** 指定 Windows 驗證。 必須針對非發行者指定 **0** 的值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` 這是連接到發行者時所用的登入。 *publisher_login* 是 **sysname**，預設值是 Null。 當*publisher_security_mode*為**0**時，必須指定*publisher_login* 。 如果 *publisher_login* 為 Null，且 *publisher_security_mode* 是 **1**，則在連接到發行者時，將會使用 *job_login* 中指定的帳號。  
  
`[ @publisher_password = ] 'publisher_password'` 這是連接到發行者時所使用的密碼。 *publisher_password* 是 **sysname**，預設值是 Null。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 若要改善安全性，我們建議您在執行階段提供登入名稱和密碼。  
  
`[ @job_login = ] 'job_login'` 這是用來執行代理程式之帳戶的登入。 在 Azure SQL 受控執行個體上，請使用 SQL Server 帳戶。 *job_login* 是 **Nvarchar (257) **，預設值是 Null。 此帳戶一律用於散發者的代理程式連接。 您必須在建立新的快照集代理程式作業時，提供這個參數。  
  
> [!NOTE]
>  如果是非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者，這必須是 [Sp_adddistpublisher &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)中指定的相同登入。  
  
`[ @job_password = ] 'job_password'` 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password* 是 **sysname**，沒有預設值。 您必須在建立新的快照集代理程式作業時，提供這個參數。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 若要改善安全性，我們建議您在執行階段提供登入名稱和密碼。  
  
`[ @publisher = ] 'publisher'` 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *publisher* 是 **sysname**，預設值是 Null。  
  
> [!NOTE]  
>  在發行者端建立快照集代理程式時，不應使用「*發行者*」 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_addpublication_snapshot** 用於快照式複寫、異動複寫和合併式複寫中。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_addpublication_snapshot**。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [建立並套用快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [sp_addpublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication_snapshot &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_startpublication_snapshot &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
