---
title: 一般 XQuery 使用案例 |Microsoft Docs
description: 查看一些一般 XQuery 使用範例，包括搜尋、抓取和列出產品目錄中的特定資料。
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, general usage cases
ms.assetid: 5187c97b-6866-474d-8bdb-a082634039cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 4756d86070e933f4c281922d54d80974832e9f5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775501"
---
# <a name="general-xquery-use-cases"></a>一般 XQuery 使用案例
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  此主題提供一般 XQuery 使用範例。  
  
## <a name="examples"></a>範例  
  
### <a name="a-query-catalog-descriptions-to-find-products-and-weights"></a>A. 查詢目錄描述來尋找產品和重量  
 下列查詢從產品目錄描述中傳回產品型號識別碼和重量 (如果有的話)。 此查詢建構具有下列格式的 XML：  
  
```  
<Product ProductModelID="...">  
  <Weight>...</Weight>  
</Product>  
```  
  
 此查詢如下：  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  <Product  ProductModelID="{ (/p1:ProductDescription/@ProductModelID)[1] }">  
     {   
       /p1:ProductDescription/p1:Specifications/Weight   
     }   
  </Product>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   XQuery 初構中的**namespace**關鍵字會定義在查詢主體中使用的命名空間前置詞。  
  
-   此查詢主體建構所需的 XML。  
  
-   在 WHERE 子句中，**存在（）** 方法只會用來尋找包含產品目錄描述的資料列。 也就是包含 <> 元素的 XML `ProductDescription` 。  
  
 以下是結果：  
  
```  
<Product ProductModelID="19"/>  
<Product ProductModelID="23"/>   
<Product ProductModelID="25"/>   
<Product ProductModelID="28"><Weight>Varies with size.</Weight></Product>  
<Product ProductModelID="34"/>  
<Product ProductModelID="35"/>  
```  
  
 下列查詢會抓取相同的資訊，但僅適用于其目錄描述包含權數的產品型號、<`Weight`> 元素（在規格中為 <> 專案） `Specifications` 。 此範例使用 WITH XMLNAMESPACES 來宣告 pd 前置詞及其命名空間繫結。 如此一來，在**query （）** 方法和**存在（）** 方法中都不會描述系結。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
          <Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
                 {   
                      /pd:ProductDescription/pd:Specifications/Weight   
                 }   
          </Product>  
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Specifications//Weight ') = 1  
```  
  
 在上一個查詢中，WHERE 子句中**xml**資料類型的**存在（）** 方法會進行檢查，查看 <> 專案中是否有 <的 `Weight`> 元素 `Specifications` 。  
  
### <a name="b-find-product-model-ids-for-product-models-whose-catalog-descriptions-include-front-angle-and-small-size-pictures"></a>B. 尋找其目錄描述中含有正面角度和小圖片之產品型號的產品型號識別碼  
 XML 產品目錄描述包含產品圖片、<`Picture`> 元素。 每一張圖片有數個屬性。 其中包括圖片角度、<`Angle`> 元素，以及大小 <`Size`> 元素。  
  
 對於目錄描述中含有正面角度和小圖片的產品型號，查詢會建構具有下列格式的 XML：  
  
```  
< Product ProductModelID="...">  
  <Picture>  
    <Angle>front</Angle>  
    <Size>small</Size>  
  </Picture>  
</Product>  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT CatalogDescription.query('  
   <pd:Product  ProductModelID="{ (/pd:ProductDescription/@ProductModelID)[1] }">  
      <Picture>  
         {  /pd:ProductDescription/pd:Picture/pd:Angle }   
         {  /pd:ProductDescription/pd:Picture/pd:Size }   
      </Picture>  
   </pd:Product>  
') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription/pd:Picture') = 1  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Angle)[1]', 'varchar(20)')  = 'front'  
AND   CatalogDescription.value('(/pd:ProductDescription/pd:Picture/pd:Size)[1]', 'varchar(20)')  = 'small'  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   在 WHERE 子句中，**存在（）** 方法只會用來抓取具有 <> 元素之產品目錄描述的資料列 `Picture` 。  
  
-   WHERE 子句會使用**value （）** 方法兩次來比較 <`Size`> 和 <`Angle`> 元素的值。  
  
 以下是部份結果：  
  
```  
<p1:Product   
  xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
  ProductModelID="19">  
  <Picture>  
    <p1:Angle>front</p1:Angle>  
    <p1:Size>small</p1:Size>  
  </Picture>  
</p1:Product>  
...  
```  
  
### <a name="c-create-a-flat-list-of-the-product-model-name-and-feature-pairs-with-each-pair-enclosed-in-the-features-element"></a>C. 建立產品型號名稱和功能配對的一般清單，並將每個配對包含在 \<Features> 元素中  
 在產品型號目錄描述中，XML 包含數個產品功能。 所有這些功能都包含在 <`Features`> 元素中。 查詢會使用[Xml 結構（XQuery）](../xquery/xml-construction-xquery.md)來建立所需的 xml。 大括號內的運算式由結果取代。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  for $pd in /p1:ProductDescription,  
   $f in $pd/p1:Features/*  
  return  
   <Feature>  
     <ProductModelName> { data($pd/@ProductModelName) } </ProductModelName>  
     { $f }  
  </Feature>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   $pd/p1： Features/* 只會傳回 <> 的元素節點子系 `Features` ，但 $pd/p1： features/node （）會傳回所有節點。 這包括元素節點、文字節點、處理指示和註解。  
  
-   兩個 FOR 迴圈產生一個 Cartesian 產品，並從中傳回產品名稱和個別功能。  
  
-   **ProductName**是一個屬性。 此查詢中的 XML 建構以元素傳回它。  
  
 以下是部份結果：  
  
```  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p1:Warranty   
   xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
</Feature>  
<Feature>  
 <ProductModelName>Mountain 100</ProductModelName>  
 <ProductModelID>19</ProductModelID>  
 <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer   
           or any AdventureWorks retail store.</p2:Description>  
    </p2:Maintenance>  
</Feature>  
...  
...      
```  
  
### <a name="d-from-the-catalog-description-of-a-product-model-list-the-product-model-name-model-id-and-features-grouped-inside-a-product-element"></a>D. 從產品型號的目錄描述中，列出產品型號名稱、模型識別碼，以及群組在元素內的功能 \<Product>  
 下列查詢會使用產品型號的目錄描述中所儲存的資訊，來列出專案內分組的產品型號名稱、模型識別碼和功能 \<Product> 。  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>  
         <ProductModelName>   
           { data(/pd:ProductDescription/@ProductModelName) }   
         </ProductModelName>  
         <ProductModelID>   
           { data(/pd:ProductDescription/@ProductModelID) }   
         </ProductModelID>  
         { /pd:ProductDescription/pd:Features/* }  
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 以下是部份結果：  
  
```  
<Product>  
  <ProductModelName>Mountain 100</ProductModelName>  
  <ProductModelID>19</ProductModelID>  
  <p1:Warranty>... </p1:Warranty>  
  <p2:Maintenance>...  </p2:Maintenance>  
  <p3:wheel xmlns:p3="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p3:wheel>  
  <p4:saddle xmlns:p4="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p5:i xmlns:p5="http://www.w3.org/1999/xhtml">Anatomic design</p5:i> and made from durable leather for a full-day of riding in comfort.</p4:saddle>  
  <p6:pedal xmlns:p6="https://www.adventure-works.com/schemas/OtherFeatures">  
    <p7:b xmlns:p7="http://www.w3.org/1999/xhtml">Top-of-the-line</p7:b> clipless pedals with adjustable tension.</p6:pedal>  
   ...  
```  
  
### <a name="e-retrieve-product-model-feature-descriptions"></a>E. 擷取產品型號功能描述  
 下列查詢會建立 XML，其中包含 `Product` 具有**ProducModelID**、 **ProductModelName**屬性和前兩個產品功能的 <> 元素。 具體而言，前兩個產品功能是 <> 元素的前兩個子項目 `Features` 。 如果有更多的功能，它會傳回空的 <`There-is-more/`> 元素。  
  
```  
SELECT CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   .。。RETURN 迴圈結構會抓取前兩個產品功能。 **Position （）** 函數是用來尋找序列中專案的位置。  
  
### <a name="f-find-element-names-from-the-product-catalog-description-that-end-with-ons"></a>F. 從產品目錄描述中尋找結尾是 "ons" 的元素名稱  
 下列查詢會搜尋目錄描述，並傳回 <`ProductDescription`> 元素中名稱結尾為 "ons" 的所有元素。  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in /p1:ProductDescription/*[substring(local-name(.),string-length(local-name(.))-2,3)="ons"]  
      return   
          <Root>  
             { $pd }  
          </Root>  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription is not NULL  
```  
  
 以下是部份結果：  
  
```  
ProductModelID   Result  
-----------------------------------------  
         19        <Root>         
                     <p1:Specifications xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">          
                          ...         
                     </p1:Specifications>         
                   </Root>          
```  
  
### <a name="g-find-summary-descriptions-that-contain-the-word-aerodynamic"></a>G. 尋找包含 "Aerodynamic" 一字的摘要描述  
 下列查詢擷取其目錄描述的摘要描述中包含 "Aerodynamic" 一字的產品型號：  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
          <Prod >  
             { /pd:ProductDescription/@ProductModelID }  
             { /pd:ProductDescription/pd:Summary }  
          </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('  
     contains( string( (/pd:ProductDescription/pd:Summary)[1] ),"Aerodynamic")','bit') = 1  
```  
  
 請注意，SELECT 查詢會指定**xml**資料類型的**query （）** 和**value （）** 方法。 因此，不在兩個不同的查詢初構中重複命名空間宣告兩次，而是在查詢中使用前置詞 pd，並且只使用 WITH XMLNAMESPACES 定義一次。  
  
 請注意下列項目是從上一個查詢而來：  
  
-   WHERE 子句是用來只抓取目錄描述在 <> 專案中包含 "Aerodynamic 一字" 一字的資料列 `Summary` 。  
  
-   **Contains （）** 函式可用來查看文字中是否包含單字。  
  
-   **Xml**資料類型的**value （）** 方法會將**contains （）** 所傳回的值與1進行比較。  
  
 以下是結果：  
  
```  
ProductModelID Result        
-------------- ------------------------------------------  
28     <Prod ProductModelID="28">  
        <pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
       <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">  
         A TRUE multi-sport bike that offers streamlined riding and a  
         revolutionary design. Aerodynamic design lets you ride with the   
         pros, and the gearing will conquer hilly roads.</p1:p>  
       </pd:Summary>  
      </Prod>    
```  
  
### <a name="h-find-product-models-whose-catalog-descriptions-do-not-include-product-model-pictures"></a>H. 尋找其目錄描述不包含產品型號圖片的產品型號  
 下列查詢會針對其目錄描述不包含 <> 元素的產品型號，抓取 ProductModelIDs `Picture` 。  
  
```  
SELECT  ProductModelID  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not NULL  
AND     CatalogDescription.exist('declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /p1:ProductDescription/p1:Picture  
') = 0  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   如果 WHERE 子句中的**存在（）** 方法傳回 False （0），則會傳回產品型號識別碼。 否則，不傳回它。  
  
-   由於所有產品描述都包含 <`Picture`> 元素，因此在此情況下，結果集是空的。  
  
## <a name="see-also"></a>另請參閱  
 [涉及階層的 Xquery](../xquery/xqueries-involving-hierarchy.md)   
 [涉及訂單的 Xquery](../xquery/xqueries-involving-order.md)   
 [Xquery 處理關聯式資料](../xquery/xqueries-handling-relational-data.md)   
 [XQuery 中的字串搜尋](../xquery/string-search-in-xquery.md)   
 [在 XQuery 中處理命名空間](../xquery/handling-namespaces-in-xquery.md)   
 [使用 WITH WITH XMLNAMESPACES 將命名空間新增至查詢](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
