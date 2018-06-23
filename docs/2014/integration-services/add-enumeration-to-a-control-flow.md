---
title: 將列舉加入控制流程 |Microsoft 文件
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- adding enumerations
- Foreach Loop containers
- control flow [Integration Services], enumerations
- repeating workflows
- enumerations [Integration Services]
ms.assetid: f212b5fb-3cc4-422e-9b7c-89eb769a812a
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 10d30541be42331b544882f8a8b85f75db7f230d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034421"
---
# <a name="add-enumeration-to-a-control-flow"></a>將列舉加入控制流程
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包括 Foreach 迴圈容器，該容器為控制流程項目，可簡化在套件的控制流程中包括列舉檔案及物件的迴圈建構。 如需詳細資訊，請參閱 [Foreach Loop Container](control-flow/foreach-loop-container.md)。  
  
 「Foreach 迴圈」容器不提供功能，僅提供可在其中建立可重複控制流程、指定列舉類型並設定列舉值的結構。 若要提供容器功能，必須在「Foreach 迴圈」容器中至少包括一個工作。 如需詳細資訊，請參閱 [Integration Services Tasks](control-flow/integration-services-tasks.md)。  
  
 「Foreach 迴圈」容器可以包括具有多個工作的控制流程及其他容器。 將工作及容器加入「Foreach 迴圈」容器與將它們加入封裝類似，只是您要將工作及容器拖曳至「Foreach 迴圈」容器而不是封裝。 如果「Foreach 迴圈」容器包含一個以上的工作或容器，則您可以如同在封裝中所做的一樣，使用優先順序條件約束來連接它們。 如需詳細資訊，請參閱 [Precedence Constraints](control-flow/precedence-constraints.md)。  
  
### <a name="to-implement-a-foreach-loop-container-in-a-control-flow"></a>在控制流程中實作 Foreach 迴圈容器  
  
1.  將「Foreach 迴圈」容器加入封裝。 如需詳細資訊，請參閱[加入或刪除工作或容器中的控制流程](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  執行個體時提供 SQL Server 登入。  
  
2.  將工作和容器加入「Foreach 迴圈」容器。 如需詳細資訊，請參閱[加入或刪除工作或容器中的控制流程](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  執行個體時提供 SQL Server 登入。  
  
3.  使用優先順序條件約束連接「Foreach 迴圈」容器中的工作和容器。 如需詳細資訊，請參閱 [使用預設的優先順序條件約束來連接工作和容器](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)。  
  
4.  設定「Foreach 迴圈」容器。 如需詳細資訊，請參閱 [設定 Foreach 迴圈容器](../../2014/integration-services/configure-a-foreach-loop-container.md)。  
  
## <a name="see-also"></a>另請參閱  
 [加入或刪除工作或容器中的控制流程](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [群組或取消群組的元件](group-or-ungroup-components.md)   
 [優先順序條件約束](control-flow/precedence-constraints.md)   
 [將反覆運算加入控制流程](add-iteration-to-a-control-flow.md)   
 [控制流程](control-flow/control-flow.md)  
  
  