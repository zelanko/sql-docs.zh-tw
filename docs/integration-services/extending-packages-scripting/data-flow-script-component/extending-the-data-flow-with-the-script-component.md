---
description: 使用指令碼元件來擴充資料流程
title: 使用指令碼元件擴充資料流程 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 82f34ab83935bee2972a4dbb2b007eb2632b9fba
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96122940"
---
# <a name="extending-the-data-flow-with-the-script-component"></a>使用指令碼元件來擴充資料流程

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  指令碼元件會以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 所撰寫且在套件執行階段編譯並執行的自訂程式碼，以擴充 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 套件的資料流程功能。 當 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 隨附的來源、轉換和目的地無法完全滿足您的需求時，指令碼元件會簡化自訂資料流程來源、轉換或目的地的開發作業。 在您使用預期的輸入和輸出來設定此元件之後，它會為您撰寫所有必要的基礎結構程式碼，讓您專門著重在自訂處理所需的程式碼。  
  
 指令碼元件會透過 **ComponentWrapper** 和 **BufferWrapper** 專案項目中自動產生的類別與包含的封裝和資料流程互動，而這些項目分別是 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 類別的執行個體。 這些類別會讓連接、變數和其他封裝項目當做具類型的物件使用，並且管理輸入和輸出。 指令碼元件也可以使用 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 命名空間和 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 類別庫以及自訂組件來實作自訂功能。  
  
 指令碼元件以及它為您產生的基礎結構程式碼，可大幅簡化開發自訂資料流程元件的程序。 不過，若要了解指令碼元件如何運作，建議您閱讀[開發自訂資料流程元件](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)一節，以了解開發自訂資料流程元件所需的步驟。  
  
 如果您要建立計畫在多個封裝中重複使用的來源、轉換或目的地，就應該考慮開發自訂元件，而非使用指令碼元件。 如需詳細資訊，請參閱 [開發自訂資料流程元件](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題提供有關指令碼元件的詳細資訊。  
  
 [在指令碼元件編輯器中設定指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
 您在 [指令碼轉換編輯器] 中設定的屬性會影響指令碼元件程式碼的功能和效能。  
  
 [編碼和偵錯指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
 您可以使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 開發環境來開發包含在指令碼元件中的指令碼。  
  
 [了解指令碼元件物件模型](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 新的指令碼元件專案包含三個專案項目，其中包含許多類別和自動產生的屬性與方法。  
  
 [在指令碼元件中使用變數](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)  
 **ComponentWrapper** 專案項目包含封裝變數的強型別存取子屬性。  
  
 [連接到指令碼元件中的資料來源](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)  
 **ComponentWrapper** 專案項目也包含封裝中定義之連接的強型別存取子屬性。  
  
 [在指令碼元件中引發事件](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md)  
 您可以引發事件來提供問題和錯誤的通知。  
  
 [在指令碼元件中記錄](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md)  
 您可以將資訊記錄至封裝所啟用的記錄提供者。  
  
 [開發特定類型的指令碼元件](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
 這些簡單的範例將說明並示範如何使用指令碼元件來開發資料流程來源、轉換和目的地。  
  
 [額外的指令碼元件範例](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
 這些簡單的範例將說明並示範一些指令碼元件的可能用法。  
  
## <a name="see-also"></a>另請參閱  
 [指令碼元件](../../../integration-services/data-flow/transformations/script-component.md)   
 [比較指令碼工作和指令碼元件](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  
