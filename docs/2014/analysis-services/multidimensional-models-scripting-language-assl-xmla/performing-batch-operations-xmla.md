---
title: 執行批次作業 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 186d5a0896814544f34531fe98ad88c8034ac63a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304588"
---
# <a name="performing-batch-operations-xmla"></a>執行批次作業 (XMLA)
  您可以使用[批次](../xmla/xml-elements-commands/batch-element-xmla.md)XML for Analysis (XMLA) 使用來執行多個 XMLA 命令的單一 XMLA 命令[Execute](../xmla/xml-elements-methods-execute.md)方法。 您可以用單一交易或每個命令的個別交易，以序列或平行方式執行 `Batch` 命令中包含的多個命令。 您也可以指定程式碼外部繫結和其他屬性`Batch`命令，以處理多個[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件。  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>執行交易式與非交易式批次命令  
 `Batch` 命令使用下列兩種方式之一來執行命令：  
  
 **異動**  
 如果`Transaction`的屬性`Batch`命令設定為 true，`Batch`命令執行命令的命令所包含的所有`Batch`命令在單一交易中 —*異動*批次。  
  
 如果交易式批次中有任何命令失敗[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]回復任何命令`Batch`失敗命令前執行的命令和`Batch`命令會立即結束。 `Batch` 命令中尚未執行的任何命令都不會被執行。 在 `Batch` 命令結束之後，`Batch` 命令會報告因為失敗的命令而發生的任何錯誤。  
  
 **非交易式**  
 如果`Transaction`屬性設為 false，`Batch`命令執行所包含的每個命令`Batch`在不同的交易命令 —*非交易式*批次。 如果非交易式批次中有任何命令失敗，`Batch` 命令會繼續執行失敗命令之後的命令。 在 `Batch` 命令嘗試執行 `Batch` 命令包含的所有命令之後，`Batch` 命令會報告所發生的任何錯誤。  
  
 所有由包含在 `Batch` 命令中的命令傳回的結果，都會按照 `Batch` 命令所含命令的相同順序來傳回。 `Batch` 命令傳回的結果，會因 `Batch` 命令是交易式或非交易式而異。  
  
> [!NOTE]  
>  如果`Batch`命令包含不會傳回輸出，例如命令[鎖定](../xmla/xml-elements-commands/lock-element-xmla.md)命令，以及該命令成功執行，`Batch`命令會傳回空白[根](../xmla/xml-elements-properties/root-element-xmla.md)項目在結果項目。 空的 `root` 元素可確保 `Batch` 命令中所含的每個命令，可與該命令結果的適當 `root` 元素相符。  
  
### <a name="returning-results-from-transactional-batch-results"></a>從交易式批次結果傳回結果  
 在交易式批次內執行的命令之結果，必須等到整個 `Batch` 命令完成後才會傳回。 不在每個命令執行後便傳回結果，是因為交易式批次中任何失敗的命令，都會造成回復整個 `Batch` 命令及所含的命令。 如果所有的命令會啟動並執行成功，[會傳回](../xmla/xml-elements-properties/return-element-xmla.md)項目[ExecuteResponse](../xmla/xml-elements-objects-executeresponse.md)所傳回的項目`Execute`方法`Batch`命令包含一個[結果](../xmla/xml-elements-properties/results-element-xmla.md)元素，其包含一個`root`中所含的每個成功執行命令的項目`Batch`命令。 如果 `Batch` 命令中有任何命令無法啟動或是無法完成，`Execute` 方法會傳回 `Batch` 命令的 SOAP 錯誤，其中包含失敗命令的錯誤。  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>從非交易式批次結果傳回結果  
 在非交易式批次內執行的命令之結果，會在每個命令傳回結果時，按照 `Batch` 命令中所含的命令順序來傳回。 如果無法成功啟動 `Batch` 命令中所含的任何命令，`Execute` 方法會傳回 SOAP 錯誤，其中包含 `Batch` 命令的錯誤。 如果至少成功啟動一個命令，則 `return` 命令的 `ExecuteResponse` 方法所傳回之 `Execute` 元素的 `Batch` 元素，會包含一個 `results` 元素，而其中會為 `root` 命令所含的每個命令，各包含一個 `Batch` 元素。 如果非交易式批次中的一個或多個命令無法啟動，或是無法完成，`root`該失敗命令的項目包含[錯誤](../xmla/xml-elements-properties/error-element-xmla.md)描述錯誤的項目。  
  
> [!NOTE]  
>  只要在非交易式批次中至少有一個命令可以啟動，便會將非交易式批次視為已成功執行，即使在非交易式批次中所含的每個命令，都在 `Batch` 命令的結果中傳回錯誤，亦然。  
  
## <a name="using-serial-and-parallel-execution"></a>使用序列和平行執行  
 您可以使用 `Batch` 命令，以序列或平行方式，執行包含的命令。 以序列方式執行命令時，`Batch` 命令中所含的下一個命令必須等到 `Batch` 命令中目前執行的命令完成時才能啟動。 以平行方式執行命令時，`Batch` 命令可以同時執行多個命令。  
  
 若要以平行方式執行命令，您可以新增要以平行方式執行的命令[平行](../xmla/xml-elements-properties/parallel-element-xmla.md)屬性`Batch`命令。 目前，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]可以只能在執行連續且循序[程序](../xmla/xml-elements-commands/process-element-xmla.md)平行的命令。 任何其他 XMLA 命令，例如[Create](../xmla/xml-elements-commands/create-element-xmla.md)或是[Alter](../xmla/xml-elements-commands/alter-element-xmla.md)，包含在`Parallel`屬性以序列方式執行。  
  
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
  
-   命令 1 完成後，會以序列方式執行命令 2。  
  
-   命令 3 會命令 2 完成之後序列執行。  
  
-   3 命令完成之後平行執行命令 4 和 5。 雖然命令 6 也是 `Process` 命令，不過，命令 6 無法與命令 4 和 5 一起平行執行，因為 `maxParallel` 屬性是設定為 2。  
  
-   命令 6 會在命令 4 和 5 完成之後序列執行。  
  
-   命令 7 會在命令 6 完成之後序列執行。  
  
-   命令 8 與 9 會在命令 7 完成之後平行執行。  
  
## <a name="using-the-batch-command-to-process-objects"></a>使用 Batch 命令處理物件  
 `Batch` 命令特別包含一些選擇性的屬性 (Property) 與屬性 (Attribute)，以支援處理多個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案：  
  
-   `ProcessAffectedObjects` 命令的 `Batch` 屬性指出執行個體是否要在 `Process` 命令中的 `Batch` 命令處理指定的物件之後，也處理需要重新處理的物件。  
  
-   [繫結](../xmla/xml-elements-properties/bindings-element-xmla.md)屬性包含的所有項目使用的程式碼外部繫結集合`Process`中的命令`Batch`命令。  
  
-   [DataSource](../xmla/xml-elements-properties/source-element-xmla.md)屬性包含所有使用的資料來源的程式碼外部繫結`Process`中的命令`Batch`命令。  
  
-   [DataSourceView](../xmla/xml-elements-properties/datasourceview-element-xmla.md)屬性包含所有使用的資料來源檢視的程式碼外部繫結`Process`中的命令`Batch`命令。  
  
-   [ErrorConfiguration](../xmla/xml-elements-properties/errorconfiguration-element-xmla.md)屬性中指定的方式`Batch`命令會處理所有發生的錯誤`Process`中所包含的命令`Batch`命令。  
  
    > [!IMPORTANT]  
    >  如果 `Process` 命令是包含在 `Bindings` 命令中，則 `DataSource` 命令無法包括 `DataSourceView`、`ErrorConfiguration`、`Process` 或 `Batch` 屬性。 如果您必須為 `Process` 命令指定這些屬性，請在包含 `Batch` 命令的 `Process` 命令的對應屬性中提供必要的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [批次項目&#40;XMLA&#41;](../xmla/xml-elements-commands/batch-element-xmla.md)   
 [處理項目&#40;XMLA&#41;](../xmla/xml-elements-commands/process-element-xmla.md)   
 [多維度模型物件處理](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
