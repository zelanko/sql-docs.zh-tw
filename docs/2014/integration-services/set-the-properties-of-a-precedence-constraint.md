---
title: 設定優先順序條件約束的屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Precedence Constraint Editor dialog box
- precedence constraints [Integration Services], properties
ms.assetid: d990f600-5c09-4cd5-8528-0a58d79dc9f2
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 679e61c37df7d31b80f47fff186589ce0081f838
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84963118"
---
# <a name="set-the-properties-of-a-precedence-constraint"></a>設定優先順序條件約束的屬性
  若要設定優先順序條件約束的屬性，您可以使用下列其中一項工具：  
  
-   您可以使用 [優先順序條件約束編輯器]**** 對話方塊。  
  
-   您可以使用 [屬性] 視窗。 [屬性] 視窗會列出屬性，以供您設定在 [優先順序條件約束編輯器]**** 視窗中無法取得的優先順序條件約束。 在 [屬性] 視窗中，您可以提供優先順序條件約束的描述和名稱，並且設定要在設計介面上顯示的優先順序條件約束註解。  
  
 下列程序將描述如何使用其中一項工具來設定優先順序條件約束的屬性。  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-precedence-constraint-editor"></a>使用優先順序條件約束編輯器來設定優先順序條件約束的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  按兩下優先順序條件約束，  
  
     [優先順序條件約束編輯器]**** 隨即開啟。  
  
5.  在 [評估作業]**** 下拉式清單中，選取評估作業。  
  
6.  在 `Value` 下拉式清單中，選取優先順序可執行檔的執行結果。  
  
7.  如果評估作業使用運算式，請在方塊中 `Expression` 輸入運算式，然後按一下 [**測試**] 來評估運算式。  
  
    > [!NOTE]  
    >  變數名稱會區分大小寫。  
  
8.  如果有多個工作或容器連接到受條件約束的可執行檔，請選取 [**邏輯 AND** ]，以指定所有先前可執行檔的執行結果都必須評估為 `true` 。 選取 [**邏輯 OR** ]，以指定只有一個執行結果必須評估為 `true` 。  
  
9. 按一下 [確定]****，以關閉 [優先順序條件約束編輯器]****。  
  
10. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-properties-window"></a>使用屬性視窗來設定優先順序條件約束的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含要修改之封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [**控制流程**] 索引標籤。在 [**控制流程**] 索引標籤的設計介面上，以滑鼠右鍵按一下優先順序條件約束，然後按一下 [**屬性**]。 在 [屬性] 視窗中，修改屬性值。  
  
4.  在 [屬性]**** 視窗中，設定優先順序條件約束的下列讀取/寫入屬性：  
  
    |讀取/寫入屬性|組態動作|  
    |--------------------------|--------------------------|  
    |描述|提供描述。|  
    |EvalOp|選取評估作業。 如果 `Expression` 已選取、 **[Expressionandconstant]** 或 **[expressionorconstant**作業，您可以指定運算式。|  
    |運算是|如果評估作業包含運算式，請提供一個運算式。 運算式必須評估為布林。 如需運算式語言的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](expressions/integration-services-ssis-expressions.md)。|  
    |LogicalAnd|設定 `LogicalAnd` 為指定當多個可執行檔在和連結到受條件約束的可執行檔時，是否要與其他優先順序條件約束一起評估優先順序條件約束|  
    |名稱|更新優先順序條件約束的名稱。|  
    |ShowAnnotation|指定要使用之註解的類型。 選擇 [Never]**** 以停用註解，選擇 [AsNeeded]**** 以視需要啟用註解，選擇 [ConstraintName]**** 以使用 Name 屬性的值來自動註解，選擇 [ConstraintDescription]**** 以使用 Description 屬性的值來自動註解，以及選擇 [ConstraintOptions]**** 以使用 Value 和 Expression 屬性的值來自動註解。|  
    |值|如果 EvalOP 屬性中指定的評估作業包含條件約束，請選取具有條件約束之可執行檔的執行結果。|  
  
5.  關閉 [屬性] 視窗。  
  
6.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [優先順序條件約束](control-flow/precedence-constraints.md)   
 [使用預設的優先順序條件約束來連接工作和容器](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [使用快捷方式功能表來設定優先順序條件約束的值](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [在優先順序條件約束中使用運算式](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
