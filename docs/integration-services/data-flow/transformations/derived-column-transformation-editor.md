---
title: "衍生資料行轉換編輯器 |Microsoft 文件"
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
- sql13.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- Derived Column Transformation Editor
ms.assetid: ff73923e-d245-43d8-bf24-af3bdc942e51
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 89b764a8ea3d4e60852092ef502eb82adcf77c91
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="derived-column-transformation-editor"></a>衍生的資料行轉換編輯器
  使用 [衍生的資料行轉換編輯器] 對話方塊，即可建立會擴展新的資料行或取代資料行的運算式。  
  
 若要深入了解「衍生的資料行」轉換，請參閱[衍生的資料行轉換](../../../integration-services/data-flow/transformations/derived-column-transformation.md)。  
  
## <a name="options"></a>選項。  
 **變數和資料行**  
 將變數或資料行從可用之變數與資料行清單中拖曳至下面窗格中現有的資料表資料列，或是拖曳至清單底部的新資料列，即可建立使用變數或輸入資料行的運算式。  
  
 **函數和運算子**  
 從清單中將函數和運算子拖曳至下面的窗格，即可建立使用函數或運算子來評估輸入資料與直接輸出資料的運算式。  
  
 **衍生的資料行名稱**  
 提供衍生的資料行名稱。 預設為衍生資料行的已編號清單；然而，您可以選擇任何唯一的描述性名稱。  
  
 **衍生的資料行**  
 從清單中選取衍生的資料行。 選擇是否要將衍生的資料行加入為新的輸出資料行，或是要取代現有資料行中的資料。  
  
 **運算式**  
 輸入運算式，或是從先前的可用資料行、變數、函數以及運算子清單中拖曳過來，以建立一個運算式。  
  
 此屬性的值可以使用屬性運算式指定。  
  
 **相關主題**︰[Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)、[運算子 &#40;SSIS 運算式&#41;](../../../integration-services/expressions/operators-ssis-expression.md)和[函數 &#40;SSIS 運算式&#41;](../../../integration-services/expressions/functions-ssis-expression.md)  
  
 **資料類型**  
 如果將資料加入新的資料行，[衍生的資料行轉換編輯器] 對話方塊就會自動評估運算式，並且適當設定資料類型。 這個資料行的值是唯讀的。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
 **長度**  
 如果將資料加入新的資料行，[衍生的資料行轉換編輯器] 對話方塊就會自動評估運算式，並且設定字串資料的資料行長度。 這個資料行的值是唯讀的。  
  
 **有效位數**  
 如果將資料加入新的資料行，[衍生的資料行轉換編輯器] 對話方塊就會自動根據資料類型來設定數值資料的有效位數。 這個資料行的值是唯讀的。  
  
 **小數位數**  
 如果將資料加入新的資料行，[衍生的資料行轉換編輯器] 對話方塊就會自動根據資料類型來設定數值資料的小數位數。 這個資料行的值是唯讀的。  
  
 **字碼頁**  
 如果將資料加入新的資料行，[衍生的資料行轉換編輯器] 對話方塊就會自動設定 DT_STR 資料類型的字碼頁。 您可以更新 [字碼頁]。  
  
 **設定錯誤輸出**  
 使用 [ [設定錯誤輸出](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) ] 對話方塊來指定如何處理錯誤。  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 錯誤和訊息參考](../../../integration-services/integration-services-error-and-message-reference.md)   
 [使用衍生的資料行轉換來衍生資料行值](../../../integration-services/data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
  
