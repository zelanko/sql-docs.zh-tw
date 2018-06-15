---
title: sp_helppullsubscription (TRANSACT-SQL) |Microsoft 文件
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
- sp_helppullsubscription_TSQL
- sp_helppullsubscription
helpviewer_keywords:
- sp_helppullsubscription
ms.assetid: a0d9c3f1-1fe9-497c-8e2f-5b74f47a7346
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ada01ed2c7e447077026e65a9ca5776911b14dcd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33003615"
---
# <a name="sphelppullsubscription-transact-sql"></a>sp_helppullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示在訂閱者端的一或多項訂閱的相關資訊。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helppullsubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @show_push = ] 'show_push' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher=**] **'***publisher***'**  
 這是遠端伺服器的名稱。 *發行者*是**sysname**，預設值是**%**，它會傳回所有發行者的資訊。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*是**sysname**，預設值是**%**，它會傳回所有發行者資料庫。  
  
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*是**sysname**，預設值是**%**，它會傳回所有發行集。 如果這個參數等於 ALL，提取訂閱 independent_agent = **0**會傳回。  
  
 [  **@show_push=**] **'***show_push***'**  
 這是指是否傳回所有發送訂閱。 *show_push*是**nvarchar （5)**，預設值是 FALSE，這不會傳回發送訂閱。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**發行者**|**sysname**|發行者的名稱。|  
|**發行者資料庫**|**sysname**|發行者資料庫的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**independent_agent**|**bit**|指出這個發行集是否有獨立的散發代理程式。|  
|**訂用帳戶類型**|**int**|發行集的訂閱類型。|  
|**散發代理程式**|**nvarchar(100)**|處理訂閱的散發代理程式。|  
|**發行集的描述**|**nvarchar(255)**|發行集的描述。|  
|**上次更新時間**|**date**|更新訂閱資訊的時間。 這是 ISO 日期 (114) + ODBC 時間 (121) 的 UNICODE 字串。 格式為 yyyymmdd hh:mi:sss.mmm，其中 'yyyy' 是年份，'mm' 是月份，'dd' 是日期，'hh' 是小時，'mi' 是分鐘，'sss' 是秒鐘，'mmm' 是毫秒。|  
|**訂用帳戶名稱**|**varchar(386)**|訂閱的名稱。|  
|**上次交易時間戳記**|**varbinary(16)**|最後一次複寫交易的時間戳記。|  
|**更新模式**|**tinyint**|允許的更新類型。|  
|**散發代理程式 job_id**|**int**|散發代理程式的作業識別碼。|  
|**enabled_for_synmgr**|**int**|是否能夠利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Synchronization Manager 同步處理訂閱。|  
|**訂用帳戶 guid**|**binary(16)**|發行集訂閱版本的全域識別碼。|  
|**subid**|**binary(16)**|匿名訂閱的全域識別碼。|  
|**immediate_sync**|**bit**|每次執行快照集代理程式時，是否要建立或重新建立同步處理檔案。|  
|**發行者登入**|**sysname**|用於發行者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼。|  
|**發行者密碼**|**nvarchar （524)**|用於發行者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼 (加密)。|  
|**發行者 security_mode**|**int**|在發行者端實作的安全性模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證<br /><br /> **1** = Windows 驗證<br /><br /> **2** = 同步處理觸發程序利用靜態**sysservers**項目來執行遠端程序呼叫 (RPC)，和*發行者*必須定義在**sysservers**資料表做為遠端伺服器或連結的伺服器。|  
|**散發者**|**sysname**|散發者的名稱。|  
|**distributor_login**|**sysname**|用於散發者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼。|  
|**distributor_password**|**nvarchar （524)**|用於散發者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼 (加密)。|  
|**distributor_security_mode**|**int**|在散發者端實作的安全性模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證<br /><br /> **1** = Windows 驗證|  
|**ftp_address**|**sysname**|只是為了與舊版相容。|  
|**ftp_port**|**int**|只是為了與舊版相容。|  
|**ftp_login**|**sysname**|只是為了與舊版相容。|  
|**ftp_password**|**nvarchar （524)**|只是為了與舊版相容。|  
|**alt_snapshot_folder**|**nvarchar(255)**|當位置不是預設位置，或在預設位置之外還有其他位置時，快照集資料夾的儲存位置。|  
|**working_directory**|**nvarchar(255)**|當指定利用檔案傳輸通訊協定 (FTP) 來傳送快照集檔案的選項時，傳送快照集檔案之目錄的完整路徑。|  
|**use_ftp**|**bit**|訂閱是透過網際網路來訂閱發行集，並設定 FTP 定址屬性。 如果**0**，訂閱便不會使用 FTP。 如果**1**，訂閱便使用 FTP。|  
|**publication_type**|**int**|指定發行集的複寫類型：<br /><br /> **0** = 異動複寫<br /><br /> **1** = 快照式複寫<br /><br /> **2** = 合併式複寫|  
|**dts_package_name**|**sysname**|指定 Data Transformation Services (DTS) 封裝的名稱。|  
|**dts_package_location**|**int**|DTS 封裝的儲存位置：<br /><br /> **0** = 散發者<br /><br /> **1** = 訂閱者|  
|**offload_agent**|**bit**|指定是否能從遠端啟動代理程式。 如果**0**，無法從遠端啟動代理程式。|  
|**offload_server**|**sysname**|指定遠端啟用所用之伺服器的網路名稱。|  
|**last_sync_status**|**int**|訂閱狀態：<br /><br /> **0** = 所有作業都在等待啟動<br /><br /> **1** = 一或多個作業都在啟動<br /><br /> **2** = 所有作業都已執行成功<br /><br /> **3** = 至少一個作業正在執行<br /><br /> **4** = 所有作業都已排程且閒置<br /><br /> **5** = 至少一個工作嘗試在上一次失敗之後執行<br /><br /> **6** = 至少一個工作已順利執行失敗|  
|**last_sync_summary**|**sysname**|上次同步處理結果的描述。|  
|**last_sync_time**|**datetime**|更新訂閱資訊的時間。 這是 ISO 日期 (114) + ODBC 時間 (121) 的 UNICODE 字串。 格式為 yyyymmdd hh:mi:sss.mmm，其中 'yyyy' 是年份，'mm' 是月份，'dd' 是日期，'hh' 是小時，'mi' 是分鐘，'sss' 是秒鐘，'mmm' 是毫秒。|  
|**job_login**|**nvarchar(512)**|Windows 帳戶的散發代理程式執行，這傳回的格式如下*網域*\\*username*。|  
|**job_password**|**sysname**|基於安全性理由，值為"**\*\*\*\*\*\*\*\*\*\***」 是一律傳回。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helppullsubscription**用於快照式和異動複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_helppullsubscription** 。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addpullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_droppullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
