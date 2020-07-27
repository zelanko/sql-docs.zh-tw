---
title: 偵錯控制流程 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.setbreakpoints.f1
helpviewer_keywords:
- progress reporting [Integration Services]
- breakpoints [Integration Services]
- debugging [Integration Services], control flow
- control flow [Integration Services], debugging
- color-coded progress reporting [Integration Services]
- Set Breakpoints dialog box
ms.assetid: 54a458cc-9f4f-4b48-8cf2-db2e0fa7756c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e3602a8e21d6d7fd9371331914c6157c5db2ca4
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920761"
---
# <a name="debugging-control-flow"></a>偵錯控制流程

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含許多功能和工具，可讓您用來對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件中的控制流程進行疑難排解。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支援容器及工作上的中斷點。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」提供執行階段的進度報表。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 提供偵錯視窗。  
  
## <a name="breakpoints"></a>中斷點  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具提供 [設定中斷點]  對話方塊，您可以啟用中斷條件，並指定套件的執行暫停之前中斷點可以出現的次數，在此設定中斷點。 中斷點可以在封裝層級啟用，也可以在個別元件層級啟用。 如果中斷條件在工作或容器層級啟用，則中斷點圖示會顯示在 [控制流程]  索引標籤之設計介面的工作或容器旁。如果中斷條件在封裝上啟用，則中斷點圖示會顯示在 [控制流程]  索引標籤的標籤上。  
  
 當叫用中斷點時，中斷點圖示會變更，以協助您識別中斷點的來源。 您可以在封裝執行時加入、刪除及變更中斷點。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供您可以在所有工作及容器上啟用的十個中斷條件。 在 [設定中斷點]  對話方塊中，您可以在滿足下列條件時啟用中斷點：  
  
|中斷條件|描述|  
|---------------------|-----------------|  
|當容器收到 **OnPreExecute** 事件時。|即將執行工作時呼叫。 工作或容器會在即將執行之前引發此事件。|  
|當容器收到 **OnPostExecute** 事件時。|在工作的執行邏輯完成之後立即呼叫。 工作或容器會在執行之後立即引發此事件。|  
|當容器收到 **OnError** 事件時。|發生錯誤時由工作或容器呼叫。|  
|當容器收到 **OnWarning** 事件時。|當工作處於還不是錯誤但需要警告的狀態時呼叫。|  
|當容器收到 **OnInformation** 事件時。|需要工作提供資訊時呼叫。|  
|當容器收到 **OnTaskFailed** 事件時。|由工作主機在失敗時呼叫。|  
|當容器收到 **OnProgress** 事件時。|呼叫以更新工作執行相關的進度。|  
|當容器收到 **OnQueryCancel** 事件時。|在可取消執行之工作處理期間的任何時間呼叫。|  
|當容器收到 **OnVariableValueChanged** 事件時。|當變數的值變更時由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行階段呼叫。 變數的 RaiseChangeEvent 必須設為 [true]  ，方可引發此事件。<br /><br /> **&#42;&#42; 警告 &#42;&#42;** 與此中斷點相關聯的變數必須在**容器**範圍定義。 如果變數在封裝範圍定義，則中斷點不會出現。|  
|當容器收到 **OnCustomEvent** 事件時。|由工作呼叫，以引發自訂工作定義的事件。|  
  
 除可用於所有工作及容器的中斷條件之外，部份工作及容器還包含用於設定中斷點的特殊中斷條件。 例如，您可以在「For 迴圈」容器上啟用中斷條件，以設定在迴圈的每個反覆運算開始時暫停執行的中斷點。  
  
 若要加強中斷點的彈性及能力，您可以藉由指定下列選項來修改中斷點的行為：  
  
-   叫用計數，或執行暫停之前中斷條件出現的最大次數。  
  
-   叫用計數類型，或指定中斷條件何時觸發中斷點的規則。  
  
 叫用計數會進一步限定「永遠」類型以外的叫用計數類型。 例如，如果類型為「叫用計數等於」而叫用計數為 5 的話，便會在第六次出現中斷條件時暫停執行。  
  
 下表描述叫用計數類型。  
  
|叫用計數類型|描述|  
|--------------------|-----------------|  
|一律|叫用中斷點時，一律暫停執行。|  
|叫用計數等於|當中斷點發生的次數等於叫用計數時，暫停執行。|  
|叫用次數大於或等於|當中斷點發生的次數大於或等於叫用計數時，暫停執行。|  
|叫用計數倍數|每當到達叫用計數的倍數時，暫停執行。 例如，若您將此選項設定為 5，則每到達五次叫用便會暫停執行。|  
  
#### <a name="to-set-breakpoints"></a>設定中斷點  
  
-   [在工作或容器設定中斷點以對套件偵錯](#debug)  
  
## <a name="progress-reporting"></a>進度報表  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具包含兩種類型的進度報告：[控制流程]  索引標籤之設計介面上的色彩編碼，以及 [進度]  索引標籤上的進度訊息。  
  
 當您執行封裝時，「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」會使用指示執行狀態的色彩來顯示每個工作或容器，以描述執行進度。 您可以根據元素的色彩判斷它是在等候執行、執行中、已順利完成，還是未成功結束。 在您停止封裝執行之後，色彩編碼會消失。  
  
 下表描述用於描述執行狀態的色彩。  
  
|Color|執行狀態|  
|-----------|----------------------|  
|灰色|等候執行|  
|黃色|執行中|  
|綠色|執行成功|  
|反白顯示|執行發生錯誤|  
  
 [進度]  索引標籤會以執行順序列出工作及容器，並包含開始與完成時間、警告及錯誤訊息。 在您停止封裝執行之後，進度資訊在 [執行結果]  索引標籤上仍然可用。  
  
> [!NOTE]  
>  若要啟用或停用 **[進度]** 索引標籤上的訊息顯示，請在 **[SSIS]** 功能表上切換 **[偵錯進度報表]** 選項。  
  
 下圖顯示 [進度]  索引標籤。  
  
 ![SSIS 設計師的 [進度] 索引標籤](../../integration-services/troubleshooting/media/mw-dtsflow04.gif "SSIS 設計師的 [進度] 索引標籤")  
  
## <a name="debug-windows"></a>偵錯視窗  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 包含許多視窗，您可將其用於處理中斷點及偵錯包含中斷點的封裝。 若要了解每個視窗的詳細資訊，請開啟該視窗並按 F1，以顯示視窗的 [說明]。  
  
 若要在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中開啟這些視窗，請按一下 [偵錯]  功能表，指向 [視窗]  ，然後按一下 [中斷點]  、[輸出]  或 [立即]  。  
  
 下表描述這些視窗。  
  
|時間範圍|描述|  
|------------|-----------------|  
|中斷點|列出封裝中的中斷點，並提供啟用及刪除中斷點的選項。|  
|輸出|在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中顯示各功能的狀態訊息。|  
|立即|用於偵錯及評估運算式並列印變數值。|  

## <a name="debug-a-package-by-setting-breakpoints-on-a-task-or-a-container"></a><a name="debug"></a> 針對工作或容器設定中斷點以偵錯封裝
  此程序描述如何在封裝、工作、「For 迴圈」容器、「Foreach 迴圈」容器或「時序」容器中設定中斷點。  
  
### <a name="to-set-breakpoints-in-a-package-a-task-or-a-container"></a>若要在封裝、工作或容器中設定中斷點  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  按兩下要在其中設定中斷點的封裝。  
  
3.  在 [SSIS 設計師] 中，執行下列動作：  
  
    -   若要在封裝物件中設定中斷點，請按一下 [控制流程]  索引標籤，並將資料指標置於設計介面背景上的任意位置，再以滑鼠右鍵按一下，然後按一下 [編輯中斷點]  。  
  
    -   若要在封裝控制流程中設定中斷點，請按一下 [控制流程]  索引標籤，並以滑鼠右鍵按一下工作、「For 迴圈」容器、「Foreach 迴圈」容器或「時序」容器，然後按一下 [編輯中斷點]  。  
  
    -   若要在事件處理常式中設定中斷點，請按一下 [事件處理常式]  索引標籤，並以滑鼠右鍵按一下工作、「For 迴圈」容器、「Foreach 迴圈」容器或「時序」容器，然後按一下 [編輯中斷點]  。  
  
4.  在 [設定中斷點 \<container name>] 對話方塊中，選取要啟用的中斷點。  
  
5.  選擇性地修改每個中斷點的叫用計數類型和叫用計數數目。  
  
6.  若要儲存封裝，請按一下 [檔案]  功能表上的 [儲存選取項目]  。  

## <a name="set-breakpoints"></a>[設定中斷點]
  使用 **[設定中斷點]** 對話方塊，即可指定要啟用中斷點的事件並控制中斷點的行為。  
  
### <a name="options"></a>選項。  
 **已啟用**  
 選取即可在事件上啟用中斷點。  
  
 **Break Condition**  
 檢視要設定中斷點之可用事件的清單。  
  
 **Hit Count Type**  
 指定中斷點生效的時間。  
  
|值|描述|  
|-----------|-----------------|  
|**永遠**|叫用中斷點時，一律暫停執行。|  
|**叫用計數等於**|當中斷點發生的次數等於叫用計數時，暫停執行。|  
|**叫用大於或等於**|當中斷點發生的次數大於或等於叫用計數時，暫停執行。|  
|**叫用計數倍數**|每當到達叫用計數的倍數時，暫停執行。 例如，若您將此選項設定為 5，則每到達五次叫用便會暫停執行。|  
  
 **叫用計數**  
 指定觸發中斷的叫用次數。 如果中斷點永遠有效，則無法使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [套件開發的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
 [在指令碼工作和指令碼元件中設定中斷點來對指令碼偵錯](../../integration-services/extending-packages-scripting/debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component.md)   
