---
description: DrilldownLevelBottom (MDX)
title: DrilldownLevelBottom (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6f761c0af97cf6a9d2a5dda4e26ac2e4503a8b4b
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193990"
---
# <a name="drilldownlevelbottom-mdx"></a>DrilldownLevelBottom (MDX)


  在特定層級中將集合的成員向下切入到下一個層級。  
  
## <a name="syntax"></a>語法  
  
```  
DrilldownLevelBottom(Set_Expression, Count [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Count*  
 有效的數值運算式，會指定要傳回的 Tuple 數目。  
  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 選擇性。 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
 *Include_Calc_Members*  
 選擇性。 可將導出成員加入向下鑽研結果的關鍵字。  
  
## <a name="remarks"></a>備註  
 如果指定了數值運算式， **DrilldownLevelBottom** 函數會根據子成員集合評估的指定值，以遞增的順序來排序指定集合中每個成員的子系。 如果沒有指定數值運算式，此函數會根據子成員集合所代表的資料格值 (由查詢內容所決定)，以遞增的順序來排序第一個集合中每個成員的子系。此行為類似 BottomCount 和 Tail (MDX) 函數，這些函數會依自然順序傳回成員的集合，不進行任何排序。  
  
 排序之後， **DrilldownLevelBottom** 函式會傳回一個集合，其中包含父成員以及依 *計數*指定的子成員數目（以最小值表示）。  
  
 **DrilldownLevelBottom**函式類似于[DrilldownLevel](../mdx/drilldownlevel-mdx.md)函式，但不包含在指定層級上每個成員的所有子系，而是由**DrilldownLevelBottom**函數傳回最底層的子成員數目。  
  
 查詢 XMLA 屬性 MdpropMdxDrillFunctions，可讓您驗證服務器為切入函數提供的支援層級;如需詳細資訊，請參閱 [&#40;xmla&#41;支援的 Xmla 屬性 ](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 。  
  
## <a name="examples"></a>範例  
 下列範例會根據預設量值來傳回 Product Category 層級的後三個子系。 在 Adventure Works 範例 Cube 中，Accessories 的後三個子系為 Tires and Tubes、Pumps 及 Panniers。 您可以在 Management Studio 的 MDX 查詢視窗中，導覽至 Products | Product Categories | Members | All Products | Accessories 以檢視完整清單。 您可以增加 Count 引數以傳回更多成員。  
  
```  
SELECT DrilldownLevelBottom   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 下一個範例說明如何使用 **include_calc_members** 旗標，用來在向下切入層級中包含匯出成員。 [轉售商訂單計數] 量值會加入至 **DrilldownLevelBottom** 語句，以確保結果會依該量值排序。 若要查看導出成員，就必須將 Count 至少增加到 9。  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELBOTTOM(  
  [Product].[Product Categories].children ,  
  9,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
