---
title: not 函數 (XQuery) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5a39312142a2d81761320c1e5f75cefe2a85b9d7
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51673487"
---
# <a name="functions-on-boolean-values---not-function"></a>布林值的相關函式 - not 函式 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  如果為 true 的有效布林值 *$arg*為 false，而且會傳回 FALSE，如果有效的布林值 *$arg*為 true。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 具有效布林值的一連串項目。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存於各種**xml**類型資料行中的 AdventureWorks 資料庫。  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>A. 使用 not （） XQuery 函數尋找的產品型號目錄描述不包含\<規格 > 項目。  
 以下查詢會建構 XML，而此 XML 包含其目錄描述不包含 <`Specifications`> 元素的產品型號所屬識別碼。  
  
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
  
-   因為此文件使用了命名空間，所以此範例會使用 WITH NAMESPACES 陳述式。 另一個選項是使用**宣告的命名空間**中的關鍵字[XQuery 初構](../xquery/modules-and-prologs-xquery-prolog.md)定義前置詞。  
  
-   然後查詢會建構 XML，其中包含 <`Product`> 項目及其**ProductModelID**屬性。  
  
-   WHERE 子句使用[exist （） 方法 （XML 資料類型）](../t-sql/xml/exist-method-xml-data-type.md)篩選資料列。 **Exist （)** 方法會傳回 True，如果有\<p > 項目沒有\<規格 > 子項目。 請注意，使用**not （)** 函式。  
  
 此結果集是空的因為每個產品型號目錄描述包含\<規格 > 項目。  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. 使用 not() XQuery 函數擷取沒有 MachineHours 屬性的工作中心位置  
 以下查詢是針對 Instructions 資料行而指定。 此資料行儲存了產品型號的製造指示。  
  
 對於特定的產品型號，此查詢會擷取未指定 MachineHours 的工作中心位置。 也就是屬性**MachineHours**未指定\<位置 > 項目。  
  
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
  
-   **Declarenamespace**中[XQuery 初構](../xquery/modules-and-prologs-xquery-prolog.md)定義 Adventure Works 製造指示命名空間前置詞。 其代表的命名空間跟製造指示文件中使用的相同。  
  
-   在查詢中，**不 (@MachineHours)** 述詞傳回 True，如果沒有任何**MachineHours**屬性。  
  
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
  
-   **Not （)** 函式只支援類型 xs: boolean 或 node （） * 中，或空的序列的引數。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
