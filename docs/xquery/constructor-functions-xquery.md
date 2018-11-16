---
title: 建構函式 (XQuery) |Microsoft 文件
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
- constructor functions [XQuery]
ms.assetid: 98562d0e-d0e0-4f62-b001-90acbac67277
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b426d7f4f5056c76e7ccc6807785366f0f12287f
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2018
ms.locfileid: "51293034"
---
# <a name="constructor-functions-xquery"></a>建構函式函數 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  U建構函式函數可由指定輸入，建立任何 XSD 內建或使用者自訂的不可部份完成類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
TYP($atomicvalue as xdt:anyAtomicType?  
  
) as TYP?  
  
```  
  
## <a name="arguments"></a>引數  
 *$strval*  
 將要轉換的字串。  
  
 *TYP*  
 任何內建的 XSD 類型。  
  
## <a name="remarks"></a>備註  
 基本及衍生的不可部份完成 XSD 類型都可以支援建構函式。 不過的子**xs: duration**，其中包括**xdt: yearmonthduration 和 xdt: daytimeduration**，並**xs: qname**， **xs**，並**xs: notation**不支援。 假如使用者自訂的不可部份完成類型是由以下的類型直接或間接衍生，您也可以使用可在相關結構描述中取得的這種類型。  
  
#### <a name="supported-base-types"></a>支援的基本類型  
 以下是支援的基本類型：  
  
-   xs:string  
  
-   xs:boolean  
  
-   xs:decimal  
  
-   xs:float  
  
-   xs:double  
  
-   xs:duration  
  
-   xs:dateTime  
  
-   xs:time  
  
-   xs:date  
  
-   xs:gYearMonth  
  
-   xs:gYear  
  
-   xs:gMonthDay  
  
-   xs:gDay  
  
-   xs:gMonth  
  
-   xs:hexBinary  
  
-   xs:base64Binary  
  
-   xs:anyURI  
  
#### <a name="supported-derived-types"></a>支援的衍生類型  
 以下是支援的衍生類型：  
  
-   xs:normalizedString  
  
-   xs:token  
  
-   xs:language  
  
-   xs:Name  
  
-   xs:NCName  
  
-   xs:ID  
  
-   xs:IDREF  
  
-   xs:ENTITY  
  
-   xs:integer  
  
-   xs:nonPositiveInteger  
  
-   xs:negativeInteger  
  
-   xs:long  
  
-   xs:int  
  
-   xs:short  
  
-   xs:byte  
  
-   xs:nonNegativeInteger  
  
-   xs:unsignedLong  
  
-   xs:unsignedInt  
  
-   xs:unsignedShort  
  
-   xs:unsignedByte  
  
-   xs:positiveInteger  
  
 SQL Server 也能以下列方式，支援建構函式引動的常數摺疊：  
  
-   如果引數是字串常值，則將會在編譯期間評估運算式。 當該值無法滿足類型條件約束時，就會發生靜態錯誤。  
  
-   如果引數是其他類型的常值，則將會在編譯期間評估運算式。 當該值無法滿足類型條件約束時，就會傳回空白時序。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存於各種**xml**類型資料行中的 AdventureWorks 資料庫。  
  
### <a name="a-using-the-datetime-xquery-function-to-retrieve-older-product-descriptions"></a>A. 使用 dateTime() XQuery 函數擷取較舊的產品描述  
 在此範例中，範例 XML 文件會先指派給**xml**類型變數。 此文件包含三個範例 <`ProductDescription`> 元素，而每個元素都包含一個 <`DateCreated`> 子元素。  
  
 然後查詢該變數，只擷取在特定日期之前建立的那些產品描述。 基於比較的詳細資訊，此查詢會使用**xs:dateTime()** 建構函式，以輸入日期。  
  
```  
declare @x xml  
set @x = '<root>  
<ProductDescription ProductID="1" >  
  <DateCreated DateValue="2000-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription  ProductID="2" >  
  <DateCreated DateValue="2001-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription ProductID="3" >  
  <DateCreated DateValue="2002-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
</root>'  
  
select @x.query('  
     for $PD in  /root/ProductDescription  
     where xs:dateTime(data( ($PD/DateCreated/@DateValue)[1] )) < xs:dateTime("2001-01-01T00:00:00Z")  
     return  
        element Product  
       {   
        ( attribute ProductID { data($PD/@ProductID ) },  
        attribute DateCreated { data( ($PD/DateCreated/@DateValue)[1] ) } )  
        }  
 ')  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   FOR ...WHERE 迴圈結構用以擷取\<ProductDescription > 滿足 WHERE 子句中指定之條件的項目。  
  
-   **Datetime （)** 建構函式用來建構**dateTime**型別值，因此它們可以進行適當地進行比較。  
  
-   然後查詢會建構產生的 XML。 因為您正在建構一連串的屬性，所以 XML 建構中會使用逗號及括號。  
  
 以下是結果：  
  
```  
<Product   
   ProductID="1"   
   DateCreated="2000-01-01T00:00:00Z"/>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 建構&#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
