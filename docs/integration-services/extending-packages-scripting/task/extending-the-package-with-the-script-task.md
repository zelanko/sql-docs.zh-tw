---
title: 以指令碼工作來擴充套件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: a51babb2df5954d35c9a2f09d02c1ddd8d49cf0c
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35402930"
---
# <a name="extending-the-package-with-the-script-task"></a>以指令碼工作擴充封裝
  指令碼工作會以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 所撰寫、並且在套件執行階段編譯並執行的自訂程式碼，來擴充 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 套件的執行階段功能。 當 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 所含的工作未完全滿足您的需求時，指令碼工作可簡化自訂執行階段工作的開發。 指令碼工作會為您撰寫所有必要的基礎結構程式碼，讓您專門著重在自訂處理所需的程式碼。  
  
 指令碼工作透過全域 **Dts** 物件與容器套件互動，這個物件是公開在指令碼編寫環境中的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel> 類別之執行個體。 您可以在指令碼工作中撰寫程式碼，以修改儲存在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 變數的值；之後，封裝可以使用這些更新的值來決定其工作流程的路徑。 指令碼工作也可以使用 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 命名空間和 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 類別庫以及自訂組件，來實作自訂功能。  
  
 指令碼工作以及它為您產生的基礎結構程式碼，可大幅簡化開發自訂工作的程序。 不過，若要了解指令碼工作如何運作，閱讀[開發自訂工作](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)一節，以了解開發自訂工作所需的步驟，可能會非常有用。  
  
 如果您建立一個計劃在多個封裝中重複使用的工作，應該考慮開發自訂工作，而不要使用指令碼工作。 如需詳細資訊，請參閱[比較指令碼解決方案和自訂物件](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題提供有關指令碼工作的詳細資訊。  
  
 [在指令碼工作編輯器設定指令碼工作](../../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)  
 說明在**指令碼工作編輯器**中設定的屬性如何影響指令碼工作中程式碼的功能與效能。  
  
 [編碼和偵錯指令碼工作](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
 說明如何使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 以開發包含在指令碼工作中的指令碼。  
  
 [在指令碼工作中使用變數](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 說明如何透過 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 屬性使用變數。  
  
 [在指令碼工作中連線至資料來源](../../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 說明如何透過 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 屬性使用連接。  
  
 [在指令碼工作中引發事件](../../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 說明如何透過 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> 屬性引發事件。  
  
 [在指令碼工作中記錄](../../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)  
 說明如何透過 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 方法記錄資訊。  
  
 [從指令碼工作傳回結果](../../../integration-services/extending-packages-scripting/task/returning-results-from-the-script-task.md)  
 說明如何透過 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> 屬性與 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> 屬性傳回結果。  
  
 [指令碼工作範例](../../../integration-services/extending-packages-scripting-task-examples/script-task-examples.md)  
 提供簡單的範例，以示範指令碼工作的幾個可能用途。  
  
## <a name="see-also"></a>另請參閱  
 [指令碼工作](../../../integration-services/control-flow/script-task.md)   
 [比較指令碼工作和指令碼元件](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  
