---
title: not 函數（XQuery） |Microsoft Docs
description: 瞭解 XQuery not （）函數如何與布林值搭配使用。
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
- effective Boolean value [XQuery]
- fn:not function
- not function [XQuery]
- EBV
ms.assetid: 93dfc377-45f1-4384-9392-560d9331a915
author: rothja
ms.author: jroth
ms.openlocfilehash: 24235099ec742d4c6d62e3d97ee1f551af24f7d4
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84524399"
---
# <a name="functions-on-boolean-values---not-function"></a>布林值的相關函式 - not 函式 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  如果 *$arg*的有效布林值為 false，則傳回 TRUE，如果 *$Arg*的有效布林值為 TRUE，則傳回 false。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 具有效布林值的一連串項目。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中。  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>A. 使用 not （） XQuery 函數來尋找其目錄描述不包含元素的產品模型 \<Specifications> 。  
 下列查詢會針對其目錄描述不包含 <> 元素的產品型號，建立包含產品型號識別碼的 XML `Specifications` 。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
       <Product   
           ProductModelID="{ sql:column("ProductModelID") }"  
        />  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications/*)]  '  
     ) = 0  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   因為此文件使用了命名空間，所以此範例會使用 WITH NAMESPACES 陳述式。 另一個選項是在[XQuery](../xquery/modules-and-prologs-xquery-prolog.md)初構中使用**declare namespace**關鍵字來定義前置詞。  
  
-   然後，此查詢會建立包含 <`Product`> 元素及其**ProductModelID**屬性的 XML。  
  
-   WHERE 子句會使用[存在（）方法（XML 資料類型）](../t-sql/xml/exist-method-xml-data-type.md)來篩選資料列。 如果有元素沒有子項目，則**存在（）** 方法會傳回 True \<ProductDescription> \<Specification> 。 請注意**not （）** 函數的用法。  
  
 此結果集是空的，因為每個產品型號目錄描述都包含 \<Specifications> 元素。  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. 使用 not() XQuery 函數擷取沒有 MachineHours 屬性的工作中心位置  
 以下查詢是針對 Instructions 資料行而指定。 此資料行儲存了產品型號的製造指示。  
  
 對於特定的產品型號，此查詢會擷取未指定 MachineHours 的工作中心位置。 也就是，未指定元素的屬性**MachineHours** \<Location> 。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in /AWMI:root/AWMI:Location[not(@MachineHours)]  
     return  
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ $i/@LaborHours }" >  
        </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7   
```  
  
 請記下前一個查詢中的以下事項：  
  
-   [XQuery](../xquery/modules-and-prologs-xquery-prolog.md)初構中的**declarenamespace**定義了「艾德作品製造指示」的命名空間前置詞。 其代表的命名空間跟製造指示文件中使用的相同。  
  
-   在查詢中，如果沒有**MachineHours**屬性， **not （ @MachineHours ）** 述詞就會傳回 True。  
  
 以下是結果：  
  
```  
ProductModelID Result   
-------------- --------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Not （）** 函數只支援 xs： boolean 或 node （） * 或空序列類型的引數。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
