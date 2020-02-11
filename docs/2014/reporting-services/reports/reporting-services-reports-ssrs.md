---
title: Reporting Services 報表 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, report creation
ms.assetid: 52ed9e74-f2c8-488b-a2c2-6dfbc2a2c8cc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 97e99e90d50b6a033f8cc2fe12ce3233ee56c959
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102465"
---
# <a name="reporting-services-reports-ssrs"></a>Reporting Services 報表 (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]報表是以 XML 為基礎的報表定義，其中包括報表資料和報表配置元素。 在用戶端檔案系統上，報表定義的副檔名為 .rdl。 在發行報表之後，其為儲存在報表伺服器或 SharePoint 網站上的報表項目。 報表是由 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 提供之伺服器架構報表平台的一部分。  
  
 若您是第一次使用 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]，請務必檢閱 [Reporting Services 概念 &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md) 中的資訊。  
  
## <a name="benefits-of-reporting-services-reports"></a>Reporting Services 報表的優點  
 您可使用 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 報表方案來：  
  
-   使用提供單一版本事實的一組資料來源。 讓報表以這些資料來源為基礎，提供統一的資料檢視，以協助商業性決策的制定。  
  
-   使用資料區，以多元互連方式將資料視覺化。 顯示以資料表、矩陣或交叉分析、展開或摺疊群組、圖表、量測計、指標或 KPI 與地圖之形式所組織的資料，且能夠在資料表中建立巢狀圖表。  
  
-   檢視自己所需的報表，或將報表發行至報表伺服器或 SharePoint 網站以與小組或組織共用。  
  
-   只定義報表一次並用各種方式來顯示。 您可將報表匯出為多種檔案格式，或以電子郵件形式將報表傳遞到訂閱者或共用的檔案。 您也可以建立套用個別參數集至相同報表定義的多個連結報表。  
  
-   使用報表組件、共用資料來源、共用查詢和子報表，以定義重複使用的資料視覺效果。  
  
-   分開管理報表資料來源與報表定義。 例如，您可將測試資料來源變更為實際資料來源，而無須變更報表。  
  
-   以自由形式的配置設計報表。 報表配置不會受限於帶狀的資訊。 您可使用有利於理解力、洞察能力與行動力的方式來組織頁面上顯示的資料。  
  
-   可啟用鑽研動作、展開/摺疊切換、排序按鈕、工具提示及報表參數，以利報告讀取器與報表互動。 使用搭配您撰寫之運算式的報表參數，可讓報告讀取器控制資料篩選、分組及排序的方式。  
  
-   定義運算式，可讓您擁有自訂報表資料篩選、分組及排序方式的能力。  
  
 ![rs_GettingStartedReport](../media/rs-gettingstartedreport.gif "rs_GettingStartedReport")  
  
##  <a name="bkmk_StagesSummary"></a>報表處理的階段  
 建立報表時，您會定義一個 XML 格式的報表定義檔案 (.rdl)。 這個檔案包含報表處理器結合報表資料與報表配置所需的所有資訊。 當您檢視報表時，會透過下列階段來處理報表：  
  
-   **正常.** 評估報表定義中的運算式，並在報表伺服器內部儲存編譯的中繼格式。  
  
-   **流程.** 執行資料集查詢，並將資料與配置合併為中繼格式。  
  
-   **使得.** 將處理的報表傳送至轉譯延伸模組，以判斷可在每個頁面上納入多少資訊並建立分頁的報表。  
  
-   **匯出（選擇性）。** 將報表匯出至不同的檔案格式。  
  
 如需詳細資訊，請參閱 [Reporting Services 概念 &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md#bkmk_StagesofReports) 中的[報表開發階段](../reporting-services-concepts-ssrs.md)。  
  
## <a name="create-reports"></a>建立報表  
 若要建立報表：  
  
-   **判斷報表的用途。** 依據使用報表的對象來識別報表的用途。 設計良好的報表會將具備洞察能力與行動力的資訊提供給報告讀取器。 在此步驟決定的設計決策會影響您所選的報表參數、報表配置設計及報表檢視經驗。 如需詳細資訊，請參閱 msdn.microsoft.com 之[報表產生器文件](../report-design/planning-a-report-report-builder.md)中的[規劃報表 &#40;報表產生器&#41;](../report-design/report-design-tips-report-builder-and-ssrs.md) 和[報表設計提示 &#40;報表產生器及 SSRS&#41;](https://go.microsoft.com/fwlink/?LinkId=154494)。  
  
-   **選取查詢的類型。** 判斷是否要使用一般化的共用資料集查詢，或專屬於您的一組報表的資料集查詢。 含有一般化查詢的共用資料集在多份報表使用中較易於維護，但每個報表設計師必須依據其特定的一組報表來篩選所需的資料。 如需詳細資訊，請參閱[報表資料 &#40;SSRS&#41;](../report-data/report-data-ssrs.md)。  
  
-   **規劃相關資料的視圖。** 規劃報表讀取器的檢視經驗。 若要處理大量資料時，利用具備向下鑽研詳細資料能力的摘要報表是很實用的方法。 如需詳細資訊，請參閱 [鑽研、向下鑽研、子報表和巢狀資料區 &#40;報表產生器及 SSRS&#41;](../report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)。  
  
-   **設定許可權。** 規劃授與適當權限等級的策略。 常用的策略是在報表伺服器上建立一個資料夾結構，並依據角色和資料夾安全性來授與報表及報表相關項目的存取權。 如需詳細資訊，請參閱＜ [確保報表安全性](#bkmk_SecureReportsSummary)。  
  
-   **選擇撰寫環境。** 撰寫工具在功能支援上各不相同。 如需詳細資訊，請參閱 [Reporting Services 工具](../tools/reporting-services-tools.md)。  
  
-   針對每份報表：  
  
    -   **識別資料來源。** 為每個資料來源定義報表資料來源。 如需詳細資訊，請參閱 [Reporting Services 中的資料連接、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
    -   **選擇要從每個來源使用的資料。** 為每個資料來源定義報表資料集。 每個資料集都包括查詢，以指定要使用的資料。 若您有報表參數，定義資料集可擴展每個參數可用的值清單。 如需詳細資訊，請參閱[將資料加入至報表 &#40;報表產生器及 SSRS&#41;](../report-data/report-datasets-ssrs.md) 和[報表參數 &#40;報表產生器和報表設計師&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)。  
  
    -   **選擇資料視覺效果。** 為每個資料集選擇要顯示資料的資料區。 從資料表、圖表、量測計及地圖清單中選擇。 如需詳細資訊，請參閱下列主題：  
  
        -   [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
        -   [圖表 &#40;報表產生器及 SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)  
  
        -   [走勢圖和資料橫條 &#40;Report Builder and SSRS&#41;](../report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
        -   [指標 &#40;報表產生器及 SSRS&#41;](../report-design/indicators-report-builder-and-ssrs.md)  
  
        -   [地圖 &#40;報表產生器及 SSRS&#41;](../report-design/maps-report-builder-and-ssrs.md)  
  
        -   [量測計 &#40;報表產生器及 SSRS&#41;](../report-design/gauges-report-builder-and-ssrs.md)  
  
    -   **自訂資料和版面配置。** 設計報表配置。 報表定義包含報表主體、資料來源、資料集、資料區、文字方塊、線條和影像。 矩形可以當做配置與視覺化元素的容器使用。 藉由撰寫運算式，並控制篩選、群組、排序、格式及顯示資料，以自訂每個資料區。 加入報表名稱、位置及其他識別資訊，以利管理數十份或數百份報表。 加入視覺化元素及容器以組織頁面上的配置元素。 如需詳細資訊，請參閱下列主題：  
  
        -   [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
        -   [報表參數 &#40;報表產生器和報表設計師&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
        -   [運算式 &#40;報表產生器及 SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
        -   [設定報表項目的格式 &#40;報表產生器及 SSRS&#41;](../report-design/formatting-report-items-report-builder-and-ssrs.md)  
  
        -   [影像、文字方塊、矩形和線條 &#40;報表產生器及 SSRS&#41;](../report-design/rectangles-and-lines-report-builder-and-ssrs.md)  
  
        -   [頁面配置和轉譯 &#40;報表產生器及 SSRS&#41;](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md)  
  
    -   **設定互動功能。** 為您的報告讀取器加入互動功能。 例如，加入檢視查詢的排序按鈕或切換項目。 如需詳細資訊，請參閱[互動式排序、文件引導模式及連結 &#40;報表產生器及 SSRS&#41;](../report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)。  
  
    -   **複習並逐一查看設計。** 預覽報表。 發行初步版本以取得報告讀取器的意見。 逐一查看設計。  
  
-   **審查報表解決方案。** 請確認此組報表有正確互動。  
  
-   **請考慮可重複使用的元件。**  判斷是否有任何資料來源或資料集查詢可共用及重複使用。 如果有，可以在報表伺服器或 SharePoint 網站上建立共用資料來源和共用資料集。 判斷資料區是否適合重複使用為報表組件。 如需詳細資訊，請參閱[報表設計師中的報表組件 &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md)。  
  
## <a name="preview-reports"></a>預覽報表  
 每個報表撰寫工具都支援預覽報表。 如需詳細資訊，請參閱 msdn.microsoft.com 之[報表產生器文件](../tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_Preview)中的[預覽](../tools/report-builder-authoring-environment-ssrs.md)、[報表產生器 &#40;SSRS&#41;](../report-builder/previewing-reports-in-report-builder.md) 和[在報表產生器中預覽報表](https://go.microsoft.com/fwlink/?LinkId=154494)。  
  
## <a name="save-or-publish-reports"></a>儲存或發行報表  
 每個報表撰寫工具都支援本機儲存報表，或是將報表發行至報表伺服器或 SharePoint 網站。 如需詳細資訊，請參閱 msdn.microsoft.com 之[報表產生器文件](../tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_SaveandDeploy)中的[儲存和部署](../tools/report-builder-authoring-environment-ssrs.md)、[報表產生器 &#40;SSRS&#41;](../report-builder/saving-reports-report-builder.md) 和[儲存報表 &#40;報表產生器&#41;](https://go.microsoft.com/fwlink/?LinkId=154494)。  
  
## <a name="view-reports"></a>檢視報表  
 您除了可以預覽儲存在本機或發行至報表伺服器的報表外，還可提供各種檢視經驗給報告讀取器。 若要檢視報表：  
  
-   **瀏覽器。**  使用報表伺服器 Web 服務或 SharePoint 網站來檢視發行的報表。 在 SharePoint 網站中，您也可以設定 Web 組件來檢視已發行的報表。 如需詳細資訊，請參閱[規劃 Reporting Services 和 Power View 瀏覽器支援 &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)、[報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md) 和 [URL 存取 &#40;SSRS&#41;](../url-access-ssrs.md)。  
  
-   **運送.**  設定訂閱，將報表以電子郵件傳遞給報告讀取器或傳送至共用檔案資料夾。  如需詳細資訊，請參閱[訂閱與傳遞 &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md)。  
  
-   **進出口.**  報告讀取器可從檢視器工具列，將報表匯出成不同的檔案格式。 報表伺服器管理員可設定匯出檔案格式。 如需詳細資訊，請參閱[匯出報表 &#40;報表產生器及 SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)  
  
-   **印刷.**  報告讀取器可依據報表檢視的方式來列印報表或報表的頁面。 如需詳細資訊，請參閱[列印報表 &#40;報表產生器及 SSRS&#41;](../report-builder/print-reports-report-builder-and-ssrs.md)。  
  
-   **Web 或 Windows Form 應用程式。**  使用 Visual Studio 來開發 ASP.NET AJAX 應用程式或主控報表檢視器控制項的 Windows Form 應用程式。 此控制項可指向報表伺服器上的已發行報表。 如需詳細資訊，請參閱＜ [Microsoft 報表](https://go.microsoft.com/fwlink/?LinkID=205399)。  
  
## <a name="manage-reports"></a>管理報表  
 若要管理發行的報表：  
  
-   **資料來源。** 共用資料來源及內嵌資料來源都是獨立管理的，與報表定義無關。  
  
-   **Vsam.**  共用資料集是獨立管理的，與報表定義無關。  
  
-   **參數.**  參數是獨立管理的，與報表定義無關。 在報表伺服器上的參數變更之後，報表撰寫用戶端即無法發行伺服器上所做的變更。  
  
-   **人員.**  ESRI 形狀檔中的影像及空間資料都是資源，因此可獨立發行及管理，而與報表定義無關。  
  
-   **報表快取。**  排程大型報表在離峰時間執行，可以減少在主要上班時間對報表伺服器的處理影響。  
  
-   **快照集.**  如果您要為必須使用同一組資料的多位使用者提供一致的結果，請使用報表快照集。 若為變動資料，視需要報表可能會在不同的時間產生不同的結果。 相對地，報表快照集可讓您針對包含相同時間資料的其他報表或分析工具，進行有效的比較。  
  
-   **報表記錄。** 藉由建立一系列的報表快照集，您可以建立報表記錄，以顯示資料是如何隨著時間變更。  
  
 如需效能的詳細資訊，請參閱[效能、快照集、快取 &#40;Reporting Services&#41;](../report-server/performance-snapshots-caching-reporting-services.md)。  
  
##  <a name="bkmk_SecureReportsSummary"></a>保護報表  
 若要保護報表的安全：  
  
-   請讓報表伺服器管理員，識別您的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 安裝所用的授權與驗證系統。 依預設， [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會使用 Windows 驗證、整合式安全性及角色指派，以協助控制發行報表的存取權。 如需詳細資訊，請參閱[角色與權限 &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md) 和 [Reporting Services 安全性與保護](../security/reporting-services-security-and-protection.md)。  
  
## <a name="create-notifications-based-on-report-data"></a>依據報表資料建立通知  
 您可以為 SharePoint 網站上的發行報表建立資料警示。 資料警示是以報表中報表資料區的資料摘要為依據。 依預設，會自動命名資料區。 報表作者可依據其商業用途來命名資料區，即可輕鬆地在其報表中建立資料警示。 建立資料警示時，若資料符合您所指定的條件，即會以電子郵件通知您。 如需詳細資訊，請參閱[從多個報表產生資料摘要 &#40;報表產生器及 SSRS&#41;](../report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)、[在資料警示設計工具中建立資料警示](../create-a-data-alert-in-data-alert-designer.md)和 [Reporting Services 資料警示](../reporting-services-data-alerts.md)。  
  
## <a name="upgrade-reports"></a>Upgrade Reports  
 
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 支援多種版本的報表定義、報表伺服器及 SharePoint 網站。 若要升級報表：  
  
-   升級報表伺服器安裝。 儲存在報表伺服器上的已編譯報表會在第一次使用時自動升級。 報表定義 (.rdl) 則不會變更。 如需詳細資訊，請參閱＜ [Upgrade and Migrate Reporting Services](../install-windows/upgrade-and-migrate-reporting-services.md)＞。  
  
-   在報表撰寫環境中開啟報表。 在大部分情況下，報表定義都會升級。 如需詳細資訊，請參閱[升級報表](../install-windows/upgrade-reports.md)和 [SQL Server Data Tools 中的部署和版本支援 &#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)。  
  
## <a name="troubleshoot-reports"></a>報表疑難排解  
 若要疑難排解報表：  
  
-   **判斷問題的發生位置。** 檢閱 [報表階段](#bkmk_StagesSummary)。  
  
-   **決定您可以在哪裡找到詳細資訊。** 例如，針對包括運算式的報表設計，報表設計師工具會比報表產生器工具在運算式評估問題方面提供更詳細的資訊。 針對報表處理錯誤，記錄檔中會包含詳細的資訊。  
  
## <a name="tasks"></a>工作  
 如需逐步指示主題的連結，請參閱本主題上節所述功能文章中的＜工作＞章節。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 工具](../tools/reporting-services-tools.md)   
 [SSRS&#41;的延伸模組 &#40;](../extensions-ssrs.md)   
 [Reporting Services Report Server](../reporting-services-report-server.md)  
  
  
