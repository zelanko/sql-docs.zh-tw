---
title: "比較表格式和多維度解決方案 (SSAS) |Microsoft 文件"
ms.custom: 
ms.date: 06/15/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-tabular
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 969a3952f113521b5f584533fd0676b33b873b53
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="comparing-tabular-and-multidimensional-solutions"></a>比較表格式和多維度解決方案
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  SQL Server Analysis Services 提供多種方法，以建立商業智慧語意模型： 表格式、 多維度和 Power Pivot for SharePoint。
  
 利用多種方法可讓您視不同的商務和使用者需求，量身訂做模型化體驗。 多維度是建基於開放標準的成熟技術，且受到許多 BI 軟體廠商的愛戴，但很難駕馭。 表格式提供許多開發人員認為更具直覺性的關聯式模型化方法。 Power Pivot 甚至更加簡易，除了在 Excel 中提供視覺化的資料模型外，還透過 SharePoint 提供伺服器支援。  
  
 所有模型皆會部署為在 Analysis Services 執行個體上執行的資料庫、由用戶端工具使用單一的資料提供者集合進行存取，並在互動式和靜態報表中，透過 Excel、Reporting Services、Power BI 和其他廠商的 BI 工具以視覺化的方式呈現。  
  
 表格式和多維度解決方案使用 SSDT 來建立，而且為了供獨立系統上執行的公司 BI 物件[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]執行個體內部，和表格式模型， [Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/)中的伺服器雲端。 這兩個解決方案都會產生可與 BI 用戶端輕易整合的高效能分析資料庫。 但是，每個解決方案的建立、使用和部署方式都不相同。 本主題大篇幅比較這兩種類型，以便讓您找出最適合您的方法。  
  
 對於新專案，建議使用表格式模型。 表格式模型速度較快，來設計、 測試和部署。將能更加配合的最新自助式 BI 應用程式和雲端服務從 Microsoft。  
  
##  <a name="bkmk_overview"></a> 模型類型概觀  
 不熟悉 Analysis Services 嗎？ 下表列舉不同的模型、摘要說明方法，並識別初始版本的工具。  
 
 > [!NOTE]  
>  **Azure Analysis Services**支援在 1200年或更高的相容性層級的表格式模型。 不過，並非所有的表格式模型化功能，本主題說明適用於 Azure Analysis Services。 建立及部署至 Azure Analysis Services 表格式模型是大致相同，所以內部部署，務必了解的差異。 若要進一步了解，請參閱[什麼是 Azure Analysis Services？](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview)
  
||||  
|-|-|-|  
|**型別**|**模型描述**|**已發行**|  
|表格式|關聯式模型建構 (模型、資料表、資料行)。 就內部而言，中繼資料繼承自 OLAP 模型建構 (Cube、維度、量值)。 程式碼和指令碼會使用 OLAP 中繼資料。|SQL Server 2012 及更新版本 (相容性層級 1050 - 1103) <sup>1</sup>|  
|SQL Server 2016 的表格式|關聯式模型建構 （模型、 資料表、 資料行），以在表格式中繼資料物件定義中[Tabular Model Scripting Language (TMSL)](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)和[表格式物件模型 (TOM)](../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)程式碼。|SQL Server 2016 (相容性層級 1200)| 
|SQL Server 2017 的表格式|關聯式模型建構 （模型、 資料表、 資料行），以在表格式中繼資料物件定義中[Tabular Model Scripting Language (TMSL)](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)和[表格式物件模型 (TOM)](../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)程式碼。|SQL Server 2017 （相容性層級 1400年）| 
|多維度|OLAP 模型建構 (Cube、維度、量值)。|SQL Server 2000 及更新版本|  
|Power Pivot|原本為增益集，現在則完全整合至 Excel。 僅限圖形化模型，透過內部表格式基礎結構。 您可以將 Power Pivot 模型匯入 SSDT，以建立在 Analysis Services 執行個體上執行的新表格式模型。|透過 Excel 和 Power Pivot BI Desktop|  
  
 <sup>1</sup>相容性層級中很重要，因為表格式中繼資料引擎與啟用案例支援目前的版本可用的功能，只能在較高的層級。 更新的版本支援舊版的相容性層級，但建議您建立新的模型，或伺服器版本所支援的最高的相容性層級升級現有的模型。
  
##  <a name="bkmk_models"></a> 模型功能  
  下表摘要列出模型層級的功能可用性。 檢閱此清單，以確定要建置的模型類型中有您想要使用的功能。  
  
|||| 
|-|-|-|
||多維度|表格式|
|動作|是|否|
|Aggregations|是|否|
|計算結果欄|否|是|  
|導出量值|是|是| 
|計算資料表|否|[是]<sup>1</sup>|  
|自訂組件|是|否|
|自訂積存|是|否| 
|預設成員|是|否|  
|顯示資料夾|是|[是]<sup>1</sup>|  
|Distinct Count|是|是 (透過 DAX)|
|鑽研|是|Yes （取決於用戶端應用程式）|
|階層|是|是|
|KPI|是|是| 
|連結物件|是|是 (連結資料表)|
|M 運算式|否|[是]<sup>1</sup>|
|多對多關聯性|是|否 (但沒有[雙向交叉篩選](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)1200年 （含） 以上的相容性層級)| 
|命名集|是|否| 
|不完全階層|是|[是]<sup>1</sup>|  
|父子式階層|是|是 (透過 DAX)|
|資料分割|是|是| 
|檢視方塊|是|是|
|資料列層級安全性|是|是| 
|物件層級安全性|是|[是]<sup>1</sup>|
|局部加總量值|是|是| 
|翻譯|[是](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|是| 
|使用者定義階層|是|是|
|回寫|是|否| 
  
 <sup>1</sup>看到[相容性層級的表格式模型中 Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)有關相容性層級之間的功能差異的資訊。  
  
##  <a name="bkmk_ds"></a> 資料考量  
 表格式和多維度模型使用從外部來源匯入的資料。 在您決定最符合資料的模型類型時，所需要匯入的資料數量和類型可能是主要的考量。  
  
 **壓縮**  
  
 表格式和多維度解決方案都使用資料壓縮來縮減 Analysis Services 資料庫的大小 (相對於您匯入資料的來源資料倉儲)。 因為實際壓縮會因為基礎資料的特性而異，所以無法精確得知當資料經過處理並用於查詢之後，解決方案將需要多少磁碟和記憶體數量。  
  
 許多 Analysis Services 開發人員使用的預估方式如下：多維度資料庫的主要儲存空間大約是原始資料大小的三分之一。 表格式資料庫有時會有更大的壓縮量，大約是十分之一的大小，特別是當大多數資料是從事實資料表匯入時。  
  
 **模型的大小和資源偏差 (記憶體內部或磁碟)**  
  
 Analysis Services 資料庫的大小僅受到可用來加以執行的資源所限。 模型類型和儲存模式也會在資料庫的成長極限中佔有一席之地。  
  
 在記憶體內部或將查詢執行卸載至外部資料庫的 DirectQuery 模式下，就會執行表格式資料庫。 表格式記憶體中分析，資料庫會完全儲存在記憶體中，這表示您必須擁有足夠的記憶體來不只載入所有資料，但是也支援的查詢建立的其他資料結構。  
  
 DirectQuery 在 SQL Server 2016，改頭換面，具備較少的限制比以前，以及更佳的效能。 善用儲存體和查詢執行的後端關聯式資料庫，讓建立大規模表格式模型比先前更加可行。  
  
 在過去，在生產環境中的最大資料庫是多維度資料庫，以處理和查詢工作負載在專用的硬體，各個皆針對其個別的使用方式最佳化獨立執行。  表格式資料庫迅速趕上，且 DirectQuery 中新的進階功能協助更進一步拉大距離。  
  
 多維度卸載資料儲存和查詢執行會提供透過 ROLAP。   在查詢伺服器上，您可以快取資料列集，並將過時的項目移出分頁。提到有效且平衡地使用記憶體和磁碟資源，客戶通常會想到多維度解決方案。  
  
 在負載之下，任一個解決方案類型的磁碟和記憶體需求應該都會隨著 Analysis Services 快取、儲存、掃描和查詢資料而增加。 如需記憶體分頁的詳細資訊，請參閱 [Memory Properties](../analysis-services/server-properties/memory-properties.md)。 如需深入了解延展，請參閱 [High availability and Scalability in Analysis Services](../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)。  
  
 適用於 Excel 的 Power Pivot 人工檔案大小限制為 2 GB，加上這個限制是為了讓適用於 Excel 的 Power Pivot 中建立的活頁簿可以上傳至 SharePoint，並設定檔案上傳大小上限。 將 PowerPivot 活頁簿移轉到獨立 Analysis Services 執行個體上之表格式解決方案的一個主要原因是為了避開檔案大小限制。 如需設定檔案上傳大小上限的詳細資訊，請參閱[設定檔案上傳的大小上限 &#40;Power Pivot for SharePoint&#41;](../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)。  
  
 **支援的資料來源**  
  
 表格式模型可以從關聯式資料來源、資料摘要和某些文件格式匯入資料。 您也可以使用 OLE DB for ODBC 提供者搭配表格式模型。 1400 相容性層級的表格式模型提供大幅提高各種從中您可以從匯入的資料來源。 這是因為現代取得資料的資料查詢，並匯入 SSDT 利用 M 公式的查詢語言中的功能簡介。   

  多維度解決方案可以使用 OLE DB 原生和 Managed 提供者從關聯式資料來源匯入資料。  
  
 若要檢視您可以匯入至每個模型中的外部資料來源清單，請參閱下列主題：  
  
-   [支援的資料來源 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  

-   [支援的資料來源 &#40;SSAS - 多維度&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  

  
##  <a name="bkmk_lang"></a> 查詢和指令碼語言支援  
 Analysis Services 包括 MDX、DMX、DAX、XML/A、ASSL 和 TMSL。 這些語言的支援會因模型類型而有所不同。 如果查詢和指令碼語言需求是其中一項考量，請檢閱以下清單。  

-   表格式模型資料庫可支援 DAX 計算、DAX 查詢和 MDX 查詢。 此在所有相容性層級皆為 true。 指令碼語言為 ASSL （透過 XMLA) 相容性層級 1050年-1103，和 TMSL （透過 XMLA) 相容性層級 1200年 （含） 以上。 

-   Power Pivot 活頁簿會將 DAX 用於計算，並將 DAX 或 MDX 用於查詢。  
  
-   多維度模型資料庫可支援 MDX 計算、 MDX 查詢、 DAX 查詢以及 ASSL。 
  
-   資料採礦模型可支援 DMX 和 ASSL。  
  
-   表格式和多維度模型以及資料庫都支援 Analysis Services PowerShell。  
  
 所有資料庫都支援 XML/A。 如需詳細資訊，請參閱[查詢及運算式語言參考 &#40;Analysis Services&#41;](http://msdn.microsoft.com/library/9597533d-35f4-4742-9d8c-7af392163527) 和[開發人員指南 (Analysis Services)](../analysis-services/analysis-services-developer-documentation.md)。  
  
##  <a name="bkmk_sec"></a> 安全性功能  
 所有 Analysis Services 方案都可以在資料庫層級維護安全。 其他細微的安全性選項會因模式而異。 如果您的方案需要細微的安全性設定，請檢閱以下清單，以確保您想要建立的方案類型可支援您想要的安全性層級：  

  
-   表格式模型資料庫可以使用資料列層級安全性，使用以角色為基礎的權限。  
  
-   多維度模型資料庫可以使用維度和資料格層級安全性，使用以角色為基礎的權限。  

-   [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 活頁簿的安全。  
  
 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 活頁簿可以還原成表格式模式伺服器。 一旦還原檔案之後，它是與 SharePoint 分離，好讓您使用所有表格式模型化功能，包括資料列層級安全性。  
  
##  <a name="bkmk_designer"></a> 設計工具  
 資料模型化技巧和技術方面的專門知識可能會因為負責建立分析模型的使用者而有很大的差異。 如果工具的熟悉度或使用者專業知識是您的方案考量之一，請比較以下的模型建立經驗。  
  
|模型化工具|使用方式|  
|-------------------|--------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|用來建立表格式、 多維度和資料採礦方案。 此撰寫環境會使用 Visual Studio Shell 來提供工作空間、屬性窗格和物件導覽。 已經使用 Visual Studio 的技術使用者最有可能偏好使用這個工具來建立商業智慧應用程式。|  
|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for Excel|用來建立 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 活頁簿，之後可以將其部署到已安裝 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 的 SharePoint 伺服器陣列。 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for Excel 有個別的應用程式工作空間，此工作空間會透過 Excel 開啟。 它會使用與 Excel 相同的視覺比喻 (索引標籤頁面、方格配置和公式列)。 非常熟悉 Excel 的使用者會偏愛這個工具勝過 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。|  
  
##  <a name="bkmk_client"></a> 用戶端應用程式支援  
 在一般、 表格式和多維度解決方案支援用戶端應用程式使用一或多個 Analysis Services 用戶端程式庫 （MSOLAP、 AMOMD、 ADOMD）。 例如，Excel、 Power BI Desktop 和自訂應用程式。   
 
 如果您正在使用 Reporting Services，則報表功能和可用性會因版本和伺服器模式而異。 因此，您想要建立的報表類型可能會影響您選擇安裝的伺服器模式。  
  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)](也就是在 SharePoint 中執行的 Reporting Services 撰寫工具)。 唯一可以搭配此報表使用的資料來源類型為 Analysis Services 表格式模型資料庫或 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 活頁簿。 這表示，您必須擁有表格式模式伺服器或 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 伺服器，才能裝載此報表類型所使用的資料來源。 您不能將多維度模型當做 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 報表的資料來源使用。 您必須建立 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] BI 語意模型連線或 Reporting Services 共用資料來源，作為 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 報表的資料來源使用。  
  
 報表產生器和報表設計師可以使用任何 Analysis Services 資料庫，包括在 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 上裝載的 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 活頁簿。  
  
 所有 Analysis Services 資料庫都支援 Excel 樞紐分析表報表。 不論您使用表格式資料庫、多維度資料庫還是 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 活頁簿，Excel 功能都相同，但是只有多維度資料庫支援回寫。  
 
  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 執行個體管理](../analysis-services/instances/analysis-services-instance-management.md)   
 [Analysis Services 的新功能](../analysis-services/what-s-new-in-analysis-services.md)     

  
  
