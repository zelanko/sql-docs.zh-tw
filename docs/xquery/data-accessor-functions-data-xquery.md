---
title: data 函數（XQuery） |Microsoft Docs
description: 瞭解如何使用 XQuery 函數資料（），傳回指定之專案序列中每個專案的具類型值。
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
- fn:data function
- data function [XQuery]
ms.assetid: 511b5d7d-c679-4cb2-a3dd-170cc126f49d
author: rothja
ms.author: jroth
ms.openlocfilehash: ac340466d1d816139249e4b007c7b2bc733dd390
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84881871"
---
# <a name="data-accessor-functions---data-xquery"></a>資料存取子函式 - data (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 *$arg*所指定的每個專案，傳回具類型的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:data ($arg as item()*) as xdt:untypedAtomic*  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 其具類型值將會傳回的項目序列。  
  
## <a name="remarks"></a>備註  
 下列規定適用於具類型的值：  
  
-   不可部份完成值的具類型值，就是不可部份完成值。  
  
-   文字節點的具類型值是文字節點的字串值。  
  
-   註解的具類型值是註解的字串值。  
  
-   處理指示的具類型值是處理指示的內容，不含處理指示目標名稱。  
  
-   文件節點的具類型值是它的字串值。  
  
 下列規定適用於屬性和元素節點：  
  
-   如果屬性節點是具有 XML 結構描述類型的類型，它的具類型值也隨之為具類型值。  
  
-   如果 [屬性] 節點不具類型，其具類型的值會等於當做 xdt 的實例傳回的字串值 **： untypedAtomic**。  
  
-   如果尚未輸入元素節點，其具類型的值會等於當做**xdt： untypedAtomic**的實例傳回的字串值。  
  
 下列規定適用於具類型的元素節點：  
  
-   如果專案具有簡單的內容類型， **data （）** 就會傳回元素的具類型值。  
  
-   如果節點是複雜型別（包括 xs： anyType）， **data （）** 就會傳回靜態錯誤。  
  
 雖然使用**data （）** 函數通常是選擇性的，如下列範例所示，指定**data （）** 函數會明確增加查詢可讀性。 如需詳細資訊，請參閱[XQuery 基本概念](../xquery/xquery-basics.md)。  
  
 您不能在已構造的 XML 上指定**data （）** ，如下所示：  
  
```  
declare @x xml  
set @x = ''  
select @x.query('data(<SomeNode>value</SomeNode>)')  
```  
  
## <a name="examples"></a>範例  
 本主題針對儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中的 xml 實例提供 XQuery 範例。  
  
### <a name="a-using-the-data-xquery-function-to-extract-typed-value-of-a-node"></a>A. 使用 data() XQuery 函數擷取節點的具類型值  
 下列查詢說明如何使用**data （）** 函數來取出屬性、專案和文位元組點的值：  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query(N'  
 for $pd in //p1:ProductDescription  
 return   
    <Root   
      ProductID = "{ data( ($pd//@ProductModelID)[1] ) }"   
      Feature =   "{ data( ($pd/p1:Features/wm:Warranty/wm:Description)[1] ) }" >  
    </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 以下是結果：  
  
```  
<Root ProductID="19" Feature="parts and labor"/>  
```  
  
 如前所述，當您要建立屬性時， **data （）** 函數是選擇性的。 如果您未指定**data （）** 函數，則會隱含假設。 下列查詢產生與上一個查詢相同的結果：  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for $pd in //p1:ProductDescription  
         return   
          <Root    
                ProductID = "{ ($pd/@ProductModelID)[1] }"    
                Feature =   "{ ($pd/p1:Features/wm:Warranty/wm:Description)[1] }" >  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 下列範例說明需要**data （）** 函數的實例。  
  
 在下列查詢中， **$pd/p1：規格/材質**會傳回 <`Material`> 元素。 此外，**資料（$pd/p1：規格/材質）** 會傳回類型為 Xdt： untypedAtomic 的字元資料，因為 <`Material`> 不具類型。 當輸入不具類型時， **data （）** 的結果會輸入為**xdt： untypedAtomic**。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in //p1:ProductDescription  
         return   
          <Root>  
             { $pd/p1:Specifications/Material }  
             { data($pd/p1:Specifications/Material) }  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 以下是結果：  
  
```  
<Root>  
  <Material>Almuminum Alloy</Material>Almuminum Alloy  
</Root>  
```  
  
 在下列查詢中，**資料（$pd/p1： Features/wm：質保）** 會傳回靜態錯誤，因為 <`Warranty`> 是複雜的類型元素。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
 <Root>  
   {     /p1:ProductDescription/p1:Features/wm:Warranty }  
   { data(/p1:ProductDescription/p1:Features/wm:Warranty) }  
 </Root>  
 ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID = 23  
```  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
