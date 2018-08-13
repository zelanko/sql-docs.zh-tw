---
title: sys.index_columns & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.index_columns
- sys.index_columns_TSQL
- index_columns
- index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.index_columns catalog view
ms.assetid: 211471aa-558a-475c-9b94-5913c143ed12
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 4d46709b314df0511faad3abc3dc9a80947264dd
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39533918"
---
# <a name="sysindexcolumns-transact-sql"></a>sys.index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  包含一個資料列，每個資料行屬於**sys.indexes**索引或未排序的資料表 （堆積）。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|索引定義所在的物件識別碼。|  
|**index_id**|**int**|資料行定義所在的索引識別碼。|  
|**index_column_id**|**int**|索引資料行的識別碼。 **index_column_id**只有在是唯一**index_id**。|  
|**column_id**|**int**|中的資料行的識別碼**object_id**。<br /><br /> 0 = 非叢集索引中的資料列識別碼 (RID)。<br /><br /> **column_id**只有在是唯一**object_id**。|  
|**key_ordinal**|**tinyint**|索引鍵資料行組中的序數 (以 1 為基底)。<br /><br /> 0 = 不是索引鍵資料行，或是 XML 索引、資料行存放區索引或空間索引。<br /><br /> 注意： XML 或空間索引不可以是金鑰因為基礎資料行無法比較，這表示其值不會按照順序。|  
|**partition_ordinal**|**tinyint**|分割區資料行組中的序數 (以 1 為基底)。 叢集資料行存放區索引最多可以有 1 個分割區資料行。<br /><br /> 0 = 不是分割區資料行。|  
|**is_descending_key**|**bit**|1 = 索引鍵資料行是以遞減方式排序。<br /><br /> 0 = 索引鍵資料行是以遞增方式排序，或者資料行是資料行存放區索引或雜湊索引的一部分。|  
|**is_included_column**|**bit**|1 = 資料行是利用 CREATE INDEX INCLUDE 子句加入索引中的非索引鍵資料行，或者資料行是資料行存放區索引的一部分。<br /><br /> 0 = 資料行並未加入。<br /><br /> 中不會列出資料行以隱含方式加入，因為它們是叢集索引鍵的一部分**sys.index_columns**。<br /><br /> 因為是分割區資料行而隱含新增的資料行會當做 0 傳回。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `Production.BillOfMaterials` 資料表的所有索引和索引資料行。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,ic.key_ordinal  
,ic.is_included_column  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
WHERE i.object_id = OBJECT_ID('Production.BillOfMaterials');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
index_name                                                 column_name        index_column_id key_ordinal is_included_column  
---------------------------------------------------------- -----------------  --------------- ----------- -------------  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate ProductAssemblyID  1               1           0  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate ComponentID        2               2           0  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate StartDate          3               3           0  
PK_BillOfMaterials_BillOfMaterialsID                       BillOfMaterialsID  1               1           0  
IX_BillOfMaterials_UnitMeasureCode                         UnitMeasureCode    1               1           0  
  
(5 row(s) affected)  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
