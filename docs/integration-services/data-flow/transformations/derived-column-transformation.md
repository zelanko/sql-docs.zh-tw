---
title: 衍生資料行轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.derivedcolumntrans.f1
- sql13.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- multiple derived columns
- expressions [Integration Services], derived columns
- derived columns
- columns [Integration Services], derivations
- Derived Column transformation
ms.assetid: 8eba755e-8e48-4233-bd1e-09a46bf2692f
caps.latest.revision: 60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 11848095ae04a257063601dc41aa8f146386775f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="derived-column-transformation"></a>衍生的資料行轉換
  「衍生的資料行」轉換會將運算式套用至轉換輸入資料行，藉此建立新的資料行值。 運算式可包含來自轉換輸入之變數、函數、運算子和資料行的任意組合。 結果可加入做為新的資料行，或插入現有資料行做為取代值。 「衍生的資料行」轉換可定義多個衍生的資料行，且任何變數或輸入資料行都可在多個運算式中出現。  
  
 您可以使用此轉換執行下列工作：  
  
-   將不同資料行的資料串連至衍生的資料行中。 例如，您可以使用運算式 **，將** FirstName **和** LastName **資料行的值結合到名為**FullName `FirstName + " " + LastName`的單一衍生資料行中。  
  
-   使用如 SUBSTRING 的函數從字串資料擷取字元，然後將結果儲存到衍生的資料行中。 例如，您可以使用運算式 **，從** FirstName `SUBSTRING(FirstName,1,1)`資料行中擷取人員的名字縮寫。  
  
-   套用數學函數至數值資料，然後將結果儲存到衍生的資料行中。 例如，您可以使用運算式 **，將數值資料行**SalesTax `ROUND(SalesTax, 2)`的長度和有效位數變更為含有兩位小數的數字。  
  
-   建立比較輸入資料行和變數的運算式。 例如，您可以使用運算式 **，對照** ProductVersion **資料行中的資料比較變數**Version **，並根據比較結果，使用** Version **或**ProductVersion `ProductVersion == @Version? ProductVersion : @Version`的值。  
  
-   擷取日期時間值的部分。 例如，您可以使用運算式 `DATEPART("year",GETDATE())`，利用 GETDATE 和 DATEPART 函數擷取目前的年份。  
  
-   使用運算式將日期字串轉換成特定格式。  
  
## <a name="configuration-of-the-derived-column-transformation"></a>設定衍生資料行轉換  
 您可以利用下列方式設定「衍生的資料行」轉換：  
  
-   為每一個要變更的輸入資料行或新資料行提供運算式。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
    > [!NOTE]  
    >  如果運算式參考「衍生的資料行」轉換所覆寫的輸入資料行，則運算式會使用資料行的原始值，而非衍生的值。  
  
-   若要將結果加入新資料行，並且資料類型是 **string**，請指定字碼頁。 如需詳細資訊，請參閱 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。  
  
 衍生的資料行轉換包括 FriendlyExpression 自訂屬性。 屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [在封裝中使用屬性運算式](../../../integration-services/expressions/use-property-expressions-in-packages.md)和 [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
 這個轉換有一個輸入、一個規則輸出及一個錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>相關工作  
  
-   [使用衍生的資料行轉換來衍生資料行值](../../../integration-services/data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
## <a name="derived-column-transformation-editor"></a>衍生的資料行轉換編輯器
  使用 [衍生的資料行轉換編輯器] 對話方塊，即可建立會擴展新的資料行或取代資料行的運算式。  
  
### <a name="options"></a>選項。  
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
 如果將資料加入新的資料行，[衍生的資料行轉換編輯器] 對話方塊就會自動評估運算式，並且適當設定資料類型。 這個資料行的值是唯讀的。 如需詳細資訊，請參閱 [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md)。  
  
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
  
## <a name="related-content"></a>相關內容  
 social.technet.microsoft.com 上的技術文件： [SSIS 運算式範例](http://go.microsoft.com/fwlink/?LinkId=220761)  
