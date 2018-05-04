---
title: string-length 函數 (XQuery) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- string-length function
- fn:string-length function
ms.assetid: 7cd69c8b-cf2c-478c-b9a3-e0e14e1aa8aa
caps.latest.revision: 46
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fcc8855c4cd41e3263e50b5e177dcdbd346d0708
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="functions-on-string-values---string-length"></a>字串值的字串長度相關函數
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回字元的字串長度。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:string-length() as xs:integer  
fn:string-length($arg as xs:string?) as xs:integer  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 要計算其長度的來源字串。  
  
## <a name="remarks"></a>備註  
 如果值 *$arg*是空的序列， **xs: integer**會傳回 0 的值。  
  
 XQuery 函數中的 Surrogate 字組行為取決於資料庫相容性層級。 如果相容性層級為 110 以上，每個 Surrogate 字組都會計算成單一字元。 對於舊版的相容性層級來說，它們會算為兩個字元。 如需詳細資訊，請參閱[ALTER DATABASE 相容性層級&#40;TRANSACT-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)和[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。  
  
 如果該值包含一個有 4 個位元組但以兩個 Surrogate 字元代表的 Unicode 字元，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 將會個別計算 Surrogate 字元。  
  
 **String-length （)** 不只能在述詞內使用的參數。 例如，以下查詢會傳回 <`ROOT`> 元素：  
  
```  
DECLARE @x xml;  
SET @x='<ROOT>Hello</ROOT>';  
SELECT @x.query('/ROOT[string-length()=5]');  
```  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 XQuery 函式中 Surrogate 字組的行為相依於資料庫相容性層級，而且在某些情況下，還相依於函式的預設命名空間 URI。 如需詳細資訊，請參閱主題中的 「 XQuery 函式是 Surrogate 感知 」 區段[SQL Server 2016 中對於 Database Engine 功能的突破性變更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。 另請參閱[ALTER DATABASE 相容性層級&#40;TRANSACT-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)和[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型 AdventureWorks 資料庫中的資料行。  
  
### <a name="a-using-the-string-length-xquery-function-to-retrieve-products-with-long-summary-descriptions"></a>A. 使用 string-length() XQuery 函式擷取摘要描述冗長的產品  
 對於摘要描述超過 50 個字元的產品，以下查詢將會擷取產品識別碼、摘要描述的長度，以及摘要本身，即 <`Summary`> 元素。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT CatalogDescription.query('  
      <Prod ProductID= "{ /pd:ProductDescription[1]/@ProductModelID }" >  
       <LongSummary SummaryLength =   
           "{string-length(string( (/pd:ProductDescription/pd:Summary)[1] )) }" >  
           { string( (/pd:ProductDescription/pd:Summary)[1] ) }  
       </LongSummary>  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('string-length( string( (/pd:ProductDescription/pd:Summary)[1]))', 'decimal') > 200;  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   WHERE 子句中的條件會擷取的資料列，只有儲存在 XML 文件中但超過 200 個字元的摘要描述。 它會使用[value （） 方法 （XML 資料類型）](../t-sql/xml/value-method-xml-data-type.md)。  
  
-   SELECT 子句只會建構您想要的 XML。 它會使用[query （） 方法 （XML 資料類型）](../t-sql/xml/query-method-xml-data-type.md)建構 XML，並指定必要的 XQuery 運算式，來擷取 XML 文件中的資料。  
  
 以下是部份結果：  
  
```  
Result  
-------------------  
<Prod ProductID="19">  
      <LongSummary SummaryLength="214">Our top-of-the-line competition   
             mountain bike. Performance-enhancing options include the  
             innovative HL Frame, super-smooth front suspension, and   
             traction for all terrain.  
      </LongSummary>  
</Prod>  
...  
```  
  
### <a name="b-using-the-string-length-xquery-function-to-retrieve-products-whose-warranty-descriptions-are-short"></a>B. 使用 string-length() XQuery 函式擷取保證描述簡短的產品  
 對於保證描述長度少於 20 個字元的產品，以下查詢將會擷取的 XML 包含產品識別碼、長度、保證描述及 <`Warranty`> 元素本身。  
  
 Warranty 是產品特性之一。 選擇性的 <`Warranty`> 子元素會跟在 <`Features`> 元素後面。  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for   $ProdDesc in /pd:ProductDescription,  
            $pf in $ProdDesc/pd:Features/wm:Warranty  
      where string-length( string(($pf/wm:Description)[1]) ) < 20  
      return   
          <Prod >  
             { $ProdDesc/@ProductModelID }  
             <ShortFeature FeatureDescLength =   
                             "{string-length( string(($pf/wm:Description)[1]) ) }" >  
                 { $pf }  
             </ShortFeature>  
          </Prod>  
     ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription')=1;  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   **pd**和**wm**會在此查詢中使用的命名空間前置詞。 它們可識別被查詢的文件中是否使用的相同名稱空間。  
  
-   XQuery 指定了巢狀的 FOR 迴圈。 外部迴圈是必要的因為您想要擷取**ProductModelID**屬性 <`ProductDescription`> 項目。 因為您只想要保證特性描述少於 20 個字元的那些產品，所以必須要內層的 FOR 迴圈。  
  
 以下是部份結果：  
  
```  
Result  
-------------------------  
<Prod ProductModelID="19">  
  <ShortFeature FeatureDescLength="15">  
    <wm:Warranty   
       xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
      <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
      <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
   </ShortFeature>  
</Prod>  
...  
```  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
