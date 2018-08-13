---
title: sys.change_tracking_tables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- change_tracking_tables_TSQL
- sys.change_tracking_tables
- change_tracking_tables
- sys.change_tracking_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], sys.change_tracking_tables
- sys.change_tracking_tables
ms.assetid: 97ec69b6-0d49-4d98-82f0-d3e77ba1ad2b
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: ebea733f742efcc02d515eae685619820dbbfcd3
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39544678"
---
# <a name="change-tracking-catalog-views---syschangetrackingtables"></a>變更追蹤目錄檢視-sys.change_tracking_tables
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  針對已啟用變更追蹤之目前資料庫中的每一個資料表，各傳回一個資料列。  
   
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|object_id|**int**|擁有變更日誌之資料表的識別碼。 即使變更追蹤目前為關閉狀態，資料表也可以擁有變更日誌。<br /><br /> 資料表識別碼在資料庫中是唯一的。|  
|is_track_columns_updated_on|**bit**|變更追蹤在資料表上的目前狀態：<br /><br /> 0 = OFF<br /><br /> 1 = ON |  
|begin_version|**bigint**|針對資料表開始變更追蹤時的資料庫版本。 這個版本通常會指出啟用變更追蹤的時間，但如果資料表遭到截斷，就會重設這個值。|  
|cleanup_version|**bigint**|清除可能已經移除變更追蹤資訊多早的版本。|  
|min_valid_version|**bigint**|可用於資料表之變更追蹤資訊的最大有效版本。<br /><br /> 從與此資料列相關聯之資料表取得變更時，last_sync_version 的值必須大於或等於此資料行所報告的版本。 如需詳細資訊，請參閱 < [CHANGE_TRACKING_MIN_VALID_VERSION &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [變更追蹤目錄檢視&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/6e8fd949-5560-4b34-879f-4e25aa24b183)   
 [追蹤資料變更 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
