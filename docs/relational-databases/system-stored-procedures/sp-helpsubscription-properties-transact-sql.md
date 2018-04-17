---
title: sp_helpsubscription_properties (TRANSACT-SQL) |Microsoft 文件
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
- sp_helpsubscription_properties
- sp_helpsubscription_properties_TSQL
helpviewer_keywords:
- sp_helpsubscription_properties
ms.assetid: 7a76a645-97eb-47ac-b3ea-e2d75012cbed
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 78637041673509151652fd1e6d4125c8e41e2aa2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpsubscriptionproperties-transact-sql"></a>sp_helpsubscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  擷取安全性資訊從[MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)資料表。 這個預存程序執行於訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpsubscription_properties [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db =] 'publisher_db' ]   
    [ , [ @publication =] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher=**] **'***publisher***'**  
 這是發行者的名稱。 *發行者*是**sysname**，預設值是**%**，傳回所有發行者的資訊。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*是**sysname**，預設值是**%**，傳回所有發行者資料庫的資訊。  
  
 [ **@publication=**] **'***publication***'**  
 這是發行集的名稱。 *發行集*是**sysname**，預設值是**%**，傳回所有發行集的資訊。  
  
 [  **@publication_type=**] *publication_type*  
 是發行集的類型。*publication_type*是**int**，預設值是 NULL。 如果提供， *publication_type*必須是下列值之一：  
  
|Value|描述|  
|-----------|-----------------|  
|**0**|交易式發行集|  
|**1**|快照式發行集|  
|**2**|合併式發行集|  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**發行者**|**sysname**|發行者的名稱。|  
|**publisher_db**|**sysname**|發行者資料庫的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**publication_type**|**int**|發行集的類型：<br /><br /> **0** = 交易式<br /><br /> **1** = 快照集<br /><br /> **2** = 合併|  
|**publisher_login**|**sysname**|用於發行者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼。|  
|**publisher_password**|**nvarchar （524)**|用於發行者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證 (加密) 的密碼。|  
|**publisher_security_mode**|**int**|發行者端所用的安全性模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證<br /><br /> **1** = Windows 驗證|  
|**散發者**|**sysname**|散發者的名稱。|  
|**distributor_login**|**sysname**|散發者登入。|  
|**distributor_password**|**nvarchar （524)**|散發者密碼 (加密)。|  
|**distributor_security_mode**|**int**|散發者端所用的安全性模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證<br /><br /> **1** = Windows 驗證|  
|**ftp_address**|**sysname**|只是為了與舊版相容。 散發者的檔案傳輸通訊協定 (FTP) 服務的網路位址。|  
|**ftp_port**|**int**|只是為了與舊版相容。 散發者的 FTP 服務通訊埠編號。|  
|**ftp_login**|**sysname**|只是為了與舊版相容。 用來連接到 FTP 服務的使用者名稱。|  
|**ftp_password**|**nvarchar （524)**|只是為了與舊版相容。 用來連接到 FTP 服務的使用者密碼。|  
|**alt_snapshot_folder**|**nvarchar(255)**|指定快照集替代資料夾的位置。|  
|**working_directory**|**nvarchar(255)**|用來儲存資料和結構描述檔案的工作目錄名稱。|  
|**use_ftp**|**bit**|指定利用 FTP 而不是一般通訊協定來擷取快照集。 如果**1**，在使用 FTP。|  
|**dts_package_name**|**sysame**|指定 Data Transformation Services (DTS) 封裝的名稱。|  
|**dts_package_password**|**nvarchar （524)**|指定封裝的密碼 (如果有的話)。|  
|**dts_package_location**|**int**|DTS 封裝的儲存位置。<br /><br /> **0** = 封裝位置是在 「 散發者 」。<br /><br /> **1** = 封裝位置是在 「 訂閱者 」。|  
|**offload_agent**|**bit**|指定是否能從遠端啟動代理程式。 如果**0**，無法從遠端啟動代理程式。|  
|**offload_server**|**sysname**|指定遠端啟用所用之伺服器的網路名稱。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|指定儲存快照集檔案的資料夾路徑。|  
|**use_web_sync**|**bit**|如果訂用帳戶可以同步處理會透過 HTTPS 值**1**表示啟用這項功能。|  
|**應**|**nvarchar(260)**|代表 Web 同步處理之複寫接聽程式位置的 URL。|  
|**internet_url**|**nvarchar(128)**|當利用基本驗證來連接到主控 Web 同步處理的 Web 伺服器時，合併代理程式所用的登入。|  
|**internet_login**|**nvarchar （524)**|當利用基本驗證來連接到主控 Web 同步處理的 Web 伺服器時，合併代理程式所用的登入密碼。|  
|**internet_security_mode**|**int**|連接到主控 Web 同步處理，值為 Web 伺服器時使用的驗證模式**1**表示 Windows 驗證，而值為**0**表示基本驗證。|  
|**internet_timeout**|**int**|Web 同步處理要求到期之前的時間長度 (以秒為單位)。|  
|**主機名稱**|**nvarchar(128)**|指定在 WHERE 子句參數化資料列篩選器中使用這個函數時的 HOST_NAME() 值。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpsubscription_properties**用於快照式複寫、 異動複寫和合併式複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_helpsubscription_properties**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
