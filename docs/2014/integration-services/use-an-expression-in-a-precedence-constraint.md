---
title: 在 優先順序條件約束中使用運算式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- precedence constraints [Integration Services], adding expressions
- expressions [Integration Services], adding
ms.assetid: 601038bb-3b17-42ac-b09d-5b3a82fb6564
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 672d9c363f64037f5f40f51fc7c6cb1c4c3bc674
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66054752"
---
# <a name="use-an-expression-in-a-precedence-constraint"></a>在優先順序條件約束中使用運算式
  此程序描述如何使用 [優先順序條件約束編輯器] 對話方塊，將運算式加入優先順序條件約束。 封裝必須包括至少兩個可執行檔 (工作或容器)，且這兩個可執行檔必須由優先順序條件約束連接，您才可以將運算式加入優先順序條件約束。  
  
### <a name="to-add-an-expression-to-a-precedence-constraint"></a>將運算式加入優先順序條件約束  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  在 [控制流程] 索引標籤的設計介面上，按兩下優先順序條件約束。 [優先順序條件約束編輯器] 隨即開啟。  
  
5.  在 [評估作業] 清單中，選取 [運算式]、[運算式與條件約束] 或 [運算式或條件約束]。  
  
6.  在 [運算式] 文字方塊中輸入運算式，或啟動運算式產生器以建立運算式。  
  
7.  若要驗證運算式語法，請按一下 [測試]。  
  
8.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [優先順序條件約束](control-flow/precedence-constraints.md)   
 [使用預設的優先順序條件約束來連線工作和容器](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [使用快顯功能表設定優先順序條件約束的值](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [設定優先順序條件約束的屬性](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)   
 [Integration Services &#40;SSIS&#41; 運算式](expressions/integration-services-ssis-expressions.md)  
  
  
