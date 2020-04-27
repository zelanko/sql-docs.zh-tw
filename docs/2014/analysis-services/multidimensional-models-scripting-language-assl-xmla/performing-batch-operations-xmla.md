---
title: 執行批次作業（XMLA） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- multiple projects
- XML for Analysis, batches
- parallel batch execution [XMLA]
- transactional batches
- serial batch execution [XMLA]
- XMLA, batches
- batches [XML for Analysis]
- nontransactional batches
ms.assetid: 731c70e5-ed51-46de-bb69-cbf5aea18dda
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bd661506dbb792eb55194c61d7284d619e63a5f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62702067"
---
# <a name="performing-batch-operations-xmla"></a>執行批次作業 (XMLA)
  您可以使用 XML for Analysis （XMLA）中的[批次](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)命令，使用單一 xmla [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法來執行多個 xmla 命令。 您可以用單一交易或每個命令的個別交易，以序列或平行方式執行 `Batch` 命令中包含的多個命令。 您也可以`Batch`在命令中指定非正規系結和其他屬性來處理多個[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件。  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>執行交易式與非交易式批次命令  
 `Batch` 命令使用下列兩種方式之一來執行命令：  
  
 **交易式**  
 `Transaction`如果`Batch`命令的屬性設定為 true，則`Batch`命令會在單一交易中執行命令所包含`Batch`的所有命令-交易式批次。 *transactional*  
  
 如果交易式批次中有任何命令[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]失敗，則會回復命令`Batch`中執行失敗的命令之前的任何命令， `Batch`而且命令會立即結束。 `Batch` 命令中尚未執行的任何命令都不會被執行。 在 `Batch` 命令結束之後，`Batch` 命令會報告因為失敗的命令而發生的任何錯誤。  
  
 **非交易式**  
 如果`Transaction`屬性設定為 false，此`Batch`命令會在個別的交易中執行`Batch`命令所包含的每個命令-*非*交易式批次。 如果非交易式批次中有任何命令失敗，`Batch` 命令會繼續執行失敗命令之後的命令。 在 `Batch` 命令嘗試執行 `Batch` 命令包含的所有命令之後，`Batch` 命令會報告所發生的任何錯誤。  
  
 所有由包含在 `Batch` 命令中的命令傳回的結果，都會按照 `Batch` 命令所含命令的相同順序來傳回。 `Batch` 命令傳回的結果，會因 `Batch` 命令是交易式或非交易式而異。  
  
> [!NOTE]  
>  如果`Batch`命令包含不會傳回輸出的命令（例如[Lock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)命令），且該命令已成功執行，則`Batch`命令會在 results 元素中傳回空的[根](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla)元素。 空的 `root` 元素可確保 `Batch` 命令中所含的每個命令，可與該命令結果的適當 `root` 元素相符。  
  
### <a name="returning-results-from-transactional-batch-results"></a>從交易式批次結果傳回結果  
 在交易式批次內執行的命令之結果，必須等到整個 `Batch` 命令完成後才會傳回。 不在每個命令執行後便傳回結果，是因為交易式批次中任何失敗的命令，都會造成回復整個 `Batch` 命令及所含的命令。 如果所有命令都啟動並順利執行，則`Execute` `Batch`命令的方法所傳回之[ExecuteResponse](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects-executeresponse)元素的[return](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/return-element-xmla)元素會包含一個[results](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/results-element-xmla)元素，而此專案會針對`root` `Batch`命令中包含的每個成功執行命令，各包含一個元素。 如果 `Batch` 命令中有任何命令無法啟動或是無法完成，`Execute` 方法會傳回 `Batch` 命令的 SOAP 錯誤，其中包含失敗命令的錯誤。  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>從非交易式批次結果傳回結果  
 在非交易式批次內執行的命令之結果，會在每個命令傳回結果時，按照 `Batch` 命令中所含的命令順序來傳回。 如果無法成功啟動 `Batch` 命令中所含的任何命令，`Execute` 方法會傳回 SOAP 錯誤，其中包含 `Batch` 命令的錯誤。 如果至少成功啟動一個命令，則 `return` 命令的 `ExecuteResponse` 方法所傳回之 `Execute` 元素的 `Batch` 元素，會包含一個 `results` 元素，而其中會為 `root` 命令所含的每個命令，各包含一個 `Batch` 元素。 如果非交易式批次中的一個或多個命令無法啟動或無法完成`root` ，則該失敗命令的元素會包含描述錯誤的[錯誤](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla)元素。  
  
> [!NOTE]  
>  只要在非交易式批次中至少有一個命令可以啟動，便會將非交易式批次視為已成功執行，即使在非交易式批次中所含的每個命令，都在 `Batch` 命令的結果中傳回錯誤，亦然。  
  
## <a name="using-serial-and-parallel-execution"></a>使用序列和平行執行  
 您可以使用 `Batch` 命令，以序列或平行方式，執行包含的命令。 以序列方式執行命令時，`Batch` 命令中所含的下一個命令必須等到 `Batch` 命令中目前執行的命令完成時才能啟動。 以平行方式執行命令時，`Batch` 命令可以同時執行多個命令。  
  
 若要以平行方式執行命令，請將要平行執行的命令加入至[Parallel](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/parallel-element-xmla) `Batch`命令的 parallel 屬性。 目前， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]只能平行執行連續的連續[進程](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)命令。 包含在屬性中的`Parallel`任何其他 XMLA 命令（例如[Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)或[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)）都會以序列循序執行。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會嘗試平行執行所有包含在 `Process` 屬性中的 `Parallel` 命令，但是無法保證所有包含的 `Process` 命令都可以平行執行。 執行個體會分析每個 `Process` 命令，而且如果執行個體判斷無法平行執行命令，就會序列執行 `Process` 命令。  
  
> [!NOTE]  
>  若要平行執行命令，必須將 `Transaction` 命令的 `Batch` 屬性設定成 True，因為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 僅支援每個連接有一個使用中交易，而且非交易式批次會在個別交易中執行每個命令。 如果您在非交易式批次中包含 `Parallel` 屬性，就會發生錯誤。  
  
### <a name="limiting-parallel-execution"></a>限制平行執行  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會嘗試盡量平行執行 `Process` 命令，最多可達執行個體執行的電腦限制。 您可以將 `Process` 屬性 (Property) 的 `maxParallel` 屬性 (Attribute)，設定為可以平行執行之 `Parallel` 命令的上限，以限制並行執行的 `Process` 命令數目。  
  
 例如，`Parallel` 屬性依序包含下列命令：  
  
1.  `Create`  
  
2.  `Process`  
  
3.  `Alter`  
  
4.  `Process`  
  
5.  `Process`  
  
6.  `Process`  
  
7.  `Delete`  
  
8.  `Process`  
  
9. `Process`  
  
 此 `maxParalle` 屬性 (Property) 的 `Parallel`l 屬性 (Attribute) 是設定為 2。 因此，執行個體會依照下列清單執行上列命令：  
  
-   命令 1 會序列執行，因為命令 1 是 `Create` 命令，而且只有 `Process` 命令可以平行執行。  
  
-   命令2會在命令1完成後循序執行。  
  
-   命令3會在命令2完成後循序執行。  
  
-   命令4和5會在命令3完成後平行執行。 雖然命令 6 也是 `Process` 命令，不過，命令 6 無法與命令 4 和 5 一起平行執行，因為 `maxParallel` 屬性是設定為 2。  
  
-   命令 6 會在命令 4 和 5 完成之後序列執行。  
  
-   命令 7 會在命令 6 完成之後序列執行。  
  
-   命令 8 與 9 會在命令 7 完成之後平行執行。  
  
## <a name="using-the-batch-command-to-process-objects"></a>使用 Batch 命令處理物件  
 `Batch` 命令特別包含一些選擇性的屬性 (Property) 與屬性 (Attribute)，以支援處理多個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案：  
  
-   `ProcessAffectedObjects` 命令的 `Batch` 屬性指出執行個體是否要在 `Process` 命令中的 `Batch` 命令處理指定的物件之後，也處理需要重新處理的物件。  
  
-   [系結] 屬性包含`Process` `Batch`命令中所有[命令所使用](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla)之非正規系結的集合。  
  
-   [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)屬性包含`Process` `Batch`命令中所有命令所使用之資料來源的非正規系結。  
  
-   [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla)屬性包含`Process` `Batch`命令中所有命令所使用之資料來源視圖的非正規系結。  
  
-   [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla)屬性會指定`Batch`命令處理`Process` `Batch`命令中包含的所有命令所遇到之錯誤的方式。  
  
    > [!IMPORTANT]  
    >  如果 `Process` 命令是包含在 `Bindings` 命令中，則 `DataSource` 命令無法包括 `DataSourceView`、`ErrorConfiguration`、`Process` 或 `Batch` 屬性。 如果您必須為 `Process` 命令指定這些屬性，請在包含 `Batch` 命令的 `Process` 命令的對應屬性中提供必要的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;XMLA&#41;的批次元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)   
 [XMLA&#41;的 Process 元素 &#40;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)   
 [多維度模型物件處理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
