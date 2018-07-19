---
title: 「 自動存在 」 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5f7c111f85e3b43a560b70171f8af470a9fc505a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024765"
---
# <a name="autoexists"></a>自動存在
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  「自動存在」的概念是將 Cube 空間限制為實際存在於 Cube 中的資料格，相對因建立相同階層中的所有屬性階層成員組合而可能存在的資料格。 這是因為某個屬性階層的成員不能與相同維度中另一個屬性階層的成員同時存在。 在 SELECT 陳述式中使用相同維度的兩個以上屬性階層時，Analysis Services 會評估屬性的運算式來確認這些屬性的成員有受到正確的限制以符合所有其他屬性的準則。  
  
 例如，假設您正在使用來自 Geography 維度的屬性。 如果您所擁有的其中一個運算式會從 City 屬性傳回所有成員，而另一個運算式會將 Country 屬性的成員限制為歐洲所有國家 (地區)，這將會使得 City 成員限制為只有屬於歐洲國家 (地區) 的城市。 這是因為 Analysis Services 的自動存在特性所致。 「自動存在」僅適用於相同維度的屬性的原因是，它會嘗試防止某個屬性運算式加入其他屬性運算式中排除的維度記錄。 您也可以將「自動存在」視為不同之屬性運算式在維度資料列上所產生的交集。  
  
## <a name="cell-existence"></a>資料格存在性  
 下列資料格永遠存在：  
  
-   與相同維度中其他階層的成員相交時，每個階層的 (全部) 成員。  
  
-   與其非導出同層級相交或與其非導出同層級的父系或下階相交時的導出成員。  
  
## <a name="providing-non-existing-cells"></a>提供不存在的資料格  
 不存在的資料格是系統所提供的資料格，以回應要求不存在於 Cube 中之資料格的查詢或計算。 例如，如果 Cube 有屬於 Geography 維度的 City 屬性階層和 Country 屬性階層，以及 Internet Sales Amount 量值，此 Cube 的空間只會包含同時存在的成員。 例如，如果 City 屬性階層包含紐約、倫敦、巴黎、東京及墨爾本等城市，並且 Country 屬性階層包含美國、英國、法國、日本及澳洲等國家 (地區)，則 Cube 的空間不會包含巴黎和美國交集的空間 (資料格)。  
  
 當查詢不存在的資料格時，不存在的資料格會傳回 Null，也就是說，它們不包含計算，而且您無法定義寫入此空間的計算。 例如，下列陳述式包括了不存在的資料格。  
  
```  
SELECT [Customer].[Gender].[Gender].Members ON COLUMNS,  
{[Customer].[Customer].[Aaron A. Allen]  
   ,[Customer].[Customer].[Abigail Clark]} ON ROWS   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  這個查詢使用 [Members (Set) (MDX)](../../../mdx/members-set-mdx.md) 函數來傳回資料行軸上 Gender 屬性階層的成員集合，並且將該集合與資料列軸上 Customer 屬性階層的指定成員集合相交。  
  
 當您執行上述查詢時，Aaron A. Allen 和 Female 交集處的資料格會顯示 Null。 同樣地，Abigail Clark 和 Male 交集處的資料格也會顯示 Null。 這些資料格不存在，也不包含值，但在查詢傳回的結果中會出現不存在的資料格。  
  
 當您使用 [Crossjoin (MDX)](../../../mdx/crossjoin-mdx.md) 函數傳回相同維度中多個屬性階層之成員的交叉乘積時，自動存在功能會將所傳回的 Tuple 限制於實際存在的 Tuple 集合，而不會傳回整個笛卡兒乘積。 例如，執行下列查詢，然後檢查執行的結果。  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
         [Customer].[State-Province].Members  
  ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
> [!NOTE]  
>  請注意，0 是用來指定資料行軸，為 axis(0) (即資料行軸) 的縮寫。  
  
 上述查詢只會針對查詢中每個屬性階層之同時存在的成員傳回資料格。 上述查詢也可以使用 [* (Crossjoin) (MDX)](../../../mdx/crossjoin-mdx-operator-reference.md) 函數中新的 * 變數，改寫如下。  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
 上述查詢也可以撰寫成下列方式：  
  
```  
SELECT [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
 所傳回的資料格值將會相同，不過結果集中的中繼資料將會不同。 例如，在上述查詢中，Country 階層已移至 slicer 座標軸 (在 WHERE 子句中)，因此不會明確出現在結果集中。  
  
 上述這三個查詢示範了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中自動存在行為的作用。  
  
## <a name="deep-and-shallow-autoexists"></a>深層和淺層自動存在  
 自動存在以「深層」或「淺層」方式套用至運算式。 「深層自動存在」表示在套用 slicer 運算式、軸中的子 SELECT 運算式等之後，會評估所有運算式以符合最深層的可能空間。 「淺層自動存在」表示在目前運算式之前評估外部運算式，並將這些結果傳遞至目前運算式。 預設值是深層自動存在。  
  
 下列案例和範例有助於說明不同類型的自動存在。 在下列範例中會建立兩個集合：一個當做計算運算式，而另一個當做常數運算式。  
  
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
  
 下列範例說明深層「自動存在」的概念。 在範例中，我們會依照 [Mountain] 群組中的 [Product].[Product Line] 屬性篩選 Top10SellingProducts。 請注意，兩個屬性 (slicer 和 axis) 都屬於相同的維度，也就是 [Product]。  
  
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
  
 在上述結果集的 Top10SellingProducts 的清單中有七個新成員，而 Mountain-200、Mountain-100 和 HL Mountain Frame 已經移到清單的頂端。 在先前的結果集中，這三個值散置各處。  
  
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
  
 此結果集也就是所謂的「淺層自動存在」。 這是因為運算式是在分割子句之前接受評估的。 在先前的範例中，此運算式是常數運算式，用以說明概念。  
  
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
  
 「 自動存在 」 行為可以修改使用 AUTOEXISTS = [1 | 2 | 3] 參數中的連接字串。請參閱[支援 XMLA 屬性&#40;XMLA&#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)和<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>參數用法。  
  
## <a name="see-also"></a>另請參閱  
 [MDX & #40; 中的重要概念Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Cube 空間](../../../analysis-services/multidimensional-models/mdx/cube-space.md)   
 [Tuple](../../../analysis-services/multidimensional-models/mdx/tuples.md)   
 [使用成員、 Tuple 及集合 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [視覺化總計和非視覺化總計](../../../analysis-services/multidimensional-models/mdx/visual-totals-and-non-visual-totals.md)   
 [MDX 語言參考 & #40;MDX & #41;](../../../mdx/mdx-language-reference-mdx.md)   
 [多維度運算式 & #40;MDX & #41;參考](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
