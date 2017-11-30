---
title: "DrilldownLevelBottom (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DRILLDOWNLEVELBOTTOM
dev_langs: kbMDX
helpviewer_keywords: DrilldownLevelBottom function
ms.assetid: c00a6a02-e618-4713-805a-870e042f2d51
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e6d4637bf9cfcdc2040affc8952ebfd8a711951d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="drilldownlevelbottom-mdx"></a>DrilldownLevelBottom (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在特定層級中將集合的成員向下切入到下一個層級。  
  
## <a name="syntax"></a>語法  
  
```  
DrilldownLevelBottom(Set_Expression, Count [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *計數*  
 有效的數值運算式，會指定要傳回的 Tuple 數目。  
  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
 *Numeric_Expression*  
 選擇性。 有效的數值運算式，這通常是傳回數字之資料格座標的多維度運算式 (MDX) 運算式。  
  
 *Include_Calc_Members*  
 選擇性。 可將導出成員加入向下鑽研結果的關鍵字。  
  
## <a name="remarks"></a>備註  
 如果指定數值運算式， **DrilldownLevelBottom**函式來排序，以子成員集合評估後遞增的順序，根據指定的值，指定集合中每個成員的子系。 如果沒有指定數值運算式，此函數會根據子成員集合所代表的資料格值 (由查詢內容所決定)，以遞增的順序來排序第一個集合中每個成員的子系。此行為類似 BottomCount 和 Tail (MDX) 函數，這些函數會依自然順序傳回成員的集合，不進行任何排序。  
  
 完成排序之後， **DrilldownLevelBottom**函式會傳回一組包含父成員中指定的子成員數目*計數*，具有最低值。  
  
 **DrilldownLevelBottom**函數很相似[DrilldownLevel](../mdx/drilldownlevel-mdx.md)函式，但不包含指定的層級的每個成員的所有子系**DrilldownLevelBottom**函式會傳回最底部的子成員。  
  
 查詢 XMLA 屬性 MdpropMdxDrillFunctions，可讓您確認伺服器為鑽研函數; 提供的支援層級請參閱[支援 XMLA 屬性 &#40;XMLA &#41;](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)如需詳細資訊。  
  
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
  
 下一個範例說明如何使用**include_calc_members**旗標，用來包含向下鑽研層中的導出的成員。 [轉售商訂單計數] 量值加入至**DrilldownLevelBottom**陳述式，以確保結果會依該量值排序。 若要查看導出成員，就必須將 Count 至少增加到 9。  
  
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
  
## <a name="see-also"></a>請參閱  
 [DrilldownLevel &#40;MDX &#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
