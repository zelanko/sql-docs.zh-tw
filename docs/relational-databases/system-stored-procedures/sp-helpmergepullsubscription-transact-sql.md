---
title: sp_helpmergepullsubscription (TRANSACT-SQL) |Microsoft Docs
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
- sp_helpmergepullsubscription
- sp_helpmergepullsubscription_TSQL
helpviewer_keywords:
- sp_helpmergepullsubscription
ms.assetid: 6f3125f3-0dfa-40bd-b725-8aa1591234f6
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 65c0ab3d3b5766c2e4cf4878fe81707295c01120
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43024266"
---
# <a name="sphelpmergepullsubscription-transact-sql"></a>sp_helpmergepullsubscription (Transact-SQL)
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
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*已**sysname**，預設值是**%**。 如果*出版物*是**%**，會傳回所有合併式發行集和目前的資料庫中的訂用帳戶的相關資訊。  
  
 [ **@publisher=**] **'***publisher***'**  
 這是發行者的名稱。 *發行者*已**sysname**，預設值是**%**。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*已**sysname**，預設值是**%**。  
  
 [  **@subscription_type=**] **'***subscription_type***'**  
 指出是否要顯示提取訂閱。 *subscription_type*已**nvarchar(10**，預設值是 **'pull'**。 有效值 **'push'**， **'pull'**，或 **'both'**。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**nvarchar(1000)**|訂閱的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**發行者**|**sysname**|發行者的名稱。|  
|**publisher_db**|**sysname**|發行者資料庫的名稱。|  
|**訂閱者**|**sysname**|訂閱者的名稱。|  
|**subscription_db**|**sysname**|訂閱資料庫的名稱。|  
|**status**|**int**|訂閱狀態：<br /><br /> **0** = 非使用中的訂用帳戶<br /><br /> **1** = 作用中訂用帳戶<br /><br /> **2** = 已刪除的訂用帳戶<br /><br /> **3** = 中斷連結的訂用帳戶<br /><br /> **4** = 附加的訂閱<br /><br /> **5** = 訂閱被標示為重新初始化使用 上傳<br /><br /> **6** = 的附加訂閱失敗<br /><br /> **7** = 從備份還原的訂用帳戶|  
|**subscriber_type**|**int**|訂閱者的類型：<br /><br /> **1** = 全域<br /><br /> **2** = 本機<br /><br /> **3** = 匿名|  
|**subscription_type**|**int**|訂閱的類型：<br /><br /> **0** = 發送<br /><br /> **1** = 提取<br /><br /> **2** = 匿名|  
|**priority**|**float(8)**|訂閱優先權。 此值必須是小於**100.00**。|  
|**sync_type**|**tinyint**|訂閱同步處理類型：<br /><br /> **1** = 自動<br /><br /> **2** = 不使用快照集。|  
|**description**|**nvarchar(255)**|這項提取訂閱的簡要描述。|  
|**merge_jobid**|**binary(16)**|合併代理程式的作業識別碼。|  
|**enabled_for_syncmgr**|**int**|是否能夠利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Synchronization Manager 同步處理訂閱。|  
|**last_updated**|**nvarchar(26)**|合併代理程式上次成功進行訂閱同步處理的時間。|  
|**publisher_login**|**sysname**|發行者的登入名稱。|  
|**publisher_password**|**sysname**|發行者密碼。|  
|**publisher_security_mode**|**int**|指定發行者的安全性模式。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證<br /><br /> **1** = Windows 驗證|  
|**散發者**|**sysname**|散發者的名稱。|  
|**distributor_login**|**sysname**|散發者的登入名稱。|  
|**distributor_password**|**sysname**|散發者密碼。|  
|**distributor_security_mode**|**int**|指定散發者的安全性模式。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證<br /><br /> **1** = Windows 驗證|  
|**ftp_address**|**sysname**|使用這個項目的目的，只是為了與舊版相容。 這是散發者的檔案傳輸通訊協定 (FTP) 服務的網路位址。|  
|**ftp_port**|**int**|使用這個項目的目的，只是為了與舊版相容。 這是散發者的 FTP 服務通訊埠編號。|  
|**ftp_login**|**sysname**|使用這個項目的目的，只是為了與舊版相容。 這是用於連接到 FTP 服務的使用者名稱。|  
|**ftp_password**|**sysname**|使用這個項目的目的，只是為了與舊版相容。 這是用來連接到 FTP 服務的使用者密碼。|  
|**alt_snapshot_folder**|**nvarchar(255)**|當位置不是預設位置，或在預設位置之外還有其他位置時，快照集資料夾的儲存位置。|  
|**working_directory**|**nvarchar(255)**|當指定利用 FTP 來傳送快照集檔案的選項時，傳送快照集檔案之目錄的完整路徑。|  
|**use_ftp**|**bit**|訂閱是透過網際網路來訂閱發行集，並設定 FTP 定址屬性。 如果**0**，訂用帳戶不使用 FTP。 如果**1**，訂閱便使用 FTP。|  
|**offload_agent**|**bit**|指定是否能從遠端啟動並執行代理程式。 如果**0**，無法從遠端啟動代理程式。|  
|**offload_server**|**sysname**|遠端啟用伺服器的名稱。|  
|**use_interactive_resolver**|**int**|傳回是否在重新調整期間使用互動式解析程式。 如果**0**，不使用互動式解析程式。|  
|**subid**|**uniqueidentifier**|訂閱者的識別碼。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|儲存快照集檔案之資料夾的路徑。|  
|**last_sync_status**|**int**|同步處理狀態：<br /><br /> **1** = 啟動<br /><br /> **2** = 成功<br /><br /> **3** = 進行中<br /><br /> **4** = 閒置<br /><br /> **5** = 正在重試之後上一次的失敗<br /><br /> **6** = 失敗<br /><br /> **7** = 驗證失敗<br /><br /> **8** = 驗證通過<br /><br /> **9** = 已要求關機|  
|**last_sync_summary**|**sysname**|上次同步處理結果的描述。|  
|**use_web_sync&lt**|**bit**|如果訂用帳戶可以同步處理，透過 HTTPS 的值**1**表示啟用這項功能。|  
|**應**|**nvarchar(260)**|代表 Web 同步處理之複寫接聽程式位置的 URL。|  
|**internet_url**|**nvarchar(128)**|當利用基本驗證來連接到主控 Web 同步處理的 Web 伺服器時，合併代理程式所用的登入。|  
|**internet_login**|**nvarchar(524)**|當利用基本驗證來連接到主控 Web 同步處理的 Web 伺服器時，合併代理程式所用的登入密碼。|  
|**internet_security_mode**|**int**|當連接到主控 Web 同步處理的 Web 伺服器時，使用驗證模式。 值為**1**表示 Windows 驗證，並針對**0**表示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。|  
|**internet_timeout**|**int**|Web 同步處理要求到期之前的時間長度 (以秒為單位)。|  
|**主機名稱**|**nvarchar(128)**|指定的值是多載[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)參數化資料列篩選的 WHERE 子句中使用此函式時。|  
|**job_login**|**nvarchar(512)**|是 Windows 帳戶在其下執行合併代理程式，這傳回的格式如下*網域*\\*username*。|  
|**job_password**|**sysname**|基於安全性理由，值為"**\*\*\*\*\*\*\*\*\*\***」 是一律傳回。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpmergepullsubscription**用於合併式複寫中。 在結果集中，傳回的日期**last_updated**格式化成*YYYYMMDD hh:mm:ss.fff*。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色並**db_owner**固定的資料庫角色可以執行**sp_helpmergepullsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addmergepullsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
