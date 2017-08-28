---
title: "條件式分割轉換 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.conditionalsplittrans.f1
- sql13.dts.designer.conditionalsplittransformation.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: 02909ff454816119e2dfbdfeb1090d0f7e9587be
ms.contentlocale: zh-tw
ms.lasthandoff: 08/19/2017

---
# <a name="conditional-split-transformation"></a>條件式分割轉換
  「條件式分割」轉換可根據資料的內容，將資料列傳送至不同的輸出。 「條件式分割」轉換的實作與程式設計語言中的 CASE 決策結構類似。 轉換會評估運算式，並根據結果將資料列導向指定的輸出。 此轉換亦提供預設輸出，如此一來，即使資料列未符合任何運算式，仍會導向預設輸出。  
  
## <a name="configuration-of-the-conditional-split-transformation"></a>設定條件式分割轉換  
 您可以利用下列方式設定「條件式分割」轉換：  
  
-   針對您要讓轉換測試的每項條件，提供評估為布林的運算式。  
  
-   指定評估條件的順序。 順序相當重要，因為資料列會傳送至對應評估為 True 之第一項條件的輸出。  
  
-   指定轉換的預設輸出。 轉換需要指定預設輸出。  
  
 每一個輸出資料列只能傳送至一項輸出，也就是評估為 True 之第一項條件的輸出。 例如，下列條件會將 **FirstName** 資料行中任何以字母 *A* 開頭的資料列導向一項輸出，以字母 *B* 開頭的資料列導向另一項輸出，而其他所有資料列則導向預設輸出。  
  
 輸出 1  
  
 `SUBSTRING(FirstName,1,1) == "A"`  
  
 輸出 2  
  
 `SUBSTRING(FirstName,1,1) == "B"`  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包含各種函數和運算子，可用來建立評估輸入資料和導向輸出資料的運算式。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
 條件式分割轉換包括 **FriendlyExpression** 自訂屬性。 屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [在封裝中使用屬性運算式](../../../integration-services/expressions/use-property-expressions-in-packages.md) 和 [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
 此轉換擁有一項輸入、一項或多項輸出，以及一項錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [使用條件式分割轉換來分割資料集](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
-   [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>相關工作  
 [使用條件式分割轉換來分割資料集](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
## <a name="conditional-split-transformation-editor"></a>條件式分割轉換編輯器
  使用 **[條件式分割轉換編輯器]** 對話方塊，即可建立運算式、設定評估運算式的順序，以及命名條件式分割的輸出。 此對話方塊包含可用來建立運算式的數學、字串，以及日期/時間函數與運算子。 評估為 True 的第一個條件會決定資料列的輸出導向。  
  
> [!NOTE]  
>  條件式分割轉換會將每個輸入資料列導向至單一輸出。 如果輸入多重條件，轉換會將每個資料列傳送到條件為 True 的第一個輸出，而略過該資料列後續的條件。 如果您需要連續評估數個條件，就可能需要在資料流程中串連多重條件式分割轉換。  
  
### <a name="options"></a>選項  
 **單**  
 選取資料列並使用右邊的方向鍵來變更評估運算式的順序。  
  
 **輸出名稱**  
 提供輸出名稱。 預設為已編號的案例清單；然而，您可選擇任何唯一的、描述性名稱。  
  
 **條件**  
 輸入運算式或從可用的資料行、變數、函數以及運算子的清單中拖曳來建立運算式。  
  
 此屬性的值可以使用屬性運算式指定。  
  
 **相關主題︰**[Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)[運算子 &#40;SSIS 運算式&#41;](../../../integration-services/expressions/operators-ssis-expression.md)和[函數 &#40;SSIS 運算式&#41;](../../../integration-services/expressions/functions-ssis-expression.md)  
  
 **預設輸出名稱**  
 輸入預設輸出的名稱，或使用預設值。  
  
 **設定錯誤輸出**  
 使用 [ [設定錯誤輸出](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) ] 對話方塊來指定如何處理錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
