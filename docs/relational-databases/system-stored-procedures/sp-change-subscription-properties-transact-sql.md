---
title: "sp_change_subscription_properties (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_change_subscription_properties_TSQL
- sp_change_subscription_properties
helpviewer_keywords:
- sp_change_subscription_properties
ms.assetid: cf8137f9-f346-4aa1-ae35-91a2d3c16f17
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3fe61cfc2088b75e2ab1af2c457073ad723dd7f2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spchangesubscriptionproperties-transact-sql"></a>sp_change_subscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新提取訂閱的資訊。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_change_subscription_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publication_type = ] publication_type ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publisher=**] **'***發行者***'**  
 這是發行者的名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
 [  **@publication=**] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@property=**] **'***屬性***'**  
 這是要變更的屬性。 *屬性*是**sysname**。  
  
 [  **@value=**] **'***值***'**  
 這是屬性的新值。 *值*是**nvarchar （1000)**，沒有預設值。  
  
 [  **@publication_type =** ] *publication_type*  
 指定發行集的複寫類型。 *publication_type*是**int**，而且可以是下列值之一。  
  
|值|發行集類型|  
|-----------|----------------------|  
|**0**|異動|  
|**1**|快照式|  
|**2**|合併式|  
|NULL (預設值)|複寫決定了發行集的類型。 由於預存程序必須查看多份資料表，因此，相較於提供確實的發行集類型，這個選項會比較慢。|  
  
 下表描述發行項的屬性及這些屬性的值。  
  
|屬性|值|Description|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||指定快照集替代資料夾的位置。 如果設為 NULL，便會從發行者所指定的預設位置中，收取快照集檔案。|  
|**distrib_job_login**||用來執行代理程式之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶的登入。|  
|**distrib_job_password**||用來執行代理程式之 Windows 帳戶的密碼。|  
|**distributor_login**||散發者登入。|  
|**distributor_password**||散發者密碼。|  
|**distributor_security_mode**|**1**|當連接到散發者時，使用 Windows 驗證。|  
||**0**|當連接到散發者時，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。|  
|**dts_package_name**||指定 SQL Server 2000 Data Transformation Services (DTS) 封裝的名稱。 只有在發行集是交易式或快照式時，才能指定這個值。|  
|**dts_package_password**||指定封裝的密碼。 *dts_package_password*是**sysname**預設值是 NULL，其指定密碼屬性維持不變。<br /><br /> 注意： DTS 封裝必須有密碼。<br /><br /> 只有在發行集是交易式或快照式時，才能指定這個值。|  
|**dts_package_location**||DTS 封裝的儲存位置。 只有在發行集是交易式或快照式時，才能指定這個值。|  
|**dynamic_snapshot_location**||指定儲存快照集檔案的資料夾路徑。 只有在發行集是合併式發行集時，才能指定這個值。|  
|**ftp_address**||只是為了與舊版相容。|  
|**ftp_login**||只是為了與舊版相容。|  
|**ftp_password**||只是為了與舊版相容。|  
|**ftp_port**||只是為了與舊版相容。|  
|**主機名稱**||連接到發行者時所用的主機名稱。|  
|**internet_url**||當利用基本驗證來連接到主控 Web 同步處理的 Web 伺服器時，合併代理程式所用的登入。|  
|**internet_login**||當利用基本驗證來連接到主控 Web 同步處理的 Web 伺服器時，合併代理程式所用的密碼。|  
|**internet_security_mode**|**1**|Web 同步處理使用 Windows 整合式驗證。 我們建議您搭配 Web 同步處理來使用基本驗證。 如需詳細資訊，請參閱 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)。|  
||**0**|Web 同步處理使用基本驗證。<br /><br /> 注意： Web 同步處理需要 Web 伺服器的 SSL 連線。|  
|**internet_timeout**||Web 同步處理要求到期之前的時間長度 (以秒為單位)。|  
|**應**||代表 Web 同步處理之複寫接聽程式位置的 URL。|  
|**merge_job_login**||用來執行代理程式之 Windows 帳戶的登入。|  
|**merge_job_password**||用來執行代理程式之 Windows 帳戶的密碼。|  
|**publisher_login**||發行者登入。 變更*publisher_login*只支援合併式發行集的訂閱。|  
|**publisher_password**||發行者密碼。 變更*publisher_password*只支援合併式發行集的訂閱。|  
|**publisher_security_mode**|**1**|當連接到發行者時，使用 Windows 驗證。 變更*publisher_security_mode*只支援合併式發行集的訂閱。|  
||**0**|當連接到發行者時，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。|  
|**use_ftp**|**true**|利用 FTP 而不是正規通訊協定來擷取快照集。|  
||**false**|利用正規通訊協定來擷取快照集。|  
|**use_web_sync**|**true**|啟用 Web 同步處理。|  
||**false**|停用 Web 同步處理。|  
|**working_directory**||在利用檔案傳輸通訊協定 (FTP) 來傳送快照集檔案時，用來暫時儲存發行集的資料檔和結構描述檔的工作目錄名稱。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_change_subscription_properties**用於所有複寫類型。  
  
 **sp_change_subscription_properties**用於提取訂閱。  
  
 Oracle 發行者，值*publisher_db*會被忽略，因為 Oracle 只允許一個資料庫，每個伺服器執行個體。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_change_subscription_properties**。  
  
## <a name="see-also"></a>請參閱＜  
 [檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [sp_addmergepullsubscription &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_addmergepullsubscription_agent &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_addpullsubscription &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_addpullsubscription_agent &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
