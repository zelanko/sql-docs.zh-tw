---
description: Order (MDX)
title: Order (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4db745ea01a56d68fe259ebb2fffb5aae250abd4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471740"
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
 **Order**函數可以是使用**ASC**或**DESC**旗標所指定的階層式 () 或使用**BASC**或**BDESC**旗標指定的非階層式 (。**B**代表「中斷階層」 ) 。 如果指定 **ASC** 或 **DESC** ， **Order** 函數會先根據其在階層中的位置來排列成員，然後再排序每個層級。 如果指定了 **BASC** 或 **BDESC** ， **Order** 函數就會排列集合中的成員，而不考慮階層。 在未指定旗標的情況下， **ASC** 是預設值。  
  
 如果 **Order** 函數是與交叉聯結兩個或多個階層的集合搭配使用，並使用 **DESC** 旗標，則只會排序集合中最後一個階層的成員。 這不同於 Analysis Services 2000，其集合內的所有階層都會排序。  
  
## <a name="examples"></a>範例  
 下列範例會從「 **艾德作品** 」 cube 傳回「日期」維度上行事曆階層中所有行事曆季的轉售商訂單數。 **Order** 函數會重新排序 ROWS 軸的集合。 **Order**函數會依 `[Reseller Order Count]` 階層所決定的遞減階層順序來排序集合 `[Calendar]` 。  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 請注意，在此範例中，當 **DESC** 旗標變更為 **BDESC**時，階層會中斷，而且會傳回日曆季清單，而不考慮階層：  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 下列範例不考慮階層，而根據 Reseller Gross Profit 傳回前五名產品銷售子類別的 Reseller Sales 量值。 在使用**Order**函數排序結果之後，會使用**子集**函數來傳回集合中的前5個元組。  
  
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
  
 下列範例會根據「轉售商銷售量」量值，使用 **rank** 函數來為 City 階層的成員進行排名，然後以排名順序顯示這些成員。 藉由使用 **Order** 函數來先排序 City 階層的成員集合，排序只會完成一次，然後再以線性掃描的形式呈現排序的順序。  
  
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
  
 下列範例會使用 **order** 函數來排序非空白的元組，然後再利用 **Filter** 函數，傳回集合中唯一的產品數目。 **CurrentOrdinal**函數是用來比較和消除系結。  
  
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
  
 若要瞭解 **DESC** 旗標如何搭配一組元組使用，請先考慮下列查詢的結果：  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 在 Rows 軸上，您可以看到銷售領域群組已經依稅額的遞減次序排序，如下：北美、歐洲、太平洋、NA。 現在，如果我們將一組銷售領域群組與一組產品子類別結合，並以相同方式套用 **Order** 函式，就會發生什麼事，如下所示：  
  
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
  
 雖然產品子類別目錄的集合已經依遞減階層次序排序，但現在銷售領域群組並未排序，而是以它們在階層中的順序出現：歐洲、NA、北美和太平洋。 這是因為只有 Tuple 集合中的最後一個階層 (即產品子類別目錄) 才會排序。 若要重現 Analysis Services 2000 的行為，請使用一連串的嵌套 **產生** 函數來排序每個集合，然後再進行交叉聯結，例如：  
  
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
  
  
