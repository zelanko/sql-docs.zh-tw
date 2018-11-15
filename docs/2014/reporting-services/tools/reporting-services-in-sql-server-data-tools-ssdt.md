---
title: SQL Server Data Tools (SSDT) 中的 Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Business Intelligence Development Studio, Reporting Services in
ms.assetid: 0903c7b2-ac59-45f1-b7d0-922ecd9d76f8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: fe561dcba4a0cff5b58ef7810b27f30b1c95e228
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/10/2018
ms.locfileid: "48906298"
---
# <a name="reporting-services-in-sql-server-data-tools-ssdt"></a>SQL Server 資料工具中的 Reporting Services (SSDT)
  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 已[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]與商業智慧方案專用增強功能的環境。 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 隨附於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 您可以使用 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] 建立及管理 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 報表與報表相關項目適用的方案及專案。 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] 提供報表設計師撰寫環境。 在 [報表設計師] 中，您可以開啟、修改、預覽、儲存及部署報表定義、共用資料來源、共用資料集和報表組件。  
  
 此主題描述用於 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] 的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]方案、專案、專案範本和組態，以及您可以在 [報表設計師] 中使用的檢視、功能表、工具列和快速鍵。  
  
 若要開始設計報表，請參閱[使用報表設計師設計報表 &#40;SSRS&#41;](design-reporting-services-paginated-reports-with-report-designer-ssrs.md)。  
  
##  <a name="bkmk_SolutionsandProjects"></a> 方案與專案  
 報表專案是做為報表定義與資源的容器。 部署專案時，報表專案中的每一個檔案都會發行至報表伺服器。 當您第一次建立專案時，同時也會建立該專案的方案，以做為專案的容器。 您可以將多個專案加入單一方案。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
##  <a name="bkmk_Configurations"></a> 組態  
 若要針對不同部署建立多組專案屬性，例如企業測試和實際報表伺服器，請使用組態管理員。 如需詳細資訊，請參閱 [SQL Server 資料工具中的部署和版本支援 &#40;SSRS&#41;](deployment-and-version-support-in-sql-server-data-tools-ssrs.md)之中。  
  
##  <a name="bkmk_ReportServerProjects"></a> 報表伺服器專案  
 當您安裝 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]時， [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]提供了下列專案範本：  
  
-   **報表伺服器專案。** 當您選取報表伺服器專案時，就會開啟報表設計師。 報表伺服器專案是由 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 所安裝的商業智慧專案範本，而且可從 **[新增專案]** 對話方塊取得。 如需詳細資訊，請參閱[將新的或現有的報表新增至報表專案 &#40;SSRS&#41;](add-a-new-or-existing-report-to-a-report-project-ssrs.md)。報表伺服器專案屬性會套用至 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 專案中的所有報表和所有共用資料來源。 這些屬性包括報表伺服器的 URL 以及報表和共用資料來源的資料夾名稱。 使用 **[專案屬性頁面]** 對話方塊可檢視目前的屬性值。 若要開啟此對話方塊中，在**專案**功能表上，按一下*\<專案名稱 >* **屬性**。  
  
-   **報表伺服器專案精靈。** 當您選取報表伺服器精靈專案時，就會自動建立報表伺服器專案，而且報表精靈會開啟。 在此精靈中，您可以遵循每一頁的指示來建立報表，以便建立與資料來源的連接字串、設定資料來源認證、設計查詢、加入資料表或矩陣資料區、指定報表資料和群組、挑選字型和色彩樣式、將報表發行到報表伺服器，以及在本機預覽報表。 當您使用精靈建立報表之後，您可以在報表伺服器專案中使用報表設計師來變更報表資料和報表設計師。  
  
 ![SSDT 中的新專案範本](../../analysis-services/media/ssdt-biprojects.png "SSDT 中的新專案範本")  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
##  <a name="bkmk_ReportDesignerWindowsandPanes"></a> 報表設計師視窗和窗格  
 報表設計師支援兩種檢視：**設計**來定義報表資料和報表配置，以及**預覽**來顯示報表的轉譯的檢視。 在每個檢視中，您可以顯示多個視窗來協助設計或檢視轉譯的報表。  
  
###  <a name="bkmk_ReportDataPane"></a> 報表資料窗格  
 [報表資料] 窗格顯示內建欄位、資料來源、資料集、欄位集合、報表參數和影像。  
  
 您可以使用 [報表資料] 窗格來檢視：  
  
-   **內建欄位** ：預先定義的報表資訊，例如報表名稱或處理報表的時間。  
  
-   **資料來源** ：資料來源代表資料來源的名稱及連接。  
  
-   **資料集** ：每個資料集都會包含指定要從資料來源中擷取哪些資料的查詢。 您可以展開資料集，以便檢視資料集查詢所指定的欄位集合。  
  
     在多維度資料集的某些查詢設計工具中，您可以在 [篩選] 窗格中指定篩選，然後指出是否要建立報表參數。 若您指定報表參數選項，系統就會自動建立特殊資料集，以擴展參數的有效值清單。  根據預設，此資料集不會出現在 [報表資料] 窗格內。 如需詳細資訊，請參閱[針對多維度資料的參數值顯示隱藏的資料集 &#40;報表產生器和 SSRS&#41;](../report-data/show-hidden-datasets-for-parameter-values-multidimensional-data.md)。  
  
-   **報表參數** ：報表參數清單。 資料集查詢包含查詢參數時，可以手動或自動建立參數。  
  
-   **影像** ：可用於併入為報表中「影像」報表項目的影像清單。  
  
 [報表資料] 窗格中的資料來源和資料集代表報表定義中的元素。 [報表資料] 窗格是多個報表撰寫環境所支援的功能。 在 [報表產生器] 中，這是唯一可用於管理資料來源和資料集的窗格。 在 [報表設計師] 中，[報表資料] 窗格是與 [方案總管] 搭配使用，而後者會將共用資料來源和共用資料集列出為檔案。 [報表資料] 窗格中的共用資料來源和共用資料集，必須指向它們在 [方案總管] 中的對應「共用資料來源」和「共用資料集」。 之後，[報表資料] 窗格元素就會包含 [方案總管] 中資料檔案的參考。 專案屬性可決定是否將共用資料來源和共用資料集部署至報表伺服器或 SharePoint 網站。 如需詳細資訊，請參閱 <<c0> [ 將資料來源從內嵌轉換為共用&#40;報表產生器及 SSRS&#41;](../report-data/convert-data-sources-report-builder-and-ssrs.md)。</c0>  
  
> [!NOTE]  
>  如果您看不到 [報表資料] 窗格，請按一下 **[檢視]** 功能表上的 **[報表資料]**。 如果 [報表資料] 窗格是浮動窗格，您可以錨定它。 如需詳細資訊，請參閱[停駐報表設計師中的報表資料窗格 &#40;SSRS&#41;](dock-the-report-data-pane-in-report-designer-ssrs.md)。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
###  <a name="bkmk_GroupingPane"></a> 群組窗格  
 使用 [群組] 窗格，即可定義 Tablix 資料區的群組。 您可以定義資料表的資料列群組和詳細資料群組，以及矩陣的資料列和資料行群組。 您無法使用 [群組] 窗格定義 [圖表] 或其他資料區的群組。 如需詳細資訊，請參閱[了解群組 &#40;報表產生器及 SSRS&#41;](../report-design/understanding-groups-report-builder-and-ssrs.md)。  
  
 [群組] 窗格有兩種模式：  
  
-   **預設值。** 使用 **[預設值]** 模式以階層格式顯示所有資料列及資料行群組，其中顯示父群組、子群組、相鄰群組及詳細資料群組的關聯性。 子群組會顯示在下一個縮排層級 (相較於其父群組而言) 的下方。 相鄰群組會與其對等或同層級群組顯示在相同的縮排層級上。  
  
     您可以使用預設模式來加入、編輯或刪除群組。 若為以單一資料集欄位為基礎的群組，則可以將欄位拖曳至 [資料列群組] 或 [資料行群組] 窗格。 您可以在現有的群組上方或下方插入群組。 若要加入相鄰群組，請以滑鼠右鍵按一下同層級群組，然後使用快速鍵功能表。 若要顯示屬於某個群組的 Tablix 資料格，請選取 [群組] 窗格中的群組。  
  
-   **進階：** 使用 **[進階]** 模式以顯示所選取 Tablix 資料區的靜態及動態資料列與資料行群組成員。  您必須使用群組成員來設定可控制與群組或群組成員相關聯之資料列和資料行可見性的屬性，或轉譯器用於嘗試將群組保持在同一頁的規則。 群組成員會顯示在設計介面上，當做資料列群組和資料行群組區域中的資料格。  
  
> [!NOTE]  
>  若要切換 **[預設值]** 與 **[進階]** 模式，請以滑鼠右鍵按一下 **[資料行群組]** 圖示右邊的向下箭頭。  
  
 如需詳細資訊，請參閱＜ [Grouping Pane](grouping-pane.md)＞。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
###  <a name="bkmk_Toolbox"></a> 工具箱  
 [工具箱] 包含可讓您拖曳至設計介面的報表項目。 資料區是指您用於在報表上組織資料的報表項目。 [資料表]、[矩陣]、[清單]、[圖表]、[量測計]、[資料橫條]、[走勢圖] 和 [指示器] 都是資料區。 其他報表項目包含 [地圖]、[文字方塊]、[矩形]、[線條]、[影像] 和 [子報表]。 如果您的系統管理員已經安裝並註冊自訂報表項目，這些項目可能也會顯示在此清單上。  
  
###  <a name="bkmk_PropertiesPane"></a> 屬性窗格  
 [屬性] 窗格是標準的 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 視窗，其中針對設計介面上目前選取的報表項目顯示屬性名稱和值。 在大部分情況下，屬性 (property) 名稱會對應至報表定義語言 (RDL) 檔案中的元素和屬性 (attribute)。 您可以使用選取項目的 [屬性] 對話方塊來設定最常用的屬性。 若要開啟對應的對話方塊，請按一下 [屬性] 窗格工具列上的 **[屬性頁]** 按鈕。 進階使用者可以直接在 [屬性] 窗格中設定屬性值。  
  
 您可以使用 [屬性] 窗格以：  
  
-   設定設計介面上目前所選取項目的屬性。 某些屬性會提供值的下拉式清單。 您也可以直接在資料格中輸入值。 某些屬性會包含值的集合，以 [(集合)] 值表示。 大部分屬性都可以接受運算式。複雜運算式會以 **\<運算式>** 值表示。 按一下 **\<運算式>** 開啟 [運算式] 對話方塊。 如需詳細資訊，請參閱＜ [Expression Dialog Box](../expression-dialog-box.md)＞。  
  
-   您可以使用 [屬性] 窗格工具列按鈕，將方格從類別目錄檢視變更為字母順序檢視。 在類別目錄檢視中，您可能必須展開類別目錄，才能看見底下的所有屬性。 若要開啟項目的 [屬性] 對話方塊，請按一下工具列上的 **[屬性頁]** 按鈕，或以滑鼠右鍵按一下項目，然後按一下 **[屬性]**。  
  
-   設定 [群組] 窗格中目前所選取群組成員的屬性。 群組成員屬性可協助控制每個群組執行個體之靜態群組頁首及頁尾資料列的重複方式。 如需詳細資訊，請參閱[與群組一起顯示頁首和頁尾 &#40;報表產生器及 SSRS&#41;](../report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)。  
  
 若要顯示 [屬性] 窗格，請在 **[檢視]** 功能表中，按一下 **[屬性視窗]**。 您可以取消停駐此窗格並將它移至 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]視窗的其他區域，或將它顯示成設計介面上的索引標籤式檢視。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
###  <a name="bkmk_SolutionExplorer"></a> 方案總管  
 [方案總管] 是標準的 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 元件，它會顯示專案中的所有項目。 若為報表伺服器專案，這包含用於組織共用資料來源、共用資料集、報表及資源的資料夾。 開啟方案檔時，會自動依字母順序來排列資料夾項目。 若要檢視 [屬性] 窗格中的項目屬性，請選取項目。  
  
###  <a name="bkmk_Output"></a> 輸出  
 當您預覽報表時，[輸出] 視窗就會顯示處理錯誤，而當您部署報表或共用資料來源時，則會顯示發行錯誤。  
  
 使用 [輸出] 及 [文件大綱] 視窗，即可協助偵錯運算式中的錯誤。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
###  <a name="bkmk_DocumentOutline"></a> 文件大綱  
 [文件大綱] 視窗會顯示報表定義中所有報表項目的階層式清單。 若要開啟 [文件大綱] 窗格，請在 **[檢視]** 功能表中，指向 **[其他視窗]** ，然後按一下 **[文件視窗]**。  
  
 您可以使用 [文件大綱] 窗格以協助依名稱識別文字方塊及其他報表項目。 在 [文件大綱] 中選取項目時，也會在 [設計介面] 上選取該項目。  
  
###  <a name="bkmk_TaskList"></a> 工作清單  
 當您從 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Access 等其他應用程式匯入報表時，[工作清單] 視窗就會顯示不支援功能的建立錯誤。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
##  <a name="bkmk_ReportDesignerDesignView"></a> 報表設計師設計檢視  
 當您建立報表伺服器專案時，預設會以 [設計檢視] 開啟 [報表設計師]，並顯示設計介面。 設計介面預設會顯示報表主體及報表背景。  
  
 背景的快速鍵功能表會提供加入頁首和頁尾的選項，以及在 [檢視] 功能表中，提供顯示尺規和 [群組] 窗格的選項。  
  
 您可以使用顯示比例控制項來增加或減少報表的縮放比例。  
  
 若要設計報表，請將報表項目從 [工具箱] 拖曳至設計介面，然後設定其屬性，並改變它們在報表上的排列方式。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
##  <a name="bkmk_ReportDesignerPreview"></a> 報表設計師預覽  
 使用 [預覽]，即可執行報表並在報表檢視器中檢視轉譯的報表。 [預覽] 會在本機快取報表資料。 您也可以將組態屬性設定成使用瀏覽器並在偵錯檢視中執行報表。  
  
 當您預覽報表時，報表設計師就會連接至報表資料來源、執行資料集查詢、在本機電腦上快取資料、處理報表以結合資料和配置，以及轉譯報表。 您可以在 [預覽] 索引標籤中檢視報表，也可以設定專案屬性，以便在偵錯模式中檢視報表，以及直接在瀏覽器中檢視報表。  
  
-   **預覽參數化報表。** 當您預覽報表時，如果所有報表參數都具有有效的預設值，系統就會自動處理報表。 如果一或多個報表參數沒有有效的預設值，您就必須針對每個未指派的參數選擇值，然後在報表工具列上，按一下 **[檢視報表]**。  
  
-   **了解本機資料快取** ：當您預覽報表時，報表處理器就會使用目前的參數預設值以執行報表中資料集的所有查詢，然後將結果儲存為本機資料快取 (.rdl.data) 檔案。 如果您沒有對報表資料集查詢或報表參數進行任何變更，就可以繼續設計報表，而不會造成再次擷取這項資料的負擔。  
  
-   **使用 [組態管理員] 和 [偵錯] 來預覽報表。** 在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，專案屬性會定義您想要如何部署和偵錯報表。 這些屬性會套用至專案中的所有報表和共用資料來源。 若要設定專案屬性，請在 **[專案]** 功能表中，按一下 **[屬性]**。 您可以使用這些設定來測試專案，並將它們發行至報表伺服器。  
  
-   **監視 [輸出] 窗格是否有錯誤訊息。** 當您預覽報表，而且報表處理器偵測到問題時，它就會將錯誤訊息寫入 [輸出] 窗格。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
##  <a name="bkmk_ReportDesignerMenus"></a> 報表設計師的功能表  
 當報表設計師專案在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中作用時，下列工具列就會加入至主要工具列。 報表設計師的功能表只會在 [設計] 檢視中顯示。  
  
###  <a name="FormatMenu"></a> 格式功能表  
 當您在設計介面上選取項目時， **[格式]** 功能表就會包含下列選項：  
  
-   **前景色彩** ：選取文字色彩。 黑色是預設文字色彩。  
  
-   **背景色彩** ：為您的文字方塊和資料區選取背景色彩。  
  
-   **字型** ：指定文字是粗體、斜體或加上底線。  
  
-   **左右對齊** ：指定文字是靠右對齊、置中或靠左對齊。  
  
-   **對齊** ：指定選取物件在報表內彼此對齊的方式。  
  
-   **設定成相同大小** ：調整選取物件在報表內的大小。  
  
-   **水平間距** ：調整選取物件在報表內的水平間距。  
  
-   **垂直間距** ：調整選取物件在報表內的垂直間距。  
  
-   **對齊表單中央** ：讓選取物件在報表設計師視窗內垂直及水平地對齊中央。  
  
-   **順序** ：將選取物件移至背景或前景。  
  
###  <a name="ReportMenu"></a> 報表功能表  
 當報表設計介面取得焦點時， **[報表]** 功能表就會包含下列選項：  
  
-   **報表屬性** ：選取即可開啟 **[報表屬性]** 對話方塊。 在這個對話方塊中，您可以指派一般報表屬性，例如作者名稱和方格間距，以及指定報表配置的屬性，例如資料行數和頁面大小。 您也可以包括自訂程式碼、組件和類別的參考、資料輸出元素的名稱、資料轉換和資料結構描述。  
  
-   **檢視** ：在兩個報表設計師索引標籤之間切換：[設計] 和 [預覽]。  
  
-   **頁首** ：在報表中加入或刪除頁首。 當您刪除頁首時，就會刪除頁首中的所有項目。  
  
-   **頁尾** ：在報表中加入或刪除頁尾。 當您刪除頁尾時，就會刪除頁尾中的所有項目。  
  
-   **群組窗格** ：顯示或隱藏 [群組] 窗格。  
  
###  <a name="ViewMenu"></a> 檢視功能表  
 您可以使用 **[檢視]** 功能表來顯示報表設計師視窗和工具列。  
  
-   **錯誤清單** ：使用這個選項，即可顯示發行或預覽報表時所偵測的錯誤。  
  
-   **輸出** ：使用這個選項，即可顯示發行或處理報表時所偵測的錯誤，或在報表顯示文字「#錯誤」時提供運算式錯誤的詳細資訊。  
  
-   **屬性視窗** ：使用這個選項，即可顯示設計介面上目前選取之報表項目的屬性值。 若要查看巢狀報表項目的屬性，您必須按許多次報表項目，才能循環瀏覽報表項目及其巢狀成員的階層。 您可以檢查顯示在 [屬性] 窗格頂端的項目名稱，以便查看顯示了哪一個報表項目的屬性。  
  
-   **工具箱** ：使用這個選項，即可顯示 [工具箱]。  
  
-   **其他視窗** ：使用這個選項，即可顯示下列窗格：  
  
    -   **文件大綱** ：使用這個選項，即可顯示報表中報表項目及其文字方塊集合的階層式檢視。  
  
-   **工具列** ：使用這個選項，即可顯示支援報表設計師功能的工具列，包括 **[報表框線]** 和 **[報表格式]**。 如需詳細資訊，請參閱「 [報表設計師的工具列](#bkmk_ReportDesignerToolbars)」。  
  
-   **報表資料** ：使用這個選項，即可顯示 [報表資料] 窗格，而且您可以在其中加入報表參數、資料來源、資料集和影像。  
  
###  <a name="ProjectMenu"></a> 專案功能表  
 您可以使用 **[專案]** 功能表來管理專案中的共用資料來源和報表。 當您在專案中加入或移除項目時，就會自動更新 [方案總管] 中專案項目的階層式顯示。  
  
-   **加入新項目** ：在專案中加入新的共用資料來源或新的報表。  
  
-   **加入現有項目** ：在專案中加入現有的共用資料來源或現有的報表。  
  
-   **匯入報表** ：從其他應用程式匯入報表，例如 Microsoft Access。  
  
-   **從專案移除** ：從專案中排除項目。 這個選項並不會從檔案系統中刪除項目。  
  
-   **顯示所有檔案** ：顯示專案中的所有檔案。  
  
-   **重新整理專案工具箱項目** ：當您在專案中安裝新的自訂報表項目時，重新整理工具箱快取。  
  
-   **屬性** ：開啟這個專案的 **[屬性頁]** 對話方塊。 如需詳細資訊，請參閱 [專案屬性頁對話方塊](project-property-pages-dialog-box.md)。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
##  <a name="bkmk_ReportDesignerToolbars"></a> 報表設計師的工具列  
 報表設計師會提供下列可在設計報表時使用的專用工具列：  
  
-   **報表** ：加入頁首或頁尾、設定報表屬性、切換尺規或 [群組] 窗格，或使用顯示比例來變更報表的檢視。  
  
-   **報表框線** ：設定所有選取線條的色彩、樣式和寬度，以及所有選取報表項目的框線。  
  
-   **報表格式** ：設定選取報表項目的格式。 若為文字方塊，您就可以使用此工具列來變更下列格式類型：字型屬性和文字色彩、背景色彩，以及文字對齊。  
  
-   **配置** ：設定資料區內報表項目和合併資料格的繪製順序。  
  
-   **標準** ：開啟或儲存專案、顯示視窗，以及選取偵錯組態。  
  
 您可以使用 **[檢視]** 功能表來控制是否要顯示這些工具列。 如果其他 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 工具列的功能不適用於報表設計師功能，這些工具列的功能可能會停用。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
##  <a name="bkmk_SourceControl"></a> 原始檔控制  
 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] 可以與來源外掛程式整合。您可以使用 **[選項]** 對話方塊中的 [專案和方案] 頁面，以指定外掛程式，並設定屬性。  
  
##  <a name="bkmk_CustomReportTemplates"></a> 自訂報表範本  
 若要使用自訂報表做為新報表的範本，您只需將自訂報表複製到裝有 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] 之電腦上的 ReportProject 資料夾即可。 根據預設，此資料夾位於\<磁碟機 >: \Program Files\Microsoft Visual Studio 10.0\Common7\IDE\Private Assemblies\ProjectItems\ReportProject。 將新項目加入報表專案時，您的自訂報表會顯示在 [範本] 窗格中。  
  
 您也可以將自訂樣式加入報表精靈。  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
##  <a name="bkmk_CommandLineSupportForssdt"></a> SQL Server 資料工具的命令列支援  
 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] 根據[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 10.0 以及基礎 devenv.exe 應用程式。 您必須先為下列兩個項目設定有效的值，才能使用這些選項：  
  
-   OverwriteDataSources、TargetDataSourceFolder、TargetReportFolder 和 TargetServerURL 的專案屬性。  
  
-   至少一組組態屬性，例如「偵錯」或「發行」。  
  
 如需詳細資訊，請參閱＜ [Publishing Data Sources and Reports](../reports/publishing-data-sources-and-reports.md)＞。  
  
 針對報表伺服器專案，您可以從命令列指定下列選項：  
  
-   **/deploy** ：使用組態檔中指定的專案屬性來部署報表。 例如，下列命令會使用專案屬性中指定的「發行」組態設定，部署方案檔 Reports.sln 所指定的報表。  
  
    ```  
    devenv.exe "C:\Users\MyUser\Documents\Visual Studio 2010\Projects\Reports\Reports.sln" /deploy "Release"  
    ```  
  
-   **/build** ：建立但不部署方案檔。 例如，下列命令會使用專案屬性中指定的「偵錯」組態設定，建立方案檔 Reports.sln 所指定的報表。  
  
    ```  
    devenv.exe "C:\Users\MyUser\Documents\Visual Studio 2010\Projects\Reports\Reports.sln" /build "Debug"  
    ```  
  
-   **/out** ：將建立方案的輸出重新導向至指定檔案。 例如，下列命令會將上一個範例中的組態輸出，重新導向到名為 mybuildlog.txt 的檔案。  
  
    ```  
    devenv.exe "C:\Users\MyUser\Documents\Visual Studio 2010\Projects\Reports\Reports.sln" /build "Debug" /out mybuildlog.txt  
    ```  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
##  <a name="bkmk_KeyboardShortcuts"></a> Reporting Services 中的鍵盤快速鍵  
 您可以使用鍵盤快速鍵以：  
  
-   控制 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]中的視窗和模式：  
  
    |描述|按鍵組合|  
    |-----------------|---------------------|  
    |建立選取的專案|CTRL+SHIFT+B|  
    |顯示 [屬性] 視窗|F4|  
    |顯示資料視窗|CTRL+Alt+D|  
    |開始偵錯|F5|  
    |從某個開啟的視窗移至下一個|F6|  
  
-   控制報表設計介面上的項目：  
  
    |描述|按鍵組合|  
    |-----------------|---------------------|  
    |將焦點從某個報表項目移到下一個報表項目|TAB|  
    |移動選取的報表項目|方向鍵|  
    |微調選取的報表項目|CTRL+方向鍵|  
    |增加或減少選定報表項目的大小|CTRL+SHIFT+方向鍵|  
    |在文字方塊中，將游標移到可見之顯示文字的開頭|CTRL+HOME|  
    |在文字方塊中，將游標移到可見之顯示文字的結尾|CTRL+END|  
    |在文字方塊中，選取從目前游標位置到可見之顯示文字開頭的文字|SHIFT+HOME|  
    |在文字方塊中，選取從目前游標位置到可見之顯示文字結尾的文字|SHIFT+END|  
    |在文字方塊中，選取從目前游標位置到運算式開頭的文字|CTRL+SHIFT+HOME|  
    |在文字方塊中，選取從目前游標位置到運算式結尾的文字|CTRL+SHIFT+END|  
    |開啟選定報表項目的快速鍵功能表|較新鍵盤上的 SHIFT+F10+屬性鍵|  
  
 ![搭配 [回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示") [回到頁首](#bkmk_Top)  
  
## <a name="see-also"></a>另請參閱  
 [方案總管](../../ssms/solution/solution-explorer.md)   
 [Reporting Services 報表 &#40;SSRS&#41;](../reports/reporting-services-reports-ssrs.md)   
 [報表定義語言 &#40;SSRS&#41;](../reports/report-definition-language-ssrs.md)   
 [SQL Server 資料工具中的部署和版本支援 &#40;SSRS&#41;](deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  
  
  
