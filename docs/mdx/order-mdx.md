---
title: Order （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d540b299fd08aa78576b19040a4cfafb9046ae7c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68055677"
---
# <a name="order-mdx"></a>Order (MDX)


  安排指定集合的成員，可以選擇保留或者打破階層架構。  
  
## <a name="syntax"></a>語法  
  
```  
  
Numeric expression syntax  
Order(Set_Expression, Numeric_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
String expression syntax  
Order(Set_Expression, String_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
 *String_Expression*  
 有效的字串運算式，這通常是傳回數字 (以字串表示) 之資料格座標的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **Order**函式可以是階層式（如使用**ASC**或**DESC**旗標所指定）或非階層式（如使用**BASC**或**BDESC**旗標所指定; **B**代表「中斷階層」）。 如果指定了**ASC**或**DESC** ， **Order**函式會先根據成員在階層中的位置排列，然後排序每個層級。 如果指定**BASC**或**BDESC** ， **Order**函式會排列集合中的成員，而不考慮階層。 在未指定任何旗標的情況下， **ASC**是預設值。  
  
 如果**Order**函式用於交叉聯結兩個或多個階層的集合，且使用**DESC**旗標，則只會排序集合中最後一個階層的成員。 這不同於 Analysis Services 2000，其集合內的所有階層都會排序。  
  
## <a name="examples"></a>範例  
 下列範例會從「**艾德工作**」 cube 傳回「日期」維度上行事曆階層中所有行事曆季的轉售商訂單數目。**Order**函數會重新排序資料列軸的集合。 **Order**函式會按照階層所`[Reseller Order Count]`決定`[Calendar]`的遞減階層順序來排序集合。  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 請注意，在此範例中，當**DESC**旗標變更為**BDESC**時，階層會中斷，而日曆季的清單則會傳回，而不考慮階層：  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 下列範例不考慮階層，而根據 Reseller Gross Profit 傳回前五名產品銷售子類別的 Reseller Sales 量值。 只有在使用**Order**函數排序結果之後，才會使用**子集**函數來傳回集合中的前5個元組。  
  
 `SELECT Subset`  
  
 `(Order`  
  
 `([Product].[Product Categories].[SubCategory].members`  
  
 `,[Measures].[Reseller Gross Profit]`  
  
 `,BDESC`  
  
 `)`  
  
 `,0`  
  
 `,5`  
  
 `) ON 0`  
  
 `FROM [Adventure Works]`  
  
 下列範例會根據「轉售商銷售量」量值，使用**rank**函數來排名 City 階層的成員，然後以順位的順序顯示。 藉由使用**Order**函數先排序 City 階層的成員集合，排序只會執行一次，然後再以排序的順序呈現線性掃描。  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
 下列範例會傳回唯一的集合中的產品數目，使用**order**函數來排序非空白的元組，然後再利用**篩選**函數。 **CurrentOrdinal**函數是用來比較和消除系結。  
  
```  
WITH MEMBER [Measures].[PrdTies] AS Count  
   (Filter  
      (Order  
        (NonEmpty  
          ([Product].[Product].[Product].Members  
          , {[Measures].[Reseller Order Quantity]}  
          )  
       , [Measures].[Reseller Order Quantity]  
       , BDESC  
       ) AS OrdPrds  
    , (OrdPrds.CurrentOrdinal < OrdPrds.Count   
       AND [Measures].[Reseller Order Quantity] =   
          ( [Measures].[Reseller Order Quantity]  
            , OrdPrds.Item  
               (OrdPrds.CurrentOrdinal  
               )  
            )  
         )  
         OR (OrdPrds.CurrentOrdinal > 1   
            AND [Measures].[Reseller Order Quantity] =   
               ([Measures].[Reseller Order Quantity]  
               , OrdPrds.Item  
                  (OrdPrds.CurrentOrdinal-2)  
                )  
             )  
          )  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
 若要瞭解**DESC**旗標如何與元組集合搭配使用，請先考慮下列查詢的結果：  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 在 Rows 軸上，您可以看到銷售領域群組已經依稅額的遞減次序排序，如下：北美、歐洲、太平洋、NA。 現在，如果我們將銷售領域群組的集合與一組產品子類別結合，並以相同方式套用**Order**函式，就會發生什麼情況，如下所示：  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 雖然產品子類別目錄的集合已經依遞減階層次序排序，但現在銷售領域群組並未排序，而是以它們在階層中的順序出現：歐洲、NA、北美和太平洋。 這是因為只有 Tuple 集合中的最後一個階層 (即產品子類別目錄) 才會排序。 若要重現 Analysis Services 2000 的行為，請在交叉聯結之前使用一系列的 nested**產生**函數來排序每個集合，例如：  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
GENERATE(  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
,  
ORDER(  
[Sales Territory].[Sales Territory].CURRENTMEMBER  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC))  
ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
