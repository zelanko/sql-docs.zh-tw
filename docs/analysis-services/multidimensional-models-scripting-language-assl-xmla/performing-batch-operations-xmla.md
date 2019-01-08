---
title: 執行批次作業 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c451d13016915c9218efb2963429f8f5a7709e2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544226"
---
# <a name="performing-batch-operations-xmla"></a>執行批次作業 (XMLA)
  您可以使用[批次](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)XML for Analysis (XMLA) 使用來執行多個 XMLA 命令的單一 XMLA 命令[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法。 您可以執行多個命令中包含**批次**命令當做單一交易或在個別的交易，每個命令，以序列或平行。 您也可以指定程式碼外部繫結和其他屬性**批次**命令，以處理多個[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件。  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>執行交易式與非交易式批次命令  
 **批次**兩種方式之一執行命令：  
  
 **異動**  
 如果**交易**屬性**批次**命令會設定為 true 時，**批次**命令執行命令的命令所包含的所有**批次**命令在交易內的單一*異動*批次。  
  
 如果交易式批次中有任何命令失敗[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]回復任何命令**批次**失敗命令前執行的命令並**批次**命令會立即結束。 中的任何命令**批次**尚未執行的命令不會執行。 在後**批次**命令結束，**批次**命令會報告失敗的命令發生任何錯誤。  
  
 **非交易式**  
 如果**交易**屬性設為 false，**批次**命令會執行所包含的每個命令**批次**命令在交易內的個別*非交易式*批次。 如果非交易式批次中有任何命令失敗**批次**命令會繼續執行命令之後失敗的命令。 在後**批次**命令會嘗試執行的所有命令，**批次**命令包含，**批次**命令會報告發生任何錯誤。  
  
 中的命令所傳回的所有結果**批次**命令會傳回中所含的命令的順序相同**批次**命令。 所傳回的結果**批次**命令異**批次**命令是交易式或非交易式。  
  
> [!NOTE]  
>  如果**批次**命令包含不會傳回輸出，例如命令[鎖定](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)命令，以及該命令成功執行，**批次**命令會傳回空的[根](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla)結果項目內的項目。 空**根**項目可確保包含在每個命令**批次**命令，可與適當比對**根**該命令結果的項目。  
  
### <a name="returning-results-from-transactional-batch-results"></a>從交易式批次結果傳回結果  
 交易式批次內執行的命令的結果不會傳回必須等到整個**批次**命令完成。 結果不會傳回每個命令會執行，因為任何命令失敗，交易式批次內導致整個之後**批次**命令，並回復所含的命令。 如果所有的命令會啟動並執行成功，[會傳回](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/return-element-xmla)項目[ExecuteResponse](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects-executeresponse)所傳回的項目**Execute**方法**批次**命令包含一個[結果](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/results-element-xmla)元素，其包含一個**根**中所含的每個成功執行命令的項目**批次**命令。 如果任何命令中**批次**命令無法啟動，或是無法完成， **Execute**方法會傳回 SOAP 錯誤**批次**命令，其中包含的錯誤失敗的命令。  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>從非交易式批次結果傳回結果  
 從非交易式批次內執行的命令的結果會傳回內所含的命令順序**批次**命令和每個命令所傳回。 如果包含在任何命令**批次**命令可以成功啟動， **Execute**方法會傳回包含錯誤的 SOAP 錯誤**批次**命令。 如果至少一個命令已順利啟動，**會傳回**項目**ExecuteResponse**所傳回的項目**Execute**方法**批次**命令包含一個**結果**元素，其包含一個**根**每個命令中所包含的項目**批次**命令. 如果非交易式批次中的一個或多個命令無法啟動，或是無法完成，**根**該失敗命令的項目包含[錯誤](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla)描述錯誤的項目。  
  
> [!NOTE]  
>  只要至少一個非交易式批次中的命令可以啟動，非交易式批次會被視為已成功執行，即使在非交易式批次中所含的每個命令的結果中傳回錯誤**批次**命令。  
  
## <a name="using-serial-and-parallel-execution"></a>使用序列和平行執行  
 您可以使用**批次**命令來執行包含命令序列或平行方式。 下一個命令會以序列方式執行命令時已納入**批次**命令無法開始直到目前執行的命令，在**批次**命令完成。 當以平行方式執行命令時，可以同時執行多個命令**批次**命令。  
  
 若要以平行方式執行命令，您可以新增要以平行方式執行的命令[平行](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/parallel-element-xmla)屬性**批次**命令。 目前，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]可以只能在執行連續且循序[程序](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)平行的命令。 任何其他 XMLA 命令，例如[Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)或是[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)，包含在**平行**屬性以序列方式執行。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 嘗試執行所有**程序**命令中包含**平行**屬性以平行方式，但是無法保證所有包含**程序**命令可以平行執行。 執行個體會分析每個**程序**命令，而如果執行個體判斷無法執行命令，以平行方式**程序**命令以序列方式執行。  
  
> [!NOTE]  
>  若要以平行方式執行命令**交易**屬性**批次**命令必須設定為 true，因為[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]支援只有一個作用中的交易，每個連線和非交易式在個別交易中執行每個命令的批次。 如果您納入**平行**非交易式批次中的屬性，則會發生錯誤。  
  
### <a name="limiting-parallel-execution"></a>限制平行執行  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體會嘗試執行多個**程序**命令以平行方式盡可能，到執行個體執行所在之電腦的上限。 您可以限制的並行執行數目**程序**藉由設定命令**maxParallel**屬性**平行**屬性值，指出最大數目**程序**可以平行執行的命令。  
  
 例如，**平行**屬性包含所列出的順序中的下列命令：  
  
1.  **建立**  
  
2.  **處理**  
  
3.  **Alter**  
  
4.  **處理**  
  
5.  **處理**  
  
6.  **處理**  
  
7.  **刪除**  
  
8.  **處理**  
  
9. **處理**  
  
 **MaxParalle**l 屬性**平行**屬性設為 2。 因此，執行個體會依照下列清單執行上列命令：  
  
-   因為命令 1 是以序列方式執行命令 1 **Create**命令，而且只有**程序**命令可以平行執行。  
  
-   命令 1 完成後，會以序列方式執行命令 2。  
  
-   命令 3 會命令 2 完成之後序列執行。  
  
-   3 命令完成之後平行執行命令 4 和 5。 雖然命令 6 也**程序**命令，命令 6 無法執行與命令 4 和 5，因為**maxParallel**屬性設為 2。  
  
-   命令 6 會在命令 4 和 5 完成之後序列執行。  
  
-   命令 7 會在命令 6 完成之後序列執行。  
  
-   命令 8 與 9 會在命令 7 完成之後平行執行。  
  
## <a name="using-the-batch-command-to-process-objects"></a>使用 Batch 命令處理物件  
 **批次**命令中包含數個選擇性的屬性和特別將其加入來支援的屬性處理多個[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案：  
  
-   **ProcessAffectedObjects**屬性**批次**命令會指示執行個體是否應該也處理需要重新處理的任何物件**程序**命令中包含**批次**命令處理指定的物件。  
  
-   [繫結](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla)屬性包含的所有項目使用的程式碼外部繫結集合**程序**中的命令**批次**命令。  
  
-   [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasource-element-xmla)屬性包含所有使用的資料來源的程式碼外部繫結**程序**中的命令**批次**命令。  
  
-   [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla)屬性包含所有使用的資料來源檢視的程式碼外部繫結**程序**中的命令**批次**命令。  
  
-   [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla)屬性中指定的方式**批次**命令會處理所有發生的錯誤**程序**中所包含的命令**批次**命令。  
  
    > [!IMPORTANT]  
    >  A**程序**不能包含命令**繫結**， **DataSource**， **DataSourceView**，或**ErrorConfiguration**屬性，如果**程序**命令會包含於**批次**命令。 如果您必須指定這些屬性，如**程序**命令，提供必要的資訊中的對應屬性**批次**命令，以包含**程序**命令。  
  
## <a name="see-also"></a>另請參閱  
 [批次項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)   
 [處理項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)   
 [處理多維度模型 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [在 Analysis Services 中使用 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
