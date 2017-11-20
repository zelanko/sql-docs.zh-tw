---
title: "擴充資料流程 with the Script Component |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- data flow task [Integration Services], components
- data flow [Integration Services], extending
- debugging [Integration Services], components
- code design mode [Integration Services]
- metadata [Integration Services]
- scripts [Integration Services], extending data flow
- data flow components [Integration Services], Script component
- components [Integration Services], data flow
- Script component [Integration Services], about Script component
- Script component [Integration Services]
- data flow [Integration Services], components
ms.assetid: 072bc4b8-363a-4131-87c3-240338e2fa5c
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c58a854082fcbd12333be63995e4fcdf2d55aac7
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="extending-the-data-flow-with-the-script-component"></a>Extending the Data Flow with the Script Component
  指令碼元件擴充資料流程功能的[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]撰寫自訂程式碼的封裝[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Visual C# 是編譯及執行在封裝執行階段。 當 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 隨附的來源、轉換和目的地無法完全滿足您的需求時，指令碼元件會簡化自訂資料流程來源、轉換或目的地的開發作業。 在您使用預期的輸入和輸出來設定此元件之後，它會為您撰寫所有必要的基礎結構程式碼，讓您專門著重在自訂處理所需的程式碼。  
  
 指令碼元件互動與包含封裝和資料流程中的自動產生類別**ComponentWrapper**和**BufferWrapper**專案項目，也就是執行個體的<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>和<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>分別類別。 這些類別會讓連接、變數和其他封裝項目當做具類型的物件使用，並且管理輸入和輸出。 指令碼元件也可以使用 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 命名空間和 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 類別庫以及自訂組件來實作自訂功能。  
  
 指令碼元件以及它為您產生的基礎結構程式碼，可大幅簡化開發自訂資料流程元件的程序。 不過，若要了解指令碼元件如何運作，您可能會發現閱讀[開發自訂資料流程元件](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)了解開發自訂資料流程元件所需的步驟。  
  
 如果您要建立計畫在多個封裝中重複使用的來源、轉換或目的地，就應該考慮開發自訂元件，而非使用指令碼元件。 如需詳細資訊，請參閱 [開發自訂資料流程元件](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題提供有關指令碼元件的詳細資訊。  
  
 [在指令碼元件編輯器中設定指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
 您在設定的屬性**指令碼轉換編輯器**功能與指令碼元件程式碼的效能影響。  
  
 [編碼和偵錯指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
 您使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 開發環境來開發包含在指令碼元件中的指令碼。  
  
 [了解指令碼元件物件模型](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 新的指令碼元件專案包含三個專案項目，其中包含許多類別和自動產生的屬性與方法。  
  
 [在指令碼元件中使用變數](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)  
 **ComponentWrapper**專案項目包含封裝變數的強型別存取子屬性。  
  
 [連接到指令碼元件中的資料來源](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)  
 **ComponentWrapper**專案項目也包含封裝中定義之連接的強型別存取子屬性。  
  
 [在指令碼元件中引發事件](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md)  
 您可以引發事件來提供問題和錯誤的通知。  
  
 [登入指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md)  
 您可以將資訊記錄至封裝所啟用的記錄提供者。  
  
 [開發特定類型的指令碼元件](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
 這些簡單的範例將說明並示範如何使用指令碼元件來開發資料流程來源、轉換和目的地。  
  
 [其他指令碼元件範例](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
 這些簡單的範例將說明並示範一些指令碼元件的可能用法。  
  
## <a name="see-also"></a>另請參閱  
 [指令碼元件](../../../integration-services/data-flow/transformations/script-component.md)   
 [比較指令碼工作和指令碼元件](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  

