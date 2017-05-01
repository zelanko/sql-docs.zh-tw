---
title: "記憶體內部 OLTP 支援的資料類型 | Microsoft Docs"
ms.custom: 
ms.date: 05/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a928c1f77586198fd0d33cafa445ea406a437c6b
ms.lasthandoff: 04/11/2017

---
# <a name="supported-data-types-for-in-memory-oltp"></a>記憶體中 OLTP 支援的資料類型
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  本文章列出記憶體中 OLTP 功能不支援的資料類型︰  
  
-   記憶體最佳化的資料表  
  
-   原生編譯的預存程序  
  
## <a name="unsupported-data-types"></a>不支援的資料類型  
 以下是不支援的資料類型：  
  
||||  
|-|-|-|  
|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)|[geography &#40;Transact-SQL&#41;](../../t-sql/spatial-geography/spatial-types-geography.md)|[geometry &#40;Transact-SQL&#41;](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)|  
|[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)|[xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md)|  
|[sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)|使用者定義類型|。|  
  
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

下列 Transact-SQL SELECT 陳述式會報告記憶體最佳化資料表的所有 off-row 資料行。 請注意：

- 所有索引鍵資料行都會 in-row 儲存。
  - 非唯一索引鍵現在可以在記憶體最佳化資料表上包含可為 Null 的資料行。
  - 索引可以在記憶體最佳化資料表上宣告為 UNIQUE。
- 所有 LOB 資料行都會 off-row 儲存。
- max_length 為 -1 表示大型物件 (LOB) 資料行。


```tsql
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


#### <a name="natively-compiled-modules-support-for-lobs"></a>LOB 的原生編譯模組支援


當您使用原生編譯模組中的內建字串函數時 (例如原生處理序)，此函數可以接受 LOB 類型的字串。 例如，在原生處理序中，LTrim 函數可以輸入 nvarchar(max) 或 varbinary(max) 類型的參數。

這些 LOB 可以是原生編譯純量 UDF (使用者定義函數) 的傳回類型。


### <a name="other-data-types"></a>其他資料類型


|其他類型|如需詳細資訊|  
|-----------------|--------------------------|  
|資料表類型|[記憶體最佳化資料表變數](http://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|  
  
## <a name="see-also"></a>另請參閱  
 [記憶體中 OLTP 的 Transact-SQL 支援](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [在記憶體最佳化資料表中實作 LOB 資料行](http://msdn.microsoft.com/en-us/bd8df0a5-12b9-4f4c-887c-2fb78dd79f4e)   
 [在記憶體最佳化資料表中實作 SQL_VARIANT](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  

