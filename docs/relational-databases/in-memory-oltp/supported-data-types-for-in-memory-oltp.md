---
title: "記憶體內部 OLTP 支援的資料類型 | Microsoft Docs"
ms.custom: 
ms.date: 06/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
caps.latest.revision: "26"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1739fcbc11cdf849292e420842b168ba653cea46
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="supported-data-types-for-in-memory-oltp"></a>記憶體中 OLTP 支援的資料類型
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  本文章列出記憶體中 OLTP 功能不支援的資料類型︰  
  
-   記憶體最佳化的資料表  
  
-   原生編譯的 T-SQL 模組  
  
## <a name="unsupported-data-types"></a>不支援的資料類型  
 以下是不支援的資料類型：  
  
||||  
|-|-|-|  
|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)|[geography &#40;Transact-SQL&#41;](../../t-sql/spatial-geography/spatial-types-geography.md)|[geometry &#40;Transact-SQL&#41;](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)|  
|[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)|[xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md)|  
|[sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)|使用者定義類型|執行個體時提供 SQL Server 登入。|  
  
## <a name="notable-supported-data-types"></a>值得注意的支援資料類型  
 記憶體中 OLTP 的功能支援大多數的資料類型。 以下是少數值得格外注意的資料類型︰  
  
|字串與二進位類型|如需詳細資訊|  
|-----------------------------|--------------------------|  
|binary 和 varbinary*|[binary 和 varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|char 和 varchar*|[char 和 varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|nchar 和 nvarchar*|[nchar 和 nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
  
針對前述字串和二進位資料類型，從 SQL Server 2016 開始：  
  
- 每個記憶體最佳化資料表也可以擁有幾個 `nvarchar(4000)`之類的長資料行，即使其長度可能會超過 8060 個位元組的實體資料列大小。  
  
- 記憶體最佳化資料表可以擁有如 `varchar(max)`之資料類型的最大長度字串和二進位資料行。  


### <a name="identify-lobs-and-other-columns-that-are-off-row"></a>識別 LOB 及其他 off-row 資料行

從 SQL Server 2016 開始，記憶體最佳化資料表[支援非資料列的資料行](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)，可讓單一資料表的資料列超過 8060 個位元組。 下列 Transact-SQL SELECT 陳述式會報告記憶體最佳化資料表的所有 off-row 資料行。 請注意：

- 所有索引鍵資料行都會 in-row 儲存。
  - 非唯一索引鍵現在可以在記憶體最佳化資料表上包含可為 Null 的資料行。
  - 索引可以在記憶體最佳化資料表上宣告為 UNIQUE。
- 所有 LOB 資料行都會 off-row 儲存。
- max_length 為 -1 表示大型物件 (LOB) 資料行。


```sql
SELECT
        OBJECT_NAME(m.object_id) as [table],
        c.name                   as [column],
        c.max_length
    FROM
             sys.memory_optimized_tables_internal_attributes AS m
        JOIN sys.columns                                     AS c
                ON  m.object_id = c.object_id
                AND m.minor_id  = c.column_id
    WHERE
        m.type = 5;
```


### <a name="other-data-types"></a>其他資料類型


|其他類型|如需詳細資訊|  
|-----------------|--------------------------|  
|資料表類型|[記憶體最佳化資料表變數](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)|  
  
## <a name="see-also"></a>另請參閱  
 [記憶體中 OLTP 的 Transact-SQL 支援](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [在記憶體最佳化資料表中實作 SQL_VARIANT](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
 [記憶體最佳化資料表中的資料表和資料列大小](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
  
