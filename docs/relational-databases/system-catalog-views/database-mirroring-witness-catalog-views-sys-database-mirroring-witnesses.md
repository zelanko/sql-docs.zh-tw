---
title: "sys.database_mirroring_witnesses (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_witnesses
- sys.database_mirroring_witnesses_TSQL
- database_mirroring_witnesses
- database_mirroring_witnesses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_witnesses catalog view
- witness [SQL Server], sys.database_mirroring_witnesses catalog view
ms.assetid: 0dd5b794-733b-4a3c-b5a4-62f9f1f0f22d
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ce23f7d9f763bf08842a1f121c881fb5fbdcee0
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="database-mirroring-witness-catalog-views---sysdatabasemirroringwitnesses"></a>資料庫鏡像見證目錄檢視-sys.database_mirroring_witnesses
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  針對伺服器在資料庫鏡像合作關係中所扮演的每個見證角色，各包含一個資料列。 
  
  在資料庫鏡像工作階段中，自動容錯移轉需要見證伺服器。 理想上，見證是在主體和鏡像伺服器之外的個別電腦中。 見證並不為資料庫提供服務。 相反地，它會監視主體和鏡像伺服器的狀態。 如果主體伺服器失敗，見證可能會初始化自動容錯移轉，將工作移轉給見證伺服器。 
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|資料庫鏡像工作階段中的兩個資料庫副本的名稱。|  
|**principal_server_name**|**sysname**|其資料庫副本目前是主體資料庫的夥伴伺服器名稱。|  
|**mirror_server_name**|**sysname**|其資料庫副本目前是鏡像資料庫的夥伴伺服器名稱。|  
|**safety_level**|**tinyint**|鏡像資料庫的更新交易安全設定：<br /><br /> 0 = 未知狀態<br /><br /> 1 = 關閉 (非同步)<br /><br /> 2 = 完整 (同步)<br /><br /> 利用見證來進行自動容錯移轉需要完整的交易安全，這是預設值。|  
|**safety_level_desc**|**nvarchar(60)**|鏡像資料庫中之更新安全保證的描述：<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL|  
|**safety_sequence_number**|**int**|若要變更的序號更新**safety_level**。|  
|**role_sequence_number**|**int**|將變更的序號更新為鏡像夥伴所扮演的主體/鏡像角色。|  
|**mirroring_guid**|**uniqueidentifier**|鏡像合作關係的識別碼。|  
|**family_guid**|**uniqueidentifier**|資料庫備份家族的識別碼。 它用來偵測相符還原狀態。|  
|**is_suspended**|**bit**|資料庫鏡像已暫停。|  
|**is_suspended_sequence_number**|**int**|設定的序號**is_suspended**。|  
|**partner_sync_state**|**tinyint**|鏡像工作階段的同步處理狀態：<br /><br /> 5 = 夥伴已同步處理。 現在可能可以進行容錯移轉。 如需有關容錯移轉，請參閱的需求資訊[角色切換期間資料庫鏡像工作階段 &#40;SQL Server &#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md).<br /><br /> 6 = 夥伴未同步處理。 現在不可能進行容錯移轉。|  
|**partner_sync_state_desc**|**nvarchar(60)**|鏡像工作階段之同步處理狀態的描述：<br /><br /> SYNCHRONIZED<br /><br /> UNSYNCHRONIZED|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像見證](../../database-engine/database-mirroring/database-mirroring-witness.md)   
 [sys.database_mirroring &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
