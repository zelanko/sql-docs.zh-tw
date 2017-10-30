---
title: "Extending the Package with the Script Task |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- scripts [Integration Services]
- SSIS Script task
- tasks [Integration Services], scripts
- Script task [Integration Services], about Script task
- scripts [Integration Services], about Script task with packages
- SSIS Script task, about Script task
ms.assetid: 911e6d26-a6fd-4fc3-a111-bf5f048e9bff
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b2e0b0a933568f8313cefd2f1d6dbdd02f5d3cbc
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="extending-the-package-with-the-script-task"></a>以指令碼工作擴充封裝
  指令碼工作擴充的執行階段功能[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]撰寫自訂程式碼的封裝[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Visual C# 是編譯及執行在封裝執行階段。 當 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 所含的工作未完全滿足您的需求時，指令碼工作可簡化自訂執行階段工作的開發。 指令碼工作會為您撰寫所有必要的基礎結構程式碼，讓您專門著重在自訂處理所需的程式碼。  
  
 指令碼工作會與透過全域包含的封裝互動**Dts**物件、 執行個體<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel>公開在指令碼環境中的類別。 您可以在指令碼工作中撰寫程式碼，以修改儲存在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 變數的值；之後，封裝可以使用這些更新的值來決定其工作流程的路徑。 指令碼工作也可以使用 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 命名空間和 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 類別庫以及自訂組件，來實作自訂功能。  
  
 指令碼工作以及它為您產生的基礎結構程式碼，可大幅簡化開發自訂工作的程序。 不過，若要了解指令碼工作的運作方式，您可能會發現閱讀節[開發自訂工作](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)了解開發自訂的工作所需的步驟。  
  
 如果您建立一個計劃在多個封裝中重複使用的工作，應該考慮開發自訂工作，而不要使用指令碼工作。 如需詳細資訊，請參閱[比較指令碼的方案和自訂物件](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題提供有關指令碼工作的詳細資訊。  
  
 [在指令碼工作編輯器中設定指令碼工作](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
 說明如何在您設定的屬性**指令碼工作編輯器**功能與指令碼工作中的程式碼的效能影響。  
  
 [編碼和偵錯指令碼工作](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
 說明如何使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 開發的指令碼工作中所包含的指令碼。  
  
 [在指令碼工作中使用變數](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 說明如何透過 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 屬性使用變數。  
  
 [連接到指令碼工作中的資料來源](../../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 說明如何透過 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 屬性使用連接。  
  
 [在指令碼工作中引發事件](../../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 說明如何透過 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> 屬性引發事件。  
  
 [登入指令碼工作](../../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)  
 說明如何透過 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 方法記錄資訊。  
  
 [傳回從指令碼工作的結果](../../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)  
 說明如何透過 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> 屬性與 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> 屬性傳回結果。  
  
 [指令碼工作範例](../../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
 提供簡單的範例，以示範指令碼工作的幾個可能用途。  
  
## <a name="see-also"></a>另請參閱  
 [指令碼工作](../../../integration-services/control-flow/script-task.md)   
 [比較指令碼工作和指令碼元件](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  

