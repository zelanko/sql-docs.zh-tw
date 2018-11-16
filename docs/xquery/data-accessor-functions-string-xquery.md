---
title: 字串函數 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- string function
- fn:string function
ms.assetid: 7baa2959-9340-429b-ad53-3df03d8e13fc
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4df87a9fedffa701858fef9101c58db12c1c3bf2
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661677"
---
# <a name="data-accessor-functions---string-xquery"></a>資料存取子函式 - string (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回的值 *$arg*表示為字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:string() as xs:string  
fn:string($arg as item()?) as xs:string  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 是一個節點或不可部份完成的值。  
  
## <a name="remarks"></a>備註  
  
-   如果 *$arg*是空的序列，會傳回長度為零的字串。  
  
-   如果 *$arg*是一個節點，函式傳回的字串值使用字串值存取子所取得的節點。 這定義在 W3C XQuery 1.0 及 XPath 2.0 Data Model 規格中。  
  
-   如果 *$arg*是不可部分完成的值，函式會傳回相同的字串轉換為運算式所傳回**xs: string**， *$arg*，明時除外。  
  
-   如果類型 *$arg*是**xs: anyuri**，URI 會轉換成字串，而不需要逸出特殊字元。  
  
-   實行中， **fn: string**沒有引數僅適用於內容相依述詞的內容中。 具體而言，它只能在括號 ([ ]) 內使用。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存於各種**xml**類型資料行中的 AdventureWorks 資料庫。  
  
### <a name="a-using-the-string-function"></a>A. 使用字串函數  
 以下查詢會擷取 <`ProductDescription`> 元素的 <`Features`> 子元素節點。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 /PD:ProductDescription/PD:Features  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 以下是部份結果：  
  
```  
<PD:Features xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   These are the product highlights.   
   <p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 years</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
   </p1:Warranty>  
       ...  
</PD:Features>  
```  
  
 如果您指定**string （)** 函式，您會收到指定的節點的字串值。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 string(/PD:ProductDescription[1]/PD:Features[1])  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 以下是部份結果。  
  
```  
These are the product highlights.   
3 yearsparts and labor...    
```  
  
### <a name="b-using-the-string-function-on-various-nodes"></a>B. 在不同節點上使用字串函數  
 在以下範例中，XML 執行個體會指定給一個 xml 類型變數。 指定查詢以說明套用的結果**string （)** 對不同節點。  
  
```  
declare @x xml  
set @x = '<?xml version="1.0" encoding="UTF-8" ?>  
<!--  This is a comment -->  
<root>  
  <a>10</a>  
just text  
  <b attr="x">20</b>  
</root>  
'  
```  
  
 以下查詢會擷取文件節點的字串值。 此值是串連所有下階文字節點的字串值而成。  
  
```  
select @x.query('string(/)')  
```  
  
 以下是結果：  
  
```  
This is a comment 10  
just text  
 20  
```  
  
 以下查詢會嘗試擷取處理指示節點的字串值。 因為並不包含文字節點，所以結果會是空白時序。  
  
```  
select @x.query('string(/processing-instruction()[1])')  
```  
  
 以下查詢會擷取註解節點的字串值，並傳回文字節點。  
  
```  
select @x.query('string(/comment()[1])')  
```  
  
 以下是結果：  
  
```  
This is a comment   
```  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
