---
title: 使用控制流程套件組件以在各套件間重複使用控制流程 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.toolboxcontrolflowtemplate.f1
- sql13.dts.designer.addcopyexistingtemplate.f1
- sql13.dts.designer.addcopyexistingpackagepart.f1
- sql13.dts.designer.packagepart.general.f1
ms.assetid: 1edc91d9-1fab-4fe5-aed3-6f581fe32c18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5951daccc88e8593c27365254d208c4b2ee84118
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753786"
---
# <a name="reuse-control-flow-across-packages-by-using-control-flow-package-parts"></a>使用控制流程封裝組件在封裝之間重複使用控制流程
  將常用的控制流程工作或容器儲存到獨立的組件檔案 (“.dtsxp” 檔案)，並使用控制流程封裝組件在一或多個封裝中多次重複使用。 這個再使用性讓 SSIS 封裝的設計和維護變得更容易。  
  
## <a name="create-a-new-control-flow-package-part"></a>建立新的控制流程封裝組件  
 若要建立新的控制流程封裝組件，請在方案總管中展開 [封裝組件]  資料夾。 以滑鼠右鍵按一下 [控制流程]，然後選取 [New Control Flow Package Part (新增控制流程封裝組件)]。  
  
 ![建立新的控制流程範本](../integration-services/media/control-flow-templates-create-new.png "建立新的控制流程範本")  
  
 [封裝組件] | [控制流程] 資料夾下即會建立新的組件檔案，副檔名為 ".dtsxp"。 同時，具有相同名稱的新項目也會加入 SSIS 工具箱中。 (只有在 Visual Studio 中開啟包含組件的專案，才會顯示工具箱項目。)  
  
 ![工具箱中的控制流程範本](../integration-services/media/control-flow-templates-in-toolbox.png "工具箱中的控制流程範本")  
  
## <a name="design-a-control-flow-package-part"></a>設計控制流程封裝組件  
 若要開啟封裝組件編輯器，請按兩下方案總管中的組件檔案。 設計組件就像設計封裝一樣。  
  
 ![控制流程範本設計的步驟 1](../integration-services/media/control-flow-template-design-step-1.png "控制流程範本設計的步驟 1")  
  
 ![控制流程範本設計的步驟 2](../integration-services/media/control-flow-template-design-step-2.png "控制流程範本設計的步驟 2")  
  
 控制流程封裝組件具有下列限制。  
  
-   組件只能有一個最上層工作或容器。 如果想要包含多個工作或容器，請將它們全部放在單一序列容器中。  
  
-   您無法在設計工具中直接執行或偵錯組件。  
  
## <a name="add-an-existing-control-flow-package-part-to-a-package"></a>將現有的控制流程封裝組件加入封裝中  
 您可以重複使用儲存在目前 Integration Services 專案或不同專案中的組件。  
  
-   若要重複使用屬於目前專案的組件，請從 [工具箱] 拖放組件。  
  
-   若要重複使用屬於不同專案的組件，請使用 [Add Existing Control Flow Package Part] (加入現有的控制流程封裝組件)  命令。  
  
### <a name="drag-and-drop-a-control-flow-package-part"></a>拖放控制流程封裝組件  
 若要重複使用專案中的組件，只要從 [工具箱] 拖放組件項目，就像拖放任何其他工作或容器一樣。 組件可以多次拖放到封裝，在封裝中的多個位置重複使用邏輯。 使用這個方法重複使用屬於目前專案的組件。  
  
 ![將控制流程範本新增至套件](../integration-services/media/control-flow-templates-add-to-package.png "將控制流程範本新增至套件")  
  
 ![具有多個控制流程範本的套件](../integration-services/media/control-flow-templates-in-package.png "具有多個控制流程範本的套件")  
  
 當您儲存封裝時，SSIS 設計工具會檢查封裝中是否有任何組件執行個體。  
  
-   如果封裝包含組件執行個體，則設計工具會產生包含所有組件相關資訊的新 .dtsx.designer 檔案。  
  
-   如果封裝不使用組件，則設計工具會刪除之前建立的任何封裝 .dtsx.designer 檔案 (也就是任何與封裝同名的 .dtsx.designer 檔案)。  
  
 ![具有控制流程範本的方案總管](../integration-services/media/control-flow-templates-in-solution-explorer.png "具有控制流程範本的方案總管")  
  
### <a name="add-a-copy-of-an-existing-control-flow-package-part-or-a-reference-to-an-existing-part"></a>將現有的控制流程封裝組件或參考的複本加入現有的組件  
 若要將檔案系統中現有的組件加入封裝中，請在方案總管中展開 [封裝組件]  資料夾。 以滑鼠右鍵按一下 [控制流程]，然後選取 [Add Existing Control Flow Package Part (加入現有的控制流程封裝組件)]。  
  
 ![從功能表新增控制流程範本](../integration-services/media/control-flow-templates-add-from-menu.png "從功能表新增控制流程範本")  
  
 ![新增現有範本的副本對話方塊](../integration-services/media/control-flow-templates-add-copy-dialog.png "新增現有範本的副本對話方塊")  
  
 **選項。**  
  
 **封裝組件路徑**  
 輸入組件檔案路徑，或按一下瀏覽按鈕 (…)，找出要複製或參考的組件檔案。  
  
 **加入為參考**  
 -   如果選取，則組件會加入 Integration Services 專案作為參考。 當您要在多個 Integration Services 專案中參考某個組件檔案的單一複本時，請選取這個選項。  
  
-   如果取消選取，則組件檔案的複本就會加入專案中。  
  
## <a name="configure-a-control-flow-package-part"></a>設定控制流程封裝組件  
 若要在控制流程封裝組件加入封裝的控制流程之後設定它們，請使用 [Package Part Configuration] (封裝組件組態)    對話方塊。  
  
#### <a name="to-open-the-package-part-configuration-dialog-box"></a>開啟 [Package Part Configuration] (封裝組件組態) 對話方塊  
  
1.  若要設定組件執行個體，請按兩下控制流程中的組件執行個體。 或以滑鼠右鍵按一下組件執行個體並選取 [編輯]。 [Package Part Configuration] (封裝組件組態)  對話方塊隨即開啟。  
  
2.  設定組件執行個體的屬性和連線管理員。  
  
### <a name="properties-tab"></a>屬性索引標籤  
 使用 [Package Part Configuration] (封裝組件組態)  對話方塊的 [屬性]   索引標籤來指定組件的屬性。  
  
 ![[範本設定] 對話方塊的 [內容] 索引標籤](../integration-services/media/template-configuration-properties-tab.png "[範本設定] 對話方塊的 [內容] 索引標籤")  
  
 左窗格的樹狀檢視階層架構會列出組件執行個體所有可設定的屬性。  
  
-   如果取消選取，就不會在組件執行個體中設定屬性。 在控制流程封裝組件中定義的組件執行個體會使用屬性的預設值。  
  
-   如果選取，您所輸入或選取的值就會覆寫預設值。  
  
 右窗格中的資料表會列出要設定的屬性。  
  
-   **屬性路徑**。 屬性的屬性路徑。  
  
-   **屬性類型**。 屬性的資料型別。  
  
-   **值**。 已設定的值。 這個值會覆寫預設值。  
  
### <a name="connection-managers-tab"></a>[連線管理員] 索引標籤  
 使用 [Package Part Configuration] (封裝組件組態)   對話方塊的 [連線管理員]   索引標籤來指定組件執行個體的連線管理員屬性。  
  
 ![[範本設定] 對話方塊的 [連線管理員] 索引標籤](../integration-services/media/template-configuration-connection-managers-tab.png "[範本設定] 對話方塊的 [連線管理員] 索引標籤")  
  
 左窗格中的資料表會列出控制流程組件中所定義的所有連線管理員。 選擇您要設定的連線管理員。  
  
 右窗格中的清單會列出所選連線管理員的屬性。  
  
-   **設定**。 檢查是否已為組件執行個體設定屬性。  
  
-   **屬性名稱**。 屬性的名稱。  
  
-   **值**。 已設定的值。 這個值會覆寫預設值。  
  
## <a name="delete-a-control-flow-part"></a>刪除控制流程組件  
 若要刪除組件，請在方案總管中以滑鼠右鍵按一下組件，然後選取 [刪除]。 選取 [確定]  確認刪除，或選取 [取消]  保留組件。  
  
 如果您刪除了專案的組件，它就會從檔案系統永久刪除，且無法還原。  
  
> [!NOTE]  
>  如果您要移除 Integration Services 專案的組件，但希望在其他專案中繼續使用，請使用 [從專案移除] 選項，不要使用 [刪除] 選項。  
  
## <a name="package-parts-are-a-design-time-feature-only"></a>封裝組件只是設計階段功能  
 封裝組件只是設計階段功能。 SSIS 設計工具會建立、開啟、儲存和更新組件，並且加入、設定或刪除封裝中的組件執行個體。 不過，SSIS 執行階段並不知道組件。 以下是設計工具達到這種區隔的方法。  
  
-   設計工具會將封裝組件執行個體及其設定的屬性儲存到 “.dtsx.designer” 檔案。  
  
-   當設計工具儲存 “.dtsx.designer” 檔案時，它也會解壓縮這個檔案參考的組件內容，用組件的內容取代封裝的組件執行個體。  
  
-   最後，不再包含組件資訊的所有內容，會存回到 “.dtsx” 封裝檔案。 這就是 SSIS 執行階段執行的檔案。  
  
 下圖示範組件 (“.dtsxp” 檔案)、SSIS 設計工具和 SSIS 執行階段之間的關聯性。  
  
 ![控制流程範本的檔案和流程](../integration-services/media/control-flow-templates-intro.png "控制流程範本的檔案和流程")  
  
  
