---
title: "DrilldownMemberTop (MDX) |Microsoft 文件"
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
- DRILLDOWNMEMBERTOP
dev_langs:
- kbMDX
helpviewer_keywords:
- DrilldownMemberTop function
ms.assetid: b6575544-1fd3-4fa1-aa2e-272d307c7750
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: da7f8a1c315d9ff3eb60c69e88726b521a59d17d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="drilldownmembertop-mdx"></a>DrilldownMemberTop (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
 *階層架構*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
 *遞迴*  
 表示遞迴比較集合的關鍵字。  
  
 *Include_Calc_Members*  
 讓導出成員包含在向下鑽研結果中的關鍵字。  
  
## <a name="remarks"></a>備註  
 如果指定數值運算式， **DrilldownMemberTop**函數會在子成員集合評估後以遞減的順序，根據值的數值運算式的第一個集合中每個成員的子系來排序。 如果沒有指定數值運算式，此函數會根據子成員集合所代表的資料格值 (由查詢內容所決定)，以遞減的順序來排序第一個集合中每個成員的子系。 此行為類似 TopCount 和 Head (MDX) 函數，這些函數會依自然順序傳回成員的集合，不進行任何排序。  
  
 完成排序之後， **DrilldownMemberTop**函式會傳回一組包含父成員中指定的子成員數目*計數，*具有最高值和都包含在兩個集合。  
  
 如果**遞迴**指定，如先前所述，函式會排序第一個集合，則遞迴比較第一個集合的成員，如同在階層中，針對第二個集合的組織方式*。* 此函數會擷取第一個集合並且也出現在第二個集合中每個成員的子系的最高數目。  
  
 第一個集合可以包含 Tuple，而非成員。 Tuple 向下鑽研是 OLE DB 的延伸模組，而且會傳回 Tuple 集合而不是傳回成員。  
  
 **DrilldownMemberTop**函數很相似[DrilldownMember](../mdx/drilldownmember-mdx.md)運作，但不包含每個成員的所有子系中第一個集合並且也存在第二個集中**DrilldownMemberTop**函式會傳回每個成員的子成員的最高數目。  
  
 查詢 XMLA 屬性 MdpropMdxDrillFunctions，可讓您確認伺服器為鑽研函數; 提供的支援層級請參閱[支援 XMLA 屬性 &#40;XMLA &#41;](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)如需詳細資訊。  
  
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
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

