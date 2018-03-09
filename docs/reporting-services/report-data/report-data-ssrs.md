---
title: "報表資料 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e22b7c24-edab-42d6-82f6-95068e1c6043
caps.latest.revision: "16"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 17eb836e4784a5f846f769b63c6002fc60af0bf5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="report-data-ssrs"></a>報表資料 (SSRS)
  報表資料可能是來自組織中的多個資料來源。 您設計報表的第一個步驟，就是建立資料來源，及代表基礎報表資料的資料集。 每個資料來源包含資料連接資訊。 每個資料集都包含將一組欄位定義使用為資料來源中資料的查詢命令。 若要視覺化每個資料集的資料，請加入資料區，例如資料表、矩陣、圖表或對應。 處理報表時，查詢會在資料來源上執行，且每個資料區會視需要展開，以顯示資料集的查詢結果。  
  
##  <a name="BkMk_ReportDataTerms"></a> 詞彙  
  
-   **資料連接。** 也稱為 *資料來源*。 資料連接包括相依於連接類型的名稱和連接屬性。 依預設，資料連接不包括認證。 資料連接不會指定要從外部資料來源擷取的資料。 若要執行這項操作，您可以在建立資料集時指定查詢。  
  
-   **共用資料來源定義。** 包含報表資料來源之 XML 表示的檔案。 報表發行時，其資料來源會儲存到報表伺服器或 SharePoint 網站上做為資料來源定義，與報表定義分開。 例如，報表伺服器管理員可能會更新連接字串或認證。 在原生報表伺服器上，檔案類型為 .rds。 在 SharePoint 網站上，檔案類型為 .rsds。  
  
-   **連接字串。** 連接字串是連接到資料來源時所需之連接屬性的字串版本。 連接屬性會依資料連接類型而有所不同。 如需範例，請參閱＜ [Data Connections, Data Sources, and Connection Strings in Report Builder](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)＞。  
  
-   **共用資料來源。** 報表伺服器或 SharePoint 網站上提供的資料來源，可供多個報表使用。  
  
-   **內嵌資料來源。** 也稱為 *「報表特定資料來源」*(report-specific data source)。 在報表中定義而且僅供該報表使用的資料來源。  
  
-   **認證。** 認證是驗證資訊，您必須提供這項資訊才能存取外部資料。  
  
##  <a name="BkMk_ReportDataTips"></a> 指定報表資料的秘訣  
 使用下列資訊可以設計您的報表資料策略。  
  
-   **資料來源** ：您可以發行資料來源並從報表伺服器或 SharePoint 網站上的報表分開進行管理。 針對每個資料來源，您或資料庫擁有人可以集中管理連接資訊。 資料來源認證會安全地儲存在報表伺服器上；不包含連接字串中的密碼。 您可以將測試伺服器的資料來源重新導向至實際伺服器。 您可以停用資料來源以暫停所有使用它的報表。  
  
-   **資料集** ：您可以發行資料集並從所相依的報表或共用資料來源分開進行管理。 您或資料庫擁有者可以提供報表作者可用的最佳化查詢。 變更查詢時，所有使用共用資料集的報表都會使用更新的查詢。 您可以啟用資料集快取以改善效能。 您可以為特定時間排程查詢快取，或使用共用排程。  
  
-   **報表組件使用的資料** ：報表組件可以包含所相依的資料。 如需報表組件的詳細資訊，請參閱[報表設計師中的報表組件 &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)。  
  
-   **篩選資料** ：在查詢或在報表中，可以篩選報表資料。 您可以使用資料集及查詢變數以建立串聯參數，並提供使用者從數千個選取中減少選擇項目的能力，以選取便於管理的數字。 您可以根據所指定的參數值或其他值，篩選資料表或圖表中的資料。  
  
-   **參數** ：包含查詢變數的資料集查詢命令會自動建立相符的報表參數。 您也可以手動建立參數。 檢視報表時，報表工具列會顯示參數。 使用者可以選取值，以控制報表資料或報告的外觀。 若要為特定對象自訂報表資料，您可以建立一組具有連結到相同報表定義之不同預設值的報表參數，或是使用內建的 **UserID** 欄位。 如需詳細資訊，請參閱[報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md) 和[運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)。  
  
-   **資料警示** ：發行報表後，您可以根據報表資料來建立警示，並在符合所指定規則時，接收電子郵件訊息。  
  
-   **群組及彙總值** ：在查詢或在報表中，可以分組及彙總報表資料。 若您彙總查詢中的數值，可繼續合併有意義條件約束內報表中的數值。  如需詳細資訊，請參閱[篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) 和[彙總函式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-function.md)。  
  
-   **排序資料** ：在查詢或在報表中，可以排序報表資料。 在資料表中，您也可以加入互動式排序按鈕，讓使用者可以控制排序次序。  
  
-   **以運算式為基礎的資料** ：因為多數的報表屬性可以運算式為基礎，而且運算式可以包含資料集欄位及報表參數的參考，您可以寫入強大的運算式以控制報表資料及外觀。 您可以提供使用者透過定義參數控制所看見資料的能力。  
  
-   **顯示資料集中的資料** ：資料集中的資料通常會顯示在一個或多個資料區，例如資料表及圖表。  
  
-   **顯示多個資料集之中的資料**  ：您可以在一個以查閱其他資料集中的數值或彙總值為基礎之資料集的資料區中，寫入運算式。 您可以包含以一個資料集為基礎之資料表中的子報表，以顯示來自不同資料來源的資料。  
  
 使用下列清單以協助定義報表資料的來源。  
  
-   考慮是否使用內嵌或共用資料來源及資料集。 與資料來源的擁有者進行共同作業，以實作及使用適用於組織的驗證及授權。  
  
-   了解組織的軟體資料層架構，以及資料類型所造成之可能發生的問題。 了解資料延伸模組及資料處理延伸模組會如何影響查詢結果。 資料類型在資料來源、資料提供者及儲存於報表定義 (.rdl) 檔案的資料類型之間會有所差異。  
  
-   了解 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 用戶端/伺服器架構及工具。 例如，在報表設計師中，您會在使用內建資料來源類型的用戶端機器上撰寫報表。 發行報表時，報表伺服器或 SharePoint 網站上必須支援資料來源類型。  如需詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
-   報表中可撰寫資料來源及資料集，並且會從用戶端撰寫工具發行至報表伺服器或 SharePoint 網站。 報表伺服器上可直接建立資料來源。 發行後，您可以設定報表伺服器上的認證及其他屬性。 如需詳細資訊，請參閱 [資料連接、資料來源及連接字串 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 和 [Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)。  
  
-   您可以使用的資料來源取決於其 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料延伸模組的安裝。 資料來源支援可視用戶端撰寫工具、報表伺服器版本及報表伺服器平台而有所差異。 如需詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
-   資料來源認證會視資料來源類型，以及您是否正在用戶端或報表伺服器或 SharePoint 網站上檢視報表而有所變化。 如需詳細資訊，請參閱[設定 SharePoint 網站上報表伺服器項目的權限 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)、[指定報表資料來源的認證及連線資訊](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)，以及 [Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)中每個工具特定的認證資訊。  
  
## <a name="related-tasks"></a>相關工作  
 建立資料連接，從外部來源、資料集及查詢加入資料的相關工作。  
  
|||  
|-|-|  
|**一般工作**|**連結**|  
|建立資料連接|[資料連接、資料來源及連接字串 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)|  
|建立資料集及查詢|[報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|  
|在發行後管理資料來源|[管理報表資料來源](../../reporting-services/report-data/manage-report-data-sources.md)|  
|在發行後共用資料集|[管理共用資料集](../../reporting-services/report-data/manage-shared-datasets.md)|  
|建立及管理資料警示|[Reporting Services Data Alerts](../../reporting-services/reporting-services-data-alerts.md)|  
|快取共用資料集|[快取共用資料集 &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)|  
|排程共用資料集以預先載入快取|[排程](../../reporting-services/subscriptions/schedules.md)|  
|加入資料延伸模組|[實作資料處理延伸模組](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)|  
  
## <a name="related-content"></a>相關內容  
  
