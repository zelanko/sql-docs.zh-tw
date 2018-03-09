---
title: "IHpublications (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHpublications_TSQL
- IHpublications
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublications system table
ms.assetid: b519a101-fa53-44be-bd55-6ea79245b5d1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 93678262e3201e9fff338abb5a978771415609b8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="ihpublications-transact-sql"></a>IHpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublications**系統資料表包含每個非 SQL Server 發行集使用目前散發者的一個資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**pubid**|**int**|提供發行集唯一識別碼的識別欄位。|  
|**name**|**sysname**|與發行集相關聯的唯一名稱。|  
|**repl_freq**|**tinyint**|複寫頻率：<br /><br /> **0** = 以交易為基礎。<br /><br /> **1** = 已排程的資料表重新整理。|  
|**status**|**tinyint**|發行集的狀態，它可以是下列項目之一。<br /><br /> **0** = 非使用中。<br /><br /> **1** = 使用。|  
|**sync_method**|**tinyint**|同步處理方法：<br /><br /> **1** = 字元大量複製。<br /><br /> **4** = Concurrent_c，表示使用字元大量複製，但在快照集期間，不鎖定資料表。|  
|**snapshot_jobid**|**binary**|已排程的工作識別碼。|  
|**enabled_for_internet**|**bit**|指出發行集的同步處理檔案是否會公開給網際網路上透過 FTP 和其他服務，其中**1**表示它們可以存取網際網路。|  
|**immediate_sync_ready**|**bit**|指出是否同步處理檔案可用，其中**1**表示可供使用。 *不支援非 SQL 發行者。*|  
|**allow_queued_tran**|**bit**|指定是否已啟用在訂閱者端將變更放入佇列中，直到可以在發行者端套用這些變更為止。 如果**1**，「 訂閱者 」 端的變更會排入佇列。 *不支援非 SQL 發行者。*|  
|**allow_sync_tran**|**bit**|指定是否允許發行集使用立即更新訂閱。 **1**表示允許立即更新訂閱。 *不支援非 SQL 發行者。*|  
|**autogen_sync_procs**|**bit**|指定是否在發行者端產生立即更新訂閱的同步處理預存程序。 **1**表示在發行者端產生它。 *不支援非 SQL 發行者。*|  
|**snapshot_in_defaultfolder**|**bit**|指定是否將快照集檔案儲存在預設資料夾中。 如果**0**，快照集檔案已儲存在所指定的替代位置*alternate_snapshot_folder*。 如果**1**，可以在預設資料夾中找到快照集檔案。|  
|**alt_snapshot_folder**|**nvarchar(510)**|指定快照集替代資料夾的位置。|  
|**pre_snapshot_script**|**nvarchar(510)**|指定指向**.sql**檔案位置。 在訂閱者端套用快照集時，散發代理程式會在執行任何複寫的物件指令碼之前，先執行前快照集 (pre-snapshot) 指令碼。|  
|**post_snapshot_script**|**nvarchar(510)**|指定指向**.sql**檔案位置。 在初始同步處理期間，散發代理程式會先套用所有其他複寫的物件指令碼和資料，然後才執行後快照集 (post-snapshot) 指令碼。|  
|**compress_snapshot**|**bit**|指定可寫入快照集*alt_snapshot_folder*位置是壓縮成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。 **0**指定不壓縮快照集。|  
|**ftp_address**|**sysname**|散發者之 FTP 服務的網路位址。 指定發行集快照集檔案所在的位置，以便散發代理程式能夠加以收取。|  
|**ftp_port**|**int**|散發者的 FTP 服務通訊埠編號。 指定發行集快照集檔案所在的位置，以便散發代理程式能夠加以收取|  
|**ftp_subdirectory**|**nvarchar(510)**|指定在發行集支援利用 FTP 來傳播快照集時，散發代理程式能夠從中收取快照集檔案的位置。|  
|**ftp_login**|**nvarchar(256)**|用於連接到 FTP 服務的使用者名稱。|  
|**ftp_password**|**nvarchar(1048)**|用來連接到 FTP 服務的使用者密碼。|  
|**allow_dts**|**bit**|指定發行集允許資料轉換。 **1**指定允許 DTS 轉換。 *不支援非 SQL 發行者。*|  
|**allow_anonymous**|**bit**|指出是否允許匿名訂閱發行集，其中**1**允許它們的表示。|  
|**centralized_conflicts**|**bit**|指定是否將衝突記錄儲存在發行者端：<br /><br /> **0** = 將衝突記錄儲存在發行者端和造成衝突的訂閱者端。<br /><br /> **1** = 將衝突記錄儲存在發行者端。<br /><br /> *不支援非 SQL 發行者。*|  
|**conflict_retention**|**int**|指定衝突保留週期 (以天為單位)。 *不支援非 SQL 發行者。*|  
|**conflict_policy**|**int**|指定使用佇列更新訂閱者選項時，所遵照的衝突解決原則。 它可以是下列值之一：<br /><br /> **1** = 發行者優先衝突。<br /><br /> **2** = 訂閱者優先衝突。<br /><br /> **3** = 重新初始化訂閱。<br /><br /> *不支援非 SQL 發行者。*|  
|**類型**|**int**|指定所用的佇列類型。 它可以是下列值之一：<br /><br /> **1** = msmq，利用[!INCLUDE[msCoName](../../includes/msconame-md.md)]Message Queuing 來儲存交易。<br /><br /> **2** = sql，會使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]來儲存交易。<br /><br /> 此資料行不是由非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。<br /><br /> 請注意： 使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]Message Queuing 已被取代，不再支援。<br /><br /> *針對非 SQL 發行者不支援這個資料行。*|  
|**ad_guidname**|**sysname**|指定發行集是否在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中發行。 有效的全域唯一識別碼 (GUID) 指定發行集是在[!INCLUDE[msCoName](../../includes/msconame-md.md)]Active Directory 中，GUID 是對應的 Active Directory 發行集物件**objectGUID**。 如果是 NULL，發行集就不會發行在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中。 *不支援非 SQL 發行者。*|  
|**backward_comp_level**|**int**|資料庫相容性層級，它可以是下列值之一：<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].<br /><br /> *不支援非 SQL 發行者。*|  
|**描述**|**nvarchar(255)**|發行集的描述項目。|  
|**independent_agent**|**bit**|指定這個發行集是否有獨立的散發代理程式。<br /><br /> **0** = 發行集使用共用的散發代理程式，以及每一組發行者資料庫/訂閱者資料庫都有單一共用代理程式。<br /><br /> **1** = 沒有獨立的散發代理程式，針對這個發行集。|  
|**immediate_sync**|**bit**|指出是否建立或重新建立快照集代理程式執行時，每次同步處理檔案位置**1**表示每次執行代理程式所建立。|  
|**allow_push**|**bit**|指出是否允許發送訂閱發行集，其中**1**允許它們的表示。|  
|**allow_pull**|**bit**|指出是否允許提取訂閱發行集，其中**1**允許它們的表示。|  
|**保留**|**int**|給定發行集的變更儲存量 (以小時為單位)。|  
|**allow_subscription_copy**|**bit**|指定是否已啟用複製訂閱這個發行集之訂閱資料庫的能力。 **1**表示允許複製。|  
|**allow_initialize_from_backup**|**bit**|指出訂閱者是否能夠從備份中，而不是從初始快照集中，對這個發行集的訂閱進行初始化。 **1**表示，從備份初始化訂閱並**0**表示無法。 如需詳細資訊，請參閱 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。 *不支援非 SQL 發行者。*|  
|**min_autonosync_lsn**|**binary(1)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|指出是否支援發行集的結構描述複寫。 **1**表示複寫在發行者端執行的 DDL 陳述式，和**0**表示不複寫 DDL 陳述式。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。 *不支援非 SQL 發行者。*|  
|**選項**|**int**|指定其他發行選項的點陣圖，位元選項值如下：<br /><br /> **0x1** -啟用端對端複寫。<br /><br /> **0x2** -只發行本機變更。<br /><br /> **0x4** -啟用非 SQL Server 訂閱者。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addpublication &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [syspublications &#40;系統檢視 &#41;&#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)   
 [syspublications &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/syspublications-transact-sql.md)  
  
  
