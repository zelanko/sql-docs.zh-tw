---
title: 將反復專案加入至控制流程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- repeating workflows
- adding iterations
- control flow [Integration Services], iterations
- expressions [Integration Services], control flow
- iterations [Integration Services]
- For Loop containers
ms.assetid: eb3a7494-88ae-4165-9d0f-58715eb1734a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b96f5f900e8c1a3adf136c7bdaf1b89f297e4921
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061975"
---
# <a name="add-iteration-to-a-control-flow"></a>將反覆運算加入控制流程
  
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包括 For 迴圈容器，該容器為控制流程項目，可簡化在套件中包括有條件地重複控制流程的迴圈。 如需詳細資訊，請參閱 [For 迴圈容器](control-flow/for-loop-container.md)為止。  
  
 「For 迴圈」容器會評估迴圈中每個反覆運算的條件，並在條件評估為 False 時停止。 「For 迴圈」容器包括許多運算式，可用於初始化迴圈，指定停止執行重複控制流程的評估條件，以及為更新評估條件之比較值的運算式指派值。 您必須提供評估條件，但初始化及指派運算式是選擇性的。  
  
 「For 迴圈」容器不提供功能，它僅提供可在其中建立可重複控制流程的結構。 若要提供容器功能，「For 迴圈」容器中必須至少包括一個工作。 如需詳細資訊，請參閱 [Integration Services Tasks](control-flow/integration-services-tasks.md)。  
  
 「For 迴圈」容器可以包括具有多個工作的控制流程，還可以包括其他容器。 將工作及容器加入「For 迴圈」容器與將它們加入封裝類似，不同之處在於，您要將工作及容器拖曳至「For 迴圈」容器而不是封裝。 如果「For 迴圈」容器包含一個以上的工作或容器，則您可以如同在封裝中所做的一樣，使用優先順序條件約束來連接它們。 如需詳細資訊，請參閱 [優先順序條件約束](control-flow/precedence-constraints.md)。  
  
## <a name="using-expressions-in-for-loop-configuration"></a>在 For 迴圈組態中使用運算式  
 藉由指定評估條件、初始化值或指派值來設定「For 迴圈」容器時，您可以使用常值或運算式。  
  
 運算式可以包含變數。 使用變數的優點是，可以在執行階段對它們進行更新，使封裝更為靈活也易於管理。 運算式的最大長度為 4000 個字元。  
  
 在運算式中指定變數時，必須在變數名稱之前加上 at 符號 (@)。 例如，針對名`Counter`為的變數，請@Counter在「for 迴圈」容器所使用的運算式中輸入。 如果您在變數中包括命名空間屬性，則您必須使用括號將變數與命名空間括起來。 例如，針對`Counter` `MyNamespace`命名空間中的變數，請輸入 [@MyNamespace::Counter]。  
  
 「For 迴圈」容器使用的變數必須定義在「For 迴圈」容器的範圍內，或封裝容器階層中任何更高容器的範圍內。 例如，「For 迴圈」容器可以使用其範圍內定義的變數，也可以使用封裝範圍內定義的變數。 如需詳細資訊，請參閱[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)和[在封裝中使用變數](../../2014/integration-services/use-variables-in-packages.md)。  
  
 
  [!INCLUDE[ssIS](../includes/ssis-md.md)] 運算式文法提供完整的運算子及函數集合，以實作評估、初始化或指派所使用的複雜運算式。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](expressions/integration-services-ssis-expressions.md)為止。  
  
### <a name="to-implement-a-for-loop-container-in-a-control-flow"></a>在控制流程中實作 For 迴圈容器  
  
1.  將「For 迴圈」容器加入封裝。 如需詳細資訊，請參閱[在控制流程中加入或刪除工作或容器](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
2.  將工作和容器加入「For 迴圈」容器。 如需詳細資訊，請參閱[在控制流程中加入或刪除工作或容器](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
3.  使用優先順序條件約束連接「For 迴圈」容器中的工作和容器。 如需詳細資訊，請參閱 [使用預設的優先順序條件約束來連接工作和容器](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)。  
  
4.  設定「For 迴圈」容器。 如需詳細資訊，請參閱 [設定 For 迴圈容器](../../2014/integration-services/configure-a-for-loop-container.md)為止。  
  
## <a name="see-also"></a>另請參閱  
 [在控制流程中加入或刪除工作或容器](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [將元件分組或取消群組](group-or-ungroup-components.md)   
 [使用預設的優先順序條件約束來連線工作和容器](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [將列舉新增至控制流程](../../2014/integration-services/add-enumeration-to-a-control-flow.md)   
 [控制流程](control-flow/control-flow.md)  
  
  
