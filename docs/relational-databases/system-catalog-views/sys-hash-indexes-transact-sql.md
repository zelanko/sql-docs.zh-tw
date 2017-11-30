---
title: "sys.hash_indexes (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.hash_indexes_TSQL
- hash_indexes
- sys.hash_indexes
- hash_indexes_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.hash_indexes catalog view
ms.assetid: d9e230fb-d3ff-486f-86ef-44898f0a703e
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f9403bdbdfa9a779651ff11c1342a70a63d4445
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="syshashindexes-transact-sql"></a>sys.hash_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示目前雜湊索引和雜湊索引屬性。 雜湊索引僅支援[記憶體內部 OLTP &#40; 記憶體內部最佳化 &#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
 Sys.hash_indexes 檢視表包含 sys.indexes 檢視相同的資料行和其他的資料行名為**bucket_count**。 如需有關 sys.hash_indexes 檢視表中的其他資料行的詳細資訊，請參閱[sys.indexes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**\<繼承資料行 >**||繼承資料行從[sys.indexes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).|  
|**bucket_count**|**int**|雜湊索引的雜湊值區計數。<br /><br /> 如需有關 bucket_count 值，包括指導方針設定值，請參閱[CREATE TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
  
```  
SELECT object_name([object_id]) AS 'table_name', [object_id],  
     [name] AS 'index_name', [type_desc], [bucket_count]   
FROM sys.hash_indexes   
WHERE OBJECT_NAME([object_id]) = 'T1';  
```  
  
## <a name="see-also"></a>請參閱  
 [物件目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
