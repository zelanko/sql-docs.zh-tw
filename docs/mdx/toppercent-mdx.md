---
title: TopPercent （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a8c92a4b6a76cb9d15048d6f058038363970cb8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036590"
---
# <a name="toppercent-mdx"></a>TopPercent (MDX)


  依遞減的順序排序集合，並傳回數值最高的 Tuple 集合，此集合的累計總和須等於或大於指定的百分比。  
  
## <a name="syntax"></a>語法  
  
```  
  
TopPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *百分比*  
 有效的數值運算式，指定要傳回的 Tuple 百分比。  
  
> [!IMPORTANT]  
>  *百分比*必須是正數值;負值會產生錯誤。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **TopPercent**函數會針對指定的集合評估指定之數值運算式的總和，以遞減順序排序集合。 然後，此函數會傳回最高值的元素，它們的總和值累計百分比至少是指定的百分比。 這個函數會傳回累計總計至少是指定百分比之集合的最小子集。 傳回從最大到最小排列的元素。  
  
> [!WARNING]  
>  如果*Numeric_Expression*傳回任何負數值，則**TopPercent**只會傳回一（1）個數據列。  
>   
>  如需有關此行為的詳細呈現，請參閱第二個範例。  
  
> [!IMPORTANT]  
>  就像[BottomPercent](../mdx/bottompercent-mdx.md)函數一樣， **TopPercent**函數一律會中斷階層。  
  
## <a name="example"></a>範例  
 下列範例為 Bike 類別目錄傳回實現轉售商銷售前 10% 的最佳城市。 結果以遞減順序排序，開頭為具有最高銷售值的城市。  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopPercent  
   ({[Geography].[Geography].[City].Members}  
   , 10  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
```  
  
 上述運算式會產生下列結果：  
  
||Reseller Sales Amount|  
|-|---------------------------|  
|Toronto|$3508904.84|  
|London|$1521530.09|  
|Seattle|$1209418.16|  
|Paris|$1170425.18|  
  
 原始資料集可透過下列查詢取得，並傳回 588 個資料列：  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
Order  
   ({[Geography].[Geography].[City].Members}  
   , [Measures].[Reseller Sales Amount]  
   , BDESC  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
  
```  
  
## <a name="example"></a>範例  
 下列逐步解說將協助您瞭解負數值在*Numeric_Expression*中的效果。 首先讓我們建立可顯示行為的一些內容。  
  
 下列查詢傳回轉銷商 'Sales Amount'、'Total Product Cost' 和 'Gross Profit' 的資料表，依收益的遞減順序排序。 請注意，只有負值的收益，因此最小的損失會顯示在最上方。  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  ORDER( [Product].[Product Categories].[Bikes].[Touring Bikes].children, [Measures].[Reseller Gross Profit], BDESC )   ON rows  
FROM [Adventure Works]  
  
```  
  
 上述查詢傳回下列結果；為提高可讀性，中間部分的資料列已移除。  
  
||Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|  
|-|---------------------------|---------------------------------|---------------------------|  
|Touring-2000 Blue, 50|$157444.56|$163112.57|（$5668.01）|  
|旅行-2000 Blue、46|$321027.03|$333021.50|（$11994.47）|  
|Touring-3000 Blue, 62|$87773.61|$100133.52|（$12359.91）|  
|...|...|...|...|  
|旅行-1000 黃色、46|$1016312.83|$1234454.27|（$218141.44）|  
|Touring-1000 Yellow, 60|$1184363.30|$1443407.51|（$259044.21）|  
  
 現在，如果要求您依收益顯示前 100% 的自行車，您要撰寫如下的查詢：  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  TOPPERCENT( [Product].[Product Categories].[Bikes].[Touring Bikes].children, 100,[Measures].[Reseller Gross Profit] )   ON rows  
FROM [Adventure Works]  
  
```  
  
 請注意，查詢要求百分百 (100%)，這表示應傳回所有資料列。 不過，因為*Numeric_Expression*中有負值，所以只會傳回一個資料列。  
  
||Reseller Sales Amount|Reseller Total Product Cost|Reseller Gross Profit|  
|-|---------------------------|---------------------------------|---------------------------|  
|Touring-2000 Blue, 50|$157444.56|$163112.57|（$5668.01）|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
