---
title: "CurrentMember (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURRENTMEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- CurrentMember function
ms.assetid: 5da76496-7d13-4f17-9cee-3e1ef70c2d97
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 068d7219727c1187e5c0c06509cfdec3fe189fa2
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="currentmember-mdx"></a>CurrentMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  反覆運算時，傳回指定階層的目前成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Hierarchy_Expression.CurrentMember  
```  
  
## <a name="arguments"></a>引數  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 反覆運算階層成員的集合時，在反覆運算的各個步驟中，進行運算的成員就是目前的成員。 **CurrentMember**函式會傳回該成員。  
  
> [!IMPORTANT]  
>  當維度只包含單一可見的階層，該階層可由維度名稱或階層名稱參考，因為維度名稱會解析成其唯一可見的階層。 例如，`Measures.CurrentMember` 即是有效的 MDX 運算式，因為它解析成量值維度上唯一的階層。  
  
## <a name="examples"></a>範例  
 下列查詢示範如何**Currentmember**可用來從資料行、 資料列和配量軸上的階層尋找目前的成員：  
  
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
  
 目前的成員會在查詢內之軸上使用的階層上變更。 因此，相同維度上不會在軸的其他階層上的目前成員也可以變更;這個行為稱為 「 自動存在 ' 和更多詳細資料位於[MDX &#40; 中的重要概念Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md). 例如，底下的查詢會顯示 Date 維度之 Calendar Year 階層上的目前成員會隨著 Calendar 階層上的目前成員而變更，後者會顯示在資料列軸上：  
  
 `WITH MEMBER MEASURES.CURRENTYEAR AS`  
  
 `[Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `{MEASURES.CURRENTYEAR}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 **CurrentMember**對於讓計算得知目前使用中的查詢內容的非常重要。 下列範例會傳回每個產品的訂單數量和訂單數量百分比依類別和型號，從**Adventure Works** cube。 **CurrentMember**函式識別會用於計算訂單數量的產品。  
  
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
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

