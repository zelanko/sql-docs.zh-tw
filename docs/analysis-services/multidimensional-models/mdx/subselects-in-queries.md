---
title: "子選擇中查詢 |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9e361798-688e-4b11-9eef-31fc793e8ba4
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 32dfe1b5c7367121bd36dae57d0175304fc2fe14
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="subselects-in-queries"></a>查詢中的子選擇
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
子選擇運算式是巢狀 SELECT 運算式，用於限制評估外部 SELECT 的 Cube 空間。 子選擇可讓您定義評估所有計算的新空間。  
  
## <a name="subselects-by-example"></a>子選擇範例  
 首先，我們先來看一個範例，了解子選擇如何協助產生所要的結果。 假設您受他人之託為多年來前 10 項暢銷產品的銷售行為產生資料表。  
  
 結果應該如下表所示：  
  
|||||  
|-|-|-|-|  
||所有年的總和|第 1 年|...|  
|前 10 項暢銷產品的總和||||  
|產品 A||||  
|...||||  
  
 若要得到如上表的結果，可以撰寫下列 MDX 運算式：  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].MEMBERS  
               , 10  
               , [Measures].[Sales Amount]  
               ) ON 1  
  FROM [Adventure Works]  
```  
  
 傳回下列結果：  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 20062|CY 2007|CY 2008|  
|All Products|$80,450,596.98|$8,065,435.31|$24,144,429.65|$32,202,669.43|$16,038,062.60|  
|Mountain-200 Black, 38|$1,634,647.94|(Null)|(Null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(Null)|(Null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(Null)|(Null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(Null)|(Null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(Null)|(Null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(Null)|(Null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(Null)|(Null)|  
|Mountain-200 Black, 38|$1,471,078.72|(Null)|$789,958.49|$681,120.23|(Null)|  
|Road-350-W Yellow, 48|$1,380,253.88|(Null)|(Null)|$744,988.37|$635,265.50|  
  
 除了查詢傳回 9 項產品而不是 10 項產品，而且 All Products 總計反映所有產品的總和而不是所傳回前 9 項產品的總和 (在此例中)，這非常接近我們所要的結果。 下列 MDX 查詢中提供另一個解決問題的嘗試：  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , TOPCOUNT( [Product].[Product].CHILDREN, 10, [Measures].[Sales Amount]) ON 1  
  FROM [Adventure Works]  
```  
  
 傳回下列結果：  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|Mountain-200 Black, 38|$1,634,647.94|(Null)|(Null)|$894,207.97|$740,439.97|  
|Mountain-200 Black, 42|$1,285,524.65|(Null)|(Null)|$722,137.65|$563,387.00|  
|Mountain-200 Silver, 38|$1,181,945.82|(Null)|(Null)|$634,600.78|$547,345.03|  
|Mountain-200 Black, 46|$995,927.43|(Null)|(Null)|$514,995.76|$480,931.68|  
|Mountain-200 Silver, 42|$1,005,111.77|(Null)|(Null)|$529,543.29|$475,568.49|  
|Mountain-200 Silver, 46|$975,932.56|(Null)|(Null)|$526,759.30|$449,173.26|  
|Road-150 Red, 56|$792,228.98|$382,159.24|$410,069.74|(Null)|(Null)|  
|Mountain-200 Black, 38|$1,471,078.72|(Null)|$789,958.49|$681,120.23|(Null)|  
|Road-350-W Yellow, 48|$1,380,253.88|(Null)|(Null)|$744,988.37|$635,265.50|  
|Road-150 Red, 62|$566,797.97|$234,018.86|$332,779.11|(Null)|(Null)|  
  
 這非常接近所要的結果，因為只遺漏產品的總和。 這時可以開始調整上述 MDX 運算式，加入遺漏的一行；不過，該項工作相當繁雜。  
  
 另一個解決問題的作法是從重新定義解析 MDX 運算式的 Cube 空間開始思考。 假設「新的」Cube 只包含前 10 項產品的資料？ 該 Cube 就會將 All 成員調整為僅限前 10 項產品，現在只要簡單查詢即可解決需求。  
  
 下列 MDX 運算式使用子選擇陳述式，將 Cube 空間重新定義為前 10 項產品並產生所要的結果：  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 上述運算式會傳回下列結果：  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$19,997,183.30|$1,696,815.63|$2,816,611.28|$7,930,797.72|$7,552,958.66|  
|Mountain-200 Silver, 38|$2,160,981.60|(Null)|(Null)|$1,024,359.10|$1,136,622.49|  
|Mountain-200 Silver, 42|$1,914,547.85|(Null)|(Null)|$903,061.68|$1,011,486.18|  
|Mountain-200 Silver, 46|$1,906,248.55|(Null)|(Null)|$877,077.79|$1,029,170.76|  
|Mountain-200 Black, 38|$1,811,229.02|(Null)|$896,511.60|$914,717.43|(Null)|  
|Mountain-200 Black, 38|$2,589,363.78|(Null)|(Null)|$1,261,406.37|$1,327,957.41|  
|Mountain-200 Black, 42|$2,265,485.38|(Null)|(Null)|$1,126,055.89|$1,139,429.49|  
|Mountain-200 Black, 46|$1,957,528.24|(Null)|(Null)|$946,453.88|$1,011,074.37|  
|Road-150 Red, 62|$1,769,096.69|$828,011.68|$941,085.01|(Null)|(Null)|  
|Road-150 Red, 56|$1,847,818.63|$868,803.96|$979,014.67|(Null)|(Null)|  
|Road-350-W Yellow, 48|$1,774,883.56|(Null)|(Null)|$877,665.59|$897,217.96|  
  
 上述結果正是我們所要的結果。  
  
 讓我們檢閱子選擇實際上執行哪些工作。 子選擇傳回新 Cube，其中包含產品的所有其他不變維度，但在產品維度中會篩選所有成員，以符合我們有興趣的前 10 項產品， 如同移除所有不符合「前 10 個」準則的所有資料並重新建立 Cube 一樣。 此範例中另一個要了解的重要概念是，前 10 項產品是對 Cube 中所有其他維度的 All 成員計算而得的；前者為 True 因為子選擇中未加入其他篩選限制。  
  
 子選擇可以視需要變得複雜，下列範例示範如何產生類似上表的資料表，但在 Sales Territory 維度上篩選 France 以及在 Sales Channel 維度上篩選 Internet。  
  
```  
SELECT [Date].[Calendar Year].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN  
                       , 10  
                       , [Measures].[Sales Amount]  
                       ) ON 0  
             , [Sales Territory].[Sales Territory].[Region].[France] on 1  
             ,  [Sales Channel].[Sales Channel].[Internet] on 2  
          FROM [Adventure Works]  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 產生下列結果：  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2005|CY 2006|CY 2007|CY 2008|  
|All Products|$748,682.49|$32,204.43|$73,125.18|$269,506.56|$373,846.32|  
|Mountain-200 Silver, 38|$90,479.61|(Null)|(Null)|$41,759.82|$48,719.79|  
|Mountain-200 Silver, 42|$97,439.58|(Null)|(Null)|$39,439.83|$57,999.75|  
|Mountain-200 Silver, 46|$102,079.56|(Null)|(Null)|$27,839.88|$74,239.68|  
|Mountain-200 Black, 38|$26,638.28|(Null)|$12,294.59|$14,343.69|(Null)|  
|Mountain-200 Black, 38|$96,389.58|(Null)|(Null)|$41,309.82|$55,079.76|  
|Mountain-200 Black, 42|$80,324.65|(Null)|(Null)|$43,604.81|$36,719.84|  
|Mountain-200 Black, 46|$107,864.53|(Null)|(Null)|$45,899.80|$61,964.73|  
|Road-150 Red, 62|$46,517.51|$14,313.08|$32,204.43|(Null)|(Null)|  
|Road-150 Red, 56|$46,517.51|$17,891.35|$28,626.16|(Null)|(Null)|  
|Road-350-W Yellow, 48|$54,431.68|(Null)|(Null)|$15,308.91|$39,122.77|  
  
 上述結果是在法國透過網際網路通路銷售的前 10 項暢銷產品。  
  
## <a name="subselect-statement"></a>子選擇陳述式  
 子選擇的 BNF 為：  
  
```  
[WITH [<calc-clause> ...]]  
SELECT [<axis-spec> [, <axis-spec> ...]]  
FROM [<identifier> | (< sub-select-statement >)]  
[WHERE <slicer>]  
[[CELL] PROPERTIES <cellprop> [, <cellprop> ...]]  
  
< sub-select-statement > :=  
   SELECT [<axis-spec> [, <axis-spec> ...]]  
   FROM [<identifier> | (< sub-select-statement >)]  
   [WHERE <slicer>]  
  
```  
  
 子選擇是另一種 Select 陳述式，其中軸規格和 slicer 規格篩選要評估外部 Select 的 Cube 空間。  
  
 在 axis 或 slicer 子句的其中一個指定成員時，該成員及其上階和下階就會包含在子選擇的 Subcube 空間中；在 axis 或 slicer 子句中，所有未提及的同層級成員 (以及其上階和下階) 都會篩選排除在子空間之外。 這樣一來，如上述，外部 Select 的空間已經限制為 axis 子句或 slicer 子句中的現有成員，以及其上階和下階。  
  
 因為 axis 或 slicer 子句中所有未提及維度的 All 成員屬於 Select 的空間，所以在這些維度上 All 成員的所有下階也會成為子選擇空間的一部分。  
  
 Subcube 空間中所有維度的 All 成員會重新評估，以反映新空間限制的影響。  
  
 下列範例示範上述說明；第一個 MDX 運算式協助顯示 Cube 中未篩選的值，第二個 MDX 示範 Subselect 子句中的篩選影響：  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM [Adventure Works]  
```  
  
 傳回下列值：  
  
||||  
|-|-|-|  
||Internet Sales Amount|Reseller Sales Amount|  
|All Customers|$29,358,677.22|$80,450,596.98|  
|United States|$9,389,789.51|$80,450,596.98|  
|Oregon|$1,170,991.54|$80,450,596.98|  
|Portland|$110,649.54|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 在上述範例中，Seattle 是 Washington 的子系，Portland 是 Oregon 的子系，Oregon 和 Washington 是 United States 的子系，而 United States 則是 [Customer Geography].[All Customers] 的子系。 這個範例中所有顯示的成員有其他同層級對父彙總值有貢獻；例如 Spokane、Tacoma 和 Everett 是 Seattle 的同層級城市，這些成員對 Washington Internet Sales Amount 都有貢獻。 Reseller Sales Amount 值獨立於 Customer Geography 屬性之外，因此 All 值會顯示在結果中。 下一個 MDX 運算式示範 Subselect 子句的篩選影響：  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,  {[Measures].[Internet Sales Amount], [Measures].[Reseller Sales Amount]} ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
```  
  
 傳回下列值：  
  
||||  
|-|-|-|  
||Internet Sales Amount|Reseller Sales Amount|  
|All Customers|$2,467,248.34|$80,450,596.98|  
|United States|$2,467,248.34|$80,450,596.98|  
|Washington|$2,467,248.34|$80,450,596.98|  
|Seattle|$75,164.86|$80,450,596.98|  
  
 上述結果顯示只有 Washington State 的上階和下階是評估外部 Select 陳述式之子空間的一部分；Oregon 和 Portland 已從 Subcube 移除，因為在提及 Washington 時子選擇中未提及 Oregon 和所有其他同層級州。  
  
 All 成員已調整反映 Washington 的篩選；不但在 [Customer Geography] 維度中，而且在與 [Customer Geography] 相交的所有其他維度中也已經調整。 未與 [Customer Geography] 相交的所有維度，在 Subcube 中則是保持不變。  
  
 下列兩個 MDX 陳述式示範在其他維度中的 All 成員如何調整，以符合子選擇的篩選影響。 第一個查詢顯示不變的結果，第二個則顯示篩選影響：  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM [Adventure Works]  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Accessory|Components|Mountain|Road|Touring|  
|All Customers|$29,358,677.22|$604,053.30|(Null)|$10,251,183.52|$14,624,108.58|$3,879,331.82|  
|United States|$9,389,789.51|$217,168.79|(Null)|$3,547,956.78|$4,322,438.41|$1,302,225.54|  
|Oregon|$1,170,991.54|$30,513.17|(Null)|$443,607.98|$565,372.10|$131,498.29|  
|Portland|$110,649.54|$2,834.17|(Null)|$47,099.91|$53,917.17|$6,798.29|  
|Washington|$2,467,248.34|$62,662.92|(Null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(Null)|$19,914.53|$44,820.06|$7,734.54|  
  
```  
SELECT { [Customer].[Customer Geography].[All Customers]  
       , [Customer].[Customer Geography].[Country].&[United States]  
       , [Customer].[Customer Geography].[State-Province].&[OR]&[US]  
       , [Customer].[Customer Geography].[City].&[Portland]&[OR]  
       , [Customer].[Customer Geography].[State-Province].&[WA]&[US]  
       , [Customer].[Customer Geography].[City].&[Seattle]&[WA]  
       } ON 1  
     ,   [Product].[Product Line].MEMBERS ON 0  
  FROM ( SELECT [Customer].[State-Province].&[WA]&[US] ON 0  
           FROM [Adventure Works]  
        )  
 WHERE [Measures].[Internet Sales Amount]  
```  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Products|Accessory|Components|Mountain|Road|Touring|  
|All Customers|$2,467,248.34|$62,662.92|(Null)|$945,219.38|$1,155,880.07|$303,485.97|  
|United States|$2,467,248.34|$62,662.92|(Null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Washington|$2,467,248.34|$62,662.92|(Null)|$945,219.38|$1,155,880.07|$303,485.97|  
|Seattle|$75,164.86|$2,695.74|(Null)|$19,914.53|$44,820.06|$7,734.54|  
  
 如預期，上述結果顯示 All Products 值已經調整為僅限來自 Washington State 的值。  
  
 除了可用記憶體的限制之外，子選擇可以巢狀處理，巢狀深度不受限制。 最內部的子選擇定義套用篩選的起始子空間，接著是下一個外部 Select。 值得注意的是巢狀不是累積作業，因此巢狀設定順序可能會產生不同的結果。 下列範例應該會顯示選擇巢狀順序時的差異。  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 傳回下列結果。  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Sales Territories|Australia|Canada|Central|Northwest|Southwest|  
|All Products|$7,591,495.49|$1,281,059.99|$1,547,298.12|$600,205.79|$1,924,763.50|$2,238,168.08|  
|Mountain-200 Silver, 38|$1,449,576.15|$248,702.93|$275,052.45|$141,103.65|$349,487.01|$435,230.12|  
|Mountain-200 Black, 38|$1,722,896.50|$218,024.05|$418,726.43|$123,929.46|$486,694.63|$475,521.93|  
|Mountain-200 Black, 42|$1,573,655.14|$239,137.96|$319,921.61|$130,102.75|$420,445.84|$464,046.98|  
|Mountain-200 Black, 46|$1,420,500.58|$192,320.16|$230,875.99|$117,044.49|$424,813.66|$455,446.27|  
|Road-150 Red, 56|$1,424,867.11|$382,874.89|$302,721.64|$88,025.44|$243,322.36|$407,922.78|  
  
```  
SELECT [Sales Territory].[Sales Territory Region].MEMBERS on 0  
     , [Product].[Product].MEMBERS on 1  
  FROM (SELECT TOPCOUNT( [Sales Territory].[Sales Territory Region].CHILDREN, 5, [Measures].[Sales Amount]) ON 0  
          FROM (SELECT TOPCOUNT( [Product].[Product].CHILDREN, 5, [Measures].[Sales Amount]) on 0  
                  FROM [Adventure Works]  
               )  
        )  
 WHERE [Measures].[Sales Amount]  
```  
  
 傳回下列結果。  
  
||||||||  
|-|-|-|-|-|-|-|  
||All Sales Territories|Australia|Canada|Northwest|Southwest|United Kingdom|  
|All Products|$7,938,218.56|$1,096,312.24|$1,474,255.49|$2,042,674.72|$2,238,099.55|$1,086,876.56|  
|Mountain-200 Silver, 38|$1,520,958.53|$248,702.93|$275,052.45|$349,487.01|$435,230.12|$212,486.03|  
|Mountain-200 Silver, 42|$1,392,237.14|$198,127.15|$229,679.01|$361,233.58|$407,854.24|$195,343.16|  
|Mountain-200 Black, 38|$1,861,703.23|$218,024.05|$418,726.43|$486,694.63|$475,521.93|$262,736.19|  
|Mountain-200 Black, 42|$1,702,427.25|$239,137.96|$319,921.61|$420,445.84|$464,046.98|$258,874.87|  
|Mountain-200 Black, 46|$1,460,892.41|$192,320.16|$230,875.99|$424,813.66|$455,446.27|$157,436.31|  
  
 如您所見，這兩組的結果有差異。 第一個查詢回答在前 5 個銷售區域中最暢銷產品為何的問題，第二個查詢回答前 5 項暢銷產品最大銷售量在哪裡的問題。  
  
### <a name="remarks"></a>備註  
 子選擇有下列限制：  
  
-   WHERE 子句不會篩選子空間。  
  
-   WHERE 子句只變更 Subcube 的預設成員。  
  
-   axis 子句中不允許 NON EMPTY 子句；請改用 [NonEmpty &#40;MDX&#41;](../../../mdx/nonempty-mdx.md) 函數運算式。  
  
-   axis 子句中不允許 HAVING 子句；請改用 [Filter &#40;MDX&#41;](../../../mdx/filter-mdx.md) 函數運算式。  
  
-   根據預設導出的成員中不允許子選擇。不過，這項限制可以變更，以每個工作階段為基礎，在所指派值給**子查詢**中的連接字串屬性<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>或**DBPROP_MSMD_SUBQUERIES** 屬性[支援的 XMLA 屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md). 如需根據 [SubQueries](../../../analysis-services/multidimensional-models/mdx/calculated-members-in-subselects-and-subcubes.md) 或 **DBPROP_MSMD_SUBQUERIES** 的值導出成員之行為的詳細說明，請參閱 **子選擇和 Subcube 中的導出成員**。  
  
  
