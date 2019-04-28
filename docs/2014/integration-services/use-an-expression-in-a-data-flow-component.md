---
title: 在資料流程元件中使用運算式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], data flow
- expressions [Integration Services], data flow components
ms.assetid: 9181b998-d24a-41fb-bb3c-14eee34f910d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f7ece364cb1d0bbe2cc36b07de58873fc95acaed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877923"
---
# <a name="use-an-expression-in-a-data-flow-component"></a>在資料流程元件中使用運算式
  此程序描述如何將運算式加入「條件式分割」轉換或「衍生的資料行」轉換。 「條件式分割」轉換會使用運算式，定義將資料列導向轉換輸出的條件，而「衍生的資料行」轉換則使用運算式，定義指派給資料行的值。  
  
 若要在轉換中實作運算式，封裝必須至少包括一個「資料流程」工作和一個來源。 如需有關將項目加入封裝的詳細資訊，請參閱下列主題：  
  
-   [在控制流程中新增或刪除工作或容器](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
    
  
-   [在資料流程中加入或刪除元件](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
-   [連接資料流程中的元件](data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-create-an-expression"></a>若要建立運算式  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中，按一下 [控制流程] 索引標籤，然後再按包含要在其中實作運算式之資料流程的「資料流程」工作。  
  
4.  按一下 [資料流程] 索引標籤，然後將「條件式分割」或「衍生的資料行」轉換，從 [工具箱] 拖曳至設計介面。  
  
5.  將綠色連接子從來源或轉換拖曳至「條件式分割」或「衍生的資料行」轉換。  
  
6.  按兩下轉換，以開啟其對話方塊。  
  
7.  在左窗格中，展開 [變數]，以顯示系統變數和使用者自訂變數，並展開 [資料行]，以顯示轉換輸入資料行。  
  
8.  在右窗格中，展開 [數學函數]、[字串函數]、[日期/時間函數]、[NULL 函數]、[類型轉換] 和 [運算子]，以存取運算式文法所提供的函數、轉換和運算子。  
  
9. 因轉換的不同，請執行下列其中之一，以建立運算式：  
  
    -   在 [條件式分割轉換編輯器] 對話方塊中，將變數、資料行、函數、運算子和轉換拖曳至 [條件] 資料行。 您也可以在 [條件] 資料行中直接鍵入運算式。  
  
    -   在 [衍生的資料行轉換編輯器] 對話方塊中，將變數、資料行、函數、運算子和轉換拖曳至 [運算式] 資料行。 您也可以在 [運算式] 資料行中直接鍵入運算式。  
  
        > [!NOTE]  
        >  從 [條件] 資料行或 [運算式] 資料行移除焦點時，運算式文字可能會反白顯示，指示運算式語法不正確。  
  
10. 按一下 [確定]，以結束對話方塊。  
  
    > [!NOTE]  
    >  如果運算式無效，則會出現警示，描述運算式中的語法錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 運算式](expressions/integration-services-ssis-expressions.md)   
 [Conditional Split Transformation](data-flow/transformations/conditional-split-transformation.md)   
 [Derived Column Transformation](data-flow/transformations/derived-column-transformation.md)   
 [資料流程工作](control-flow/data-flow-task.md)   
 [資料流程](data-flow/data-flow.md)  
  
  
