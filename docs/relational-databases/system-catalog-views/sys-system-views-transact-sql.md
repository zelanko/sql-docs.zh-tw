---
title: sys.databases system_views （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.system_views_TSQL
- system_views
- system_views_TSQL
- sys.system_views
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_views catalog view
ms.assetid: a526c410-e7b5-4075-8103-e1f3c6837c3c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dbfca799f3c3dc4b3930f487fb45413c7711af48
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821296"
---
# <a name="syssystem_views-transact-sql"></a>sys.system_views (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所提供的每份系統檢視，各包含一個資料列。 所有系統檢視都包含在名為**sys**或**INFORMATION_SCHEMA**的架構中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|\<繼承的資料行>||如需此視圖所繼承之資料行的清單，請參閱[sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**is_replicated**|**bit**|1 = 檢視已被複寫。|  
|**has_replication_filter**|**bit**|1 = 檢視具有複寫篩選。|  
|**has_opaque_metadata**|**bit**|1 = 針對檢視所指定的 VIEW_METADATA 選項。 如需詳細資訊，請參閱 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)。|  
|**has_unchecked_assembly_data**|**bit**|1 = 資料表包含保存資料，這些保存資料會隨著上次 ALTER ASSEMBLY 期間變更定義的組件而不同。 在下次 DBCC CHECKDB 或 DBCC CHECKTABLE 順利完成之後，將重設為 0。|  
|**with_check_option**|**bit**|1 = WITH CHECK OPTION 是在檢視定義中指定。|  
|**is_date_correlation_view**|**bit**|1 = 系統會自動建立 View，以儲存**datetime**資料行之間的相互關聯資訊。 若要建立這份檢視，請將 DATE_CORRELATION_OPTIMIZATION 設為 ON。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的物件目錄檢視](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-sql&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-sql&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
