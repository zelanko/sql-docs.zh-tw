---
title: "concat 函數 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:concat function
- concat function [XQuery]
ms.assetid: d50afd20-a297-445e-be9e-13b48017e7ca
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5f4970f431b3929268414fd78d7e834d7a835919
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="functions-on-string-values---concat"></a>針對字串值-concat 函數
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  接受零個或多個字串做為引數，並傳回串連每個引數的值所建立的字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:concat ($string as xs:string?  
           ,$string as xs:string?  
           [, ...]) as xs:string  
```  
  
## <a name="arguments"></a>引數  
 *$string*  
 要串連的選擇性字串。  
  
## <a name="remarks"></a>備註  
 函式至少需要兩個引數。 如果引數是空白時序，將以零長度的字串處理。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 XQuery 函式中 Surrogate 字組的行為相依於資料庫相容性層級，而且在某些情況下，還相依於函式的預設命名空間 URI。 如需詳細資訊，請參閱主題中的 「 XQuery 函式是 Surrogate 感知 」 區段[SQL Server 2016 中對於 Database Engine 功能的突破性變更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。 另請參閱[ALTER DATABASE 相容性層級 &#40;TRANSACT-SQL &#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)和[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型資料行中的 AdventureWorks 範例資料庫。  
  
### <a name="a-using-the-concat-xquery-function-to-concatenate-strings"></a>A. 使用 concat() XQuery 函式串連字串  
 對於特定產品型號，此查詢將傳回透過串連警告期限與警告描述所建立的字串。 在目錄描述文件中，<`Warranty`> 元素是由 <`WarrantyPeriod`> 與 <`Description`> 子元素所構成。  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
SELECT CatalogDescription.query('  
    <Product   
        ProductModelID= "{ (/pd:ProductDescription/@ProductModelID)[1] }"  
        ProductModelName = "{ sql:column("PD.Name") }" >  
        {   
          concat( string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:WarrantyPeriod)[1]), "-",  
                  string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:Description)[1]))   
         }   
     </Product>  
 ') as Result  
FROM Production.ProductModel PD  
WHERE  PD.ProductModelID=28  
  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   在 SELECT 子句中，CatalogDescription 是**xml**類型資料行。 因此， [query （） 方法 （XML 資料類型）](../t-sql/xml/query-method-xml-data-type.md)、 instructions.query。 XQuery 陳述式是指定成查詢方法的引數。  
  
-   查詢所執行的文件將會使用命名空間。 因此，**命名空間**關鍵字用來定義命名空間前置詞。 如需詳細資訊，請參閱[XQuery 初構](../xquery/modules-and-prologs-xquery-prolog.md)。  
  
 以下是結果：  
  
```  
<Product ProductModelID="28" ProductModelName="Road-450">1 year-parts and labor</Product>  
```  
  
 下列查詢會擷取特定產品的資訊。 下列查詢會擷取儲存 XML 目錄描述的所有產品之相同資訊。 **Exist （)**方法**xml** WHERE 子句會傳回 True，則資料列中的 XML 文件中的資料類型 <`ProductDescription`> 項目。  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
    <Product   
        ProductModelID= "{ (/pd:ProductDescription/@ProductModelID)[1] }"   
        ProductName = "{ sql:column("PD.Name") }" >  
        {   
          concat( string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:WarrantyPeriod)[1]), "-",  
                  string((/pd:ProductDescription/pd:Features/wm:Warranty/wm:Description)[1]))   
         }   
     </Product>  
 ') as Result  
FROM Production.ProductModel PD  
WHERE CatalogDescription.exist('//pd:ProductDescription ') = 1  
  
```  
  
 請注意，所傳回的布林值**exist （)**方法**xml**與 1 比較類型。  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Concat （)** SQL Server 中的函式只接受 xs: string 類型的值。 其他的值必須明確地轉換成 xs:string 或 xdt:untypedAtomic。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
