---
title: syspublications (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- syspublications
- syspublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspublications system table
ms.assetid: a86eb4f5-1f7b-493e-af55-3d15cf878228
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ec8c1f12755afa1a12e4e28c9f84c2f21963fc9f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33012725"
---
# <a name="syspublications-transact-sql"></a>syspublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對資料庫中每個已定義的發行集，各包含一個資料列。 這份資料表儲存在發行集資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**描述**|**nvarchar(255)**|發行集的描述性項目。|  
|**name**|**sysname**|與發行集相關聯的唯一名稱。|  
|**pubid**|**int**|提供發行集唯一識別碼的識別欄位。|  
|**repl_freq**|**tinyint**|複寫頻率：<br /><br /> **0** = 以交易為基礎。<br /><br /> **1** = 已排程的資料表重新整理。|  
|**status**|**tinyint**|狀態：<br /><br /> **0** = 非使用中。<br /><br /> **1** = 使用。|  
|**sync_method**|**tinyint**|同步處理方法：<br /><br /> **0** = 原生模式大量複製程式公用程式 (**BCP**)。<br /><br /> **1** = 字元模式 BCP。<br /><br /> **3** = concurrent，表示使用原生模式 BCP，但在快照集期間，不鎖定資料表。<br /><br /> **4** = Concurrent_c，表示使用字元模式 BCP，但在快照集期間，不鎖定資料表。|  
|**snapshot_jobid**|**binary(16)**|已排程的工作識別碼。|  
|**independent_agent**|**bit**|指定這個發行集是否有獨立的散發代理程式。<br /><br /> **0** = 發行集使用共用的散發代理程式，以及每一組發行者資料庫/訂閱者資料庫都有單一共用代理程式。<br /><br /> **1** = 沒有獨立的散發代理程式，針對這個發行集。|  
|**immediate_sync**|**bit**|指出是否建立或重新建立快照集代理程式執行時，每次同步處理檔案位置**1**表示每次執行代理程式所建立。|  
|**enabled_for_internet**|**bit**|指出是否利用檔案傳輸通訊協定 (FTP) 和其他服務中，網際網路公開發行集的同步處理檔案位置**1**表示它們可以存取網際網路。|  
|**allow_push**|**bit**|指出是否允許發送訂閱發行集，其中**1**允許它們的表示。|  
|**allow_pull**|**bit**|指出是否允許提取訂閱發行集，其中**1**允許它們的表示。|  
|**allow_anonymous**|**bit**|指出是否允許匿名訂閱發行集，其中**1**允許它們的表示。|  
|**immediate_sync_ready**|**bit**|指出快照集代理程式是否已產生快照集，且快照集是否已備妥，可供新的訂閱使用。 它只對立即更新發行集有意義。 **1**表示快照集已就緒。|  
|**allow_sync_tran**|**bit**|指定是否允許發行集使用立即更新訂閱。 **1**表示允許立即更新訂閱。|  
|**autogen_sync_procs**|**bit**|指定是否在發行者端產生立即更新訂閱的同步處理預存程序。 **1**表示在發行者端產生它。|  
|**保留**|**int**|給定發行集的變更儲存量 (以小時為單位)。|  
|**allowed_queued_tran**|**bit**|指定是否已啟用在訂閱者端將變更放入佇列中，直到可以在發行者端套用這些變更為止。 如果**1**，「 訂閱者 」 端的變更會排入佇列。|  
|**snapshot_in_defaultfolder**|**bit**|指定是否將快照集檔案儲存在預設資料夾中。<br /><br /> **0** = 快照集檔案已儲存在所指定的替代位置*alternate_snapshot_folder*。<br /><br /> **1** = 快照集可以在預設資料夾中找到檔案。|  
|**alt_snapshot_folder**|**nvarchar(255)**|指定快照集替代資料夾的位置。|  
|**pre_snapshot_script**|**nvarchar(255)**|指定指向 **.sql**檔案位置。 在訂閱者端套用快照集時，散發代理程式會在執行任何複寫的物件指令碼之前，先執行前快照集 (pre-snapshot) 指令碼。|  
|**post_snapshot_script**|**nvarchar(255)**|指定指向 **.sql**檔案位置。 在初始同步處理期間，散發代理程式會先套用所有其他複寫的物件指令碼和資料，然後才執行後快照集 (post-snapshot) 指令碼。|  
|**compress_snapshot**|**bit**|指定可寫入快照集*alt_snapshot_folder*位置是壓縮成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。**1**表示將壓縮快照集。|  
|**ftp_address**|**sysname**|散發者之 FTP 服務的網路位址。 指定發行集快照集檔案所在的位置，以便散發代理程式能夠加以收取。|  
|**ftp_port**|**int**|散發者的 FTP 服務通訊埠編號。 指定發行集快照集檔案所在的位置，以便散發代理程式能夠加以收取|  
|**ftp_subdirectory**|**nvarchar(255)**|指定在發行集支援利用 FTP 來傳播快照集時，散發代理程式能夠從中收取快照集檔案的位置。|  
|**ftp_login**|**sysname**|用於連接到 FTP 服務的使用者名稱。|  
|**ftp_password**|**nvarchar （524)**|用來連接到 FTP 服務的使用者密碼。|  
|**allow_dts**|**bit**|指定發行集是否允許轉換資料。 **1**指定允許 DTS 轉換。|  
|**allow_subscription_copy**|**bit**|指定是否已啟用複製訂閱這個發行集之訂閱資料庫的能力。 **1**表示允許複製。|  
|**centralized_conflicts**|**bit**|指定是否將衝突記錄儲存在發行者端：<br /><br /> **0** = 將衝突記錄儲存在發行者端和造成衝突的訂閱者端。<br /><br /> **1** = 將衝突記錄儲存在發行者端。|  
|**conflict_retention**|**int**|指定衝突保留週期 (以天為單位)。|  
|**conflict_policy**|**int**|指定使用佇列更新訂閱者選項時，所遵照的衝突解決原則。 它可以是下列值之一：<br /><br /> **1** = 發行者優先衝突。<br /><br /> **2** = 訂閱者優先衝突。<br /><br /> **3** = 重新初始化訂閱。|  
|**queue_type**|**int**|指定所用的佇列類型。 它可以是下列值之一：<br /><br /> **1** = msmq，利用[!INCLUDE[msCoName](../../includes/msconame-md.md)]Message Queuing 來儲存交易。<br /><br /> **2** = sql，會使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]來儲存交易。<br /><br /> 請注意： 使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]Message Queuing 已被取代，不再提供。|  
|**ad_guidname**|**sysname**|指定發行集是否在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中發行。 有效的全域唯一識別碼 (GUID) 指定，發行集發行在 Active Directory 中，GUID 是對應的 Active Directory 發行集物件**objectGUID**。 如果是 NULL，發行集就不會發行在 Active Directory 中。|  
|**backward_comp_level**|**int**|資料庫相容性層級，它可以是下列值之一：<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].<br /><br /> **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].|  
|**allow_initialize_from_backup**|**bit**|指出訂閱者是否能夠從備份中，而不是從初始快照集中，對這個發行集的訂閱進行初始化。 **1**表示，從備份初始化訂閱並**0**表示無法。 如需詳細資訊，請參閱 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。|  
|**min_autonosync_lsn**|**binary**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|指出是否支援發行集的結構描述複寫。 **1**表示複寫在發行者端執行的資料定義語言 (DDL) 陳述式，和**0**表示不複寫 DDL 陳述式。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。|  
|**options**|**int**|指定其他發行選項的點陣圖，位元選項值如下：<br /><br /> **0x1** -啟用端對端複寫。<br /><br /> **0x2** -只發行本機變更至點對點複寫。<br /><br /> **0x4** -啟用非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]「 訂閱者 」。<br /><br /> **0x8** -啟用對等衝突偵測。|  
|**originator_id**|**smallint**|針對衝突偵測的目的，識別點對點複寫拓撲中的每個節點。 如需詳細資訊，請參閱 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addpublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)  
  
  
