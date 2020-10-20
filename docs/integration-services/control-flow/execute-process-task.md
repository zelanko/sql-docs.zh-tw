---
description: 執行處理工作
title: 執行處理工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executeprocesstask.f1
- sql13.dts.designer.executeprocesstask.general.f1
- sql13.dts.designer.executeprocesstask.process.f1
helpviewer_keywords:
- Execute Process task [Integration Services]
ms.assetid: aca5a0b5-34a9-45bc-a234-8e63ea51a1ee
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b19a591448da6e14c6275462ba6cb5ae595092a0
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92197209"
---
# <a name="execute-process-task"></a>執行處理工作

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  「執行處理」工作會隨 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件工作流程來執行應用程式或批次檔。 雖然可以使用「執行處理」工作來開啟任何標準應用程式，例如 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 或 [!INCLUDE[ofprword](../../includes/ofprword-md.md)]，但通常您會使用它來執行處理資料來源的商業應用程式或批次檔。 例如，您可以使用「執行處理」工作展開壓縮的文字檔。 然後封裝就可以使用文字檔做為封裝中資料流程的資料來源。 另一項範例為：您可以使用「執行處理」工作來執行產生每日銷售報表的自訂 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 應用程式。 接著，您就可將報告附加至「傳送郵件」工作，並將報告轉寄到通訊群組清單。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含執行工作流程作業的其他工作，例如執行封裝。 如需詳細資訊，請參閱 [執行封裝工作](../../integration-services/control-flow/execute-package-task.md)  
  
## <a name="custom-log-entries-available-on-the-execute-process-task"></a>執行處理工作上可用的自訂記錄項目  
 下表列出「執行處理」工作的自訂記錄項目。 如需詳細資訊，請參閱 [集成服務 &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|提供將工作設定為執行之相關的程序資訊。<br /><br /> 將會寫入兩個記錄項目。 其中一個包含工作所執行之可執行檔的名稱和位置的相關資訊，另一個項目則記錄可執行檔的結束。|  
|**ExecuteProcessVariableRouting**|提供有關哪些變數會傳到可執行檔之輸入和輸出的相關資訊。 將會寫入 stdin (輸入)、stdout (輸出) 和 stderr (錯誤輸出) 的記錄項目。|  
  
## <a name="configuration-of-the-execute-process-task"></a>執行處理工作的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
### <a name="property-settings"></a>屬性設定  
 當「執行處理」工作執行自訂應用程式時，此工作會透過下列一個或兩個方法提供輸入給應用程式：  
  
-   您在 [StandardInputVariable]  屬性設定中指定的變數。 如需變數的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[在封裝中使用變數](../integration-services-ssis-variables.md)。  
  
-   您在 **Arguments** 屬性設定中指定的引數。 (例如，如果工作使用 Word 開啟文件，則引數可能命名為 .doc 檔)。  
  
 若要在一個「執行處理」工作中將多個引數傳遞到自訂應用程式，請使用空格來分隔引數。 引數不得包含空格，否則此工作將無法執行。 您可以使用運算式以引數的方式傳遞變數值。 在下列範例中，運算式會以引數的方式傳遞兩個變數值，並使用空格來分隔引數：  
  
 `@variable1 + " " + @variable2`  
  
 您可以使用運算式來設定各種「執行處理」工作屬性。  
  
 當您使用 **StandardInputVariable** 屬性設定「執行處理」工作來提供輸入時，請從應用程式呼叫 **Console.ReadLine** 方法來讀取輸入。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 類別庫中的 [Console.ReadLine 方法](/dotnet/api/system.console.readline)主題。  
  
 當您使用 **Arguments** 屬性設定「執行處理」工作來提供輸入時，請執行下列其中一個步驟來取得引數：  
  
-   如果您使用 Microsoft Visual Basic 撰寫應用程式，請設定 **My.Application.CommandLineArgs** 屬性。 下列範例設定 **My.Application.CommandLineArgs** 屬性來擷取兩個引數：  
  
    ```vb  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     如需詳細資訊，請參閱 [參考中的](https://go.microsoft.com/fwlink/?LinkId=129200)My.Application.CommandLineArgs 屬性 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 主題。  
  
-   如果您使用 Microsoft Visual C# 撰寫應用程式，請使用 **Main** 方法。  
  
     如需詳細資訊，請參閱《C# 程式設計手冊》中的 [命令列引數 (C# 程式設計手冊)](/dotnet/csharp/programming-guide/main-and-command-args/command-line-arguments)主題。  
  
 「執行處理」工作也包含 **StandardOutputVariable** 和 **StandardErrorVariable** 屬性，分別用來指定使用應用程式的標準輸出和錯誤輸出。  
  
 此外，您可以設定讓「執行處理」工作指定工作目錄、逾時期限，或表示可執行檔成功執行的值。 如果可執行檔的傳回碼與表示成功的值不符，或在指定的位置找不到可執行檔，亦可將此工作設定為失敗。  
  
## <a name="programmatic-configuration-of-the-execute-process-task"></a>執行處理工作的程式設計組態  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## <a name="execute-process-task-editor-general-page"></a>執行處理工作編輯器 (一般頁面)
  使用 [執行處理工作編輯器]  對話方塊的 [一般]  頁面，來命名和描述執行處理工作。  
  
### <a name="options"></a>選項。  
 **名稱**  
 為執行處理工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入執行處理工作的描述。  
  
## <a name="execute-process-task-editor-process-page"></a>執行處理工作編輯器 (處理頁面)
  使用 **[執行處理工作編輯器]** 對話方塊的 **[處理]** 頁面，即可設定執行處理的選項。 這些選項包括要執行的可執行檔、其位置、命令提示字元引數，以及提供輸入和擷取輸出的變數。  
  
### <a name="options"></a>選項。  
 **RequireFullFileName**  
 指出如果在指定位置找不到可執行檔時，工作是否失敗。  
  
 **可執行檔**  
 輸入要執行的可執行檔名稱。  
  
 **引數**  
 提供命令提示字元引數。  
  
 **WorkingDirectory**  
 鍵入包含可執行檔的資料夾路徑，或按一下瀏覽按鈕 **(...)** 並尋找資料夾。  
  
 **StandardInputVariable**  
 選取變數來提供處理序的輸入，或按一下 [\<**New variable...**>] 以建立新的變數：  
  
 **相關主題：** [新增變數](../integration-services-ssis-variables.md)  
  
 **StandardOutputVariable**  
 選取變數來擷取處理序的輸出，或按一下 [\<**New variable...**>] 以建立新的變數。  
  
 **StandardErrorVariable**  
 選取變數來擷取處理器的錯誤輸出，或按一下 [\<**New variable...**>] 以建立新的變數。  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 指出如果處理序的結束碼和 **SuccessValue**中指定的值不同時，工作是否失敗。  
  
 **SuccessValue**  
 指定可執行檔要表示成功時將傳回的值。 依預設，此值設定為 **0**。  
  
 **TimeOut**  
 指定處理序可以執行的秒數。 若值為 **0** ，表示不使用逾時值，則處理序會一直執行到完成或發生錯誤為止。  
  
 **TerminateProcessAfterTimeOut**  
 指出是否要在 **TimeOut** 選項指定的逾時期限之後，強制結束處理序。 只有在 **TimeOut** 不是 **0**時，才可以使用此選項。  
  
 **WindowStyle**  
 指定用來執行處理序的視窗樣式。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [控制流程](../../integration-services/control-flow/control-flow.md)  
  
