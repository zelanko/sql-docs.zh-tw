---
title: sp_helpmergepullsubscription （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepullsubscription
- sp_helpmergepullsubscription_TSQL
helpviewer_keywords:
- sp_helpmergepullsubscription
ms.assetid: 6f3125f3-0dfa-40bd-b725-8aa1591234f6
author: stevestein
ms.author: sstein
ms.openlocfilehash: c92ea8e2f172d9cb5b40559c2a7b77a60153065b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68137706"
---
# <a name="sp_helpmergepullsubscription-transact-sql"></a>sp_helpmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回存在於訂閱者端之提取訂閱的相關資訊。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpmergepullsubscription [ [ @publication=] 'publication']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
```  
  
## <a name="argument"></a>引數  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，預設值是**%**。 如果*發行*集**%** 為，則會傳回目前資料庫中所有合併式發行集和訂閱的相關資訊。  
  
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**，預設值是**%**。  
  
`[ @publisher_db = ] 'publisher_db'`這是發行者資料庫的名稱。 *publisher_db*是**sysname**，預設值是**%**。  
  
`[ @subscription_type = ] 'subscription_type'`這是指是否要顯示提取訂閱。 *subscription_type*是**Nvarchar （10）**，預設值是 **' pull '**。 有效的值為 **' push '**、 **' pull '** 或 **' both '**。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**Nvarchar （1000）**|訂用帳戶的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**發行者**|**sysname**|發行者的名稱。|  
|**publisher_db**|**sysname**|發行者資料庫的名稱。|  
|**預訂**|**sysname**|訂閱者的名稱。|  
|**subscription_db**|**sysname**|訂閱資料庫的名稱。|  
|**狀態**|**int**|訂閱狀態：<br /><br /> **0** = 非使用中的訂用帳戶<br /><br /> **1** = 使用中的訂用帳戶<br /><br /> **2** = 已刪除的訂用帳戶<br /><br /> **3** = 卸離訂閱<br /><br /> **4** = 附加的訂用帳戶<br /><br /> **5** = 訂用帳戶已標示為要重新初始化，使用上傳<br /><br /> **6** = 附加訂閱失敗<br /><br /> **7** = 從備份還原的訂用帳戶|  
|**subscriber_type**|**int**|訂閱者的類型：<br /><br /> **1** = 全域<br /><br /> **2** = 本機<br /><br /> **3** = 匿名|  
|**subscription_type**|**int**|訂閱的類型：<br /><br /> **0** = 推播<br /><br /> **1** = 提取<br /><br /> **2** = 匿名|  
|**優先順序**|**float （8）**|訂閱優先權。 此值必須小於**100.00**。|  
|**sync_type**|**tinyint**|訂閱同步處理類型：<br /><br /> **1** = 自動<br /><br /> **2** = 不使用快照集。|  
|**描述**|**nvarchar(255)**|這項提取訂閱的簡要描述。|  
|**merge_jobid**|**binary （16）**|合併代理程式的作業識別碼。|  
|**enabled_for_syncmgr**|**int**|是否能夠利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Synchronization Manager 同步處理訂閱。|  
|**last_updated**|**Nvarchar （26）**|合併代理程式上次成功進行訂閱同步處理的時間。|  
|**publisher_login**|**sysname**|發行者的登入名稱。|  
|**publisher_password**|**sysname**|發行者密碼。|  
|**publisher_security_mode**|**int**|指定發行者的安全性模式。<br /><br /> ****  =  0[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證<br /><br /> **1** = Windows 驗證|  
|**伺服器**|**sysname**|散發者的名稱。|  
|**distributor_login**|**sysname**|散發者的登入名稱。|  
|**distributor_password**|**sysname**|散發者密碼。|  
|**distributor_security_mode**|**int**|指定散發者的安全性模式。<br /><br /> ****  =  0[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證<br /><br /> **1** = Windows 驗證|  
|**ftp_address**|**sysname**|使用這個項目的目的，只是為了與舊版相容。 這是散發者的檔案傳輸通訊協定 (FTP) 服務的網路位址。|  
|**ftp_port**|**int**|使用這個項目的目的，只是為了與舊版相容。 這是散發者的 FTP 服務通訊埠編號。|  
|**ftp_login**|**sysname**|使用這個項目的目的，只是為了與舊版相容。 這是用於連接到 FTP 服務的使用者名稱。|  
|**ftp_password**|**sysname**|使用這個項目的目的，只是為了與舊版相容。 這是用來連接到 FTP 服務的使用者密碼。|  
|**alt_snapshot_folder**|**nvarchar(255)**|當位置不是預設位置，或在預設位置之外還有其他位置時，快照集資料夾的儲存位置。|  
|**working_directory**|**nvarchar(255)**|當指定利用 FTP 來傳送快照集檔案的選項時，傳送快照集檔案之目錄的完整路徑。|  
|**use_ftp**|**bit**|訂閱是透過網際網路來訂閱發行集，並設定 FTP 定址屬性。 如果是**0**，訂閱就不會使用 FTP。 如果是**1**，訂閱會使用 FTP。|  
|**offload_agent**|**bit**|指定是否能從遠端啟動並執行代理程式。 如果是**0**，就無法從遠端啟動代理程式。|  
|**offload_server**|**sysname**|遠端啟用伺服器的名稱。|  
|**use_interactive_resolver**|**int**|傳回是否在重新調整期間使用互動式解析程式。 如果是**0**，則不會使用互動式解析程式。|  
|**subid**|**uniqueidentifier**|訂閱者的識別碼。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|儲存快照集檔案之資料夾的路徑。|  
|**last_sync_status**|**int**|同步處理狀態：<br /><br /> **1** = 正在啟動<br /><br /> **2** = 成功<br /><br /> **3** = 進行中<br /><br /> **4** = 閒置<br /><br /> **5** = 在上一次失敗後重試<br /><br /> **6** = 失敗<br /><br /> **7** = 驗證失敗<br /><br /> **8** = 通過驗證<br /><br /> **9** = 要求關閉|  
|**last_sync_summary**|**sysname**|上次同步處理結果的描述。|  
|**use_web_sync**|**bit**|指定訂用帳戶是否可以透過 HTTPS 進行同步處理，其中**1**值表示已啟用這項功能。|  
|**internet_url**|**nvarchar(260)**|代表 Web 同步處理之複寫接聽程式位置的 URL。|  
|**internet_login**|**nvarchar(128)**|當利用基本驗證來連接到主控 Web 同步處理的 Web 伺服器時，合併代理程式所用的登入。|  
|**internet_password**|**Nvarchar （524）**|當利用基本驗證來連接到主控 Web 同步處理的 Web 伺服器時，合併代理程式所用的登入密碼。|  
|**internet_security_mode**|**int**|當連接到主控 Web 同步處理的 Web 伺服器時，使用驗證模式。 值為**1**表示 Windows 驗證，值為**0**表示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。|  
|**internet_timeout**|**int**|Web 同步處理要求到期之前的時間長度 (以秒為單位)。|  
|**名稱**|**nvarchar(128)**|指定在參數化資料列篩選的 WHERE 子句中使用這個函數時， [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)的多載值。|  
|**job_login**|**nvarchar(512)**|這是用來執行合併代理程式的 Windows 帳戶，傳回的格式為*domain*\\*username*。|  
|**job_password**|**sysname**|基於安全性理由，一律會傳回**\*\*\*\*\*\*\*\*"\***" 的值。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpmergepullsubscription**用於合併式複寫中。 在結果集中， **last_updated**中傳回的日期格式為*YYYYMMDD hh： mm： ss. fff*。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色和**db_owner**固定資料庫角色的成員，才能夠執行**sp_helpmergepullsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
