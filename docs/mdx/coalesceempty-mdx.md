---
title: CoalesceEmpty (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 78e4f59ab1e994e34a7f0b1a0c519f34e20a2bd4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306700"
---
# <a name="coalesceempty-mdx"></a>CoalesceEmpty (MDX)


  將空資料格的值轉換成指定的非空資料格的值，該值可以是數字或字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
Numeric syntax  
CoalesceEmpty( Numeric_Expression1 [ ,Numeric_Expression2,...n] )  
  
String syntax  
CoalesceEmpty(String_Expression1 [ ,String_Expression2,...n] )  
```  
  
## <a name="arguments"></a>引數  
 *Numeric_Expression1*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression2*  
 一般是指定之數值的有效數值運算式。  
  
 *String_Expression1*  
 有效的字串運算式，這通常是傳回字串之資料格座標的多維度運算式 (MDX) 運算式。  
  
 *String_Expression2*  
 有效的字串運算式，一般是用來替代第一個字串運算式所傳回之 NULL 的指定字串值。  
  
## <a name="remarks"></a>備註  
 如果指定了一個或多個數值運算式， **CoalesceEmpty**函式會傳回第一個數值運算式 （從左到右） 是可解析成非空白值的數值。 如果指定的數值運算式都無法解析成非空白值，那麼此函數會傳回空白資料格的值。 一般說來，第二個數值運算式的值是用來替代第一個數值運算式所傳回之 NULL 的數值。  
  
 如果指定了一個或多個字串運算式，此函數會傳回能解析為非空白值之第一個字串運算式的字串值 (從左到右)。 如果指定的字串運算式都無法解析成非空白值，那麼此函數會傳回空白資料格的值。 一般說來，第二個字串運算式的值是用來替代第一個字串運算式所傳回之 NULL 的字串值。  
  
 **CoalesceEmpty**函式只能接受相同類型的值。 換句話說，所有指定的值運算式只能評估為數值資料類型或空白資料格的值，否則所有指定的值運算式必須評估為字串資料類型或空白資料格的值。 單次呼叫此函數無法包含數值與字串運算式。  
  
 如需有關空的資料格的詳細資訊，請參閱 OLE DB 文件集。  
  
## <a name="example"></a>範例  
 下列範例會查詢**Adventure Works** cube。 此範例會傳回每個產品的訂單數量，以及按類別計算的訂單數量百分比。 **CoalesceEmpty**函式可確保格式化的導出的成員時，將 null 值會表示為零 (0)。  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty(   
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
  
  
