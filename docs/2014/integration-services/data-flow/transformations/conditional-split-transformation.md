---
title: 條件式分割轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittrans.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dcfbbac9eacc96384a723088cf8f20cc939bdc48
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62900822"
---
# <a name="conditional-split-transformation"></a>條件式分割轉換
  「條件式分割」轉換可根據資料的內容，將資料列傳送至不同的輸出。 條件式分割轉換的實作類似程式設計語言中的 CASE 決策結構。 轉換會評估運算式，並根據結果將資料列導向指定的輸出。 此轉換也提供預設輸出，因此若某個資料列不符合任何運算式，它會被導向到預設輸出。  
  
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
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包含各種函數和運算子，可用來建立評估輸入資料和導向輸出資料的運算式。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../expressions/integration-services-ssis-expressions.md)為止。  
  
 條件式分割轉換包括 `FriendlyExpression` 自訂屬性。 屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [在封裝中使用屬性運算式](../../expressions/use-property-expressions-in-packages.md) 和 [轉換自訂屬性](transformation-custom-properties.md)。  
  
 此轉換擁有一項輸入、一項或多項輸出，以及一項錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關 **[條件式分割轉換編輯器]** 對話方塊中可設定屬性的詳細資訊，請參閱＜ [Conditional Split Transformation Editor](../../conditional-split-transformation-editor.md)＞。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [使用條件式分割轉換來分割資料集](conditional-split-transformation.md)  
  
-   [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>相關工作  
 [使用條件式分割轉換來分割資料集](conditional-split-transformation.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../data-flow.md)   
 [Integration Services 轉換](integration-services-transformations.md)  
  
  
