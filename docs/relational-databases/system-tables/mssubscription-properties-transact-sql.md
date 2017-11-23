---
title: "P (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSsubscription_properties
- MSsubscription_properties_TSQL
dev_langs: TSQL
helpviewer_keywords: MSsubscription_properties system table
ms.assetid: f96fc1ae-b798-4b05-82a7-564ae6ef23b8
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0811b4b8705fda92ff57e782d04f6543b9fd1ebb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssubscriptionproperties-transact-sql"></a>MSsubscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscription_properties**資料表包含訂閱者端執行複寫代理程式所需之參數資訊的資料列。 這個資料表是儲存在「訂閱者」的訂閱資料庫中以供提取訂閱之用，或是儲存在「散發者」的散發資料庫中供發送訂閱之用。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**發行者**|**sysname**|發行者的名稱。|  
|**publisher_db**|**sysname**|發行者資料庫的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**publication_type**|**int**|發行集類型：<br /><br /> **0** = 交易式。<br /><br /> **2** = 合併式。|  
|**publisher_login**|**sysname**|用於發行者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼。|  
|**publisher_password**|**nvarchar （524)**|用於發行者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼 (已加密)。|  
|**publisher_security_mode**|**int**|在發行者端實作的安全性模式：<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 驗證。<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證。<br /><br /> **2** = 同步處理觸發程序利用靜態**sysservers**項目來執行遠端程序呼叫 (RPC)，和*發行者*必須定義在**sysservers**資料表做為遠端伺服器或連結的伺服器。|  
|**散發者**|**sysname**|散發者的名稱。|  
|**distributor_login**|**sysname**|在散發者上用於 SQL Server 驗證的登入識別碼。|  
|**distributor_password**|**nvarchar （524)**|用於散發者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼 (已加密)。|  
|**distributor_security_mode**|**int**|在散發者端實作的安全性模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。<br /><br /> **1** = Windows 驗證。|  
|**ftp_address**|**sysname**|散發者的檔案傳輸通訊協定 (FTP) 服務的網路位址。|  
|**ftp_port**|**int**|散發者的 FTP 服務通訊埠編號。|  
|**ftp_login**|**sysname**|用於連接到 FTP 服務的使用者名稱。|  
|**ftp_password**|**nvarchar （524)**|用於連接到 FTP 服務的使用者密碼。|  
|**alt_snapshot_folder**|**nvarchar(255)**|指定快照集替代資料夾的位置。|  
|**working_directory**|**nvarchar(255)**|用於儲存資料和結構描述檔案的工作目錄名稱。|  
|**use_ftp**|**bit**|指定利用 FTP 而不是一般通訊協定來擷取快照集。 如果**1**，在使用 FTP。|  
|**dts_package_name**|**sysname**|指定 Data Transformation Services (DTS) 封裝的名稱。|  
|**dts_package_password**|**nvarchar （524)**|指定封裝的密碼。|  
|**dts_package_location**|**int**|DTS 封裝的儲存位置。|  
|**enabled_for_syncmgr**|**bit**|指定是否能夠利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Synchronization Manager 來同步處理訂閱。<br /><br /> **0** = 利用 Synchronization Manager 未註冊訂用帳戶。<br /><br /> **1** = 訂用帳戶已登錄使用 Synchronization Manager，且可以同步處理，而不啟動[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。|  
|**offload_agent**|**bit**|指定是否能從遠端啟動代理程式。 如果**0**，無法從遠端啟動代理程式。|  
|**offload_server**|**sysname**|指定遠端啟用所用之伺服器的網路名稱。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|指定儲存快照集檔案的資料夾路徑。|  
|**use_web_sync**|**bit**|指定是否能夠利用 HTTP 來同步處理訂閱。 值為**1**表示啟用這項功能。|  
|**應**|**nvarchar （260)**|代表複寫接聽程式之 Web 同步處理位置的 URL。|  
|**internet_url**|**sysname**|連接到主控 Web 同步處理使用的 Web 伺服器時，會使用合併代理程式的登入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。|  
|**internet_login**|**nvarchar （524)**|連接到主控 Web 同步處理使用的 Web 伺服器時，合併代理程式會使用登入的密碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。|  
|**internet_security_mode**|**int**|連接到主控 Web 同步處理，值為 Web 伺服器時使用的驗證模式**1**表示 Windows 驗證，而值為**0**表示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。|  
|**internet_timeout**|**int**|Web 同步處理要求到期之前的時間長度 (以秒為單位)。|  
|**主機名稱**|**sysname**|指定的值**HOST_NAME**中使用此函式時**其中**子句的聯結篩選或邏輯記錄關聯性。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
