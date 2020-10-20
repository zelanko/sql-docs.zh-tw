---
description: DrilldownLevelTop (MDX)
title: DrilldownLevelTop (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: af0ecdd3e53df131793f4703e154f96c51efc4e1
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194000"
---
# <a name="drilldownleveltop-mdx"></a>DrilldownLevelTop (MDX)


  在特定層級中將集合的成員向下切入到下一個層級。  
  
## <a name="syntax"></a>語法  
  
```  
  
DrilldownLevelTop(<Set_Expression>, <Count> [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Count*  
 有效的數值運算式，會指定要傳回的 Tuple 數目。  
  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
 *Include_Calc_Members*  
 可將導出成員加入向下鑽研結果的關鍵字。  
  
## <a name="remarks"></a>備註  
 如果指定了數值運算式， **DrilldownLevelTop** 函數會根據子成員集合的值，以遞減的順序排序指定集合中每個成員的子系。 如果沒有指定數值運算式，此函數會根據子成員集合所代表的資料格值 (由查詢內容所決定)，以遞減的順序來排序指定集合中每個成員的子系。  
  
 排序之後， **DrilldownLevelTop** 函式會傳回一個集合，其中包含父成員，以及在 [ *計數* ] 中指定之子成員的數目（具有最高值）。  
  
 **DrilldownLevelTop**函式類似于[DrilldownLevel](../mdx/drilldownlevel-mdx.md)函式，但不包含在指定層級上每個成員的所有子系，而是**DrilldownLevelTop**函式會傳回子成員的最高數目。  
  
 查詢 XMLA 屬性 MdpropMdxDrillFunctions，可讓您驗證服務器為切入函數提供的支援層級;如需詳細資訊，請參閱 [&#40;xmla&#41;支援的 Xmla 屬性 ](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 。  
  
## <a name="examples"></a>範例  
 下列範例會根據預設量值來傳回 Product Category 層級的前三個子系。 在 Adventure Works 範例 Cube 中，Accessories 的前三個子系為 Bike Racks、Bike Stands 及 Bottles and Cages。 您可以在 Management Studio 的 MDX 查詢視窗中，導覽至 Products | Product Categories | Members | All Products | Accessories 以檢視完整清單。 您可以增加 Count 引數以傳回更多成員。  
  
```  
SELECT DrilldownLevelTop   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 下一個範例說明如何使用 **include_calc_members** 旗標，用來在向下切入層級中包含匯出成員。 [轉售商訂單計數] 量值會包含在 **DrilldownLevelTop** 語句中，以確保傳回值會依該量值排序。  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELTOP(  
  [Product].[Product Categories].children ,  
  2,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
