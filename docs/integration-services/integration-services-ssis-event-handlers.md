---
description: Integration Services (SSIS) 事件處理常式
title: Integration Services (SSIS) 事件處理常式 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, events
- run-time [Integration Services]
- SQL Server Integration Services packages, events
- event handlers [Integration Services], about event handlers
- events [Integration Services]
- packages [Integration Services], events
- event handlers [Integration Services]
- SSIS packages, events
- containers [Integration Services], events
- events [Integration Services], about events
ms.assetid: 6f60cf93-35dc-431c-908d-2049c4ab66ba
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7e2c7fb36708d615bd19dfb2c5854748081a9dbb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449830"
---
# <a name="integration-services-ssis-event-handlers"></a>Integration Services (SSIS) 事件處理常式

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  在執行階段，可執行檔 (封裝和「Foreach 迴圈」、「For 迴圈」、「時序」，以及工作主機容器) 會引發事件。 例如，當發生錯誤時，會引發 OnError 事件。 您可以建立這些事件的自訂事件處理常式，以擴充封裝功能，並使封裝在執行階段易於管理。 事件處理常式可以執行下列工作：  
  
-   封裝或工作完成執行後，清除暫存資料儲存。  
  
-   擷取系統資訊，以在封裝執行之前評估資源可用性。  
  
-   當查閱參考資料表失敗時，重新整理資料表中的資料。  
  
-   當發生錯誤或警告時，或工作失敗時，傳送電子郵件訊息。  
  
 如果事件不具有事件處理常式，則該事件會被提升到封裝中容器階層上的下一個容器。 如果此容器具有事件處理常式，則會執行事件處理常式，以回應該事件。 若否，則該事件會被提升到容器階層上的下一個容器。  
  
 下圖顯示一個具有「For 迴圈」容器的簡單封裝，該容器包含一個「執行 SQL」工作。  
  
 ![套件、For 迴圈、工作主機和執行 SQL 工作](../integration-services/media/mw-dts-eventhandlerpkg.gif "套件、For 迴圈、工作主機和執行 SQL 工作")  
  
 針對其 **OnError** 事件，僅封裝具有事件處理常式。 如果在「執行 SQL」工作執行時發生錯誤，則會執行封裝的 **OnError** 事件處理常式。 下圖顯示引發封裝執行 **OnError** 事件處理常式的呼叫順序。  
  
 ![事件處理常式流程](../integration-services/media/mw-dts-eventhandlers.gif "事件處理常式流程")  
  
 事件處理常式是事件處理常式集合的成員，所有容器都包含此集合。 如果使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師建立封裝，則您可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師之 [封裝總管]**** 索引標籤上的 [事件處理常式]**** 資料夾中，查看事件處理常式集合的成員。  
  
 您可以利用下列方式設定事件處理常式容器：  
  
-   指定事件處理常式的名稱和描述。  
  
-   指出是否執行事件處理常式，如果事件處理常式失敗則封裝是否也將失敗，以及事件處理常式失敗之前可發生錯誤的數目。  
  
-   指定要傳回的執行結果，而非事件處理常式在執行階段傳回的實際執行結果。  
  
-   指定事件處理常式的交易選項。  
  
-   指定事件處理常式使用的記錄模式。  
  
## <a name="event-handler-content"></a>事件處理常式內容  
 建立事件處理常式與建立封裝相似；事件處理常式具有工作和容器，它們會循序進入控制流程，並且事件處理常式還可以包含資料流程。 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師包含 [事件處理常式]**** 索引標籤，用以建立自訂事件處理常式。  
  
 您還可以程式設計方式建立事件處理常式。 如需詳細資訊，請參閱 [以程式設計方式處理事件](../integration-services/building-packages-programmatically/handling-events-programmatically.md)。  
  
## <a name="run-time-events"></a>執行階段事件  
 下表列出 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 所提供的事件處理常式，並描述引發事件處理常式執行的執行階段事件。  
  
|事件處理常式|事件|  
|-------------------|-----------|  
|**OnError**|**OnError** 事件的事件處理常式。 當發生錯誤時，可執行檔會引發此事件。|  
|**OnExecStatusChanged**|**OnExecStatusChanged** 事件的事件處理常式。 當可執行檔的執行狀態變更時，它會引發此事件。|  
|**OnInformation**|**OnInformation** 事件的事件處理常式。 在驗證和執行可執行檔以報告資訊期間，會引發此事件。 此事件僅傳遞資訊，而不傳遞錯誤或警告。|  
|**OnPostExecute**|**OnPostExecute** 事件的事件處理常式。 可執行檔完成執行後，它會立即引發此事件。|  
|**OnPostValidate**|**OnPostValidate** 事件的事件處理常式。 可執行檔的驗證完成後，它會引發此事件。|  
|**OnPreExecute**|**OnPreExecute** 事件的事件處理常式。 可執行檔執行之前，它會立即引發此事件。|  
|**OnPreValidate**|**OnPreValidate** 事件的事件處理常式。 可執行檔驗證開始時，它會引發此事件。|  
|**OnProgress**|**OnProgress** 事件的事件處理常式。 可執行檔的進度可測量時，它會引發此事件。|  
|**OnQueryCancel**|**OnQueryCancel** 事件的事件處理常式。 可執行檔會引發此事件，以判斷其是否應停止執行。|  
|**OnTaskFailed**|**OnTaskFailed** 事件的事件處理常式。 工作失敗時，它引發此事件。|  
|**OnVariableValueChanged**|**OnVariableValueChanged** 事件的事件處理常式。 當變數變更時，可執行檔會引發此事件。 定義變數所在的可執行檔會引發此事件。 如果您將變數的 **RaiseChangeEvent** 屬性設定為 **False**，則不會引發此事件。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services/integration-services-ssis-variables.md)。|  
|**OnWarning**|**OnWarning** 事件的事件處理常式。 當發生警告時，可執行檔會引發此事件。|  

## <a name="add-an-event-handler-to-a-package"></a>將事件處理常式加入封裝中
在執行階段，容器及工作會引發事件。 藉由在引發事件時執行工作流程，您可以建立自訂事件處理常式，以回應這些事件。 例如，您可以建立在工作失敗時傳送電子郵件訊息的事件處理常式。  
  
 事件處理常式與封裝相似。 事件處理常式與封裝相似，可提供變數的範圍，並包括控制流程和選擇性的資料流程。 您可以為封裝、「Foreach 迴圈」容器、「For 迴圈」容器、「時序」容器及所有工作建立事件處理常式。  
  
 您可以使用 [!INCLUDE[ssIS](../includes/ssis-md.md)]設計師中 [事件處理常式]**** 索引標籤的設計介面，來建立事件處理常式。  
  
 當 [事件處理常式]**** 索引標籤為使用中時，[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中 [工具箱] 的 [控制流程項目]**** 和 [維護計畫工作]**** 節點，會包含用於在事件處理常式中建立控制流程的工作及容器。 [資料流程來源]****、[轉換]**** 及 [資料流程目的地]**** 節點包含用於在事件處理常式中建立資料流程的資料來源、轉換及目的地。 如需詳細資訊，請參閱[控制流程](../integration-services/control-flow/control-flow.md)和[資料流程](../integration-services/data-flow/data-flow.md)。  
  
 [事件處理常式]**** 索引標籤還包含 [連線管理員]**** 區域，在此區域中，您可以建立並修改事件處理常式用於連接到伺服器和資料來源的連線管理員。 如需詳細資訊，請參閱[建立連線管理員](https://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)。  
  
### <a name="add-an-event-handler-on-the-event-handlers-tab"></a>在事件處理常式索引標籤上新增事件處理常式  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [事件處理常式]**** 索引標籤。  
  
     ![含事件處理常式的設計介面螢幕擷取畫面](../integration-services/media/eventhandlers.gif "含事件處理常式的設計介面螢幕擷取畫面")  
  
     在事件處理常式中建立控制流程和資料流程，與在封裝中建立控制流程和資料流程相似。 如需詳細資訊，請參閱[控制流程](../integration-services/control-flow/control-flow.md)和[資料流程](../integration-services/data-flow/data-flow.md)。  
  
4.  在 [可執行檔]**** 清單中，選取要為其建立事件處理常式的可執行檔。  
  
5.  在 [事件處理常式]**** 清單中，選取要建立的事件處理常式。  
  
6.  按一下 [事件處理常式]**** 索引標籤之設計介面上的連結。  
  
7.  將控制流程項目加入事件處理常式，並使用優先順序條件約束連接項目，方法是將條件約束從一個控制流程項目拖曳到另一個控制流程項目。 如需詳細資訊，請參閱 [控制流程](../integration-services/control-flow/control-flow.md)。  
  
8.  選擇性地加入「資料流程」工作，並在 [資料流程]**** 索引標籤的設計介面上，為事件處理常式建立資料流程。 如需詳細資訊，請參閱 [資料流程](../integration-services/data-flow/data-flow.md)。  
  
9. 在 [檔案]**** 功能表上，按一下 [儲存選取項目]****，以儲存封裝。  

## <a name="set-the-properties-of-an-event-handler"></a>設定事件處理常式的屬性  
 您可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的 [屬性]**** 視窗中，或以程式設計方式設定屬性。  
  
 如需如何在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中設定這些屬性的相關資訊，請參閱 [設定工作或容器的屬性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)。  
  
 如需以程式設計方式設定這些屬性的詳細資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>。  
  
## <a name="related-tasks"></a>相關工作  
 如需如何將事件處理常式加入封裝的相關資訊，請參閱 [將事件處理常式加入封裝中](https://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)。  
  
  
