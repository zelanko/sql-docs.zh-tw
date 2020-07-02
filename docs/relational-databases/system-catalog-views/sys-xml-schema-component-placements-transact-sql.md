---
title: sys.xml_schema_component_placements （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
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
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 5d8528718d29a1bb1d8ad8867ac38021a169b4c5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754332"
---
# <a name="sysxml_schema_component_placements-transact-sql"></a>sys.xml_schema_component_placements (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

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
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架構 &#40;XML 類型系統&#41; 目錄檢視 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
