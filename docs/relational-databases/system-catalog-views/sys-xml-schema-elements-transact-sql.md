---
title: sys.xml_schema_elements (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_elements
- sys.xml_schema_elements_TSQL
- xml_schema_elements
- xml_schema_elements_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_elements catalog view
ms.assetid: 190ed0cd-0c5e-4607-9db4-9e77cacf17d7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ed5c7efe1c5adacba99b74ab40e2978a51ba7517
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47716686"
---
# <a name="sysxmlschemaelements-transact-sql"></a>sys.xml_schema_elements (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回每個 XML 結構描述元件是型別，一個資料列**symbol_space**的**E**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<繼承資料行 >**|**--**|繼承資料行從[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)。|  
|**is_default_fixed**|**bit**|1 = 預設值是固定值。 在 XML 執行個體中不能覆寫這個值。<br /><br /> 0 = 預設值不是元素的固定值。 (預設值)。|  
|**is_abstract**|**bit**|1 = 元素是抽象的，無法使用於執行個體文件中。 元素的替代群組成員必須出現在執行個體文件中。<br /><br /> 0 = 元素不是抽象的。 (預設值)。|  
|**is_nillable**|**bit**|1 = 元素為 Nillable。<br /><br /> 0 = 元素不是 Nillable。 (預設值)|  
|**must_be_qualified**|**bit**|1 = 元素必須明確限定命名空間。<br /><br /> 0 = 元素可隱含限定命名空間。 (預設值)|  
|**is_extension_blocked**|**bit**|1 = 封鎖取代成某延伸類型的執行個體。<br /><br /> 0 = 允許取代成延伸類型。 (預設值)|  
|**is_restriction_blocked**|**bit**|1 = 封鎖取代成某限制類型的執行個體。<br /><br /> 0 = 允許具有限制類型的取代。 (預設值)|  
|**is_substitution_blocked**|**bit**|1 = 無法使用替代群組的執行個體。<br /><br /> 0 = 允許取代成替代群組。 (預設值)|  
|**is_final_extension**|**bit**|1 = 不允許取代成某延伸類型的執行個體。<br /><br /> 0 = 允許取代成某延伸類型的執行個體。 (預設值)|  
|**is_final_restriction**|**bit**|1 = 不允許取代成某限制類型的執行個體。<br /><br /> 0 = 允許取代成某限制類型的執行個體。 (預設值)|  
|**default_value**|**nvarchar (4000)**|元素的預設值。 如果沒有提供預設值，則為 NULL。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 結構描述&#40;XML 型別系統&#41;目錄檢視&#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
