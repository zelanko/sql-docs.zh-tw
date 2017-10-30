---
title: "DrilldownLevelTop (MDX) |Microsoft 文件"
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
- DRILLDOWNLEVELTOP
dev_langs:
- kbMDX
helpviewer_keywords:
- DrilldownLevelTop function
ms.assetid: b3b45dd6-2ade-4dd7-83dd-849231e2e517
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d094ec3e2897bef5dfed1d98eddf82e115d84df5
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="drilldownleveltop-mdx"></a>DrilldownLevelTop (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 如果指定數值運算式， **DrilldownLevelTop**函數會在子成員集合評估後以遞減的順序，根據值的數值運算式，指定集合中每個成員的子系來排序。 如果沒有指定數值運算式，此函數會根據子成員集合所代表的資料格值 (由查詢內容所決定)，以遞減的順序來排序指定集合中每個成員的子系。  
  
 完成排序之後， **DrilldownLevelTop**函式會傳回一組包含父成員中指定的子成員數目*計數，*具有最高值。  
  
 **DrilldownLevelTop**函數很相似[DrilldownLevel](../mdx/drilldownlevel-mdx.md)函式，但不包含指定的層級的每個成員的所有子系**DrilldownLevelTop**函式會傳回子成員的最高數目。  
  
 查詢 XMLA 屬性 MdpropMdxDrillFunctions，可讓您確認伺服器為鑽研函數; 提供的支援層級請參閱[支援 XMLA 屬性 &#40;XMLA &#41;](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)如需詳細資訊。  
  
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
  
 下一個範例說明如何使用**include_calc_members**旗標，用來包含向下鑽研層中的導出的成員。 [轉售商訂單計數] 量值包含在**DrilldownLevelTop**陳述式，以確保傳回值會依該量值排序。  
  
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
 [DrilldownLevel &#40;MDX &#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

