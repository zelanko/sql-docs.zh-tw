---
title: 條件式分割轉換編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittransformation.f1
helpviewer_keywords:
- Conditional Split Transformation Editor
ms.assetid: c30e1633-537a-4837-9991-6203c6f2a21e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 920ec41ae30d53853cfb757fb7fc33610953dc86
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66060890"
---
# <a name="conditional-split-transformation-editor"></a>條件式分割轉換編輯器
  使用 **[條件式分割轉換編輯器]** 對話方塊，即可建立運算式、設定評估運算式的順序，以及命名條件式分割的輸出。 此對話方塊包含可用來建立運算式的數學、字串，以及日期/時間函數與運算子。 評估為 True 的第一個條件會決定資料列的輸出導向。  
  
> [!NOTE]  
>  條件式分割轉換會將每個輸入資料列導向至單一輸出。 如果輸入多重條件，轉換會將每個資料列傳送到條件為 True 的第一個輸出，而略過該資料列後續的條件。 如果您需要連續評估數個條件，就可能需要在資料流程中串連多重條件式分割轉換。  
  
 若要深入了解條件式分割轉換，請參閱 [條件式分割轉換](data-flow/transformations/conditional-split-transformation.md)。  
  
## <a name="options"></a>選項。  
 **單**  
 選取資料列並使用右邊的方向鍵來變更評估運算式的順序。  
  
 **輸出名稱**  
 提供輸出名稱。 預設為已編號的案例清單；然而，您可選擇任何唯一的、描述性名稱。  
  
 **條件**  
 輸入運算式或從可用的資料行、變數、函數以及運算子的清單中拖曳來建立運算式。  
  
 此屬性的值可以使用屬性運算式指定。  
  
 **相關主題：**[Integration Services &#40;ssis&#41; 運算式](expressions/integration-services-ssis-expressions.md)、 [&#40;ssis 運算式&#41;的運算子](expressions/operators-ssis-expression.md)，以及[&#40;ssis 運算式的函數](expressions/functions-ssis-expression.md)&#41;   
  
 **預設輸出名稱**  
 輸入預設輸出的名稱，或使用預設值。  
  
 **設定錯誤輸出**  
 使用 [ [設定錯誤輸出](../../2014/integration-services/configure-error-output.md) ] 對話方塊來指定如何處理錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用條件式分割轉換來分割資料集](data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
  
