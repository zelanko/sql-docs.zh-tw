---
title: sys.xml_schema_components (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xml_schema_components
- sys.xml_schema_components_TSQL
- sys.xml_schema_components
- xml_schema_components_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_components catalog view
ms.assetid: 70142d3a-f8b5-4ee2-8287-3935f0f67aa2
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 90fbd2b92ccfcf01da2c2742a3b5a083f30f1e03
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2018
ms.locfileid: "33221949"
---
# <a name="sysxmlschemacomponents-transact-sql"></a>sys.xml_schema_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對 XML 結構描述的每個元件，各傳回一個資料列。 配對 (**collection_id**， **namespace_id**) 是包含命名空間的複合外部索引鍵。 具名的值，元件**symbol_space**，**名稱**， **scoping_xml_component_id**， **is_qualified**， **xml_namespace_id**， **xml_collection_id**是唯一的。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|資料庫中 XML 結構描述元件的唯一識別碼。|  
|**xml_collection_id**|**int**|包含這個元件之命名空間的 XML 結構描述集合識別碼。|  
|**xml_namespace_id**|**int**|集合內 XML 命名空間的識別碼。|  
|**is_qualified**|**bit**|1 = 這個元件具有明確命名空間限定詞。<br /><br /> 0 = 這是本機範圍元件。 在此情況下，配對， **namespace_id**， **collection_id**，指的是"no namespace" **targetNamespace**。<br /><br /> 如果是萬用字元元件，這個值將會等於 1。|  
|**name**|**nvarchar**<br /><br /> **(4000)**|XML 結構描述元件的唯一名稱。 如果元件未命名，則為 NULL。|  
|**symbol_space**|**char(1)**|這個符號名稱是唯一的空間根據**種類**:<br /><br /> N = 無<br /><br /> T = 類型<br /><br /> E = 元素<br /><br /> M = 模型群組<br /><br /> A = 屬性<br /><br /> G = 屬性群組|  
|**symbol_space_desc**|**nvarchar**<br /><br /> **(60)**|這個符號名稱是唯一的空間的描述根據**種類**:<br /><br /> 無<br /><br /> TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP|  
|**類型**|**char(1)**|XML 結構描述元件的種類。<br /><br /> N = 任何類型 (特殊內建元件)<br /><br /> Z = 任何簡單類型 (特殊內建元件)<br /><br /> P = 基本類型 (內建類型)<br /><br /> S = 簡單類型<br /><br /> L = 清單類型<br /><br /> U = 聯集類型<br /><br /> C = 複雜簡單類型 (從「簡單」衍生)<br /><br /> K = 複雜類型<br /><br /> E = 元素<br /><br /> M = 模型群組<br /><br /> W = 元素萬用字元<br /><br /> A = 屬性<br /><br /> G = 屬性群組<br /><br /> V = 屬性萬用字元|  
|**kind_desc**|**nvarchar**<br /><br /> **(60)**|XML 結構描述元件種類的描述：<br /><br /> ANY_TYPE<br /><br /> ANY_SIMPLE_TYPE<br /><br /> PRIMITIVE_TYPE<br /><br /> SIMPLE_TYPE<br /><br /> LIST_TYPE<br /><br /> UNION_TYPE<br /><br /> COMPLEX_SIMPLE_TYPE<br /><br /> COMPLEX_TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ELEMENT_WILDCARD<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP<br /><br /> ATTRIBUTE_WILDCARD|  
|**衍生**|**char(1)**|衍生類型的衍生方法：<br /><br /> N = 無 (不衍生)<br /><br /> X = 延伸<br /><br /> R = 限制<br /><br /> S = 替代|  
|**derivation_desc**|**nvarchar**<br /><br /> **(60)**|衍生類型之衍生方法的描述：<br /><br /> 無<br /><br /> EXTENSION<br /><br /> RESTRICTION<br /><br /> SUBSTITUTION|  
|**base_xml_component_id**|**int**|從中衍生這個元件的元件識別碼。 如果沒有，則為 NULL。|  
|**scoping_xml_component_id**|**int**|範圍元件的唯一識別碼。 如果沒有 (全域範圍)，則為 NULL。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 結構描述&#40;XML 類型系統&#41;目錄檢視&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
