---
description: sp_helppullsubscription (Transact-SQL)
title: sp_helppullsubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppullsubscription_TSQL
- sp_helppullsubscription
helpviewer_keywords:
- sp_helppullsubscription
ms.assetid: a0d9c3f1-1fe9-497c-8e2f-5b74f47a7346
author: markingmyname
ms.author: maghan
ms.openlocfilehash: abad011197d58876915ce242c4c38198b13105ab
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535171"
---
# <a name="sp_helppullsubscription-transact-sql"></a>sp_helppullsubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

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
`[ @publisher = ] 'publisher'` 這是遠端伺服器的名稱。 *publisher* 是 **sysname**，預設值是 **%** ，它會傳回所有發行者的資訊。  
  
`[ @publisher_db = ] 'publisher_db'` 這是發行者資料庫的名稱。 *publisher_db* 是 **sysname**，預設值是 **%** ，它會傳回所有發行者資料庫。  
  
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，預設值是 **%** ，它會傳回所有發行集。 如果這個參數等於 ALL，則只會傳回 independent_agent = **0** 的提取訂閱。  
  
`[ @show_push = ] 'show_push'` 這是指是否傳回所有發送訂閱。 *show_push*是 **Nvarchar (5) **，預設值是 FALSE，不會傳回發送訂閱。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|發行者的名稱。|  
|**發行者資料庫**|**sysname**|發行者資料庫的名稱。|  
|**出版**|**sysname**|發行集的名稱。|  
|**independent_agent**|**bit**|指出這個發行集是否有獨立的散發代理程式。|  
|**訂用帳戶類型**|**int**|發行集的訂閱類型。|  
|**散發代理程式**|**Nvarchar (100) **|處理訂閱的散發代理程式。|  
|**publication description**|**nvarchar(255)**|發行集的描述。|  
|**last updating time**|**date**|更新訂閱資訊的時間。 這是 ISO 日期 (114) + ODBC 時間 (121) 的 UNICODE 字串。 格式為 yyyymmdd hh:mi:sss.mmm，其中 'yyyy' 是年份，'mm' 是月份，'dd' 是日期，'hh' 是小時，'mi' 是分鐘，'sss' 是秒鐘，'mmm' 是毫秒。|  
|**訂用帳戶名稱**|**Varchar (386) **|訂閱的名稱。|  
|**上次交易時間戳記**|**varbinary(16)**|最後一次複寫交易的時間戳記。|  
|**update mode**|**tinyint**|允許的更新類型。|  
|**distribution agent job_id**|**int**|散發代理程式的作業識別碼。|  
|**enabled_for_synmgr**|**int**|是否能夠利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Synchronization Manager 同步處理訂閱。|  
|**訂用帳戶 guid**|**binary(16)**|發行集訂閱版本的全域識別碼。|  
|**subid**|**binary(16)**|匿名訂閱的全域識別碼。|  
|**immediate_sync**|**bit**|每次執行快照集代理程式時，是否要建立或重新建立同步處理檔案。|  
|**發行者登入**|**sysname**|用於發行者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼。|  
|**發行者密碼**|**Nvarchar (524) **|用於發行者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼 (加密)。|  
|**publisher security_mode**|**int**|在發行者端實作的安全性模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證<br /><br /> **1** = Windows 驗證<br /><br /> **2** = 同步處理觸發程式會使用靜態**sysservers**專案來執行遠端程序呼叫 (RPC) ，而且必須在**sysservers**資料表中將「*發行者*」定義為遠端伺服器或連結的伺服器。|  
|**轉銷商**|**sysname**|散發者的名稱。|  
|**distributor_login**|**sysname**|用於散發者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼。|  
|**distributor_password**|**Nvarchar (524) **|用於散發者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼 (加密)。|  
|**distributor_security_mode**|**int**|在散發者端實作的安全性模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證<br /><br /> **1** = Windows 驗證|  
|**ftp_address**|**sysname**|只是為了與舊版相容。|  
|**ftp_port**|**int**|只是為了與舊版相容。|  
|**ftp_login**|**sysname**|只是為了與舊版相容。|  
|**ftp_password**|**Nvarchar (524) **|只是為了與舊版相容。|  
|**alt_snapshot_folder**|**nvarchar(255)**|當位置不是預設位置，或在預設位置之外還有其他位置時，快照集資料夾的儲存位置。|  
|**working_directory**|**nvarchar(255)**|當指定利用檔案傳輸通訊協定 (FTP) 來傳送快照集檔案的選項時，傳送快照集檔案之目錄的完整路徑。|  
|**use_ftp**|**bit**|訂閱是透過網際網路來訂閱發行集，並設定 FTP 定址屬性。 如果是 **0**，訂用帳戶就不會使用 FTP。 如果是 **1**，則訂用帳戶會使用 FTP。|  
|**publication_type**|**int**|指定發行集的複寫類型：<br /><br /> **0** = 異動複寫<br /><br /> **1** = 快照式複寫<br /><br /> **2** = 合併式複寫|  
|**dts_package_name**|**sysname**|指定 Data Transformation Services (DTS) 封裝的名稱。|  
|**dts_package_location**|**int**|DTS 封裝的儲存位置：<br /><br /> **0** = 散發者<br /><br /> **1** = 訂閱者|  
|**offload_agent**|**bit**|指定是否能從遠端啟動代理程式。 如果是 **0**，則無法從遠端啟動代理程式。|  
|**offload_server**|**sysname**|指定遠端啟用所用之伺服器的網路名稱。|  
|**last_sync_status**|**int**|訂閱狀態：<br /><br /> **0** = 所有作業都在等待啟動<br /><br /> **1** = 一或多個作業正在啟動<br /><br /> **2** = 所有作業都已成功執行<br /><br /> **3** = 至少有一項工作正在執行<br /><br /> **4** = 所有作業都已排程和閒置<br /><br /> **5** = 至少有一項作業在先前的失敗之後嘗試執行<br /><br /> **6** = 至少有一項作業無法成功執行|  
|**last_sync_summary**|**sysname**|上次同步處理結果的描述。|  
|**last_sync_time**|**datetime**|更新訂閱資訊的時間。 這是 ISO 日期 (114) + ODBC 時間 (121) 的 UNICODE 字串。 格式為 yyyymmdd hh:mi:sss.mmm，其中 'yyyy' 是年份，'mm' 是月份，'dd' 是日期，'hh' 是小時，'mi' 是分鐘，'sss' 是秒鐘，'mmm' 是毫秒。|  
|**job_login**|**nvarchar(512)**|這是散發代理程式執行時所用的 Windows 帳戶，以*網域*使用者名稱的格式傳回 \\ * *。|  
|**job_password**|**sysname**|基於安全性考慮， **\*\*\*\*\*\*\*\*\*\*** 一律會傳回 "" 值。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_helppullsubscription** 用於快照式和異動複寫中。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_helppullsubscription** 。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addpullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_droppullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
