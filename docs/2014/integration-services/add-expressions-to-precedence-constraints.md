---
title: 將運算式加入優先順序條件約束 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- precedence executables [Integration Services]
- precedence constraints [Integration Services], adding expressions
- adding expressions
- constrained executables [Integration Services]
- combining constraints
- expressions [Integration Services], constraints
ms.assetid: 5574d89a-a68e-4b84-80ea-da93305e5ca1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 93b9b60d3042e690d2e3e23b05131fabe384e945
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84926109"
---
# <a name="add-expressions-to-precedence-constraints"></a>將運算式加入優先順序條件約束
  優先順序條件約束可以使用運算式來定義兩個可執行檔之間的條件約束：優先順序可執行檔和受條件約束的可執行檔。 可執行檔可以是工作或容器。 運算式可以單獨使用，或與優先順序可執行檔的執行結果組合使用。 可執行檔的執行結果為成功或失敗。 設定優先順序條件約束的執行結果時，可以將執行結果設為 `Success`、`Failure` 或 `Completion`。 `Success` 表示優先順序可執行檔必須執行成功；`Failure` 表示優先順序可執行檔必須執行失敗；`Completion` 則指示不論優先順序工作成功與否，受條件約束的可執行檔都應該執行。 如需詳細資訊，請參閱 [優先順序條件約束](control-flow/precedence-constraints.md)。  
  
 運算式必須評估為 `True` 或 `False`，且必須是有效的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 運算式。 運算式可以使用常值、系統及自訂變數，以及 [!INCLUDE[ssIS](../includes/ssis-md.md)] 運算式文法提供的函數與運算子。 例如，運算式 `@Count == SQRT(144) + 10` 使用變數 `Count`、SQRT 函數及等於 (==) 和加 (+) 運算子。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](expressions/integration-services-ssis-expressions.md)為止。  
  
 在下圖中，工作 A 及工作 B 由使用執行結果及運算式的優先順序條件約束連結。 條件約束值設為 `Success` 且運算式為 `@X >== @Z`。 工作 B (受條件約束的工作) 只在工作 A 順利完成且變數 `X` 的值大於或等於變數 `Z` 的值時執行。  
  
 ![兩個工作之間的優先順序條件約束](media/mw-dts-03.gif "兩個工作之間的優先順序條件約束")  
  
 可執行檔也可以使用包含不同運算式的多個優先順序條件約束來連結。 例如在下圖中，工作 B 和 C 由使用執行結果及運算式的優先順序條件約束連結至工作 A。 兩個條件約束值都設為 `Success.`。一個優先順序條件約束包含運算式 `@X >== @Z`，另一個優先順序條件約束包含運算式 `@X < @Z`。 視變數 `X` 與 `Z` 的值而定，工作 C 或工作 B 會執行。  
  
 ![優先順序條件約束上的運算式](media/mw-dts-04.gif "優先順序條件約束上的運算式")  
  
 使用 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中的 [優先順序條件約束編輯器]**** 及 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供的 [屬性] 視窗，可以新增或修改運算式。 然而，[屬性] 視窗不提供運算式語法的驗證。  
  
 如果優先順序條件約束包含運算式，則會在 [控制流程]**** 索引標籤之設計介面上優先順序條件約束的旁邊出現圖示，且圖示上的工具提示會顯示運算式。  
  
## <a name="combining-execution-values-and-expressions"></a>組合執行值與運算式  
 下表描述將執行值條件約束與優先順序條件約束中的運算式進行組合的影響。  
  
|評估作業|條件約束評估為|運算式評估為|受條件約束的可執行檔執行|  
|--------------------------|-----------------------------|-----------------------------|---------------------------------|  
|條件約束|True|N/A|True|  
|條件約束|False|N/A|False|  
|運算是|N/A|True|True|  
|運算是|N/A|False|False|  
|條件約束與運算式|True|True|True|  
|條件約束與運算式|True|False|False|  
|條件約束與運算式|False|True|False|  
|條件約束與運算式|False|False|False|  
|條件約束或運算式|True|True|True|  
|條件約束或運算式|True|False|True|  
|條件約束或運算式|False|True|True|  
|條件約束或運算式|False|False|False|  
  
### <a name="to-add-an-expression-to-a-precedence-constraint"></a>將運算式加入優先順序條件約束  
  
-   [在優先順序條件約束中使用運算式](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
-   [設定優先順序條件約束的屬性](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
## <a name="external-resources"></a>外部資源  
 social.technet.microsoft.com 上的技術文件： [SSIS 運算式範例](https://go.microsoft.com/fwlink/?LinkId=220761)  
  
## <a name="see-also"></a>另請參閱  
 [多個優先順序條件約束](../../2014/integration-services/multiple-precedence-constraints.md)   
 [優先順序條件約束](control-flow/precedence-constraints.md)  
  
  
