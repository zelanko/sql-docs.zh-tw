---
title: sys.xml_schema_types (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ce5530e160fe6473ff84fca0978b5fc467fe688
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/30/2019
ms.locfileid: "64945858"
---
# <a name="sysxmlschematypes-transact-sql"></a>sys.xml_schema_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回每個 XML 結構描述元件是型別，一個資料列**symbol_space**的**T**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<繼承資料行 >**||繼承資料行從[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)。|  
|**is_abstract**|**bit**|1 = 類型是抽象類型。 此類型的元素的所有執行個體必須使用**xsi: type**表示不是抽象的衍生的類型。<br /><br /> 0 = 類型不是抽象的。 (預設值)|  
|**allows_mixed_content**|**bit**|1 = 允許混合內容<br /><br /> 0 = 不允許混合內容。 (預設值)|  
|**is_extension_blocked**|**bit**|1 = 時的 block 屬性上，將會封鎖執行個體中的取代成類型的延伸模組**complexType**定義或**blockDefault**屬性的上階\<結構描述 >項目資訊項目設定為"extension"或"#all 」。<br /><br /> 0 = 取代成延伸模組不會遭到封鎖。|  
|**is_restriction_blocked**|**bit**|1 = 取代類型的限制會遭到封鎖執行個體中時的 block 屬性上**complexType**定義或**blockDefault**屬性的上階\<結構描述 >項目資訊項目設定為"restriction"或"#all 」。<br /><br /> 0 = 取代成限制不會遭到封鎖。 (預設值)|  
|**is_final_extension**|**bit**|1 = 衍生類型的延伸模組時封鎖上的 final 屬性**complexType**定義或**finalDefault**屬性的上階\<結構描述 > 元素資訊項目設定為"extension"或"#all 」。<br /><br /> 0 = 允許延伸模組。 (預設值)|  
|**is_final_restriction**|**bit**|1 = 衍生型別的限制時封鎖上簡單的 final 屬性或**complexType**定義或**finalDefault**屬性的上階\<結構描述 > 項目資訊項目設定為"restriction"或"#all 」。<br /><br /> 0 = 允許限制。 (預設值)|  
|**is_final_list_member**|**bit**|1 = 這個簡單類型不可作為清單中的項目類型使用。<br /><br /> 0 = 這個類型是複雜類型，或可作為清單項目類型使用。 (預設值)|  
|**is_final_union_member**|**bit**|1 = 這個簡單類型不可作為聯集類型的成員類型。<br /><br /> 0 = 這個類型是複雜類型， 或可用作聯集成員類型。 (預設值)|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 結構描述&#40;XML 型別系統&#41;目錄檢視&#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
