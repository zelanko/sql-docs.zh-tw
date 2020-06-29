---
title: 開發自訂資料流程元件 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], extending
- data flow [Integration Services], extending
- extending data flow task [Integration Services]
- components [Integration Services], data flow
ms.assetid: be126913-2a9a-41c9-9bf5-a7b0a0aea2f8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ee2b30cf0796953d12f976745fb195169de86c68
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437075"
---
# <a name="developing-a-custom-data-flow-component"></a>開發自訂資料流程元件
  資料流程工作是由連接至各種資料來源然後以高速轉換和路由資料的元件組成。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 所提供可延伸物件模型可讓開發人員建立可在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 及已部署套件中使用的自訂來源、轉換和目的地。 本章節包含將引導您開發自訂資料流程元件的主題。

## <a name="in-this-section"></a>本節內容
 [建立自訂資料流程元件](creating-a-custom-data-flow-component.md)描述建立自訂資料流程元件的初始步驟。

 [資料流程元件的設計階段方法](design-time-methods-of-a-data-flow-component.md)描述要在自訂資料流程元件中執行的設計階段方法。

 [資料流程元件的執行時間方法](run-time-methods-of-a-data-flow-component.md)描述要在自訂資料流程元件中執行的執行時間方法。

 [執行計畫和緩衝區配置](execution-plan-and-buffer-allocation.md)說明資料流程執行計畫和資料緩衝區的配置。

 [使用資料流程中的資料類型](working-with-data-types-in-the-data-flow.md)說明資料流程如何將 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 資料類型對應到 .NET Framework 的 managed 資料類型。

 [驗證資料流程元件](validating-a-data-flow-component.md)說明用來驗證元件設定以及重新設定元件中繼資料的方法。

 [執行外部中繼資料](implementing-external-metadata.md)說明如何使用外部中繼資料行進行資料驗證。

 [在資料流程元件中引發和定義事件](raising-and-defining-events-in-a-data-flow-component.md)說明如何引發預先定義和自訂的事件。

 [在資料流程元件中記錄和定義記錄專案](logging-and-defining-log-entries-in-a-data-flow-component.md)說明如何建立和寫入自訂記錄專案。

 [在資料流程元件中使用錯誤輸出](using-error-outputs-in-a-data-flow-component.md)說明如何將錯誤資料列重新導向至替代輸出。

 [升級資料流程元件的版本](upgrading-the-version-of-a-data-flow-component.md)說明當第一次使用元件的新版本時，如何更新已儲存的元件中繼資料。

 [開發資料流程元件的使用者介面](developing-a-user-interface-for-a-data-flow-component.md)說明如何執行元件的自訂編輯器。

 [開發特定類型的資料流程元件](../../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)包含開發三種資料流程元件類型的相關資訊：來源、轉換和目的地。

## <a name="reference"></a>參考
 <xref:Microsoft.SqlServer.Dts.Pipeline>包含用來建立自訂資料流程元件的類別和介面。

 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>包含組成「資料流程」工作物件模型的類別和介面，可用來建立自訂資料流程元件或建立「資料流程」工作。

 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>包含用來建立資料流程元件之使用者介面的類別和介面。

 [Integration Services 錯誤和訊息參考](../../integration-services-error-and-message-reference.md)列出預先定義的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 錯誤碼及其符號名稱和描述。

## <a name="related-sections"></a>相關章節

### <a name="information-common-to-all-custom-objects"></a>所有自訂物件的共通資訊
 如需有關 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中可以建立之所有類型自訂物件適用的共通資訊，請參閱下列主題：

 [開發 Integration Services 的自訂物件](../../extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)說明為執行所有類型之自訂物件的基本步驟 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 。

 [保存自訂物件](../../extending-packages-custom-objects/persisting-custom-objects.md)描述自訂持續性，並在必要時加以說明。

 [建立、部署和調試自訂物件](../../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)說明建立、簽署、部署和偵錯工具自訂物件的技術。

### <a name="information-about-other-custom-objects"></a>其他自訂物件的相關資訊
 如需有關在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中可以建立之其他類型自訂物件的詳細資訊，請參閱下列主題：

 [開發自訂工作](../../extending-packages-custom-objects/task/developing-a-custom-task.md)討論如何編寫自訂工作的程式。

 [開發自訂連線管理員](../../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)討論如何編寫自訂連接管理員的程式。

 [開發自訂記錄提供者](../../extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)討論如何編寫自訂記錄提供者的程式。

 [開發自訂 ForEach 列舉](../../extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)值討論如何編寫自訂枚舉器的程式。

![Integration Services 圖示（小型）](../../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。

## <a name="see-also"></a>另請參閱
 [以腳本元件擴充資料流程](../..[比較腳本解決方案和自訂物件的](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md


