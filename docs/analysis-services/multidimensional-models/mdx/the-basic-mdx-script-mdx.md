---
title: 基本 MDX 指令碼 (MDX) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2bebee1057180259c9813d7a650594c0c6d4736d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="the-basic-mdx-script-mdx"></a>基本 MDX 指令碼 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  多維度運算式 (MDX) 指令碼可在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中定義 Cube 的計算處理序。 MDX 指令碼有以下兩種類型：  
  
 **預設的 MDX 指令碼**  
 當您建立 Cube 時， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會為那個 Cube 建立預設的 MDX 指令碼。 此指令碼會定義整個 Cube 的計算行程。  
  
 **使用者自訂 MDX 指令碼**  
 建立 Cube 之後，您可以增加擴充 Cube 之計算能力的使用者自訂 MDX 指令碼。  
  
## <a name="the-default-mdx-script"></a>預設的 MDX 指令碼  
 當您定義的 Cube 包含一個 CALCULATE 陳述式時， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 就會建立預設的 MDX 指令碼。 這一個 CALCULATE 陳述式位於預設 MDX 指令碼的開始處，而且可指出在第一個計算行程期間應要計算的整個 Cube。  
  
 預設的 MDX 指令碼也包含指令碼命令，此命令可以建立命名集、指派，以及「Cube 設計師」中建立的導出成員：  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會將指令碼命令直接增加到預設的 MDX 指令碼。  
  
-   對於 Cube 中的每個命名集，預設的 MDX 指令碼中會有對應的 CREATE SET 陳述式存在。  
  
-   對於 Cube 中定義的每個導出成員，預設的 MDX 指令碼中會有對應的 CREATE MEMBER 陳述式存在。  
  
 您可以使用 Cube 設計師的 [計算] 索引標籤，在預設的 MDX 指令碼中、控制指令碼命令、命名集與導出成員的順序。 如需定義預設 MDX 指令碼中儲存之計算的詳細資訊，請參閱[多維度模型中的計算](../../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)。  
  
 如果沒有與 Cube 相關的  MDX 指令碼，Cube 會假設與其相關的是預設的 MDX 指令碼。 因為 Cube 仰賴 MDX 指令碼來決定計算行為，所以 Cube 必須至少與一個 MDX 指令碼相關。 換句話說，沒有與 Cube 相關的 MDX 指令碼，或是與空白 MDX 指令碼相關的 Cube ，無法計算任何資料格。 如果使用 Analysis Services 指令碼語言 (ASSL) 命令，或使用分析管理物件 (AMO)， 透過設計程式的方式建立 Cube，建議您建立會包含該 Cube 的單一 CALCULATE 陳述式的預設 MDX 指令碼。  
  
## <a name="mdx-script-content"></a>MDX 指令碼內容  
 MDX 指令碼可包含以下陳述式及運算式：  
  
 所有 MDX 指令碼陳述式  
 在 MDX 指令碼中，MDX 指令碼陳述式可控制計算的內容及範圍，還能管理 MDX 指令碼中其他陳述式的行為。 此類別目錄包括以下陳述式：  
  
-   [計算](../../../mdx/mdx-scripting-calculate.md)  
  
-   [凍結](../../../mdx/mdx-scripting-freeze.md)  
  
-   [範圍](../../../mdx/mdx-scripting-scope.md)  
  
 如需 MDX 指令碼陳述式的詳細資訊，請參閱 [MDX 指令碼陳述式 &#40;MDX&#41;](../../../mdx/mdx-scripting-statements-mdx.md)。  
  
 [建立成員](../../../mdx/mdx-data-definition-create-member.md)  
 CREATE MEMBER 陳述式可建立導出成員。 如需如何建立導出成員的詳細資訊，請參閱[在 MDX 中建立導出成員 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md)。  
  
 [建立集合](../../../mdx/mdx-data-definition-create-set.md)  
 CREATE SET 陳述式可建立命名集。 如需如何建立命名集的詳細資訊，請參閱[在 MDX 中建立命名集 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md)。  
  
 條件陳述式  
 條件陳述式可將條件式邏輯加入 MDX 指令碼。 此類別目錄包括 [CASE](../../../mdx/case-statement-mdx.md) 及 [IF](../../../mdx/mdx-scripting-if.md) 陳述式。  
  
 指派運算式  
 指派陳述式可將運算式 (例如一個值) 指派給受條件約束的 Subcube。 受條件約束的 Subcube 運算式是受條件約束之集合運算式的集合，定義了 MDX 指令碼內 Subcube 的「邊緣」。 以下程式顯示受條件約束的 Subcube 運算式語法：  
  
```  
<Constrained subcube> ::= (   
    ( <Constrained set> [<Crossjoin operator> <Constrained set>...] |  
    <ROOT function> |  
    <TREE function> |  
    LEAVES() |  
    * ) [, <Constrained subcube>...]  
<Constrained set> ::=   
    <Natural hierarchy>.MEMBERS |   
    <Natural hierarchy>.LEVEL(<numeric expression>).MEMBERS |   
    { <Natural hierarchy member> } |   
    DESCENDANTS( <Natural hierarchy member>, <Level expression>, ( SELF | AFTER | SELF_AND_AFTER ) ) |   
    DESCENDANTS( <Natural hierarchy member>, , LEAVES )  
<Natural hierarchy> ::= <Hierarchy identifier>  
<Natural hierarchy member> ::= <Natural hierarchy>.<identifier>[.<identifier>...]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 語言參考 & #40;MDX & #41;](../../../mdx/mdx-language-reference-mdx.md)   
 [MDX 指令碼基礎觀念 & #40;Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  
