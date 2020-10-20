---
description: DrilldownMember (MDX)
title: DrilldownMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0dfc26c52cbd478979cbbaad4a69e66bc58138a5
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194020"
---
# <a name="drilldownmember-mdx"></a>DrilldownMember (MDX)


  向下切入特定集合中出現在第二個特定集合裡的成員。  
  
 或者，此函數會使用第一個 Tuple 階層或選擇性指定的階層，向下鑽研一組 Tuple。  
  
## <a name="syntax"></a>語法  
  
```  
  
DrillDownMember(<Set_Expression1>, <Set_Expression2> [,[<Target_Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]])  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression1*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Set_Expression2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Target_Hierarchy*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
 *遞 歸*  
 表示遞迴比較集合的關鍵字。  
  
 *Include_Calc_Members*  
 讓導出成員包含在向下鑽研結果中的關鍵字。  
  
## <a name="remarks"></a>備註  
 此函數會傳回依階層排序的子成員集合，並加入第一個集合中有指定，同時也出現在第二個集合中的成員。 若第一個集合包含父成員及一或多個子系，父成員將不會向下鑽研。 第一個集合可以是任何維度，但第二個集合只能包含一維集合。 會保留第一個集合中原始成員的順序，但在函數之結果集中的所有子成員則在其父成員底下。 函數會擷取屬於第一個集合並且也存在第二個集合內之每個成員的子系，來建構結果集。 如果指定了 **遞迴** ，函式會繼續以遞迴方式比較結果集的成員與第二個集合，並針對結果集中的每一個成員，取得也出現在第二個集合中的子系，直到第二個集合中找不到來自結果集的成員為止。  
  
 查詢 XMLA 屬性 **MdpropMdxDrillFunctions** ，可讓您驗證服務器為切入函數提供的支援層級;如需詳細資訊，請參閱 [&#40;xmla&#41;支援的 Xmla 屬性 ](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 。  
  
 第一個集合可以包含 Tuple，而非成員。 Tuple 向下鑽研是 OLE DB 的擴充功能，會傳回 Tuple 集合而不是傳回成員。  
  
> [!IMPORTANT]  
>  如果成員後面緊跟著它的子系之一，就不會向下鑽研該成員。 集合中成員的順序對於深入的 * 和 Drillup 的函式系列有重要性 \* 。  
  
## <a name="examples"></a>範例  
 下列範例會向下鑽研至 Australia，這是屬於第一個集合並且同時存在第二個集合中的成員。  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   )  
   ON 0  
   FROM [Adventure Works]  
```  
  
 下列範例會向下鑽研至 Australia，這是屬於第一個集合並且同時存在第二個集合中的成員。 然而，因為存在 RECURSIVE 引數，所以函數會繼續和第二個集合遞迴比較結果集的成員 (State-Province 層級的成員)，擷取在結果集中並且同時存在第二個集合中之每個成員的子系 (City 層級的成員)，直到在第二個集合中找不到結果集中的成員為止。  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   ,RECURSIVE)  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
