---
title: string 函數（XQuery） |Microsoft Docs
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
ms.openlocfilehash: 9cb30d81102c17f2c3ce04b31ac7ff2b9689343e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68038937"
---
# <a name="data-accessor-functions---string-xquery"></a>資料存取子函式 - string (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回以字串表示的 *$arg*值。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:string() as xs:string  
fn:string($arg as item()?) as xs:string  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 是一個節點或不可部份完成的值。  
  
## <a name="remarks"></a>備註  
  
-   如果 *$arg*是空的序列，則會傳回長度為零的字串。  
  
-   如果 *$arg*是節點，此函數會傳回使用字串值存取子所取得之節點的字串值。 這定義在 W3C XQuery 1.0 及 XPath 2.0 Data Model 規格中。  
  
-   如果 *$arg*是不可部分完成的值，此函式會傳回運算式轉換成**xs： string**， *$arg*的相同字串，除非另有說明。  
  
-   如果 *$arg*的類型為**xs： ANYURI**，則 URI 會轉換成字串，而不會將特殊字元轉義。  
  
-   沒有引數的 Inthis 執行、 **fn： string （）** 只能用於內容相依述詞的內容中。 具體而言，它只能在括號 ([ ]) 內使用。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中。  
  
### <a name="a-using-the-string-function"></a>A. 使用字串函數  
 下列查詢會抓取 <`Features` `ProductDescription`> 元素的 <> 子項目節點。  
  
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
  
 如果您指定**string （）** 函式，就會收到指定節點的字串值。  
  
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
 在以下範例中，XML 執行個體會指定給一個 xml 類型變數。 系統會指定查詢，以說明將**string （）** 套用至各種節點的結果。  
  
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
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
