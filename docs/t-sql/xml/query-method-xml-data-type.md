---
title: "query （) 方法 (xml 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- query method
- query() method
ms.assetid: f48f6f7b-219f-463a-bf36-bc10f21afaeb
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 22770e7338ef7a3dff5a4f4486d0543cdf75d76c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="query-method-xml-data-type"></a>query() 方法 (xml 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定執行個體的 XQuery **xml**資料型別。 結果會是**xml**型別。 該方法會傳回不具類型的 XML 執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
query ('XQuery')  
```  
  
## <a name="arguments"></a>引數  
 XQuery  
 是字串類型的 XQuery 運算式，可查詢 XML 執行個體中如元素、屬性等 XML 節點。  
  
## <a name="examples"></a>範例  
 本節提供使用 query （） 方法的範例**xml**資料型別。  
  
### <a name="a-using-the-query-method-against-an-xml-type-variable"></a>A. 針對 xml 類型變數使用 query() 方法  
 下列範例宣告一個變數 **@myDoc** 的**xml**輸入，並將 XML 執行個體指派給它。 **Query （)**方法可用來指定 XQuery，以針對文件。  
  
 查詢會擷取 <`ProductDescription`> 元素的 <`Features`> 子元素：  
  
```  
declare @myDoc xml  
set @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc.query('/Root/ProductDescription/Features')  
```  
  
 以下是結果：  
  
```  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>        
```  
  
### <a name="b-using-the-query-method-against-an-xml-type-column"></a>B. 使用針對 XML 類型資料行的 query() 方法  
 在下列範例中， **query （)**方法用來針對指定 XQuery **CatalogDescription**資料行**xml**輸入**AdventureWorks**資料庫：  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   CatalogDescription 資料行是具類型**xml**資料行。 這表示該資料行具有關聯的結構描述集合。 在[XQuery 初構](../../xquery/modules-and-prologs-xquery-prolog.md)、**命名空間**關鍵字用來定義查詢主體中稍後使用的首碼。  
  
-   **Query （)**方法會建構 XML，<`Product`> 項目具有**ProductModelID**屬性，在其中**ProductModelID**屬性值從資料庫擷取。 如需 XML 建構的詳細資訊，請參閱[XML 建構 &#40;XQuery &#41;](../../xquery/xml-construction-xquery.md).  
  
-   [Exist （） 方法 （XML 資料類型）](../../t-sql/xml/exist-method-xml-data-type.md)在 WHERE 子句用來尋找包含資料列 <`Warranty`> 在 XML 中的項目。 同樣地，**命名空間**關鍵字用來定義兩個命名空間前置詞。  
  
 以下是部份結果：  
  
```  
<Product ProductModelID="19"/>   
<Product ProductModelID="23"/>   
...  
```  
  
 注意 query() 與 exist() 方法兩個都會宣告 PD 前置詞。 在此情況下，您可以使用 WITH XMLNAMESPACES 先定義前置詞並在查詢中使用它。  
  
```  
WITH XMLNAMESPACES (  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
SELECT CatalogDescription.query('  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
## <a name="see-also"></a>請參閱＜  
 [使用 WITH XMLNAMESPACES 將命名空間加入至查詢](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
