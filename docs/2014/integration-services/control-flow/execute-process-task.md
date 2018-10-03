---
title: 執行處理工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executeprocesstask.f1
helpviewer_keywords:
- Execute Process task [Integration Services]
ms.assetid: aca5a0b5-34a9-45bc-a234-8e63ea51a1ee
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 02f00d9846176edabb2da486906b5d1946c94124
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205618"
---
# <a name="execute-process-task"></a>執行處理工作
  「執行處理」工作會隨 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝工作流程執行應用程式或批次檔。 雖然可以使用「執行處理」工作來開啟任何標準應用程式，例如 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 或 [!INCLUDE[ofprword](../../includes/ofprword-md.md)]，但通常您會使用它來執行處理資料來源的商業應用程式或批次檔。 例如，您可以使用「執行處理」工作展開壓縮的文字檔。 然後封裝就可以使用文字檔做為封裝中資料流程的資料來源。 另一項範例為：您可以使用「執行處理」工作來執行產生每日銷售報表的自訂 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 應用程式。 接著，您就可將報告附加至「傳送郵件」工作，並將報告轉寄到通訊群組清單。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含執行工作流程作業的其他工作，例如執行封裝。 如需詳細資訊，請參閱 [執行封裝工作](execute-package-task.md)  
  
## <a name="custom-log-entries-available-on-the-execute-process-task"></a>執行處理工作上可用的自訂記錄項目  
 下表列出「執行處理」工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)和[自訂訊息以進行記錄](../custom-messages-for-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`ExecuteProcessExecutingProcess`|提供將工作設定為執行之相關的程序資訊。<br /><br /> 將會寫入兩個記錄項目。 其中一個包含工作所執行之可執行檔的名稱和位置的相關資訊，另一個項目則記錄可執行檔的結束。|  
|`ExecuteProcessVariableRouting`|提供有關哪些變數會傳到可執行檔之輸入和輸出的相關資訊。 將會寫入 stdin (輸入)、stdout (輸出) 和 stderr (錯誤輸出) 的記錄項目。|  
  
## <a name="configuration-of-the-execute-process-task"></a>執行處理工作的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [執行處理工作編輯器&#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [執行處理工作編輯器&#40;處理頁面&#41;](../execute-process-task-editor-process-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="property-settings"></a>屬性設定  
 當「執行處理」工作執行自訂應用程式時，此工作會透過下列一個或兩個方法提供輸入給應用程式：  
  
-   您在 [StandardInputVariable] 屬性設定中指定的變數。 如需變數的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)和[在封裝中使用變數](../use-variables-in-packages.md)。  
  
-   您在 **Arguments** 屬性設定中指定的引數。 (例如，如果工作使用 Word 開啟文件，則引數可能命名為 .doc 檔)。  
  
 若要在一個「執行處理」工作中將多個引數傳遞到自訂應用程式，請使用空格來分隔引數。 引數不得包含空格，否則此工作將無法執行。 您可以使用運算式以引數的方式傳遞變數值。 在下列範例中，運算式會以引數的方式傳遞兩個變數值，並使用空格來分隔引數：  
  
 `@variable1 + " " + @variable2`  
  
 您可以使用運算式來設定各種「執行處理」工作屬性。  
  
 當您使用 **[standardinputvariable]** 屬性來設定 「 執行處理工作，來提供輸入時，呼叫`Console.ReadLine`從應用程式來讀取輸入的方法。 如需詳細資訊，請參閱 [Console.ReadLine 方法](http://go.microsoft.com/fwlink/?LinkId=129201)類別庫中的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Class Library.  
  
 當您使用 **Arguments** 屬性設定「執行處理」工作來提供輸入時，請執行下列其中一個步驟來取得引數：  
  
-   如果您使用 Microsoft Visual Basic 撰寫應用程式時，請設定`My.Application.CommandLineArgs`屬性。 下列範例設定 `My.Application.CommandLineArgs` 屬性來擷取兩個引數：  
  
    ```  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     如需詳細資訊，請參閱 [參考中的](http://go.microsoft.com/fwlink/?LinkId=129200)My.Application.CommandLineArgs 屬性 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 主題。  
  
-   如果您使用 Microsoft Visual C# 撰寫應用程式，請使用 `Main` 方法。  
  
     如需詳細資訊，請參閱《C# 程式設計手冊》中的 [命令列引數 (C# 程式設計手冊)](http://go.microsoft.com/fwlink/?LinkId=129406)主題。  
  
 「執行處理」工作也包含 **StandardOutputVariable** 和 **StandardErrorVariable** 屬性，分別用來指定使用應用程式的標準輸出和錯誤輸出。  
  
 此外，您可以設定讓「執行處理」工作指定工作目錄、逾時期限，或表示可執行檔成功執行的值。 如果可執行檔的傳回碼與表示成功的值不符，或在指定的位置找不到可執行檔，亦可將此工作設定為失敗。  
  
## <a name="programmatic-configuration-of-the-execute-process-task"></a>執行處理工作的程式設計組態  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](integration-services-tasks.md)   
 [控制流程](control-flow.md)  
  
  
