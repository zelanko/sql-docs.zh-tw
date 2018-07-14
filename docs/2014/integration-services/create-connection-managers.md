---
title: 建立連線管理員 |Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.connectionmanager.f1
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- packages [Integration Services], connections
- connection managers [Integration Services], creating
- SQL Server Integration Services packages, connections
ms.assetid: 6ca317b8-0061-4d9d-b830-ee8c21268345
caps.latest.revision: 54
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f09d663dd371c037c3f2b44b42b202c18377b7cb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37252540"
---
# <a name="create-connection-managers"></a>建立連接管理員
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含各種連接管理員，以符合連接到不同類型伺服器和資料來源之工作的需要。 連接管理員可由在不同類型資料儲存區中擷取和載入之資料的資料流程元件使用，也可由將記錄寫入伺服器、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料表或檔案的記錄提供者使用。 例如，具有傳送郵件工作的封裝使用 SMTP 連接管理員類型，來連接到 Simple Mail Transfer Protocol (SMTP) 伺服器。 具有執行 SQL 工作的封裝，可以使用 OLE DB 連線管理員來連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 連接](connection-manager/integration-services-ssis-connections.md)。  
  
 若要在您建立新的封裝時自動建立及設定連線管理員，您可以使用 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 匯入和匯出精靈]。 精靈也可以幫助您建立及設定使用連線管理員的來源和目的地。 如需詳細資訊，請參閱 [在 SQL Server 資料工具中建立封裝](create-packages-in-sql-server-data-tools.md)。  
  
 若要手動建立新的連線管理員，並將其加入至現有的封裝，請使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師之 [控制流程]、[資料流程] 和 [事件處理常式] 索引標籤上所出現的 [連線管理員] 區域。 從 [連線管理員] 區域，您可以使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師所提供的對話方塊，來選擇要建立的連線管理員類型，然後再設定連線管理員的屬性。 如需詳細資訊，請參閱本主題稍後的「使用連線管理員區域」一節。  
  
 將連接管理員加入封裝之後，您就可以在工作、「Foreach 迴圈」容器、來源、轉換和目的地中使用它。 如需詳細資訊，請參閱 [Integration Services 工作](control-flow/integration-services-tasks.md)、[Foreach 迴圈容器](control-flow/foreach-loop-container.md)和[資料流程](data-flow/data-flow.md)。  
  
## <a name="using-the-connection-managers-area"></a>使用連接管理員區域  
 當 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師的 [控制流程]、[資料流程] 或 [事件處理常式] 索引標籤處於作用中時，您可以建立連線管理員。  
  
 下圖顯示 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師之 [控制流程] 索引標籤上的 [連線管理員] 區域。  
  
 ![具有套件之控制流程設計工具的螢幕擷取畫面](media/samplecontrolflow.gif "具有套件之控制流程設計工具的螢幕擷取畫面")  
  
#### <a name="to-add-configure-or-delete-a-connection-manager-in-ssis-designer"></a>在 SSIS 設計師中加入、設定或刪除連線管理員  
  
-   [新增、刪除或共用套件中的連線管理員](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)  
  
-   [設定連線管理員的屬性](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
## <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>連接管理員的 32 位元和 64 位元提供者  
 連接管理員使用的許多提供者都有 32 位元和 64 位元兩種版本。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 設計環境是 32 位元的環境；設計封裝時，您只會看到 32 位元的提供者。 因此，如果要將連接管理員設定成使用特定的 64 位元提供者，您必須同時安裝 32 位元版本的同一個提供者。  
  
 執行階段中會使用正確的版本，而且就算您在設計階段中指定了 32 位元版本的提供者也沒有關係。 即使封裝是在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中執行，還是可以執行 64 位元版本的提供者。  
  
 兩個版本的提供者具有相同的識別碼。 若要指定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 執行階段是否使用可用的 64 位元版本提供者，請設定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案的 Run64BitRuntime 屬性。 如果 Run64BitRuntime 屬性設定為`true`，執行階段會尋找並使用 64 位元提供者中; 如果 Run64BitRuntime 是`false`，執行階段會尋找並使用 32 位元提供者。 如需可在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案上設定之屬性的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 和 Studio 環境](integration-services-ssis-development-and-management-tools.md)。  
  
## <a name="see-also"></a>另請參閱  
 [控制流程](control-flow/control-flow.md)   
 [資料流程](data-flow/data-flow.md)   
 [Integration Services &#40;SSIS&#41;事件處理常式](integration-services-ssis-event-handlers.md)  
  
  
