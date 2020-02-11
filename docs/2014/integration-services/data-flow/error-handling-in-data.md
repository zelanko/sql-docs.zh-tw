---
title: 處理資料中的錯誤 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- truncating data
- data conversion errors [Integration Services]
- errors [Integration Services], data flow components
- lookups [Integration Services]
- errors [Integration Services]
- errors [Integration Services], data flow outputs
- error outputs [Integration Services]
- data flow [Integration Services], errors
- expressions [Integration Services], errors
ms.assetid: c61667b4-25cb-4d45-a52f-a733e32863f4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8b5a98877e04a077bf1bb1c0c527500f3102b862
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62827141"
---
# <a name="error-handling-in-data"></a>處理資料中的錯誤
  當資料流程元件將轉換套用至資料行資料、從來源擷取資料或將資料載入目的地時，可能會發生錯誤。 錯誤通常是因為非預期的資料值所產生的。 例如，資料轉換失敗的原因是資料行包含字串而非數字；向資料庫資料行插入失敗的原因是資料為日期，而資料行是數值資料類型；運算式評估失敗的原因是資料行值為零，導致數學運算無效。  
  
 通常，錯誤可歸類為下列類別之一：  
  
-   資料轉換錯誤，當轉換導致遺失有效數位、遺失無效位數以及字串截斷時，會發生此錯誤。 如果所要求的轉換不受支援，也會發生資料轉換錯誤。  
  
-   運算式評估錯誤，如果在執行階段評估的運算式執行無效作業，或者，由於遺失或錯誤的資料值而語法不正確，則會發生此錯誤。  
  
-   查閱錯誤，如果查閱作業無法在查閱資料表中找到相符部分，則會發生此錯誤。  
  
 許多資料流程元件都支援錯誤輸出，這可讓您控制元件處理內送資料與外送資料中資料列層級錯誤的方式。 您可以藉由設定輸入或輸出中個別資料行的選項，來指定發生截斷或錯誤時元件的行為方式。 例如，您可以指定，如果客戶名稱資料被截斷則元件應失敗，但忽略包含不重要資料之其他資料行的錯誤。  
  
 錯誤輸出可以連接到其他轉換的輸入，或載入無錯誤輸出以外的其他目的地。 例如，錯誤輸出可以連接到為空白資料行提供字串之「衍生的資料行」轉換。  
  
 下圖顯示包含錯誤輸出的簡單資料流程。  
  
 ![具有錯誤輸出的資料流程](../media/mw-dts-11.gif "具有錯誤輸出的資料流程")  
  
 除資料行之外，錯誤輸出還包含 **ErrorCode** 和 **ErrorColumn** 資料行。 
  **ErrorCode** 資料行可以識別錯誤， **ErrorColumn** 包含錯誤資料行的歷程識別碼。 若要檢視這些資料行的中繼資料，請按一下將錯誤輸出連接到資料流程中之下一個元件的路徑。 在某些情況下， **ErrorColumn** 資料行的值會被設定為零。 當錯誤狀況影響整個資料列而非單一資料行時，就會發生這種情況。 其中一個例子是查閱轉換中的查閱失敗時。  
  
 如需詳細資訊，請參閱 [資料流程](data-flow.md) 和 [Integration Services 路徑](integration-services-paths.md)。  
  
 如需 Integration Services 錯誤、警告和其他訊息的清單，請參閱 [Integration Services 錯誤和訊息參考](../integration-services-error-and-message-reference.md)。  
  
## <a name="error-and-truncation-options"></a>錯誤與截斷選項  
 錯誤可以歸類為下列兩種類別之一：錯誤或截斷。 錯誤表示明確的失敗，並產生 NULL 結果。 此類錯誤可以包含資料轉換錯誤或運算式評估錯誤。 例如，嘗試將包含字母字元的字串轉換為數值時，會導致錯誤。 資料轉換、運算式評估，以及運算式結果指派至變數、屬性和資料行可能會因為不合法的轉型和不相容的資料類型而失敗。 如需詳細資訊，請參閱 [Cast &#40;SSIS 運算式&#41;](../expressions/cast-ssis-expression.md)、[運算式中的 Integration Services 資料類型](../expressions/integration-services-data-types-in-expressions.md)和 [Integration Services 資料類型](integration-services-data-types.md)。  
  
 截斷的嚴重性低於錯誤。 截斷產生的結果可能是可使用的，甚至可能是想要的結果。 您可以選擇將截斷視為錯誤或可接受的條件。 例如，如果您要將 15 個字元的字串插入寬度僅為一個字元的資料行中，則您可以選擇截斷字串。  
  
 您可以設定來源、轉換及目的地處理錯誤和截斷的方式。 下表描述這些選項。  
  
|選項|描述|  
|------------|-----------------|  
|失敗元件|當發生錯誤或截斷時，資料流程工作將失敗。 失敗是錯誤和截斷的預設選項。|  
|忽略失敗|會忽略錯誤或截斷，並會將資料列導向轉換或來源的輸出。|  
|重新導向資料列|會將錯誤或截斷資料列導向來源、轉換或目的地的錯誤輸出。|  
  
## <a name="adding-the-error-description"></a>新增錯誤描述  
 依預設，錯誤輸出會提供數值錯誤碼，且通常包含發生錯誤之資料行的識別碼。 您可以使用「指令碼」元件，利用單行指令碼來呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> 介面的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 方法，以便將錯誤描述包含在其他的資料行中。  
  
 「指令碼」元件可以加入資料流程之錯誤區段的任何位置，但必須在您想擷取錯誤之資料流程元件的下游；不過這個元件通常是在將錯誤資料列寫入目的地之前才放入。 如此一來指令碼就只會查閱寫入之錯誤資料列的描述。 例如，資料流程的錯誤區段可能會更新某些錯誤，而且不會將這些資料列寫入錯誤目的地。 如需詳細資訊，請參閱[使用腳本元件增強錯誤輸出](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md)。  
  
### <a name="to-configure-an-error-output"></a>設定錯誤輸出  
  
-   [在資料流程元件中設定錯誤輸出](../configure-an-error-output-in-a-data-flow-component.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](data-flow.md)   
 [使用轉換來轉換資料](transformations/transform-data-with-transformations.md)   
 [以路徑連接元件](../connect-components-with-paths.md)   
 [資料流程工作](../control-flow/data-flow-task.md)   
 [資料流程](data-flow.md)  
  
  
