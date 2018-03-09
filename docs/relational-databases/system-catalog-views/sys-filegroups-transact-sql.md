---
title: "sys.filegroups (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.filegroups_TSQL
- filegroups
- sys.filegroups
- filegroups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filegroups catalog view
ms.assetid: 9e851f72-1f8e-4515-a25d-152ebc12ed56
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 91198ea3ed94496ff116014e0df2b1b067e4bf16
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysfilegroups-transact-sql"></a>sys.filegroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對身為檔案群組的每個資料空間，各包含一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**\<繼承資料行 >**|--|如需這個檢視所繼承的資料行的清單，請參閱[sys.data_spaces &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md).|  
|**filegroup_guid**|**uniqueidentifier**|檔案群組的 GUID。<br /><br /> NULL = PRIMARY 檔案群組|  
|**log_filegroup_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個值是 NULL。|  
|**is_read_only**|**bit**|1 = 檔案群組是唯讀的。<br /><br /> 0 = 檔案群組是可讀寫的。|  
|**is_autogrow_all_files**|**bit**|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。<br /><br /> 1 = 當自動成長臨界值，而檔案群組中的所有檔案成長的檔案群組符合中的檔案。<br /><br /> 0 = 時自動成長臨界值，只有該檔案成長的檔案群組符合中的檔案。 這是預設值。|  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [空間資料 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)  
  
  
