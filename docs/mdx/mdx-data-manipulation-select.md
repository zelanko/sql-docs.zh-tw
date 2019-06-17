---
title: SELECT 陳述式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f803ea892166819cee846a7dc97ef435802e9ae3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187636"
---
# <a name="mdx-data-manipulation---select"></a>MDX 資料操作 - SELECT


  擷取指定 Cube 的資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
[ WITH <SELECT WITH clause>   
   [ , <SELECT WITH clause>...n ]   
]   
SELECT   
     [ *   
    | ( <SELECT query axis clause>   
                  [ , <SELECT query axis clause>,...n ]   
            )   
            ]  
FROM   
   <SELECT subcube clause>   
      [ <SELECT slicer axis clause> ]  
      [ <SELECT cell property list clause> ]  
  
<SELECT WITH clause> ::=  
     ( CELL CALCULATION <CREATE CELL CALCULATION body clause> )   
   | ( [ CALCULATED ] MEMBER <CREATE MEMBER body clause>)   
   | ( SET <CREATE SET body clause>)  
   | ( MEASURE = <measure body clause> )  
  
<SELECT query axis clause> ::=  
   [ NON EMPTY ] Set_Expression  
   [ <SELECT dimension property list clause> ]   
      ON   
            Integer_Expression   
       | AXIS(Integer)   
       | COLUMNS   
       | ROWS   
       | PAGES   
       | SECTIONS   
       | CHAPTERS   
  
<SELECT subcube clause> ::=  
      Cube_Name   
   | [NON VISUAL] (SELECT   
                  [ *   
       | ( <SELECT query axis clause> [ ,   
           <SELECT query axis clause>,...n ] )   
         ]   
            FROM   
         <SELECT subcube clause>   
         <SELECT slicer axis clause> )  
  
<SELECT slicer axis clause> ::=   
      WHERE Tuple_Expression  
  
<SELECT cell property list clause> ::=   
   [ CELL ] PROPERTIES CellProperty_Name   
      [ , CellProperty_Name,...n ]  
  
<SELECT dimension property list clause> ::=  
   [DIMENSION] PROPERTIES   
      (DimensionProperty_Name   
         [,DimensionProperty_Name,...n ] )   
    | (LevelProperty_Name   
         [, LevelProperty_Name,...n ] )   
    | (MemberProperty_Name   
         [, MemberProperty_Name,...n ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Integer*  
 介於 0 和 127 之間的整數。  
  
 *Cube_Name*  
 提供 Cube 名稱的有效字串。  
  
 *Tuple_Expression*  
 傳回 Tuple 的有效多維度運算式 (MDX) 運算式。  
  
 *CellProperty_Name*  
 代表資料格屬性的有效字串。  
  
 *DimensionProperty_Name*  
 代表維度屬性的有效字串。  
  
 *LevelProperty_Name*  
 代表層級屬性的有效字串。  
  
 *MemberProperty_Name*  
 代表成員屬性的有效字串。  
  
## <a name="remarks"></a>備註  
 `<SELECT slicer axis clause>` 運算式必須包含維度與階層中的成員，除了指定的 `<SELECT query axis clause>` 運算式中所參考的以外。  
  
 如果指定的 `<SELECT query axis clause>` 運算式與 `<SELECT slicer axis clause>` 值省略了 Cube 中的屬性，屬性的預設成員便會隱含地加入 Slicer 座標軸。  
  
 子選擇陳述式中的 NON VISUAL 選項，可以讓您在篩選出成員的同時，保留實際總計而非篩選後的總計。 如此一來，您可以查詢前十筆銷售 (人員/產品/地區) 並取得所有查詢成員的實際銷售總計，而不只是傳回的前十筆銷售額總計。 如需詳細資訊，請參閱以下範例。  
  
 導出的成員可以包含在\<query axis clause>&lt > 只要使用連接字串參數開啟連線*子查詢 = 1*; 請參閱[支援的 XMLA 屬性&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)並<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>參數用法。 以下提供子選擇中的導出成員範例。  
  
## <a name="autoexists"></a>自動存在  
 在 SELECT 陳述式中使用兩個或多個維度屬性時，Analysis Services 會評估屬性的運算式來確認這些屬性的成員有受到正確的限制以符合所有其他屬性的準則。 例如，假設您正在使用來自 Geography 維度的屬性。 如果您所擁有的其中一個運算式會從 City 屬性傳回所有成員，而另一個運算式會將 Country 屬性的成員限制為歐洲所有國家 (地區)，這將會使得 City 成員限制為只有屬於歐洲國家 (地區) 的城市。 Analysis Services 的這個特性稱為「自動存在」，僅適用於相同維度中的屬性。 「自動存在」僅適用於相同維度的屬性的原因是，它會嘗試防止某個屬性運算式加入其他屬性運算式中排除的維度記錄。 您也可以將「自動存在」視為不同之屬性運算式在維度記錄上所產生的交集。 請參閱下列範例：  
  
 `//Obtain the Top 10 best reseller selling products by Name`  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 取得的結果集為：  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**折扣量**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0.04%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2.47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0.05%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0.57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
|**Road-150**|**$2,363,805.16**|**$0.00**|**0.00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3.89%**|  
  
 取得的產品集似乎與 Preferred10Products 相同，因此，確認 Preferred10Products 集合：  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 根據以下結果，兩個集合 (Top10SellingProducts、Preferred10Products) 相同  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**折扣量**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0.04%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2.47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0.05%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0.57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
|**Road-150**|**$2,363,805.16**|**$0.00**|**0.00%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3.89%**|  
  
 在先前的範例中，我們建立了兩個集合：一個當做計算運算式，而另一個當做常數運算式。 這些範例說明「自動存在」的不同類別。  
  
 「自動存在」可以深層或淺層套用到運算式。 預設值是深層。 下列範例說明深層「自動存在」的概念。 在範例中，我們會依照 [Mountain] 群組中的 [Product].[Product Line] 屬性篩選 Top10SellingProducts。 請注意，兩個屬性 (slicer 和 axis) 都屬於相同的維度，也就是 [Product]。  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `// Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 產生下列結果集：  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**折扣量**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
|**Mountain-300**|**$1,907,249.38**|**$876.95**|**0.05%**|  
|**Mountain-500**|**$1,067,327.31**|**$17,266.09**|**1.62%**|  
|**Mountain-400-W**|**$592,450.05**|**$303.49**|**0.05%**|  
|**LL Mountain Frame**|**$521,864.42**|**$252.41**|**0.05%**|  
|**ML Mountain Frame-W**|**$482,953.16**|**$206.95**|**0.04%**|  
|**ML Mountain Frame**|**$343,785.29**|**$161.82**|**0.05%**|  
|**Women's Mountain Shorts**|**$260,304.09**|**$6,675.56**|**2.56%**|  
  
 在先前結果集的 Top10SellingProducts 的清單中有七個新成員，而 Mountain-200、Mountain-100 和 HL Mountain Frame 已經移到清單的頂端。 在先前的結果集中，這三個值會顛倒  
  
 這稱為「深層自動存在」，因為 Top10SellingProducts 集合經過評估以符合查詢的分割條件。 「深層自動存在」表示在套用 slicer 運算式、軸中的子 SELECT 運算式等之後，會評估所有運算式以符合最深層的可能空間。  
  
 不過，使用者可能會想要能夠針對相當於 Preferred10Products 的 Top10SellingProducts 進行分析，如以下範例所示：  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 產生下列結果集：  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**折扣量**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
  
 在以上的結果中，分割的結果如預期般僅包含屬於 [Product].[Product Line] 中之 [Mountain] 群組的 Preferred10Products 產品，因為 Preferred10Products 是常數運算式。  
  
 此結果集也就是所謂的淺層「自動存在」。 這是因為運算式是在分割子句之前接受評估的。 在先前的範例中，此運算式是常數運算式，用以說明概念。  
  
 「自動存在」行為可以在工作階段層級使用 **Autoexists** 連接字串屬性進行修改。 下列範例會先開啟新的工作階段，並將 *Autoexists=3* 屬性加入到連接字串。 您必須開啟一個新的連接才能執行範例。 一旦利用「自動存在」設定建立連接之後，在該連接完成之前，它都會保持在作用中。  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `//Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 下列結果集現在會顯示「自動存在」的淺層行為。  
  
|||||  
|-|-|-|-|  
||**Reseller Sales Amount**|**折扣量**|**PCT Discount**|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0.13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1.63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0.01%**|  
  
 「 自動存在 」 行為可以修改使用 「 自動存在 」 = [1 | 2 | 3] 參數中的連接字串;請參閱[支援的 XMLA 屬性&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)並<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>參數用法。  
  
## <a name="examples"></a>範例  
 下列範例會傳回的總和`Measures.[Order Quantity]`成員前, 八個月 2003年日曆年度中包含在彙總`Date`維度中，從**Adventure Works** cube。  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 若要了解**NON VISUAL，** 下列範例是如何取得 [Reseller Sales Amount] 數字，其中產品類別目錄的資料行和轉售商商務類型的資料列的資料表中的 [Adventure Works] 的查詢。 請注意，產品和轉售商的總計都有提供。  
  
 下列 SELECT 陳述式：  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 會產生下列結果：  
  
|||||||  
|-|-|-|-|-|-|  
||**All Products**|**Accessories**|**Bikes**|**服裝**|**Components**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$66,302,381.56**|**$1,777,840.84**|**$11,799,076.66**|  
|**Specialty Bike Shop**|**$6,756,166.18**|**$65,125.48**|**$6,080,117.73**|**$252,933.91**|**$357,989.07**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$30,892,354.33**|**$592,385.71**|**$3,307,774.48**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$29,329,909.50**|**$932,521.23**|**$8,133,313.11**|  
  
 若要只針對產品為 Accessories 和 Clothing，且轉售商為 Value Added Reseller 和 Warehouse 的資料產生資料表，但同時保留全部項目的總計，可以使用 NON VISUAL 撰寫如下：  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 會產生下列結果：  
  
|||||  
|-|-|-|-|  
||**All Products**|**Accessories**|**Clothing**|  
|**All Resellers**|**$80,450,596.98**|**$571,297.93**|**$1,777,840.84**|  
|**Value Added Reseller**|**$34,967,517.33**|**$175,002.81**|**$592,385.71**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$932,521.23**|  
  
 若要產生可以視覺化總計資料行，但就資料列總計傳回所有 [Category] 的實際總計，應發出下列查詢：  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0`  
  
 `from ( Select {[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 0`  
  
 `from [Adventure Works])`  
  
 `)`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 請注意如何將 NON VISUAL 只套用到 [Category]。  
  
 上述的查詢會產生下列結果：  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 與前一個結果相比，您可以發現 [All Resellers] 資料列現在只總計 [Value Added Reseller] 和 [Warehouse] 的顯示值，但 [All Products] 資料行顯示所有產品 (包括未顯示產品) 的總計值。  
  
 以下範例示範如何在子選擇中使用導出成員，以篩選出這些成員。 若要能夠重現此範例中，建立的連接必須使用連接字串參數*的子查詢 = 1*。  
  
 `select Measures.allmembers on 0`  
  
 `from (`  
  
 `Select { [Measures].[Reseller Sales Amount]`  
  
 `, [Measures].[Reseller Total Product Cost]`  
  
 `, [Measures].[Reseller Gross Profit]`  
  
 `, [Measures].[Reseller Gross Profit Margin]`  
  
 `} on 0`  
  
 `from [Adventure Works]`  
  
 `)`  
  
 上述的查詢會產生下列結果：  
  
|||||  
|-|-|-|-|  
|Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|Reseller Gross Profit Margin|  
|$80,450,596.98|$79,980,114.38|$470,482.60|0.58%|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 的關鍵概念 &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [MDX 資料操作陳述式&#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [利用查詢與 Slicer 軸限制查詢&#40;MDX&#41;](~/analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)  
  
  

