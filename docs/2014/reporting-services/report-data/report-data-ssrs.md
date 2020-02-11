---
title: 報表資料
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: be36e61a44a416283e77638f01005f1b3e16883b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67413052"
---
# <a name="report-data-in-sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS) 中的報表資料

  報表資料可能是來自組織中的多個資料來源。 您設計報表的第一個步驟，就是建立資料來源，及代表基礎報表資料的資料集。 每個資料來源包含資料連接資訊。 每個資料集都包含將一組欄位定義使用為資料來源中資料的查詢命令。 若要視覺化每個資料集的資料，請加入資料區，例如資料表、矩陣、圖表或對應。 處理報表時，查詢會在資料來源上執行，且每個資料區會視需要展開，以顯示資料集的查詢結果。  
  
##  <a name="BkMk_ReportDataTerms"></a>條款

 如果您不熟悉這些[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]概念，請參閱下列 Reporting Services 概念中的詞彙[&#40;SSRS&#41;](../reporting-services-concepts-ssrs.md)：*資料連線*、*內嵌資料來源*、*共用資料來源*、*內嵌*資料集、*共用資料集*、*資料集查詢*、*報表元件*和*資料警示*。  
  
##  <a name="BkMk_ReportDataTips"></a>指定報表資料的秘訣

 使用下列資訊可以設計您的報表資料策略。  
  
- **資料來源**您可以從報表伺服器或 SharePoint 網站上的報表，獨立發行及管理資料來源。 針對每個資料來源，您或資料庫擁有人可以集中管理連接資訊。 資料來源認證會安全地儲存在報表伺服器上；不包含連接字串中的密碼。 您可以將測試伺服器的資料來源重新導向至實際伺服器。 您可以停用資料來源以暫停所有使用它的報表。 如需支援的資料來源清單，請參閱[Reporting Services 中的資料連線、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
- **資料集**您可以從報表或其相依的共用資料來源，獨立發行和管理資料集。 您或資料庫擁有者可以提供報表作者可用的最佳化查詢。 變更查詢時，所有使用共用資料集的報表都會使用更新的查詢。 您可以啟用資料集快取以改善效能。 您可以為特定時間排程查詢快取，或使用共用排程。  
  
- **報表元件所使用的資料**報表元件可以包含它們所依賴的資料。 如需報表組件的詳細資訊，請參閱[報表設計師中的報表組件 &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md)。  
  
- **篩選資料**您可以在查詢或報表中篩選報表資料。 您可以使用資料集及查詢變數以建立串聯參數，並提供使用者從數千個選取中減少選擇項目的能力，以選取便於管理的數字。 您可以根據所指定的參數值或其他值，篩選資料表或圖表中的資料。  
  
- **參數**包含查詢變數的資料集查詢命令會自動建立相符的報表參數。 您也可以手動建立參數。 檢視報表時，報表工具列會顯示參數。 使用者可以選取值，以控制報表資料或報告的外觀。 若要為特定對象自訂報表資料，您可以建立一組具有連結到相同報表定義之不同預設值的報表參數，或是使用內建的 `UserID` 欄位。 如需詳細資訊，請參閱[報表參數 &#40;報表產生器和報表設計師&#41;](../report-design/report-parameters-report-builder-and-report-designer.md) 和[運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md)。  
  
- **資料警示**發行報表之後，您可以根據報表資料來建立警示，並在符合您指定的規則時，接收電子郵件訊息。  
  
- **群組和匯總資料**報表資料可以在查詢或報表中進行分組和匯總。 若您彙總查詢中的數值，可繼續合併有意義條件約束內報表中的數值。  如需詳細資訊，請參閱[篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) 和[彙總函式 &#40;報表產生器及 SSRS&#41;](../report-design/report-builder-functions-aggregate-function.md)。  
  
- **排序資料**報表資料可以在查詢或報表中進行排序。 在資料表中，您也可以加入互動式排序按鈕，讓使用者可以控制排序次序。  
  
- 以**運算式為基礎的資料**因為大部分的報表屬性可以是以運算式為基礎的，而且運算式可以包含資料集欄位和報表參數的參考，所以您可以撰寫強大的運算式來控制報表資料和外觀。 您可以提供使用者透過定義參數控制所看見資料的能力。  
  
- **從資料集顯示資料**來自資料集的資料通常會顯示在一或多個資料區，例如資料表和圖表。  
  
- **顯示來自多個資料集的資料** 您可以根據查詢其他資料集中的值或匯總的一個資料集，在資料區域中撰寫運算式。 您可以包含以一個資料集為基礎之資料表中的子報表，以顯示來自不同資料來源的資料。  
  
## <a name="data-connections-data-sources-and-datasets"></a>資料連接、資料來源及資料集

 使用下列清單以協助定義報表資料的來源。  
  
- 考慮是否使用內嵌或共用資料來源及資料集。 與資料來源的擁有者進行共同作業，以實作及使用適用於組織的驗證及授權。  
  
- 了解組織的軟體資料層架構，以及資料類型所造成之可能發生的問題。 了解資料延伸模組及資料處理延伸模組會如何影響查詢結果。 資料類型在資料來源、資料提供者及儲存於報表定義 (.rdl) 檔案的資料類型之間會有所差異。  
  
- 了解 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 用戶端/伺服器架構及工具。 例如，在報表設計師中，您會在使用內建資料來源類型的用戶端機器上撰寫報表。 發行報表時，報表伺服器或 SharePoint 網站上必須支援資料來源類型。  如需詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
- 報表中可撰寫資料來源及資料集，並且會從用戶端撰寫工具發行至報表伺服器或 SharePoint 網站。 報表伺服器上可直接建立資料來源。 發行後，您可以設定報表伺服器上的認證及其他屬性。 如需詳細資訊，請參閱 Reporting Services 和[Reporting Services 工具](../tools/reporting-services-tools.md)[中的資料連線、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)。  
  
- 您可以使用的資料來源取決於其 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料延伸模組的安裝。 資料來源支援可視用戶端撰寫工具、報表伺服器版本及報表伺服器平台而有所差異。 如需詳細資訊，請參閱 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
- 資料來源認證會視資料來源類型，以及您是否正在用戶端或報表伺服器或 SharePoint 網站上檢視報表而有所變化。 如需詳細資訊，請參閱[設定 SharePoint 網站上報表伺服器項目的權限 &#40;SharePoint 整合模式的 Reporting Services&#41;](../security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)、[指定報表資料來源的認證及連線資訊](../../integration-services/connection-manager/data-sources.md)，以及 [Reporting Services 工具](../tools/reporting-services-tools.md)中每個工具特定的認證資訊。  
  
## <a name="related-tasks"></a>相關工作

 建立資料連接，從外部來源、資料集及查詢加入資料的相關工作。  
  
|||  
|-|-|  
|**一般工作**|**連結**|  
|建立資料連接|[Data Connections, Data Sources, and Connection Strings in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|建立資料集及查詢|[報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|  
|在發行後管理資料來源|[管理報表資料來源](manage-report-data-sources.md)|  
|在發行後共用資料集|[管理共用資料集](manage-shared-datasets.md)|  
|建立及管理資料警示|[Reporting Services Data Alerts](../tutorial-creating-a-basic-table-report-report-builder.md)|  
|快取共用資料集|[快取共用資料集 &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)|  
|排程共用資料集以預先載入快取|[排程](../subscriptions/schedules.md)|  
|加入資料延伸模組|[實作資料處理延伸模組](../extensions/data-processing/implementing-a-data-processing-extension.md)|