---
title: 卸除 XML 索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- removing indexes
- dropping indexes
- XML indexes [SQL Server], dropping
ms.assetid: 7591ebea-34af-4925-8553-b2adb5b487c2
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 88db7af7bbca5a202b79ec42d8cade77e85cd258
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137025"
---
# <a name="drop-xml-indexes"></a>卸除 XML 索引
  [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式可用以卸除現有的主要或次要 XML 及非 XML 索引。 不過，DROP INDEX 沒有任何選項會套用至 XML 索引。 如果您卸除主要 XML 索引，也會刪除任何存在的次要索引。  
  
 具有 *TableName.IndexName* 的 DROP 語法已捨棄不用，XML 索引也不支援它。  
  
## <a name="example-creating-and-dropping-a-primary-xml-index"></a>範例：建立和卸除主要 XML 索引  
 在下列範例中，建立 XML 索引上`xml`類型資料行。  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create Primary XML index   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Verify the index creation.   
-- Note index type is 3 for xml indexes.  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'   
-- Drop the index.  
DROP INDEX PIdx_T_XmlCol ON T  
```  
  
 當卸除資料表時，也會自動卸除在該資料表上的所有 XML 索引。 不過，如果在資料行上有 XML 索引，將無法從資料表卸除 XML 資料行。  
  
 在下列範例中，建立 XML 索引上`xml`類型資料行。 如需詳細資訊，請參閱 [比較具類型的 XML 與不具類型的 XML](../xml/compare-typed-xml-to-untyped-xml.md)。  
  
```  
CREATE TABLE TestTable(  
 Col1 int primary key,   
 Col2 xml (Production.ProductDescriptionSchemaCollection))   
GO  
```  
  
 現在，您可以在 `Co12`上建立主要 XML索引。  
  
```  
CREATE PRIMARY XML INDEX PIdx_TestTable_Col2   
ON TestTable(Col2)  
GO  
```  
  
## <a name="example-creating-an-xml-index-by-using-the-dropexisting-index-option"></a>範例：使用 DROP_EXISTING 索引選項建立 XML 索引  
 在下列範例中，會在資料行 (`XmlColx`) 上建立 XML 索引。 接著，會在不同資料行 (`XmlColy`) 上建立另一個具有相同名稱的 XML 索引。 因為指定了 `DROP_EXISTING` 選項，所以會卸除 (`XmlColx)` 上的現有 XML 索引，並在 (`XmlColy`) 上建立新 XML 索引。  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T(Col1 int primary key, XmlColx xml, XmlColy xml)  
GO  
-- Create XML index on XmlColx.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColx)  
GO  
-- Create same name XML index on XmlColy.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColy)   
WITH (DROP_EXISTING = ON)  
-- Verify the index is created on XmlColy.d.  
SELECT sc.name   
FROM   sys.xml_indexes si inner join sys.index_columns sic   
ON     sic.object_id=si.object_id and sic.index_id=si.index_id  
INNER  join sys.columns sc on sc.object_id=sic.object_id   
AND    sc.column_id=sic.column_id  
WHERE  si.name='PIdx_T_XmlCol'   
AND    si.object_id=object_id('T')  
```  
  
 此查詢會傳回已建立的指定 XML 索引的資料行名稱。  
  
## <a name="see-also"></a>另請參閱  
 [XML 索引 &#40;SQL Server&#41;](xml-indexes-sql-server.md)  
  
  
