---
title: SSIS 設計師 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services, SSIS Designer
- Business Intelligence Development Studio, Integration Services in
- tools [Integration Services], SSIS Designer
- SSIS, SSIS Designer
- SSIS Designer, about SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: 006d68ea-1b5c-4c1e-8079-3910288e012c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 049197a6b1b862dccd2ae1c8c89d939bf050469d
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421095"
---
# <a name="ssis-designer"></a>SSIS 設計師
  [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師是可以用於建立及維護 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的圖形工具。 [!INCLUDE[ssIS](../includes/ssis-md.md)][!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供的設計師是 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案的一部分。

 您可以使用「 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」執行下列工作：

-   建構封裝中的控制流程。

-   建構封裝中的資料流程。

-   將事件處理常式加入封裝和封裝物件。

-   檢視封裝內容。

-   在執行階段，檢視封裝的執行進度。

 下圖顯示 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師與 [工具箱]  視窗。

 ![SSIS 設計師與工具箱的螢幕擷取畫面](media/denali-designerandtoolbox.gif "SSIS 設計師與工具箱的螢幕擷取畫面")

 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含用來在封裝中加入功能的其他對話方塊和視窗， [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 則提供用於設定開發環境及使用封裝的視窗和對話方塊。 如需詳細資訊，請參閱 [Integration Services User Interface](integration-services-user-interface.md)(Integration Services 使用者介面)。

 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師不具有對 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務 (管理和監視封裝的服務) 的相依性，且不需要執行該服務即可在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中建立或修改封裝。 不過，如果在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師處於開啟狀態時停止該服務，則將無法再開啟 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師所提供的對話方塊，同時您可能會接收到「RPC 伺服器無法使用」這樣的錯誤訊息。 若要重設 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師並繼續使用封裝，必須關閉設計師，結束 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，然後重新開啟 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ([!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案) 和封裝。

## <a name="undo-and-redo"></a>復原和取消復原
 您可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中復原和取消復原最多可達 20 個動作。 針對封裝，[控制流程]  、[資料流程]  、[事件處理常式]  及 [參數]  索引標籤，以及 [變數]  視窗中可以進行復原/取消復原。 針對專案，則可以在 [專案參數]  視窗中進行復原/取消復原。

 您無法復原和取消復原針對新 [SSIS 工具箱]  所做的變更。

 使用元件編輯器針對元件進行變更時，您可以將變更做為一個組進行復原和取消復原，而不是針對個別變更進行復原和取消復原。 變更組在復原與取消復原下拉式清單中顯示為單一動作。

 若要復原某個動作，按一下 [復原] 工具列按鈕、[編輯/復原]  功能表項目，或按 CTRL + Z。 若要復原某個動作，請按一下 [復原] 工具列按鈕、[編輯/復原]  功能表項目，或按 CTRL + Y。按一下工具列按鈕旁的箭頭、反白顯示下拉式清單中的多個動作，然後在清單中按一下，可以復原和取消復原多個動作。

## <a name="parts-of-the-ssis-designer"></a>SSIS 設計師的組件
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師有五個永久的索引標籤：各有一個索引標籤用於建立封裝控制流程、資料流程、參數和事件處理常式，還有一個索引標籤用於檢視封裝的內容。 在執行階段會出現第六個索引標籤，它會在封裝執行中顯示執行進度，並在完成時顯示執行結果。

 此外， [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師還包含「連接管理員」區域，用於加入和設定由封裝用來連接到資料的連接管理員。

### <a name="control-flow-tab"></a>控制流程索引標籤
 您可以在 [控制流程]  索引標籤的設計介面上，建構封裝中的控制流程。請從 [工具箱]  將項目拖曳至設計介面，並透過按一下項目的圖示將其連接到控制流程中，然後從一個項目拖曳箭頭到另一個項目。

 如需詳細資訊，請參閱 [控制流程](control-flow/control-flow.md)。

### <a name="data-flow-tab"></a>資料流程索引標籤
 如果封裝包含資料流程工作，您可以將資料流程加入封裝中。 您可以在 [資料流程]  索引標籤的設計介面上，建構封裝中的資料流程。請從 [工具箱]  將項目拖曳至設計介面，並透過按一下項目的圖示將其連接到資料流程中，然後從一個項目拖曳箭頭到另一個項目。

 如需詳細資訊，請參閱 [資料流程](data-flow/data-flow.md)。

### <a name="parameters-tab"></a>參數索引標籤
 Integration Services (SSIS) 參數可讓您在封裝執行時，將值指派給封裝內的屬性。 您可以在專案層級建立專案參數，並在封裝層級建立封裝參數。 專案參數可用於向專案中的一個或多個封裝提供專案接收的任何外部輸入。 封裝參數可讓您修改封裝執行，而不需要編輯和重新部署封裝。 此索引標籤可讓您管理封裝參數。

 如需參數的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 參數](integration-services-ssis-package-and-project-parameters.md)。

> [!IMPORTANT]
>  參數只能用於針對專案部署模型而開發的專案。 因此，僅對於屬於設定為使用專案部署模型之專案一部分的封裝，您才會看到 [參數] 索引標籤。

### <a name="event-handlers-tab"></a>事件處理常式索引標籤
 您可以在 [**事件處理常式**] 索引標籤的設計介面上，建立封裝中的事件。在 [**事件處理常式**] 索引標籤上，選取您要為其建立事件處理常式的封裝或封裝物件，然後選取要與事件處理常式建立關聯的事件。 事件處理常式具有控制流程和選擇性的資料流程。

 如需詳細資訊，請參閱 [Add an Event Handler to a Package](../../2014/integration-services/add-an-event-handler-to-a-package.md)(將事件處理常式加入封裝中)。

### <a name="package-explorer-tab"></a>封裝總管索引標籤
 封裝可能相當複雜，其中包括許多工作、連接管理員、變數和其他元素等。 封裝總管檢視可讓您查看封裝元素的完整清單。

 如需詳細資訊，請參閱 [View Package Objects](view-package-objects.md)(檢視封裝物件)。

#### <a name="progressexecution-result-tab"></a>進度/執行結果索引標籤
 當封裝正在執行時，[進度]**** 索引標籤會顯示封裝的執行進度。 在完成執行封裝後，執行結果會在 [執行結果]**** 索引標籤上保持可用。

> [!NOTE]
>  若要啟用或停用 **[進度]** 索引標籤上的訊息顯示，請在 **[SSIS]** 功能表上切換 **[偵錯進度報表]** 選項。

##### <a name="connection-managers-area"></a>連接管理員區域
 您可以在 [連線管理員]**** 區域中，加入及修改封裝所使用的連線管理員。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含可以連接到各種不同的資料來源 (例如文字檔、OLE DB 資料庫及 .NET 提供者) 的連線管理員。

 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 連接](connection-manager/integration-services-ssis-connections.md)和[建立連接管理員](../../2014/integration-services/create-connection-managers.md)。

## <a name="related-tasks"></a>相關工作

-   [在 SQL Server 資料工具中建立封裝](create-packages-in-sql-server-data-tools.md)

## <a name="see-also"></a>另請參閱
 [Integration Services 使用者介面](integration-services-user-interface.md)


