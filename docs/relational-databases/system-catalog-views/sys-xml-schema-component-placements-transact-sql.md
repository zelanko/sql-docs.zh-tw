---
title: sys.xml_schema_component_placements (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_component_placements
- xml_schema_component_placements_TSQL
- xml_schema_component_placements
- sys.xml_schema_component_placements_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_component_placements catalog view
ms.assetid: 2d3c8828-e4b3-423d-bf11-990464c1341b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 78403dd04dc4fb1e531032c9f80639134f58b6ef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818276"
---
# <a name="sysxmlschemacomponentplacements-transact-sql"></a>sys.xml_schema_component_placements (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對 XML 結構描述元件的每個位置，各傳回一個資料列。  
   
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|擁有這個位置的 XML 結構描述元件的識別碼。|  
|**placement_id**|**int**|位置的識別碼。 這在擁有的 XML 結構描述元件內是唯一的。|  
|**placed_xml_component_id**|**int**|已放置的 XML 結構描述元件的識別碼。|  
|**is_default_fixed**|**bit**|1 = 預設值是固定值。 在 XML 執行個體中不能覆寫這個值。<br /><br /> 0 = 可覆寫這個值。(預設)|  
|**min_occurrences**|**int**|出現已放置元件的最小數目。|  
|**max_occurrences**|**int**|出現已放置元件的最大數目。|  
|**default_value**|**nvarchar (4000)**|如果有提供預設值，則為預設值。 如果沒有提供預設值，則為 NULL。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 結構描述&#40;XML 型別系統&#41;目錄檢視&#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
