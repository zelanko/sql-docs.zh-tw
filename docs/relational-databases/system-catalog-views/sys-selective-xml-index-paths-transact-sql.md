---
title: sys.selective_xml_index_paths (TRANSACT-SQL) |Microsoft 文件
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
- xml_schema_attributes_TSQL
- xml_schema_attributes
- sys.xml_schema_attributes_TSQL
- sys.xml_schema_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_attributes catalog view
ms.assetid: 07a73d71-ec3e-4894-947a-5859ca62c606
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 64f1dad5208cc8e0f72ef5a90c08d8820154d7df
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysselectivexmlindexpaths-transact-sql"></a>sys.selective_xml_index_paths (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 開始可供使用，sys.selective_xml_index_paths 中的每個資料列都代表特定選擇性 xml 索引的一個升級路徑。  
  
 如果您使用以下陳述式，在資料表 T 的 xmlcol 上建立選擇性 xml 索引：  
  
```  
CREATE SELECTIVE XML INDEX sxi1 ON T(xmlcol)   
FOR ( path1 = '/a/b/c' AS XQUERY 'xs:string',  
      path2 = '/a/b/d' AS XQUERY 'xs:double'  
    )  
```  
  
 則 sys.selective_xml_index_paths 中將會有兩個新的資料列對應到索引 sxi1。  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|具有 XML 資料行之資料表的識別碼。|  
|**index_id**|**int**|選擇性 xml 索引的唯一識別碼。|  
|**path_id**|**int**|升級 XML 路徑識別碼。|  
|**path**|**nvarchar(4000)**|升級路徑。 例如，'/a/b/c/d/e'。|  
|**name**|**sysname**|路徑名稱。|  
|**path_type**|**tinyint**|0 = XQUERY<br /><br /> 1 = SQL|  
|**path_type_desc**|**sysname**|根據**path_type** 'XQUERY' 或 'SQL' 值。|  
|**xml_component_id**|**int**|資料庫中 XML 結構描述元件的唯一識別碼。|  
|**xquery_type_description**|**nvarchar(4000)**|指定之 xsd 類型的名稱。|  
|**is_xquery_type_inferred**|**bit**|1 = 推斷類型。|  
|**xquery_max_length**|**smallint**|最大長度 (以 xsd 類型的字元為單位)。|  
|**is_xquery_max_length_inferred**|**bit**|1 = 推斷最大長度。|  
|**is_node**|**bit**|0 = node() 提示未出現。<br /><br /> 1 = node() 最佳化提示已套用。|  
|**system_type_id**|**tinyint**|資料行的系統類型識別碼。|  
|**user_type_id**|**tinyint**|資料行之使用者類型的識別碼。|  
|**max_length**|**smallint**|類型的最大長度 (以位元組為單位)。<br /><br /> -1 = 資料行的資料類型是 varchar(max)、nvarchar(max)、varbinary(max) 或 xml。|  
|**有效位數**|**tinyint**|如果是以數值為基礎，便是類型的最大有效位數。 否則為 0。|  
|**scale**|**tinyint**|如果是以數值為基礎，便是類型的最大小數位數。 否則為 0。|  
|**collation_name**|**sysname**|如果是以字元為基礎，便是類型的定序名稱。 否則為 NULL。|  
|**is_singleton**|**bit**|0 = SINGLETON 提示未出現。<br /><br /> 1 = SINGLETON 最佳化提示已套用。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 結構描述&#40;XML 類型系統&#41;目錄檢視&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
