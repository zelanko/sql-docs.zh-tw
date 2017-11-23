---
title: "sys.system_views (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.system_views_TSQL
- system_views
- system_views_TSQL
- sys.system_views
dev_langs: TSQL
helpviewer_keywords: sys.system_views catalog view
ms.assetid: a526c410-e7b5-4075-8103-e1f3c6837c3c
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5db3ad63df2d57856ffd9d89122290999f69a860
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="syssystemviews-transact-sql"></a>sys.system_views (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所提供的每份系統檢視，各包含一個資料列。 所有的系統檢視都包含在名為結構描述中**sys**或**INFORMATION_SCHEMA**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|\<繼承資料行 >||如需這個檢視所繼承的資料行的清單，請參閱[sys.objects &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_replicated**|**bit**|1 = 檢視已被複寫。|  
|**has_replication_filter**|**bit**|1 = 檢視具有複寫篩選。|  
|**has_opaque_metadata**|**bit**|1 = 針對檢視所指定的 VIEW_METADATA 選項。 如需詳細資訊，請參閱 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)。|  
|**has_unchecked_assembly_data**|**bit**|1 = 資料表包含保存資料，這些保存資料會隨著上次 ALTER ASSEMBLY 期間變更定義的組件而不同。 在下次 DBCC CHECKDB 或 DBCC CHECKTABLE 順利完成之後，將重設為 0。|  
|**with_check_option**|**bit**|1 = WITH CHECK OPTION 是在檢視定義中指定。|  
|**sys.views**|**bit**|1 = 檢視由系統存放區之間的相互關聯資訊自動建立**datetime**資料行。 若要建立這份檢視，請將 DATE_CORRELATION_OPTIMIZATION 設為 ON。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [物件目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
