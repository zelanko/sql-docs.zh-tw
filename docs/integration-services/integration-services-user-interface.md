---
title: "Integration Services 使用者介面 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Integration Services, SSIS Designer
- tools [Integration Services], SSIS Designer
- SSIS Designer
- SSIS, SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: d2c48cff-46f4-4c70-b1f3-c88f9b8757f3
caps.latest.revision: "54"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 53d4cd6d44f33b05ca586077a33307616aa45986
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-user-interface"></a>Integration Services 使用者介面
  除了 [ [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 索引標籤上的設計介面以外，使用者介面還提供對下列視窗和對話方塊 (用以將功能加入封裝及設定封裝物件屬性) 的存取權：  
  
-   用來將功能 (例如，記錄和組態) 加入封裝的對話方塊和視窗。  
  
-   用來設定封裝物件屬性的自訂編輯器。 幾乎每種類型的容器、工作和資料流程元件都擁有自己的自訂編輯器。  
  
-   而 [進階編輯器] 對話方塊是一種一般編輯器，可為許多資料流程元件提供更詳細的組態選項。  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 還提供用來設定環境與使用封裝的視窗和對話方塊。  
  
## <a name="dialog-boxes-and-windows"></a>對話方塊和視窗  
 在「[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」中開啟封裝或新建封裝後，可以使用下列對話方塊和視窗。  
  
 下表列出 [SSIS] 功能表和 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 之設計介面中可用的對話方塊。  
  
|對話方塊|目的|存取|  
|----------------|-------------|------------|  
|**快速入門**|存取範例、教學課程和影片。|在 [控制流程] 索引標籤或 [資料流程] 索引標籤的設計介面上按一下滑鼠右鍵，然後按一下 [使用者入門]。<br /><br /> 若要在建立新 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案時自動顯示 [使用者入門] 視窗，請選取視窗最下方的 [Always show in new project (永遠在新專案中顯示)]。|  
|**[設定 SSIS 記錄]**|透過加入記錄和設定記錄詳細資料來設定封裝及其工作的記錄。|在 **[SSIS]** 功能表上，按一下 **[記錄]**。<br /><br /> -或-<br /><br /> 以滑鼠右鍵按一下 [控制流程] 索引標籤之設計介面的任意位置，然後按一下 [記錄]。|  
|**[封裝組態組合管理]**|加入並編輯封裝組態。 您可從此對話方塊執行「封裝組態精靈」。|在 [SSIS] 功能表上，按一下 [封裝組態]。<br /><br /> -或-<br /><br /> 以滑鼠右鍵按一下 [控制流程] 索引標籤之設計介面的任意位置，然後按一下 [封裝組態]。|  
|**數位簽章**|簽署封裝或從封裝中移除簽章。|在 **[SSIS]** 功能表上，按一下 **數位簽章**。<br /><br /> -或-<br /><br /> 以滑鼠右鍵按一下 [控制流程] 索引標籤之設計介面的任意位置，然後按一下 [數位簽章]。|  
|**[設定中斷點]**|啟用工作上的中斷點並設定中斷點屬性。|在 [控制流程] 索引標籤的設計介面上，以滑鼠右鍵按一下工作或容器，然後按一下 [編輯中斷點]。 若要設定封裝上的中斷點，請以滑鼠右鍵按一下 [控制流程] 索引標籤之設計介面的任意位置，然後按一下 [編輯中斷點]。|  
  
 [使用者入門] 視窗提供範例、教學課程和影片的連結。 若要加入其他內容的連結，請修改目前版本 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]隨附的 SamplesSites.xml 檔案。 建議您不要修改指定 RSS 摘要 URL 的 \<GettingStartedSamples> 元素值。 檔案位於 \<磁碟機>:\Program Files\Microsoft SQL Server\110\DTS\Binn 資料夾。 在 64 位元電腦上，檔案位於 \<磁碟機>:\Program Files(x86)\Microsoft SQL Server\110\DTS\Binn 資料夾  
  
 如果 SamplesSites.xml 檔案未損毀，請使用下列預設 xml 取代檔案中的 xml。  
  
 `<?xml version="1.0" ?>`  
  
 `- <SamplesSites>`  
  
 `<GettingStartedSamples>http://go.microsoft.com/fwlink/?LinkID=203147</GettingStartedSamples>`  
  
 `- <ToolboxSamples>`  
  
 `<Site>http://go.microsoft.com/fwlink/?LinkID=203286&query=SSIS%20{0}</Site>`  
  
 `</ToolboxSamples>`  
  
 `</SamplesSites>`  
  
 下表列出 [SSIS] 和 [檢視] 功能表，以及 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 之設計介面中可用的視窗。  
  
|視窗|目的|存取|  
|------------|-------------|------------|  
|**變數**|加入並管理自訂變數。|在 **[SSIS]** 功能表上，按一下 **變數**。<br /><br /> -或-<br /><br /> 以滑鼠右鍵按一下 [控制流程] 和 [資料流程] 索引標籤之設計介面的任意位置，然後按一下 [變數]。<br /><br /> -或-<br /><br /> 在 [檢視] 功能表上，指向 [其他視窗]，然後按一下 [變數]。|  
|**記錄事件**|檢視執行階段的記錄項目。|在 **[SSIS]** 功能表上，按一下 **記錄事件**。<br /><br /> -或-<br /><br /> 以滑鼠右鍵按一下 [控制流程] 和 [資料流程] 索引標籤之設計介面的任意位置，然後按一下 [記錄事件]。<br /><br /> -或-<br /><br /> 在 [檢視] 功能表上，指向 [其他視窗]，然後按一下 [記錄事件]。|  
  
## <a name="custom-editors"></a>自訂編輯器  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 為大多數容器、工作、來源、轉換和目的地提供自訂對話方塊。  
  
 下表描述如何存取自訂對話方塊。  
  
|編輯器類型|存取|  
|-----------------|------------|  
|容器。 如需詳細資訊，請參閱[整合服務容器](../integration-services/control-flow/integration-services-containers.md)。|在 [控制流程] 索引標籤的設計介面上，按兩下容器。|  
|工作。 如需詳細資訊，請參閱 [Integration Services Tasks](../integration-services/control-flow/integration-services-tasks.md)。|在 [控制流程] 索引標籤的設計介面上，按兩下工作。|  
|來源。|在 [資料流程] 索引標籤的設計介面上，按兩下來源。|  
|轉換。 如需詳細資訊，請參閱 [Integration Services 轉換](../integration-services/data-flow/transformations/integration-services-transformations.md)。|在 [資料流程] 索引標籤的設計介面上，按兩下轉換。|  
|目的地。|在 [資料流程] 索引標籤的設計介面上，按兩下目的地。|  
  
## <a name="advanced-editor"></a>進階編輯器  
 [進階編輯器] 對話方塊是用於設定資料流程元件的使用者介面。 它反映使用一般配置之元件的屬性。 [進階編輯器] 對話方塊不可用於具有多個輸入的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 轉換。  
  
 若要開啟此編輯器，請在 [屬性] 視窗中按一下 [顯示進階編輯器]，或以滑鼠右鍵按一下資料流程元件，然後按一下 [顯示進階編輯器]。  
  
 如果您要建立自訂來源、轉換或目的地，但不想寫入自訂使用者介面，可改用 [進階編輯器]。  
  
## <a name="sql-server-data-tools-features"></a>SQL Server Data Tools 功能  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的視窗、對話方塊和功能表選項。  
  
 以下是可用視窗和功能表的摘要。  
  
-   方案總管視窗會列出專案 (包括開發 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案) 及專案檔案。  
  
     若要依名稱排序專案中包含的封裝，請以滑鼠右鍵按一下 [SSIS 封裝] 節點，然後按一下 [依名稱排序]。  
  
-   [工具箱] 視窗會列出用於建立控制流程和資料流程的控制流程項目和資料流程項目。  
  
-   [屬性] 視窗會列出物件屬性。  
  
-   [格式] 功能表提供用於調整封裝中控制項的大小以及對齊這些控制項的選項。  
  
-   [編輯] 功能表提供用於在設計介面上複製物件的複製和貼上功能。  
  
-   [檢視] 功能表提供用於在 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中修改物件之圖形表示的選項  
  
 如需有關其他視窗和功能表的詳細資訊，請參閱 Visual Studio 文件集。  
  
## <a name="related-tasks"></a>相關工作  
 如需如何在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中建立封裝的資訊，請參閱 [在 SQL Server 資料工具中建立封裝](../integration-services/create-packages-in-sql-server-data-tools.md)  
  
## <a name="see-also"></a>另請參閱  
 [SSIS 設計師](../integration-services/ssis-designer.md)  
  
  
