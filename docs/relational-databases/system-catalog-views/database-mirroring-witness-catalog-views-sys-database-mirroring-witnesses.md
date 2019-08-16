---
title: sys.database_mirroring_witnesses & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 10fbd3ac410ee5b6944ffe7b32285008f8b11776
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033086"
---
# <a name="database-mirroring-witness-catalog-views---sysdatabase_mirroring_witnesses"></a>資料庫鏡像見證目錄檢視-sys.database_mirroring_witnesses
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  針對伺服器在資料庫鏡像合作關係中所扮演的每個見證角色，各包含一個資料列。 
  
  在資料庫鏡像工作階段中，自動容錯移轉需要見證伺服器。 理想上，見證是在主體和鏡像伺服器之外的個別電腦中。 見證並不為資料庫提供服務。 相反地，它會監視主體和鏡像伺服器的狀態。 如果主體伺服器失敗，見證可能會起始自動容錯移轉至鏡像伺服器。 
  
|資料行名稱|資料類型|描述|  
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
|**is_suspended_sequence_number**|**int**|設定序號**is_suspended**。|  
|**partner_sync_state**|**tinyint**|鏡像工作階段的同步處理狀態：<br /><br /> 5 = 夥伴已同步處理。 現在可能可以進行容錯移轉。 如需容錯移轉，請參閱需求的詳細資訊[角色切換資料庫鏡像工作階段期間的&#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)。<br /><br /> 6 = 夥伴不同步。 現在不可能進行容錯移轉。|  
|**partner_sync_state_desc**|**nvarchar(60)**|鏡像工作階段之同步處理狀態的描述：<br /><br /> SYNCHRONIZED<br /><br /> UNSYNCHRONIZED|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像見證](../../database-engine/database-mirroring/database-mirroring-witness.md)   
 [sys.database_mirroring &#40;-SQL&AMP;&#41;&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
