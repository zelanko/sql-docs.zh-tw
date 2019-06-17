---
title: DrilldownMemberTop (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3dd1128bfafb052936e742f7ce56529b1222333a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690850"
---
# <a name="drilldownmembertop-mdx"></a>DrilldownMemberTop (MDX)


  向下切入特定集合中出現在第二個特定集合的成員，所得到的集合成員限制在特定的數目內。 或者，此函數會使用第一個 Tuple 階層或選擇性指定的階層，向下鑽研一組 Tuple。  
  
## <a name="syntax"></a>語法  
  
```  
  
DrillDownMemberTop(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expression>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression1*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Set_Expression2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *計數*  
 有效的數值運算式，會指定要傳回的 Tuple 數目。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
 *Hierarchy*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
 *遞迴*  
 表示遞迴比較集合的關鍵字。  
  
 *Include_Calc_Members*  
 讓導出成員包含在向下鑽研結果中的關鍵字。  
  
## <a name="remarks"></a>備註  
 如果指定數值運算式，則**DrilldownMemberTop**函式，會以遞減排序順序，根據值的數值運算式的第一個集合中每個成員的子系的子集合上評估成員。 如果沒有指定數值運算式，此函數會根據子成員集合所代表的資料格值 (由查詢內容所決定)，以遞減的順序來排序第一個集合中每個成員的子系。 此行為類似 TopCount 和 Head (MDX) 函數，這些函數會依自然順序傳回成員的集合，不進行任何排序。  
  
 完成排序之後， **DrilldownMemberTop**函式會傳回一組包含父成員中指定的子成員數目*計數*最高值及包含在兩個集合.  
  
 如果**遞迴**指定，則函式會如先前所述來排序第一個集合，然後遞迴比較第一個集合的成員，如同在階層中，針對第二個集合的組織方式 *。* 函式會擷取第一個集合並且也出現在第二個集合中每個成員的子系的最高數目。  
  
 第一個集合可以包含 Tuple，而非成員。 Tuple 向下鑽研是 OLE DB 的延伸模組，而且會傳回 Tuple 集合而不是傳回成員。  
  
 **DrilldownMemberTop**函數很相似[DrilldownMember](../mdx/drilldownmember-mdx.md)函式，但不包括每個成員的所有子系中第一個集合並且也出現在第二個集合，也就是**DrilldownMemberTop**函式會傳回每個成員的子成員的最高數目。  
  
 查詢 XMLA 屬性 MdpropMdxDrillFunctions，可讓您確認伺服器提供鑽研函數; 支援的層級請參閱[支援的 XMLA 屬性&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)如需詳細資訊。  
  
## <a name="example"></a>範例  
 下列範例會向下鑽研至 clothing 類別目錄，以傳回出貨訂單中，數量排名前三名的子類別目錄。  
  
```  
SELECT DrilldownMemberTop   ({[Product].[Product Categories].[All Products],        
[Product].[Product Categories].[Category].Bikes,        
[Product].[Product Categories].[Category].Clothing},     
{[Product].[Product Categories].[Category].Clothing},     
3,     
[Measures].[Reseller Order Quantity])     
ON 0     
FROM [Adventure Works]     
WHERE [Measures].[Reseller Order Quantity]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
