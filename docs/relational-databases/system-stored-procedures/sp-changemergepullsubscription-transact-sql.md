---
title: sp_changemergepullsubscription (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_changemergepullsubscription
- sp_changemergepullsubscription_TSQL
helpviewer_keywords:
- sp_changemergepullsubscription
ms.assetid: 5e0d04f2-6175-44a2-ad96-a8e2986ce4c9
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c39a3c28f96fe662888a86c49cdfce66c2314c58
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spchangemergepullsubscription-transact-sql"></a>sp_changemergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更合併提取訂閱的屬性。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changemergepullsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @publisher= ] 'publisher' ]  
    [ , [ @publisher_db= ] 'publisher_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*是**sysname**，預設值是 %。  
  
 [ **@publisher=**] **'***publisher***'**  
 這是發行者的名稱。 *發行者*是**sysname**，預設值是 %。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*是**sysname**，預設值是 %。  
  
 [  **@property=**] **'***屬性***'**  
 這是要變更的屬性名稱。 *屬性*是**sysname**，而且可以是下列其中一個資料表中的值。  
  
 [  **@value=**] **'***值***'**  
 這是指定之屬性的新值。 *值*是**nvarchar （255)**，而且可以是下列其中一個資料表中的值。  
  
|屬性|Value|Description|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||當位置不是預設位置，或在預設位置之外還有其他位置時，快照集資料夾的儲存位置。|  
|**描述**||這個合併提取訂閱的描述。|  
|**散發者**||散發者的名稱。|  
|**distributor_login**||用於散發者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼|  
|**distributor_password**||用於散發者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼 (加密)。|  
|**distributor_security_mode**|**1**|當連接到散發者時，使用 Windows 驗證。|  
||**0**|當連接到散發者時，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。|  
|**dynamic_snapshot_location**||儲存快照集檔案之資料夾的路徑。|  
|**ftp_address**||使用這個項目的目的，只是為了與舊版相容。 這是散發者的檔案傳輸通訊協定 (FTP) 服務的網路位址。|  
|**ftp_login**||使用這個項目的目的，只是為了與舊版相容。 這是用於連接到 FTP 服務的使用者名稱。|  
|**ftp_password**||使用這個項目的目的，只是為了與舊版相容。 這是用來連接到 FTP 服務的使用者密碼。|  
|**ftp_port**||使用這個項目的目的，只是為了與舊版相容。 這是散發者的 FTP 服務通訊埠編號。|  
|**主機名稱**||指定在聯結篩選的 WHERE 子句或邏輯記錄關聯性中使用這個函數時的 HOST_NAME() 值。|  
|**internet_url**||當利用基本驗證來連接到主控 Web 同步處理的 Web 伺服器時，合併代理程式所用的登入。|  
|**internet_login**||當利用基本驗證來連接到主控 Web 同步處理的 Web 伺服器時，合併代理程式所用的登入密碼。|  
|**internet_security_mode**|**1**|當連接到主控 Web 同步處理的 Web 伺服器時，使用 Windows 驗證。|  
||**0**|當連接到主控 Web 同步處理的 Web 伺服器時，使用基本驗證。|  
|**internet_timeout**||Web 同步處理要求到期之前的時間長度 (以秒為單位)。|  
|**應**||代表 Web 同步處理之複寫接聽程式位置的 URL。|  
|**merge_job_login**||用來執行代理程式之 Windows 帳戶的登入。|  
|**merge_job_password**||用來執行代理程式之 Windows 帳戶的密碼。|  
|**priority**||適用於回溯相容性。執行[sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)在發行者端而是要修改的訂用帳戶的優先權。|  
|**publisher_login**||用於發行者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼。|  
|**publisher_password**||用於發行者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼 (加密)。|  
|**publisher_security_mode**|**0**|當連接到發行者時，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。|  
||**1**|當連接到發行者時，使用 Windows 驗證。|  
||**2**|同步處理觸發程序會利用靜態**sysservers**項目來執行遠端程序呼叫 (RPC) 和 「 發行者 」 必須定義在**sysservers**資料表做為遠端伺服器或連結的伺服器。|  
|**sync_type**|**自動**|先將發行資料表的結構描述和初始資料傳送給訂閱者。|  
||**無**|訂閱者已有發行資料表的結構描述和初始資料；一律會傳送系統資料表和資料。|  
|**use_ftp**|**true**|利用 FTP 而不是一般通訊協定來擷取快照集。|  
||**false**|利用一般通訊協定來擷取快照集。|  
|**use_web_sync**|**true**|訂閱可以透過 HTTP 來同步處理。|  
||**false**|訂閱不能透過 HTTP 來同步處理。|  
|**use_interactive_resolver**|**true**|在協調期間，使用互動式解析程式。|  
||**false**|不使用互動式解析程式。|  
|**working_directory**||當指定利用 FTP 來傳送快照集檔案的選項時，傳送快照集檔案之目錄的完整路徑。|  
|NULL (預設值)||傳回支援的值清單*屬性*。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changemergepullsubscription**用於合併式複寫中。  
  
 假設目前伺服器和目前資料庫是訂閱者和訂閱者資料庫。  
  
 變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_changemergepullsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [sp_addmergepullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
