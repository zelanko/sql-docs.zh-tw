---
description: CurrentMember (MDX)
title: CurrentMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5778a8b1d56fa568fe97dba104c1b46da1a005cf
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196042"
---
# <a name="currentmember-mdx"></a>CurrentMember (MDX)


  反覆運算時，傳回指定階層的目前成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Hierarchy_Expression.CurrentMember  
```  
  
## <a name="arguments"></a>引數  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 反覆運算階層成員的集合時，在反覆運算的各個步驟中，進行運算的成員就是目前的成員。 **CurrentMember**函數會傳回該成員。  
  
> [!IMPORTANT]  
>  當維度只包含單一可見的階層，該階層可由維度名稱或階層名稱參考，因為維度名稱會解析成其唯一可見的階層。 例如，`Measures.CurrentMember` 即是有效的 MDX 運算式，因為它解析成量值維度上唯一的階層。  
  
## <a name="examples"></a>範例  
 下列查詢會顯示如何使用 **Currentmember** ，從資料行、資料列和配量軸上的階層中尋找目前的成員：  
  
 `WITH MEMBER MEASURES.CURRENTDATE AS`  
  
 `[Date].[Calendar].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTPRODUCT AS`  
  
 `[Product].[Product Categories].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTMEASURE AS`  
  
 `MEASURES.CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTCUSTOMER AS`  
  
 `[Customer].[Customer Geography].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `[Product].[Product Categories].[Category].MEMBERS`  
  
 `*`  
  
 `{MEASURES.CURRENTDATE, MEASURES.CURRENTPRODUCT,MEASURES.CURRENTMEASURE, MEASURES.CURRENTCUSTOMER}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Customer].[Customer Geography].[Country].&[Australia])`  
  
 目前的成員會在查詢內之軸上使用的階層上變更。 因此，在軸上未使用的相同維度上，其他階層上的目前成員也可以變更;這種行為稱為「自動存在」，而在 [MDX &#40;Analysis Services&#41;的重要概念 ](/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)中可以找到更多詳細資料。 例如，底下的查詢會顯示 Date 維度之 Calendar Year 階層上的目前成員會隨著 Calendar 階層上的目前成員而變更，後者會顯示在資料列軸上：  
  
 `WITH MEMBER MEASURES.CURRENTYEAR AS`  
  
 `[Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `{MEASURES.CURRENTYEAR}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 **CurrentMember** 對於讓計算知道正在使用的查詢內容而言非常重要。 下列範例會傳回每個產品的訂單數量，以及來自「寄件者 **工作** 」 cube 之依類別和型號的訂單數量百分比。 **CurrentMember**函式會識別要在計算期間使用其訂單數量的產品。  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty  
(   
      ([Product].[Product Categories].CurrentMember,  
        Measures.[Order Quantity]) /   
          (  
           Ancestor  
           ( [Product].[Product Categories].CurrentMember,   
             [Product].[Product Categories].[Category]  
           ), Measures.[Order Quantity]  
       ), 0  
   ), FORMAT_STRING='Percent'  
SELECT   
   {Measures.[Order Quantity],  
      [Measures].[Order Percent by Category]} ON COLUMNS,  
{[Product].[Product].Members} ON ROWS  
FROM [Adventure Works]  
WHERE {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
