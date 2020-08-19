---
title: concat 函數 (XQuery) |Microsoft Docs
description: '深入瞭解 XQuery 函數 concat ( # A1，此函式會傳回藉由將指定為引數的零或多個字串串連而建立的字串。'
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
- fn:concat function
- concat function [XQuery]
ms.assetid: d50afd20-a297-445e-be9e-13b48017e7ca
author: rothja
ms.author: jroth
ms.openlocfilehash: f6fadf3bed15869ccd3d3307dcfe8b70c53d5310
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85737864"
---
# <a name="functions-on-string-values---concat"></a>字串值的相關函式 - concat
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

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
 XQuery 函式中 Surrogate 字組的行為相依於資料庫相容性層級，而且在某些情況下，還相依於函式的預設命名空間 URI。 如需詳細資訊，請參閱 [SQL Server 2016 中資料庫引擎功能的重大變更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)主題中的「XQuery 函式是可代理感知」一節。 另請參閱 [ALTER DATABASE 相容性層級 &#40;transact-sql&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 和定 [序和 Unicode 支援](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 範例資料庫的各種 **xml** 類型資料行中。  
  
### <a name="a-using-the-concat-xquery-function-to-concatenate-strings"></a>A. 使用 concat() XQuery 函式串連字串  
 對於特定產品型號，此查詢將傳回透過串連警告期限與警告描述所建立的字串。 在目錄描述檔中，<`Warranty`> 元素是由 <`WarrantyPeriod`> 和 <`Description` 子項目所組成。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
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
  
-   在 SELECT 子句中，CatalogDescription 是 **xml** 類型資料行。 因此，會使用 [查詢 ( # A1 方法 (XML 資料類型) ](../t-sql/xml/query-method-xml-data-type.md)，指示. 查詢 ( # A5）。 XQuery 陳述式是指定成查詢方法的引數。  
  
-   查詢所執行的文件將會使用命名空間。 因此， **namespace** 關鍵字是用來定義命名空間的前置詞。 如需詳細資訊，請參閱 [XQuery](../xquery/modules-and-prologs-xquery-prolog.md)初構。  
  
 以下是結果：  
  
```  
<Product ProductModelID="28" ProductModelName="Road-450">1 year-parts and labor</Product>  
```  
  
 下列查詢會擷取特定產品的資訊。 下列查詢會擷取儲存 XML 目錄描述的所有產品之相同資訊。 如果資料列中的 XML 檔有 <> 元素，WHERE 子句中的**xml**資料類型** ( # B1**方法會傳回 True `ProductDescription` 。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
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
  
 請注意，所傳回的布林值 ( **xml**類型的 **# B1**方法會與1比較。  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   SQL Server 中的 **concat ( # B1 ** 函數只接受 xs： string 類型的值。 其他的值必須明確地轉換成 xs:string 或 xdt:untypedAtomic。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
