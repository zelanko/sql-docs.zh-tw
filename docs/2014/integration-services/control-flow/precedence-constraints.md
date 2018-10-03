---
title: 優先順序條件約束 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- control flow [Integration Services], precedence constraints
- precedence constraints [Integration Services]
- constraints [Integration Services]
- sequence execution options [Integration Services]
- containers [Integration Services], precedence constraints
ms.assetid: c5ce5435-fd89-4156-a11f-68470a69aa9f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d233d2ee94a611c63e8466102c66bd01e77b0513
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063458"
---
# <a name="precedence-constraints"></a>優先順序條件約束
  優先順序條件約束可在控制流程中，連結封裝中的可執行檔、容器和工作，並指定判斷可執行檔是否執行的條件。 可執行檔可以是「For 迴圈」容器、「Foreach 迴圈」容器、「時序」容器、工作或事件處理常式。 事件處理常式也可使用優先順序條件約束，以將其可執行檔連結至控制流程。  
  
 優先順序條件約束會連結兩個可執行檔：優先順序可執行檔和受條件約束的可執行檔。 優先順序可執行檔在條件約束可執行檔之前執行，且優先順序可執行檔的執行結果可以決定條件約束可執行檔是否執行。 下圖顯示了由優先順序條件約束連結的兩個可執行檔。  
  
 ![以優先順序條件約束連接的可執行檔](../media/ssis-pcsimple.gif "以優先順序條件約束連接的可執行檔")  
  
 在線性控制流程 (即沒有分支的控制流程) 中，優先順序條件約束單獨管理工作執行的順序。 在控制流程分支中，[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 執行階段引擎決定直接跟隨在分支後面的工作和容器之執行順序。 執行階段引擎也決定控制流程中未連接的工作流程之執行順序。  
  
 除僅封裝單一工作的工作主機容器之外，[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 的巢狀容器架構會啟用所有容器，用以包含每個都具有其各自控制流程的其他容器。 「For 迴圈」容器、「Foreach 迴圈」容器和「時序」容器可以包含多個工作和其他容器，而工作和其他容器進而可以包含多個工作和容器。 例如，具有「指令碼」工作和「時序」容器的封裝具有連結「指令碼」工作和「時序」容器的優先順序條件約束。 「時序」容器包括三個「指令碼」工作，且其優先順序條件約束會將這三個「指令碼」工作連結至一個控制流程。 下圖顯示具有兩個巢狀層級之封裝中的優先順序條件約束。  
  
 ![封裝中的優先順序條件約束](../media/mw-dts-12.gif "封裝中的優先順序條件約束")  
  
 因為封裝位於 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 容器架構的最上層，所以優先順序條件約束無法連結多個封裝；但是，您可以將「執行封裝」工作加入封裝，然後間接地將其他封裝連結至控制流程。  
  
 您可以利用下列方式設定優先順序條件約束：  
  
-   指定評估作業。 優先順序條件約束同時使用條件約束值和運算式，或使用其中之一，來決定條件約束可執行檔是否執行。  
  
-   如果優先順序條件約束使用執行結果，則您可以將執行結果指定為成功、失敗或完成。  
  
-   如果優先順序條件約束使用評估結果，則您可以提供評估為布林的運算式。  
  
-   指定只評估優先順序條件約束，還是同時評估套用至條件約束可執行檔的其他條件約束。  
  
## <a name="evaluation-operations"></a>評估作業  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 提供下列評估作業：  
  
-   僅使用優先順序可執行檔之執行結果的條件約束，以決定條件約束可執行檔是否執行。 優先順序可執行檔的執行結果可以是完成、成功或失敗。 這是預設作業。  
  
-   運算式，對其進行評估以決定條件約束可執行檔是否執行。 如果運算式評估為 true，則條件約束可執行檔會執行。  
  
-   運算式與條件約束，此條件約束會組合優先順序可執行檔之執行結果與評估運算式之傳回結果兩者的需求。  
  
-   運算式或條件約束，此條件約束會使用優先順序可執行檔的執行結果或評估運算式的傳回結果。  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師使用色彩識別優先順序條件約束的類型。 「成功」條件約束為綠色，「失敗」條件約束為紅色，而「完成」條件約束則為藍色。 若要在顯示條件約束類型的 [[!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師] 中顯示文字標籤，則必須設定 [[!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師] 的協助工具功能。  
  
 運算式必須為有效的 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 運算式，並且它可以包括函數、運算子、系統和自訂變數。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../expressions/integration-services-ssis-expressions.md)和 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)。  
  
## <a name="execution-results"></a>執行結果  
 優先順序條件約束可以只使用下列執行結果，或與運算式一起使用。  
  
-   完成，只要求優先順序可執行檔完成 (無須考慮結果)，就可執行條件約束可執行檔。  
  
-   成功，要求優先順序可執行檔必須成功完成，才可執行條件約束可執行檔。  
  
-   失敗，要求優先順序可執行檔失敗時，才可執行條件約束可執行檔。  
  
> [!NOTE]  
>  只有成員相同的優先順序條件約束`Precedence Constraint`集合可以分組邏輯的 AND 條件。 例如，您無法結合來自兩個「Foreach 迴圈」容器的優先順序條件約束。  
  
## <a name="configuration-of-the-precedence-constraint"></a>優先順序條件約束的組態  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [[!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師] 中設定之屬性的詳細資訊，請參閱[優先順序條件約束編輯器](../precedence-constraint-editor.md)。  
  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>。  
  
## <a name="related-tasks"></a>相關工作  
 如需有關如何在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中設定這些屬性的詳細資訊，請按下列主題之一：  
  
-   [設定優先順序條件約束的屬性](../set-the-properties-of-a-precedence-constraint.md)  
  
-   [使用捷徑功能表來設定優先順序條件約束的值](../set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)  
  
-   [使用預設的優先順序條件約束來連接工作和容器](../connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)  
  
     本主題會提供有關如何設定優先順序條件約束的預設行為，以及如何使用預設的優先順序條件約束來連接可執行檔的詳細資訊。  
  
## <a name="related-content"></a>相關內容  
 social.technet.microsoft.com 上的技術文件： [SSIS 運算式範例](http://go.microsoft.com/fwlink/?LinkId=220761)  
  
## <a name="see-also"></a>另請參閱  
 [將運算式加入優先順序條件約束](../add-expressions-to-precedence-constraints.md)   
 [多個優先順序條件約束](../multiple-precedence-constraints.md)  
  
  
