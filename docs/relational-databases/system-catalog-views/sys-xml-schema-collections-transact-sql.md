---
title: sys.xml_schema_collections (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_collections_TSQL
- sys.xml_schema_collections
- xml_schema_collections
- xml_schema_collections_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_collections catalog view
ms.assetid: f3f7f3dc-029f-4942-ab3c-75fa9814e40f
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3f3964cb8af73ad3dbcdc67bec70cd9153f122a0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysxmlschemacollections-transact-sql"></a>sys.xml_schema_collections (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對每個 XML 結構描述集合，各傳回一個資料列。 XML 結構描述集合是 XSD 定義的具名集合。 XML 結構描述集合本身包含在關聯式結構描述中，由結構描述範圍 [!INCLUDE[tsql](../../includes/tsql-md.md)] 名稱加以識別。 下列 Tuple 是唯一的：xml_collection_id、schema_id 和 name。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|xml_collection_id|**int**|XML 結構描述集合的識別碼。 在資料庫中，這是唯一的。|  
|schema_id|**int**|包含這個 XML 結構描述集合的關聯式結構描述識別碼。|  
|principal_id|**int**|如果個別擁有者不是結構描述擁有者，這便是個別擁有者的識別碼。 依預設，結構描述包含的物件就是結構描述擁有者所擁有的物件。 不過，您也可以利用 ALTER AUTHORIZATION 陳述式來變更擁有權，指定替代的擁有者。<br /><br /> NULL = 無替代的個別擁有者。|  
|name|**sysname**|XML 結構描述集合的名稱。|  
|create_date|**datetime**|建立 XML 結構描述集合的日期。|  
|modify_date|**datetime**|上次變更 XML 結構描述集合的日期。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 結構描述&#40;XML 類型系統&#41;目錄檢視&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
