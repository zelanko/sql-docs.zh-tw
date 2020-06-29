---
title: 使用預設的優先順序條件約束來連接工作和容器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- precedence constraints [Integration Services], connecting tasks
- default precedence constraints
- containers [Integration Services], precedence constraints
ms.assetid: 8f31f15f-98ff-4c35-b41f-8b8cfd148d75
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4d453b4a24da893515aafd29b0398685a7155d4e
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85434475"
---
# <a name="connect-tasks-and-containers-by-using-a-default-precedence-constraint"></a>使用預設的優先順序條件約束來連接工作和容器
  優先順序條件約束可以連接兩個可執行檔。 可執行檔可以是任何工作或「For 迴圈」、「Foreach 迴圈」或「時序」容器。 此程序描述如何設定優先順序條件約束的預設行為，及如何使用預設的優先順序條件約束來連接可執行檔。  
  
## <a name="creating-default-precedence-constraints"></a>建立預設的優先順序條件約束  
 首次使用「[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」時，優先順序條件約束的預設值為 `Success`。 請遵循下列步驟來設定「 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」，以便使用優先順序條件約束的其他預設值。  
  
#### <a name="to-set-the-default-value-for-precedence-constraints"></a>設定優先順序條件約束的預設值  
  
1.  開啟 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
2.  在 **[工具]** 功能表上，按一下 **[選項]** 。  
  
3.  在 [選項]**** 對話方塊中，展開 [商業智慧設計師]****，然後展開 [Integration Services 設計師]****。  
  
4.  按一下 [控制流程自動連接]****，然後選取 [依預設，將新形狀連接到選取的形狀]****。  
  
5.  在下拉式清單中，選擇 [在新形狀使用「失敗」條件約束]**** 或 [在新形狀使用「完成」條件約束]****。  
  
6.  按一下 [確定]****。  
  
#### <a name="to-create-a-default-precedence-constraint"></a>建立預設的優先順序條件約束  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  在 [控制流程]**** 索引標籤的設計介面上，按一下工作或容器，然後將其連接子拖曳到您要套用優先順序條件約束的可執行檔。  
  
5.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [優先順序條件約束](control-flow/precedence-constraints.md)   
 [使用快捷方式功能表來設定優先順序條件約束的值](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [設定優先順序條件約束的屬性](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)   
 [在優先順序條件約束中使用運算式](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
