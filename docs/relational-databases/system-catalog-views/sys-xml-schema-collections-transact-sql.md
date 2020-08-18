---
description: sys.xml_schema_collections (Transact-SQL)
title: sys.xml_schema_collections (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
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
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d54502963e0a6464d4a437a46c83db53667bab5a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400734"
---
# <a name="sysxml_schema_collections-transact-sql"></a>sys.xml_schema_collections (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  針對每個 XML 結構描述集合，各傳回一個資料列。 XML 結構描述集合是 XSD 定義的具名集合。 XML 結構描述集合本身包含在關聯式結構描述中，由結構描述範圍 [!INCLUDE[tsql](../../includes/tsql-md.md)] 名稱加以識別。 下列 Tuple 是唯一的：xml_collection_id、schema_id 和 name。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|xml_collection_id|**int**|XML 結構描述集合的識別碼。 在資料庫中，這是唯一的。|  
|schema_id|**int**|包含這個 XML 結構描述集合的關聯式結構描述識別碼。|  
|principal_id|**int**|如果個別擁有者不是結構描述擁有者，這便是個別擁有者的識別碼。 依預設，結構描述包含的物件就是結構描述擁有者所擁有的物件。 不過，您也可以利用 ALTER AUTHORIZATION 陳述式來變更擁有權，指定替代的擁有者。<br /><br /> NULL = 無替代的個別擁有者。|  
|NAME|**sysname**|XML 結構描述集合的名稱。|  
|create_date|**datetime**|建立 XML 結構描述集合的日期。|  
|modify_date|**datetime**|上次變更 XML 結構描述集合的日期。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML 架構 &#40;XML 類型系統&#41; 目錄檢視 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
