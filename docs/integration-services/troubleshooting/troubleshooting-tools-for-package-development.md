---
title: 套件開發的疑難排解工具 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: 41dd248c-dab3-4318-b8ba-789a42d5c00c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 7eef65de8d840961c57de89102a495d2cc374962
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126626"
---
# <a name="troubleshooting-tools-for-package-development"></a>疑難排解封裝開發的工具

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中開發封裝時可以用於疑難排解封裝的功能和工具。  
  
## <a name="troubleshooting-design-time-validation-issues"></a>疑難排解設計階段驗證問題  
 在最新版的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中開啟封裝時，系統會先驗證所有連線，然後才驗證所有資料流程元件，並將緩慢或無法使用的所有連線設為離線工作。 這有助於減少驗證封裝資料流程的延遲。  
  
 開啟封裝之後，您也可以以滑鼠右鍵按一下 [連接管理員]  區域中的連接管理員，然後按一下 [離線工作]  來關閉連接。 這可以在 SSIS 設計師中加快作業。  
  
 已設為離線工作的連接將保持離線狀態，直到您執行下列其中一項作業為止：  
  
-   以滑鼠右鍵按一下 SSIS 設計師之 [連接管理員]  區域中的連接管理員，然後按一下 [測試連接性]  來測試連接。  
  
     例如，開啟封裝之後，一開始會將連線設為離線工作。 您要修改連接字串來解決問題，然後按一下 **[測試連接性]** 來測試連線。  
  
-   重新開啟封裝或重新開啟包含封裝的專案。 在封裝的所有連線中會再次執行驗證。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含以下額外的功能，以協助您避免驗證錯誤：  
  
-   **無法使用資料來源時，將所有封裝和所有連線設為離線工作**。 您可以從 **[SSIS]** 功能表啟用 **[離線工作]** 。 不同於 **DelayValidation** 屬性，在尚未開啟封裝之前， **[離線工作]** 就已經可供使用。 您也可以啟用 **[離線工作]** 來加速設計師中的作業，並只有在想要驗證封裝時才停用這個功能。  
  
-   **在執行階段前無效的封裝元素上設定 DelayValidation 屬性**。 您可以將封裝元素 (其組態在設計階段無效) 的 **DelayValidation** 設為 **True** ，以避免發生驗證錯誤。 例如，您可能有一項會使用目的地資料表的資料流程工作，而這個目的地資料表卻要等到執行 SQL 工作在執行階段建立資料表後才會存在。 **DelayValidation** 屬性可以在封裝層級啟用，也可以在封裝所包含的個別工作和容器層級啟用。 一般而言，當您部署封裝時，必須讓相同封裝元素上的這個屬性設為 **True** ，以避免在執行階段發生相同的驗證錯誤。  
  
     您可以針對資料流程工作設定 **DelayValidation** 屬性，但無法針對個別資料流程元件設定這個屬性。 將個別資料流程元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> 屬性設為 **false**中開發封裝時可以用於疑難排解封裝的功能和工具。 不過，當這個屬性的值是 **false**時，元件不會察覺對外部資料來源之中繼資料所做的變更。  
  
 如果發生驗證時，此封裝所使用的資料庫物件遭到鎖定，驗證程序可能會停止回應。 在這些情況下， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師也會停止回應。 您可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的關聯工作階段，以便繼續驗證。 您也可以使用本章節所述的設定來避開此問題。  
  
## <a name="troubleshooting-control-flow"></a>疑難排解控制流程  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含下列功能與工具，可以用來在封裝開發期間疑難排解封裝中的控制流程：  
  
-   **設定工作、容器及封裝的中斷點**。 可以使用「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」提供的圖形工具來設定中斷點。 中斷點可以在封裝層級啟用，也可以在封裝包含之個別工作和容器層級啟用。 有些工作和容器會提供設定中斷點的其他中斷條件， 例如，您可以在「For 迴圈」容器上啟用中斷條件，以便在迴圈的每個反覆運算開始時暫停執行。  
  
-   **使用偵錯視窗**。 執行具有中斷點的封裝時， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的偵錯視窗可讓您存取變數值和狀態訊息。  
  
-   **檢視 [進度] 索引標籤上的資訊**。[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」會提供在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 [進度] 索引標籤會以執行順序列出工作和容器，並包含每個工作和容器 (包括封裝本身) 的開始與完成時間、警告及錯誤訊息。  
  
 如需這些功能的詳細資訊，請參閱＜ [Debugging Control Flow](../../integration-services/troubleshooting/debugging-control-flow.md)＞。  
  
## <a name="troubleshooting-data-flow"></a>疑難排解資料流程  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含下列功能與工具，可以用來在封裝開發期間疑難排解封裝中的資料流程：  
  
-   **只使用部分資料進行測試**。 如果只使用資料集的範例來疑難排解封裝中的資料流程，則可以包括「百分比取樣」或「資料列取樣」轉換，以在執行階段建立內嵌資料範例。 如需相關資訊，請參閱 [Percentage Sampling Transformation](../../integration-services/data-flow/transformations/percentage-sampling-transformation.md) 及 [Row Sampling Transformation](../../integration-services/data-flow/transformations/row-sampling-transformation.md)。  
  
-   **使用資料檢視器監看資料在資料流程中的移動**。 資料檢視器會在資料於來源、轉換和目的地之間移動時顯示資料值。 資料檢視器可以在方格中顯示資料。 您可以將資料檢視器中的資料複製到 [剪貼簿] 中，然後將資料貼到檔案或 Excel 試算表中。 如需相關資訊，請參閱 [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md) 中開發封裝時可以用於疑難排解封裝的功能和工具。  
  
-   **設定支援錯誤輸出之資料流程元件中的錯誤輸出**。 許多資料流程來源、轉換和目的地也都支援錯誤輸出。 經由設定資料流程元件的錯誤輸出，可以將有錯誤的資料導向其他目的地； 例如，您可以在另一個文字檔中擷取失敗或被截斷的資料。 您也可以將資料檢視器附加至錯誤輸出，並且只檢查錯誤的資料。 在設計階段，錯誤輸出會擷取有問題的資料值，協助您開發可有效處理實際資料的封裝。 不過，其他疑難排解工具與功能通常都只能用於設計階段，但錯誤輸出即使在實際執行環境中還是很有用。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。  
  
-   **擷取已處理的資料列計數**。 當您在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中執行封裝時，經由路徑傳送的資料列數目會顯示在資料流程設計師中。 隨著資料不斷經由路徑移動，這個數目會定期更新。 您也可以將「資料列計數」轉換加入資料流程，以擷取變數中的最後資料列計數。 如需詳細資訊，請參閱 [Row Count Transformation](../../integration-services/data-flow/transformations/row-count-transformation.md)。  
  
-   **檢視 [進度] 索引標籤上的資訊**。[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」會提供在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 [進度] 索引標籤會以執行順序列出資料流程元件，並包含封裝每個階段的進度資訊 (以完成百分比顯示)，以及包含寫入目的地之資料列數目的資訊。  
  
 如需這些功能的詳細資訊，請參閱＜ [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md)＞。  
  
## <a name="troubleshooting-scripts"></a>疑難排解指令碼  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 是一種開發環境，您會在此環境中撰寫指令碼工作和指令碼元件所使用的指令碼。 VSTA 包含下列功能與工具，可以用來在封裝開發期間針對指令碼進行疑難排解：  
  
-   **在指令碼工作的指令碼中設定中斷點。** VSTA 只針對指令碼工作中的指令碼提供偵錯支援。 在指令碼工作中設定的中斷點會與封裝中設定的中斷點，以及封裝中的工作和容器整合，以便可以對所有的封裝元素進行嚴密的偵錯。  
  
    > [!NOTE]  
    >  當您為包含多個指令碼工作的封裝偵錯時，偵錯工具只會在一個指令碼工作中叫用中斷點，而且將會忽略其他指令碼工作中的中斷點。 如果指令碼工作是 [Foreach 迴圈] 或 [For 迴圈] 容器的一部分，偵錯工具會在迴圈的第一次反覆運算後，忽略指令碼工作中的中斷點。  
  
 如需詳細資訊，請參閱 [Debugging Script](../../integration-services/troubleshooting/debugging-script.md)。 如需如何偵錯指令碼元件的建議，請參閱 [指令碼元件的程式碼撰寫和偵錯](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
## <a name="troubleshooting-errors-without-a-description"></a>疑難排解沒有隨附描述的錯誤  
 如果您在封裝開發期間遇到沒有隨附描述的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤號碼，可以在 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)中找到描述。 此清單這次沒有包含疑難排解資訊。  
  
## <a name="see-also"></a>另請參閱  
 [封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)   
 [Data Flow Performance Features](../../integration-services/data-flow/data-flow-performance-features.md)  
  
  
