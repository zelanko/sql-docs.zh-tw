---
title: 函式函數（XQuery） |Microsoft Docs
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
ms.openlocfilehash: 7f64c9ff6664410983d9c3ce7ebdbf07e493ca03
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68038988"
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
 基本及衍生的不可部份完成 XSD 類型都可以支援建構函式。 不過，不支援**xs： duration**的子類型，**包括 xdt： yearMonthDuration 和 xdt： dayTimeDuration**，以及**xs： QName**、 **xs： NMTOKEN**和**xs： NOTATION** 。 假如使用者自訂的不可部份完成類型是由以下的類型直接或間接衍生，您也可以使用可在相關結構描述中取得的這種類型。  
  
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
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中。  
  
### <a name="a-using-the-datetime-xquery-function-to-retrieve-older-product-descriptions"></a>A. 使用 dateTime() XQuery 函數擷取較舊的產品描述  
 在此範例中，會先將範例 XML 檔指派給**xml**類型變數。 本檔包含三個範例`ProductDescription` <> 元素，其中每個專案都包含`DateCreated` <的> 子項目。  
  
 然後查詢該變數，只擷取在特定日期之前建立的那些產品描述。 為了進行比較，查詢會使用**xs： dateTime （）** 函式函數來輸入日期。  
  
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
  
-   .。。WHERE 迴圈結構用來抓取滿足 WHERE \<子句中指定之條件的 ProductDescription> 專案。  
  
-   **Datetime （）** function 函數是用來建立**日期時間**類型值，以便適當地進行比較。  
  
-   然後查詢會建構產生的 XML。 因為您正在建構一連串的屬性，所以 XML 建構中會使用逗號及括號。  
  
 以下是結果：  
  
```  
<Product   
   ProductID="1"   
   DateCreated="2000-01-01T00:00:00Z"/>  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;XQuery&#41;的 XML 結構](../xquery/xml-construction-xquery.md)   
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
