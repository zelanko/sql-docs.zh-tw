---
title: "sys.pdw_health_component_properties (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 55d033f0e0001377cb0a7d5be6e4bbff35833c24
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwhealthcomponentproperties-transact-sql"></a>sys.pdw_health_component_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  描述裝置的存放區屬性。 某些屬性顯示裝置狀態，而某些屬性會描述裝置本身。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|元件屬性的唯一識別碼。<br /><br /> 屬性識別碼與 component_id 形成這個檢視的索引鍵。|NOT NULL|  
|component_id|**int**|元件的識別碼。 請參閱[sys.pdw_health_components &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> 屬性識別碼與 component_id 形成這個檢視的索引鍵。|NOT NULL|  
|property_name|**nvarchar(255)**|屬性的名稱。|NOT NULL|  
|physical_name|**nvarchar(32)**|製造商所定義的屬性名稱。|NOT NULL|  
|is_key|**bit**|判斷裝置的執行個體是否為唯一。|NOT NULL<br /><br /> 0-裝置執行個體是唯一的。<br /><br /> 1-裝置執行個體不是唯一的。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
