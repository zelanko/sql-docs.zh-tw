---
title: 將事件處理常式新增至封裝 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- event handlers [Integration Services], creating
ms.assetid: 5e56885d-8658-480a-bed9-3f2f8003fd78
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 589d90b52647241b22929473efc9c6e54eb3b75f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062032"
---
# <a name="add-an-event-handler-to-a-package"></a>將事件處理常式加入封裝中
  在執行階段，容器及工作會引發事件。 藉由在引發事件時執行工作流程，您可以建立自訂事件處理常式，以回應這些事件。 例如，您可以建立在工作失敗時傳送電子郵件訊息的事件處理常式。  
  
 事件處理常式與封裝相似。 事件處理常式與封裝相似，可提供變數的範圍，並包括控制流程和選擇性的資料流程。 您可以為封裝、「Foreach 迴圈」容器、「For 迴圈」容器、「時序」容器及所有工作建立事件處理常式。  
  
 您可以使用 **設計師中 [事件處理常式]**[!INCLUDE[ssIS](../includes/ssis-md.md)] 索引標籤的設計介面，來建立事件處理常式。  
  
 當 [事件處理常式]**** 索引標籤為使用中時，** 設計師中 [工具箱] 的 [控制流程項目]**** 和 [維護計畫工作]**[!INCLUDE[ssIS](../includes/ssis-md.md)] 節點，會包含用於在事件處理常式中建立控制流程的工作及容器。 [資料流程來源]****、[轉換]**** 及 [資料流程目的地]**** 節點包含用於在事件處理常式中建立資料流程的資料來源、轉換及目的地。 如需詳細資訊，請參閱[控制流程](control-flow/control-flow.md)和[資料流程](data-flow/data-flow.md)。  
  
 [事件處理常式]**** 索引標籤還包含 [連線管理員]**** 區域，在此區域中，您可以建立並修改事件處理常式用於連接到伺服器和資料來源的連線管理員。 如需詳細資訊，請參閱[建立連線管理員](../../2014/integration-services/create-connection-managers.md)。  
  
### <a name="to-create-an-event-handler"></a>建立事件處理常式  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [事件處理常式]**** 索引標籤。  
  
     ![含事件處理常式之設計介面的螢幕擷取畫面](media/eventhandlers.gif "含事件處理常式之設計介面的螢幕擷取畫面")  
  
     在事件處理常式中建立控制流程和資料流程，與在封裝中建立控制流程和資料流程相似。 如需詳細資訊，請參閱[控制流程](control-flow/control-flow.md)和[資料流程](data-flow/data-flow.md)。  
  
4.  在 [可執行檔]**** 清單中，選取要為其建立事件處理常式的可執行檔。  
  
5.  在 [事件處理常式]**** 清單中，選取要建立的事件處理常式。  
  
6.  按一下 [事件處理常式]**** 索引標籤之設計介面上的連結。  
  
7.  將控制流程項目加入事件處理常式，並使用優先順序條件約束連接項目，方法是將條件約束從一個控制流程項目拖曳到另一個控制流程項目。 如需詳細資訊，請參閱 [控制流程](control-flow/control-flow.md)。  
  
8.  選擇性地加入「資料流程」工作，並在 [資料流程]**** 索引標籤的設計介面上，為事件處理常式建立資料流程。 如需詳細資訊，請參閱 [資料流程](data-flow/data-flow.md)。  
  
9. 在 [檔案]**** 功能表上，按一下 [儲存選取項目]****，以儲存封裝。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Integration Services](../../2014/integration-services/sql-server-integration-services.md)   
 [Integration Services &#40;SSIS&#41; 記錄](performance/integration-services-ssis-logging.md)  
  
  
