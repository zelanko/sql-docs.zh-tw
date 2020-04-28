---
title: DrilldownMemberTop （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1ebb3054ab25729ef5d75034dbee1d720f4dd928
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68031245"
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
  
 *Count*  
 有效的數值運算式，會指定要傳回的 Tuple 數目。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
 *階層*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
 *式*  
 表示遞迴比較集合的關鍵字。  
  
 *Include_Calc_Members*  
 讓導出成員包含在向下鑽研結果中的關鍵字。  
  
## <a name="remarks"></a>備註  
 如果指定了數值運算式， **DrilldownMemberTop**函數會根據子成員集合評估的數值運算式的值，以遞減的順序來排序第一個集合中每個成員的子系。 如果沒有指定數值運算式，此函數會根據子成員集合所代表的資料格值 (由查詢內容所決定)，以遞減的順序來排序第一個集合中每個成員的子系。 此行為類似 TopCount 和 Head (MDX) 函數，這些函數會依自然順序傳回成員的集合，不進行任何排序。  
  
 排序之後， **DrilldownMemberTop**函數會傳回一個集合，其中包含父成員，以及在 [*計數*] 中指定之子成員的數目，其值最高，且包含在這兩個集合中。  
  
 如果指定了**RECURSIVE** ，此函式會排序第一個集合（如先前所述），然後以遞迴方式將第一個集合的成員（如階層中的組織）與第二個集合進行比對。 函式會針對第一個集合中同時出現在第二個集合中的每個成員，抓取最上層的子係數目。  
  
 第一個集合可以包含 Tuple，而非成員。 Tuple 向下鑽研是 OLE DB 的延伸模組，而且會傳回 Tuple 集合而不是傳回成員。  
  
 **DrilldownMemberTop**函數與[DrilldownMember](../mdx/drilldownmember-mdx.md)函數類似，但不是包含第一個集合中同時也出現在第二個集合中之每個成員的所有子系，而**DrilldownMemberTop**函數會傳回每個成員的最高子成員數目。  
  
 查詢 XMLA 屬性 MdpropMdxDrillFunctions 可讓您驗證服務器為鑽孔函數提供的支援層級;如需詳細資訊，請參閱[支援的 Xmla 屬性 &#40;xmla&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 。  
  
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
  
  
