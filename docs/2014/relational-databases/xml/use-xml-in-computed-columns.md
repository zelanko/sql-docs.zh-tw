---
title: 在計算資料行中使用 XML | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- computed columns, XML
- XML [SQL Server], computed columns
ms.assetid: 1313b889-69b4-4018-9868-0496dd83bf44
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9bfa88e56e5f914afd4f027634d0f069406c009
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530600"
---
# <a name="use-xml-in-computed-columns"></a>使用計算資料行中的 XML
  XML 執行個體可依計算資料行的來源或依計算資料行的類型顯示。 本主題的範例將示範如何搭配計算資料行使用 XML。  
  
## <a name="creating-computed-columns-from-xml-columns"></a>從 XML 資料行建立計算資料行  
 在下列 `CREATE TABLE` 陳述式中，從 `xml` 計算出`col2`類型資料行 ( `col1`)：  
  
```  
CREATE TABLE T(col1 varchar(max), col2 AS CAST(col1 AS xml) )    
```  
  
 `xml` 資料類型也可依建立計算資料行的來源顯示，如下列 `CREATE TABLE` 陳述式所示：  
  
```  
CREATE TABLE T (col1 xml, col2 as cast(col1 as varchar(1000) ))   
```  
  
 您可以從 `xml` 類型的資料行擷取值以建立計算資料行，如下列範例所示。 因為 `xml` 資料類型方法無法直接用來建立計算資料行，本範例先定義一個函數 (`my_udf`)，以傳回 XML 執行個體的值。 該函數會包裝 `value()` 類型的 `xml` 方法。 接著會在計算資料行的 `CREATE TABLE` 陳述式中指定函數名稱。  
  
```  
CREATE FUNCTION my_udf(@var xml) returns int  
AS BEGIN   
RETURN @var.value('(/ProductDescription/@ProductModelID)[1]' , 'int')  
END  
GO  
-- Use the function in CREATE TABLE.  
CREATE TABLE T (col1 xml, col2 as dbo.my_udf(col1) )  
GO  
-- Try adding a row.   
INSERT INTO T values('<ProductDescription ProductModelID="1" />')  
GO  
-- Verify results.  
SELECT col2, col1  
FROM T  
  
```  
  
 就如同上述範例，下列範例定義一個函數，以傳回計算資料行的 `xml` 類型執行個體。 在函數中， `query()` 資料類型的 `xml` 方法會擷取 `xml` 類型參數中的值。  
  
```  
CREATE FUNCTION my_udf(@var xml)   
  RETURNS xml AS   
BEGIN   
   RETURN @var.query('ProductDescription/Features')  
END  
```  
  
 在下列 `CREATE TABLE` 陳述式中， `Col2` 是一個計算資料行，它使用了該函數所傳回的 XML 資料 (`<Features>` 元素)：  
  
```  
CREATE TABLE T (Col1 xml, Col2 as dbo.my_udf(Col1) )  
-- Insert a row in table T.  
INSERT INTO T VALUES('  
<ProductDescription ProductModelID="1" >  
  <Features>  
    <Feature1>description</Feature1>  
    <Feature2>description</Feature2>  
  </Features>  
</ProductDescription>')  
-- Verify the results.  
SELECT *  
FROM T  
```  
  
### <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[使用計算資料行升級常用的 XML 值](promote-frequently-used-xml-values-with-computed-columns.md)|描述如何搭配計算資料行和屬性資料表使用屬性升級。|  
  
  
