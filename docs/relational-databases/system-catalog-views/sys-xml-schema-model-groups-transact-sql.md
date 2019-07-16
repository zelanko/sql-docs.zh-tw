---
title: sys.xml_schema_model_groups (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_model_groups
- xml_schema_model_groups
- sys.xml_schema_model_groups_TSQL
- xml_schema_model_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_model_groups catalog view
ms.assetid: 566556dc-a8c8-465c-9196-c7e0ae092a8a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 041b09d544d5301d42d929e29c7f42b3502e294b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060528"
---
# <a name="sysxmlschemamodelgroups-transact-sql"></a>sys.xml_schema_model_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回一個資料列，每個 XML 結構描述元件的模型群組所**symbol_space**的**M**...  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<繼承資料行 >**||繼承資料行從[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)。|  
|**compositor**|**char(1)**|群組的 Compositor 種類：<br /><br /> A = XSD\<所有 > 群組<br /><br /> C = XSD\<選擇 > 群組<br /><br /> S = XSD\<順序 > 群組|  
|**compositor_desc**|**nvarchar (60)**|群組的 Compositor 種類的描述：<br /><br /> XSD_ALL_GROUP<br /><br /> XSD_CHOICE_GROUP<br /><br /> XSD_SEQUENCE_GROUP|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 結構描述&#40;XML 型別系統&#41;目錄檢視&#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
