---
title: Order (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 43a75f4a42193c231c1acc710512b05537675991
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63277850"
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
 **順序**函式可以是階層式 (使用如同指定**ASC**或**DESC**旗標) 或非階層式 (依照使用**BASC**或是**BDESC**旗標; **B**代表 「 破壞階層 」)。 如果**ASC**或是**DESC**指定，則**順序**函式先排列成員根據其位置在階層中，然後排列每個層級。 如果**BASC**或是**BDESC**指定，則**順序**函式會排列集合，而不考慮階層中的成員。 指定在沒有旗標時， **ASC**是預設值。  
  
 如果**順序**函數搭配使用，一組兩個或多個階層所在交叉聯結，而**DESC**使用旗標時，只有在集合中的最後一個階層的成員會排序。 這不同於 Analysis Services 2000，其集合內的所有階層都會排序。  
  
## <a name="examples"></a>範例  
 下列範例會傳回，從**Adventure Works** cube，[日期] 維度之日曆階層所有日曆季的零售商訂單數目。**順序**函式會重新排列 ROWS 軸的集合。 **順序**函式排序的集合`[Reseller Order Count]`的遞減階層順序所決定的`[Calendar]`階層。  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 請注意在這個範例中，當**DESC**旗標會變成**BDESC**時會破壞階層，會傳回日曆季的清單，而不考慮階層：  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 下列範例不考慮階層，而根據 Reseller Gross Profit 傳回前五名產品銷售子類別的 Reseller Sales 量值。 **子集**函數用來傳回集合中只有前 5 個 tuple 之後使用排序結果,**順序**函式。  
  
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
  
 下列範例會使用**陣序規範**來排名縣 （市） 階層的成員函式根據 Reseller Sales Amount 量值，然後依此次序顯示。 藉由使用**順序**函數，先排序 City 階層的成員集合，排序是只進行一次，再接著線性掃描之前正在依排序順序呈現。  
  
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
  
 下列範例會傳回產品的數目是唯一的使用集中**順序**函式來排序非空的 tuple，再利用**篩選**函式。 **CurrentOrdinal**函數用來比較和刪除繫結。  
  
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
  
 若要了解如何**DESC**旗標與 tuple 集合的運作方式，請先考慮下列查詢的結果：  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 資料列軸上您所見，有的如下所示 Tax Amount，依遞減順序排序銷售領域群組：北美洲、 歐洲、 太平洋、 na。 發生什麼情況現在會看到我們交叉聯結將的銷售領域群組與產品子類別目錄的集合，並套用**順序**函式中相同的方式，如下所示：  
  
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
  
 雖然產品子類別目錄的集合已經依遞減階層順序，銷售領域群組現在並未排序，並會出現在階層所顯示的順序：歐洲、 NA、 北美和太平洋。 這是因為只有 Tuple 集合中的最後一個階層 (即產品子類別目錄) 才會排序。 若要重現 Analysis Services 2000 的行為，請使用一系列的巢狀**產生**函式來排序每個集合之前它交叉聯結，例如,：  
  
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
  
  
