---
title: "路徑運算式步驟中指定述詞 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- axis step [XQuery]
- predicates [XQuery]
- qualifiers [XQuery]
- path expressions [XQuery]
ms.assetid: 2660ceca-b8b4-4a1f-98a0-719ad5f89f81
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 05290d3f2906136a1d058b63b182877a3226f64e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="path-expressions---specifying-predicates"></a>路徑運算式-指定述詞
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  主題中所述[中 XQuery 路徑運算式](../xquery/path-expressions-xquery.md)，路徑運算式中的軸步包含下列元件：  
  
-   [軸](../xquery/path-expressions-specifying-axis.md)。  
  
-   節點測試。 如需詳細資訊，請參閱[路徑運算式步驟中指定節點測試](../xquery/path-expressions-specifying-node-test.md)。  
  
-   零或多個述詞。 這是選擇性的。  
  
 選擇性的述詞是路徑運算式中軸步驟的第三個部份。  
  
## <a name="predicates"></a>述詞  
 述詞是用來套用指定的測試，以篩選節點序列。 述詞運算式是用方括號括住，並會繫結到路徑運算式中的最後一個節點。  
  
 例如，假設 SQL 參數值 (x) **xml**宣告資料型別，如下列所示：  
  
```  
declare @x xml  
set @x = '  
<People>  
  <Person>  
    <Name>John</Name>  
    <Age>24</Age>  
  </Person>  
  <Person>  
    <Name>Goofy</Name>  
    <Age>54</Age>  
  </Person>  
  <Person>  
    <Name>Daffy</Name>  
    <Age>30</Age>  
  </Person>  
</People>  
'  
```  
  
 在此情況下，下列是在三個不同節點層級的每個層級中，使用述詞值 [1] 的有效運算式：  
  
```  
select @x.query('/People/Person/Name[1]')  
select @x.query('/People/Person[1]/Name')  
select @x.query('/People[1]/Person/Name')  
```  
  
 請注意，在每個情況下，述詞都會繫結到路徑運算式中述詞所套用到的節點。 例如，第一個路徑運算式會選取每個 /People/Person 節點內的第一個 <`Name`> 元素，並以提供的 XML 執行個體傳回下列項目：  
  
```  
<Name>John</Name><Name>Goofy</Name><Name>Daffy</Name>  
```  
  
 但是，第二個路徑運算式會選取第一個 /People/Person 節點下的所有 <`Name`> 元素。 因此，它會傳回下列項目：  
  
```  
<Name>John</Name>  
```  
  
 括號也可以用來變更述詞的評估順序。 例如，在下列運算式中，會使用一組括號將 (/People/Person/Name) 路徑與述詞 [1] 隔開：  
  
```  
select @x.query('(/People/Person/Name)[1]')  
```  
  
 在此範例中，套用述詞的順序會變更。 這是因為會先評估括住的路徑 (/People/Person/Name)，然後述詞 [1] 運算子會套用到含有符合括住路徑之所有節點的集合。 若沒有括號，則作業的順序會與套用 [1] 做為 `child::Name` 節點測試不同，但類似第一個路徑運算式的範例。  
  
### <a name="quantifiers-and-predicates"></a>數量詞及述詞  
 在述詞本身的括號內，可多次使用及加入數量詞。 例如，沿用上一個範例，以下是在複雜的述詞子運算式內，有效使用一個以上數量詞的範例。  
  
```  
select @x.query('/People/Person[contains(Name[1], "J") and xs:integer(Age[1]) < 40]/Name/text()')  
```  
  
 述詞運算式的結果會轉換為布林值，而且會被參考為述詞真值。 只有述詞真值為 True 之序列中的節點，會在結果中傳回。 其他所有的節點都會被捨棄。  
  
 例如，下列路徑運算式在它的第二個步驟包括了述詞：  
  
```  
/child::root/child::Location[attribute::LocationID=10]  
```  
  
 此述詞指定的條件會套用到所有 <`Location`> 元素節點子系。 結果是，只會傳回 LocationID 屬性值為 10 的那些工作中心位置。  
  
 上一個路徑運算式會在下列的 SELECT 陳述式中執行：  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
 /child::AWMI:root/child::AWMI:Location[attribute::LocationID=10]  
')  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
### <a name="computing-predicate-truth-values"></a>計算述詞真值  
 根據 XQuery 規格，套用下列規則以判斷述詞真值：  
  
1.  若述詞運算式的值是空的序列，則述詞真值為 False。  
  
     例如：  
  
    ```  
    SELECT Instructions.query('  
    declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     /child::AWMI:root/child::AWMI:Location[attribute::LotSize]  
    ')  
    FROM Production.ProductModel  
    WHERE ProductModelID=7  
    ```  
  
     此查詢中的路徑運算式只會傳回那些指定了 LotSize 屬性的 <`Location`> 元素節點。 若述詞針對特定的 <`Location`> 傳回空的序列，則結果中就不會傳回該工作中心位置。  
  
2.  述詞值只能是 xs: integer、 xs: boolean 或節點\*。 節點\*，述詞評估為任何節點，如果為 True 和 False 空的序列。 任何其他數值類型 (例如 Double 和浮點類型) 都會產生靜態類型錯誤。 只有當產生的整數等於內容位置的值時，運算式的述詞真值才是 True。 此外，只有整數常值和**last （)**函數減少為 1 的已篩選之步驟運算式的基數。  
  
     例如，下列查詢會擷取 <`Features`> 元素的第三個子元素節點。  
  
    ```  
    SELECT CatalogDescription.query('  
    declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /child::PD:ProductDescription/child::PD:Features/child::*[3]  
    ')  
    FROM Production.ProductModel  
    WHERE ProductModelID=19  
    ```  
  
     請注意下列項目是從上一個查詢而來：  
  
    -   運算式中的第三個步驟會指定其值為 3 的述詞運算式。 因此，只有在節點的內容位置為 3 時，這個運算式的述詞真值才會是 True。  
  
    -   第三個步驟也指定了萬用字元 (*)，表示節點測試中的所有節點。 但是，述詞會篩選節點，並且只會傳回在第三個位置的節點。  
  
    -   查詢會傳回文件根節點之 <`ProductDescription`> 元素子系之 <`Features`> 元素子系的第三個子元素節點。  
  
3.  若述詞運算式的值是一個簡單類型的布林類型值，則此述詞真值會等於述詞運算式的值。  
  
     例如，下列查詢針對指定**xml**保留 XML 執行個體時，客戶調查 XML 執行個體的型別變數。 此查詢會擷取那些有孩童的客戶。 在此查詢中，也就是\<h > 1\</HasChildren >。  
  
    ```  
    declare @x xml  
    set @x='  
    <Survey>  
      <Customer CustomerID="1" >  
      <Age>27</Age>  
      <Income>20000</Income>  
      <HasChildren>1</HasChildren>  
      </Customer>  
      <Customer CustomerID="2" >  
      <Age>27</Age>  
      <Income>20000</Income>  
      <HasChildren>0</HasChildren>  
      </Customer>  
    </Survey>  
    '  
    declare @y xml  
    set @y = @x.query('  
      for $c in /child::Survey/child::Customer[( child::HasChildren[1] cast as xs:boolean ? )]  
      return   
          <CustomerWithChildren>  
              { $c/attribute::CustomerID }  
          </CustomerWithChildren>  
    ')  
    select @y  
    ```  
  
     請注意下列項目是從上一個查詢而來：  
  
    -   中的運算式**如**迴圈具有兩個步驟，和第二個步驟指定述詞。 此述詞的值是布林類型的值。 若此值是 True，則此述詞的真值也會是 True。  
  
    -   此查詢會傳回 <`Customer`> 元素子系，其述詞的值為 True 的\<調查 > 文件根項目子系。 以下是結果：  
  
        ```  
        <CustomerWithChildren CustomerID="1"/>   
        ```  
  
4.  若述詞運算式的值是包含至少一個節點的序列，則述詞真值為 True。  
  
 例如，下列查詢擷取其 XML 目錄描述都包含至少一個功能的子元素的產品型號的 ProductModelID <`Features`> 項目，從相關聯的命名空間**wm**前置詞。  
  
```  
SELECT ProductModelID  
FROM   Production.ProductModel  
WHERE CatalogDescription.exist('  
             declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
             /child::PD:ProductDescription/child::PD:Features[wm:*]  
             ') = 1  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   WHERE 子句會指定[exist （） 方法 （XML 資料類型）](../t-sql/xml/exist-method-xml-data-type.md)。  
  
-   內的路徑運算式**exist （)**方法在第二個步驟中指定述詞。 如果述詞運算式傳回至少有一項功能的序列，則這個述詞運算式的真值為 True。 在此情況下，因為**exist （)**方法會傳回 True，因此會傳回 ProductModelID。  
  
## <a name="static-typing-and-predicate-filters"></a>靜態類型及述詞篩選  
 述詞也可能會影響運算式的靜態推斷類型。 整數常值和**last （)**函數最多一個已篩選之步驟運算式的基數減少。  
  
  
