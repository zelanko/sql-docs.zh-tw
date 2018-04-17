---
title: sys.xml_schema_types (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_types_TSQL
- xml_schema_types_TSQL
- sys.xml_schema_types
- xml_schema_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_types catalog view
ms.assetid: 441ba49d-f778-4fa1-98c4-ced375a01a34
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa26533f0b54cbc93639f41c097d5ee3b7c25325
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysxmlschematypes-transact-sql"></a>sys.xml_schema_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回一個資料列，每個 XML 結構描述元件是型別， **symbol_space**的**T**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**\<繼承資料行 >**||繼承資料行從[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)。|  
|**is_abstract**|**bit**|1 = 類型是抽象類型。 此類型的元素的所有執行個體必須使用**xsi: type**表示不是抽象的衍生的類型。<br /><br /> 0 = 類型不是抽象的。 (預設值)|  
|**allows_mixed_content**|**bit**|1 = 允許混合內容<br /><br /> 0 = 不允許混合內容。 (預設值)|  
|**is_extension_blocked**|**bit**|1 = 取代類型的擴充功能會遭到封鎖的執行個體時的 block 屬性上**complexType**定義或**blockDefault**屬性上階\<結構描述 >元素資訊項目設為"extension"或"#all"。<br /><br /> 0 = 取代成延伸模組不會遭到封鎖。|  
|**is_restriction_blocked**|**bit**|1 = 取代該類型之限制會遭到封鎖的執行個體時的 block 屬性上**complexType**定義或**blockDefault**屬性上階\<結構描述 >元素資訊項目設為"restriction"或"#all"。<br /><br /> 0 = 取代成限制不會遭到封鎖。 (預設值)|  
|**is_final_extension**|**bit**|1 = 衍生型別延伸所遭到封鎖時上的 final 屬性**complexType**定義或**finalDefault**屬性上階\<結構描述 > 項目資訊項目設為"extension"或"#all"。<br /><br /> 0 = 允許延伸模組。 (預設值)|  
|**is_final_restriction**|**bit**|1 = 限制型別衍生時封鎖簡單上的 final 屬性或**complexType**定義或**finalDefault**屬性上階\<結構描述 > 項目資訊項目設為"restriction"或"#all"。<br /><br /> 0 = 允許限制。 (預設值)|  
|**is_final_list_member**|**bit**|1 = 這個簡單類型不可作為清單中的項目類型使用。<br /><br /> 0 = 這個類型是複雜類型，或可作為清單項目類型使用。 (預設值)|  
|**is_final_union_member**|**bit**|1 = 這個簡單類型不可作為聯集類型的成員類型。<br /><br /> 0 = 這個類型是複雜類型， 或可用作聯集成員類型。 (預設值)|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 結構描述&#40;XML 類型系統&#41;目錄檢視&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
