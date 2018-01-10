---
title: "開發自訂資料流程元件 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], extending
- data flow [Integration Services], extending
- extending data flow task [Integration Services]
- components [Integration Services], data flow
ms.assetid: be126913-2a9a-41c9-9bf5-a7b0a0aea2f8
caps.latest.revision: "57"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 60c5b673e22aabcd0ed3f6064e1a5d8c94a73f97
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="developing-a-custom-data-flow-component"></a>開發自訂資料流程元件
  資料流程工作是由連接至各種資料來源然後以高速轉換和路由資料的元件組成。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 提供的可延伸物件模型，讓開發人員建立可在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 及部署的套件中使用的自訂來源、轉換和目的地。 本章節包含將引導您開發自訂資料流程元件的主題。  
  
## <a name="in-this-section"></a>本節內容  
 [建立自訂資料流程元件](../../../integration-services/extending-packages-custom-objects/data-flow/creating-a-custom-data-flow-component.md)  
 描述建立自訂資料流程元件的初始步驟。  
  
 [資料流程元件的設計階段方法](../../../integration-services/extending-packages-custom-objects/data-flow/design-time-methods-of-a-data-flow-component.md)  
 描述自訂資料流程元件中實作的設計階段方法。  
  
 [資料流程元件的執行階段方法](../../../integration-services/extending-packages-custom-objects/data-flow/run-time-methods-of-a-data-flow-component.md)  
 描述自訂資料流程元件中實作的執行階段方法。  
  
 [執行計劃和緩衝配置](../../../integration-services/extending-packages-custom-objects/data-flow/execution-plan-and-buffer-allocation.md)  
 描述資料流程執行計劃以及資料緩衝區的配置。  
  
 [在資料流程中使用資料類型](../../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)  
 說明資料流程如何將 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型對應至 .NET Framework Managed 資料類型。  
  
 [驗證資料流程元件](../../../integration-services/extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md)  
 說明用以驗證元件組態的方法以及重新設定元件中繼資料的方法。  
  
 [實作外部中繼資料](../../../integration-services/extending-packages-custom-objects/data-flow/implementing-external-metadata.md)  
 說明如何使用外部中繼資料行進行資料驗證。  
  
 [在資料流程元件中引發和定義事件](../../../integration-services/extending-packages-custom-objects/data-flow/raising-and-defining-events-in-a-data-flow-component.md)  
 說明如何引發預先定義事件和自訂事件。  
  
 [在資料流程元件中記錄和定義記錄項目](../../../integration-services/extending-packages-custom-objects/data-flow/logging-and-defining-log-entries-in-a-data-flow-component.md)  
 說明如何建立和寫入自訂記錄項目。  
  
 [在資料流程元件中使用錯誤輸出](../../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)  
 說明如何將錯誤資料列重新導向至替代輸出。  
  
 [升級資料流程元件的版本](../../../integration-services/extending-packages-custom-objects/data-flow/upgrading-the-version-of-a-data-flow-component.md)  
 說明第一次使用新版的元件時，如何更新儲存的元件中繼資料。  
  
 [開發資料流程元件的使用者介面](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-user-interface-for-a-data-flow-component.md)  
 說明如何實作元件的自訂編輯器。  
  
 [開發特定類型的資料流程元件](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
 包含開發三種資料流程元件的相關資訊：來源、轉換和目的地。  
  
## <a name="reference"></a>參考  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 包含用以建立自訂資料流程元件的類別與介面。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 包含可用來建立自訂資料流程元件或建立資料流程工作之資料流程工作物件模型的組成類別和介面。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>  
 包含用以建立資料流程元件的使用者介面之類別與介面。  
  
 [Integration Services 錯誤和訊息參考](../../../integration-services/integration-services-error-and-message-reference.md)  
 列出預先定義的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 錯誤碼，以及其符號名稱與描述。  
  
## <a name="related-sections"></a>相關章節  
  
### <a name="information-common-to-all-custom-objects"></a>所有自訂物件的共通資訊  
 如需有關 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中可以建立之所有類型自訂物件適用的共通資訊，請參閱下列主題：  
  
 [開發 Integration Services 的自訂物件](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 描述為 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 實作所有類型的自訂物件之基本步驟。  
  
 [保存自訂物件](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 描述自訂的持續性並解釋必須實作它的時機。  
  
 [自訂物件的建立、部署和偵錯](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 描述建立、簽署、部署和偵錯自訂物件的技術。  
  
### <a name="information-about-other-custom-objects"></a>其他自訂物件的相關資訊  
 如需有關在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中可以建立之其他類型自訂物件的詳細資訊，請參閱下列主題：  
  
 [開發自訂工作](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 討論如何進行自訂工作的程式設計。  
  
 [開發自訂連線管理員](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 討論如何進行自訂連接管理員的程式設計。  
  
 [開發自訂記錄提供者](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 討論如何進行自訂記錄提供者的程式設計。  
  
 [開發自訂 Foreach 列舉程式](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 討論如何進行自訂列舉值的程式設計。  
  
## <a name="see-also"></a>另請參閱  
 [使用指令碼元件擴充資料流程](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
 [比較指令碼解決方案和自訂物件](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
