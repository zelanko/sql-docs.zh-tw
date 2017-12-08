---
title: "使用成員、 Tuple 和集合 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MDX [Analysis Services], tuples
- member keys [MDX]
- MDX [Analysis Services], sets
- calculated members [MDX]
- members [MDX]
- Multidimensional Expressions [Analysis Services], members
- named sets [MDX]
- Multidimensional Expressions [Analysis Services], tuples
- member functions [MDX]
- sets [MDX]
- MDX [Analysis Services], members
- member names [MDX]
- Multidimensional Expressions [Analysis Services], sets
- tuple functions
- tuples
- set functions [MDX]
ms.assetid: b6ec2439-caef-46d3-9fd7-5f4526cee334
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 56f991716d78e8b4638ab57e7dc981c5942d81b0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="working-with-members-tuples-and-sets-mdx"></a>使用成員、Tuple 和集合 (MDX)
  MDX 提供許多會傳回一或多個成員、Tuple 或集合的函數，或作用於成員、Tuple 或集合的函數。  
  
## <a name="member-functions"></a>成員函數  
 MDX 提供數個函數，用來從其他 MDX 實體 (例如維度、層級、集合或 Tuple) 擷取成員。 例如， [FirstChild](../../../mdx/firstchild-mdx.md) 函數會在成員上作用並且會傳回成員。  
  
 若要取得 Time 維度的第一個子成員，您可以明確陳述該成員，如下列範例所示。  
  
```  
SELECT [Date].[Calendar Year].[CY 2001] on 0  
FROM [Adventure Works]  
  
```  
  
 您也可以使用 **FirstChild** 函數來傳回相同的成員，如下列範例所示。  
  
```  
SELECT [Date].[Calendar Year].FirstChild on 0  
FROM [Adventure Works]  
  
```  
  
 如需 MDX 成員函數的詳細資訊，請參閱 [MDX 函數參考 &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)。  
  
## <a name="tuple-functions"></a>Tuple 函數  
 MDX 提供數個會傳回 Tuple 的函數，在接受 Tuple 的任何地方都可以使用這些函數。 例如，[Item &#40;Tuple&#41; &#40;MDX&#41;](../../../mdx/item-tuple-mdx.md) 函數可以用來擷取集合中的第一個 Tuple，當您知道集合由單一 Tuple 組成，並且您要提供該 Tuple 給需要 Tuple 的函數時，此函數會非常有用。  
  
 下列範例會從資料行軸上的 Tuple 集合傳回第一個 Tuple。  
  
```  
SELECT {  
   ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2003]  
   )  
, ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2004]  
   )  
}.Item(0)  
ON COLUMNS   
FROM [Adventure Works]  
```  
  
 如需 Tuple 函數的詳細資訊，請參閱 [MDX 函數參考 &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)。  
  
## <a name="set-functions"></a>集合函數  
 MDX 提供數個會傳回集合的函數。 明顯的輸入 Tuple 並將它們以大括號括起來並不是擷取集合的唯一方式。 如需傳回集合之成員函數的詳細資訊，請參閱 [MDX 的關鍵概念 &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)。 還有許多其他集合函數。  
  
 您可以使用冒號運算子以成員的自然順序來建立集合。 例如，下列範例中顯示的集合包含 2002 日曆年度第一季到第四季的 Tuple：  
  
```  
SELECT   
   {[Calendar Quarter].[Q1 CY 2002]:[Calendar Quarter].[Q4 CY 2002]}   
ON 0  
FROM [Adventure Works]  
```  
  
 如果不要使用冒號運算子來建立集合，您也可以指定 Tuple 來建立相同的成員集合，如下列範例所示。  
  
```  
SELECT {  
   [Calendar Quarter].[Q1 CY 2002],   
   [Calendar Quarter].[Q2 CY 2002],   
   [Calendar Quarter].[Q3 CY 2002],   
   [Calendar Quarter].[Q4 CY 2002]  
   } ON 0  
FROM [Adventure Works]  
  
```  
  
 冒號運算式是一個包含函數。 冒號運算子兩旁的成員都會包含在結果集中。  
  
 如需集合函數的詳細資訊，請參閱 [MDX 函數參考 &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)。  
  
## <a name="array-functions"></a>陣列函數  
 陣列函數會作用於集合並且會傳回陣列。 如需陣列函數的詳細資訊，請參閱 [MDX 函數參考 &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)。  
  
## <a name="hierarchy-functions"></a>階層函數  
 階層函數會作用於成員、層級、階層或字串，然後傳回階層。 如需階層函數的詳細資訊，請參閱 [MDX 函數參考 &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)。  
  
## <a name="level-functions"></a>層級函數  
 層級函數會作用在成員、層級或字串，然後傳回層級。 如需層級函數的詳細資訊，請參閱 [MDX 函數參考 &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)。  
  
## <a name="logical-functions"></a>邏輯函數  
 邏輯函數會作用在 MDX 運算式，以傳回運算式中 Tuple、成員或集合的相關資訊。 例如，[IsEmpty &#40;MDX&#41;](../../../mdx/isempty-mdx.md) 函數會評估運算式傳回的是否為空資料格值。 如需邏輯函數的詳細資訊，請參閱 [MDX 函數參考 &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)。  
  
## <a name="numeric-functions"></a>數值函數  
 數值函數會作用在 MDX 運算式以傳回純量值。 例如，[Aggregate &#40;MDX&#41;](../../../mdx/aggregate-mdx.md) 函數會彙總指定集合中 Tuple 的量值後，傳回導出的純量值。 如需數值函數的詳細資訊，請參閱 [MDX 函數參考 &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)。  
  
## <a name="string-functions"></a>字串函數  
 字串函數會作用在 MDX 運算式以傳回字串。 例如，[UniqueName &#40;MDX&#41;](../../../mdx/uniquename-mdx.md) 函數會傳回包含維度、階層、層級或成員唯一名稱的字串值。 如需字串函數的詳細資訊，請參閱 [MDX 函數參考 &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [MDX 的關鍵概念 &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [MDX 查詢基礎觀念 &#40;Analysis Services &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [MDX 函數參考 &#40;MDX &#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
