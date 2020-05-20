---
title: sys.databases xml_schema_types （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 356e73e2b90d059117cadef436bcea27498c9871
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824961"
---
# <a name="sysxml_schema_types-transact-sql"></a>sys.xml_schema_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回每個 XML 架構元件的資料列，這是類型， **symbol_space**的**T**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<繼承的資料行>**||從 sys.databases 繼承資料行[xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)。|  
|**is_abstract**|**bit**|1 = 類型是抽象類型。 此類型之專案的所有實例都必須使用**xsi： type**來表示不是抽象的衍生類型。<br /><br /> 0 = 類型不是抽象的。 (預設值)|  
|**allows_mixed_content**|**bit**|1 = 允許混合內容<br /><br /> 0 = 不允許混合內容。 (預設值)|  
|**is_extension_blocked**|**bit**|1 = 當**complexType**定義上的 block 屬性或上階**blockDefault** \< 架構> 元素資訊專案的 blockDefault 屬性設為 "extension" 或 "#all" 時，取代為類型的擴充功能會遭到封鎖。<br /><br /> 0 = 取代成延伸模組不會遭到封鎖。|  
|**is_restriction_blocked**|**bit**|1 = 當**complexType**定義上的 block 屬性或上階**blockDefault** \< 架構> 元素資訊專案的 blockDefault 屬性設定為 "限制" 或 "#all" 時，取代為類型的限制會遭到封鎖。<br /><br /> 0 = 取代成限制不會遭到封鎖。 (預設值)|  
|**is_final_extension**|**bit**|1 = 當**complexType**定義上的 final 屬性或上階架構的**finalDefault**屬性 \<> 元素資訊專案設為 "extension" 或 "#all" 時，由類型的延伸模組衍生會遭到封鎖。<br /><br /> 0 = 允許延伸模組。 (預設值)|  
|**is_final_restriction**|**bit**|1 = 當 simple 或**complexType**定義上的 final 屬性或上階架構的**finalDefault**屬性 \<> 元素資訊專案設定為 "限制" 或 "#all" 時，會封鎖類型的衍生。<br /><br /> 0 = 允許限制。 (預設值)|  
|**is_final_list_member**|**bit**|1 = 這個簡單類型不可作為清單中的項目類型使用。<br /><br /> 0 = 這個類型是複雜類型，或可作為清單項目類型使用。 (預設值)|  
|**is_final_union_member**|**bit**|1 = 這個簡單類型不可作為聯集類型的成員類型。<br /><br /> 0 = 這個類型是複雜類型， 或可用作聯集成員類型。 (預設值)|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架構 &#40;XML 類型系統&#41; 目錄檢視 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
