---
title: 比較表格式和多維度解決方案 (SSAS) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b5cfb7c473e16dde04a87a05e3d727d161c62583
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033155"
---
# <a name="comparing-tabular-and-multidimensional-solutions-ssas"></a>比較表格式和多維度解決方案 (SSAS)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供兩個不同方法的資料模型化： 表格式和多維度。 雖然這兩種方法有很多重疊之處，但在告知關於後續進展方式的決策這一點上卻有著重大差異。 本主題將會進行功能比較，並說明每一種方法如何應付常見的專案需求。 例如，如果主要的考量是要支援特定資料來源，在關於資料來源的章節可引導您決定要使用哪一個模型化方法。  
  
 本主題包含下列各節：  
  
-   [在 Analysis Services 模型的概觀](#bkmk_overview)  
  
-   [依解決方案類型的資料來源支援](#bkmk_ds)  
  
-   [模型功能](#bkmk_models)  
  
-   [模型大小](#bkmk_modelsize)  
  
-   [可程式性和開發人員體驗](#bkmk_ext)  
  
-   [查詢和指令碼語言支援](#bkmk_lang)  
  
-   [安全性功能支援](#bkmk_sec)  
  
-   [設計工具](#bkmk_designer)  
  
-   [用戶端和報告應用程式](#bkmk_client)  
  
-   [裝載平台](#bkmk_sharePoint)  
  
-   [多維度和表格式解決方案的伺服器部署模式](#bkmk_deploymentmode)  
  
-   [下一步： 建立解決方案](#bkmk_Next)  
  
 在 MSDN 上，可以在此技術文章中找到其他資訊： [在 SQL Server 2012 Analysis Services 中選擇表格式或多維度模型化體驗](http://go.microsoft.com/fwlink/?LinkId=251588)(英文)。  
  
##  <a name="bkmk_overview"></a> 在 Analysis Services 模型的概觀  
 Analysis Services 提供模型開發體驗，以及透過裝載於 Analysis Services 執行個體上的資料庫進行的模型部署。 模型類型包含表格式和多維度。 如您所料，資料庫裝載支援您所建立的表格式和多維度解決方案，但資料庫裝載也包含 PowerPivot for SharePoint。  
  
 PowerPivot for SharePoint 是 *SharePoint 模式的 Analysis Services*，在此模式中，Analysis Services 會做為 SharePoint 的附屬服務，協助裝載和管理先前在 Excel 中所建立然後儲存到 SharePoint 的 Excel 資料模型。 在此內容中的 Analysis Services 角色負責將資料模型載入到記憶體中、重新整理來自外部資料來源的資料，以及對模型執行查詢。 在此組態中，Analysis Services 會在幕後運作。 所有對 Analysis Services 所做的連接和要求都是由 SharePoint 進行，而且只有當 Excel 活頁簿包含資料模型 (資料模型在 Excel 活頁簿中為選用) 時才會這麼做。 如果建立資料模型在 Excel 中，並將裝載在 SharePoint 中符合您的專案需求，請參閱[Power Pivot： 強大資料分析與在 Excel 中的資料模型化](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b)和[PowerPivot for SharePoint &#40;SSAS&#41; ](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)如需詳細資訊。  
  
> [!NOTE]  
>  Excel 資料模型和表格式模型的架構很類似。 如果您需要支援大量資料，或使用其他不適用於 Excel 的模型功能，您可以將 Excel 資料模型匯入到表格式模型。  
  
 表格式和多維度解決方案可利用[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]而且為了供獨立系統上執行的公司 BI 物件[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]執行個體。 這兩個解決方案都會產生高效能分析資料庫，這些資料庫可與 Excel、Reporting Services 報表以及 Microsoft 的其他 BI 應用程式和協力廠商應用程式輕鬆地整合在一起。 這兩種解決方案都會產生獨立資料庫，並可供支援 Analysis Services 的用戶端應用程式使用。  
  
 整體來說，表格式模型和多維度模型之間的差異具有以下特點：  
  
-   多維度和資料採礦解決方案使用 OLAP 模型建構 (Cube 和維度) 以及 MOLAP、ROLAP 或 HOLAP 儲存體，將磁碟做為主要的資料儲存空間來儲存預先彙總的資料。  
  
-   表格式解決方案會使用關聯式模型建構 (例如資料表和關聯性) 來模型化資料，並使用記憶體中分析引擎來儲存及計算資料。 整個模型幾乎都儲存在 RAM 中，而且通常比在多維度解決方案中的模型更快速。  
  
 如果是新的專案，請優先考慮表格式方法。 此方法將有助於更快速地設計、測試和部署，而且搭配 Microsoft 的最新自助式 BI 應用程式使用會更順暢。  
  
##  <a name="bkmk_ds"></a> 依解決方案類型的資料來源支援  
 多維度和表格式模型使用從外部來源匯入的資料。 大部分的開發人員使用設計來支援報告資料結構的資料倉儲，做為模型背後的主要資料來源。 資料倉儲通常是以星形或雪花式結構描述做為架構基礎，並使用 SSIS 來將資料從 OLTP 解決方案載入到資料倉儲。 將資料倉儲做為後端資料來源時，模型化作業會變得更加簡單。  
  
|**連結**|**支援選項摘要**|  
|--------------|--------------------------------------|  
|[支援的資料來源&#40;SSAS 多維度&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)|多維度模型使用來自關聯式資料來源的資料。|  
|[支援的資料來源 &#40;SSAS 表格式&#41;](tabular-models/data-sources-supported-ssas-tabular.md)|表格式模型支援廣泛的資料來源，包括一般檔案、資料摘要以及透過 ODBC 資料提供者加以存取的資料來源。|  
  
 這兩個模型化方法都可以在相同模型中使用來自多個資料來源的資料。  
  
 如果您的解決方案需要儲存關聯式資料庫模型之外的模型資料 (資料大小需求特別大時所使用的技術)，則資料來源類型必須是 SQL Server 關聯式資料庫。 適用於多維度模型的 ROLAP 儲存體和適用於表格式模型的 DirectQuery 都有此需求。  
  
 **資料大小**  
  
 表格式和多維度解決方案都使用資料壓縮來縮減 Analysis Services 資料庫的大小 (相對於您匯入資料的來源資料倉儲)。 因為實際壓縮會因為基礎資料的特性而異，所以無法精確得知當資料經過處理並用於查詢之後，解決方案將需要多少磁碟和記憶體數量。 許多 Analysis Services 開發人員使用的預估方式如下：多維度資料庫的主要儲存空間大約是原始資料大小的三分之一。  
  
 表格式資料庫有時會有更大的壓縮量，大約是十分之一的大小，特別是當大多數資料是從事實資料表匯入時。 對於表格式資料庫而言，記憶體需求將會大於磁碟資料大小，因為將表格式資料庫載入記憶體時會產生額外的資料結構。 在負載之下，任一個解決方案類型的磁碟和記憶體需求應該都會隨著 Analysis Services 快取、儲存、掃描和查詢資料而增加。  
  
 對於某些專案而言，資料需求可能會很大，而變成了選擇模型類型的一個考量因素。 如果您需要載入的資料大小多達許多 TB，則當可用記憶體無法容納資料時，表格式解決方案可能無法滿足您的需求。 有一個分頁選項可將記憶體中的資料交換到磁碟上，但是如果要容納非常大量的資料，則比較適合多維度解決方案。 目前生產的最大 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫就是多維度資料庫。 如需有關表格式解決方案的記憶體分頁選項的詳細資訊，請參閱[記憶體屬性](server-properties/memory-properties.md)。 如需有關擴充多維度解決方案的詳細資訊，請參閱 [向外擴充查詢包含唯讀資料庫的 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=251711)。  
  
##  <a name="bkmk_models"></a> 模型功能  
 下表摘要列出模型層級的功能可用性。 如果您已經安裝 Analysis Services，您可以使用此資訊來了解您所安裝之伺服器模式的功能。 如果您已經熟悉 Analysis Services 中的模型功能，而且您的商業需求包括這些功能當中的一項或多項，您可以檢閱此清單，以確保您想要使用的功能存在於您打算建立的模型類型中。  
  
 如需有關如何依照模型化方法比較功能的詳細資訊，請參閱 MSDN 上的技術文件： [在 SQL Server 2012 Analysis Services 中選擇表格式或多維度模型化體驗](http://go.microsoft.com/fwlink/?LinkId=251588) 。  
  
> [!NOTE]  
>  表格式模型在特定的 SQL Server 版本中有支援。 如需詳細資訊，請參閱＜ [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)＞。  
  
||||  
|-|-|-|  
||**多維度**|**表格式**|  
|動作|[是](multidimensional-models/actions-in-multidimensional-models.md)|否|  
|Aggregation 物件|[是](multidimensional-models/designing-aggregations-analysis-services-multidimensional.md)|否|  
|導出量值|[是](multidimensional-models/create-calculated-members.md)|是|  
|自訂組件|[是](multidimensional-models/multidimensional-model-assemblies-management.md)|否|  
|自訂積存|是|否|  
|Distinct Count|[是](multidimensional-models/use-aggregate-functions.md)|是 （透過 DAX) *|  
|鑽研|[是](multidimensional-models/actions-in-multidimensional-models.md)|是|  
|階層|[是](multidimensional-models/user-defined-hierarchies-create.md)|是|  
|KPI|[是](multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)|是|  
|連結量值群組|[是](multidimensional-models/linked-measure-groups.md)|否|  
|多對多關聯性|[是](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)|否|  
|父子式階層|[是](multidimensional-models/parent-child-dimension.md)|是 (透過 DAX)|  
|資料分割|[是](tabular-models/partitions-ssas-tabular.md)|  
|「檢視方塊」|[是](multidimensional-models/perspectives-in-multidimensional-models.md)|[是](tabular-models/partitions-ssas-tabular.md)|  
|局部加總量值|[是](multidimensional-models/define-semiadditive-behavior.md)|是 (透過 DAX)|  
|翻譯|[是](multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|否|  
|使用者定義階層|[是](multidimensional-models/user-defined-hierarchies-create.md)|是|  
|回寫|[是](multidimensional-models/set-partition-writeback.md)|否|  
  
 * 如果您的解決方案必須支援非常大量的相異計數 （例如數以百萬計的客戶 Id），請優先考慮表格式。 它在這種案例中往往會有更好的效能。 請參閱技術白皮書中有關相異計數的章節： [Analysis Services 案例研究：在大規模的商業方案中使用表格式模型](http://msdn.microsoft.com/library/dn751533.aspx)。  
  
##  <a name="bkmk_modelsize"></a> 模型大小  
 模型的大小 (就物件總數而言) 不會因解決方案類型而異。 但是，用來建立每個解決方案的設計工具，會因為其適應處理大量物件的方式而有所不同。 較大的模型比較容易在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中建立，因為它會在 [物件總管] 和 [方案總管] 中提供更多的功能來依據類型繪製物件圖表及列出物件。  
  
 由數以百計的資料表或維度組成的極大模型通常會以程式設計方式在 Visual Studio 中建立，而不是在設計工具中建立。 如需有關在模型中的物件數目上限的詳細資訊，請參閱[最大容量規格&#40;Analysis Services&#41;](multidimensional-models/olap-physical/maximum-capacity-specifications-analysis-services.md)。  
  
##  <a name="bkmk_ext"></a> 可程式性和開發人員體驗  
 如果是表格式和多維度模型，這兩種型態會共用一個物件模型。 AMO 和 ADOMD.NET 支援這兩個模式。 兩者都不會針對表格式建構修改用戶端程式庫，所以您必須了解多維度和表格式建構與命名慣例彼此之間的關係。 在第一個步驟中，請檢閱 AMO 對表格式程式設計範例，以了解 AMO 針對表格式模型的程式設計方式。 如需詳細資訊，請從 [codeplex 網站](http://go.microsoft.com/fwlink/?LinkID=221036)下載範例。  
  
 表格式解決方案只支援每個解決方案一個 model.bim 檔案，這表示所有工作都必須在單一檔案中完成。 習慣於單一解決方案中處理多個專案的開發團隊在建立共用表格式解決方案時，可能必須改變其工作方式。  
  
##  <a name="bkmk_lang"></a> 查詢和指令碼語言支援  
 Analysis Services 包括 MDX、DMX、DAX、XML/A 和 ASSL。 這些語言的支援會因模型類型而稍有不同。 如果查詢和指令碼語言需求是其中一項考量，請檢閱以下清單。  
  
-   表格式模型資料庫可支援 DAX 計算、DAX 查詢和 MDX 查詢。  
  
-   多維度模型資料庫可支援 MDX 計算和 MDX 查詢以及 ASSL。  
  
-   資料採礦模型可支援 DMX 和 ASSL。  
  
-   Analysis Services PowerShell 支援進行伺服器和資料庫管理。 模型類型 (或伺服器模式) 並不是影響使用 PowerShell Cmdlet 的因素。  
  
 所有資料庫都支援 XML/A。  
  
##  <a name="bkmk_sec"></a> 安全性功能支援  
 所有 Analysis Services 方案都可以在資料庫層級維護安全。 其他細微的安全性選項會因模式而異。 如果您的方案需要細微的安全性設定，請檢閱以下清單，以確保您想要建立的方案類型可支援您想要的安全性層級：  
  
-   表格式模型資料庫可以透過 Analysis Services 中以角色為基礎的權限來使用資料列層級安全性。  
  
-   多維度模型資料庫可以透過 Analysis Services 中以角色為基礎的權限來使用維度和資料格層級安全性。  
  
 Excel 資料模型可以還原成表格式模式伺服器。 一旦還原檔案之後，它就會與 SharePoint 分離 (假設您是從 SharePoint 位置還原)，讓您幾乎可以使用所有表格式模型化功能，包括資料列層級安全性。 您無法在已還原的活頁簿上使用的一個表格式模型化功能就是連結資料表。  
  
##  <a name="bkmk_designer"></a> 設計工具  
 資料模型化技巧和技術方面的專門知識可能會因為負責建立分析模型的使用者而有很大的差異。 如果工具的熟悉度或使用者專業知識是您的方案考量之一，請比較以下的模型建立經驗。  
  
|**模型化工具**|**使用方式**|  
|-----------------------|------------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|用來建立表格式、多維度和資料採礦方案。 此撰寫環境會使用 Visual Studio Shell 來提供工作空間、屬性窗格和物件導覽。 已經使用 Visual Studio 的技術使用者最有可能偏好使用這個工具來建立商業智慧應用程式。 請參閱[工具和 Analysis Services 中使用的應用程式](tools-and-applications-used-in-analysis-services.md)如需詳細資訊。|  
|Excel 2013 和更新版本 (含 Powerpivot for Excel 增益集)|PowerPivot for Excel 是用來編輯和增強 Excel 資料模型的工具。 它有個別的應用程式工作區，會透過 Excel 開啟，但與 Excel 使用相同的視覺介面 (索引標籤式的頁面、方格配置和公式列)。 使用者是非常熟悉 Excel 通常會偏愛這個工具勝過[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。 請參閱 [Power Pivot：Excel 中的強大資料分析與資料模型](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b)。|  
  
##  <a name="bkmk_client"></a> 用戶端和報告應用程式  
 在舊版中，您所選擇的模型類型會影響您可以使用的用戶端應用程式，但隨著時間的推進，影響的程度已減弱。 對於連接到 Analysis Services 資料的用戶端應用程式，表格式和多維度模型所提供的支援大致相同。 下表列出可搭配 Analysis Services 資料模型使用的 Microsoft 用戶端應用程式。  
  
|**應用程式**|**說明**|  
|---------------------|---------------------|  
|Excel 樞紐分析表報表|表格式和多維度模型所能使用的 Excel 功能相同，但只有多維度模型能支援回寫 (Excel 所實作的 Analysis Services 功能)。|  
|Reporting Services RDL 報表|報表產生器或報表設計師中所建立的 RDL 報表可以使用任何 Analysis Services 模型，以及裝載在 PowerPivot for SharePoint 的 Excel 資料模型。|  
|PerformancePoint 儀表板|在 SharePoint 中，PerformancePoint 儀表板可以連接到所有 Analysis Services 資料庫，包括 Excel 資料模型。 如需詳細資訊，請參閱 [建立資料連接 (PerformancePoint Services)](http://go.microsoft.com/fwlink/?linkdID=218155)。|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 在 Office 365 或 Power BI 網站|僅限表格式模型。|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 在 SharePoint 內部部署|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 是來自 SharePoint 的 ClickOnce 應用程式，可以使用 Analysis Services Cube 或表格式模型。|  
  
##  <a name="bkmk_deploymentmode"></a> 多維度和表格式解決方案的伺服器部署模式  
 Analysis Services 執行個體會使用設定伺服器操作內容的三個模式的其中一個模式來安裝。 您安裝的伺服器模式將會決定可以部署到該伺服器的方案類型。 儲存體和記憶體架構是模式之間的主要差異，但是還有其他差異存在。 下表簡短描述這三種伺服器模式。 如需詳細資訊，請參閱[判斷 Analysis Services 執行個體的伺服器模式](instances/determine-the-server-mode-of-an-analysis-services-instance.md)。  
  
|部署模式|描述|  
|---------------------|-----------------|  
|0 - 多維度和資料採礦|執行多維度和資料採礦解決方案，您會將這些解決方案部署到 Analysis Services 預設執行個體。 部署模式 0 是 Analysis Services 安裝的預設值。 如需詳細資訊，請參閱[以多維度和資料採礦模式安裝 Analysis Services](../../2014/sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)。|  
|1 - PowerPivot for SharePoint|就 Excel 資料模型的存取而言，Analysis Services 是 SharePoint 的內部元件。 Analysis Services 會以部署模式 1 進行安裝，並且只接受來自 SharePoint 環境中 Excel Services 的要求。 如需詳細資訊，請參閱＜ [PowerPivot for SharePoint 2010 Installation](../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)＞。|  
|2 - 表格式|在設定部署模式 2 的獨立 Analysis Services 執行個體上執行表格式解決方案。 如需詳細資訊，請參閱[以表格式模式安裝 Analysis Services](instances/install-windows/install-analysis-services.md)。|  
  
 請注意，伺服器模型不能互換。 進行安裝時，就會選擇伺服器的作業模式。 您應該安裝多個執行個體，讓每種伺服器模式各有一個執行個體，以支援所有工作負載。  
  
##  <a name="bkmk_sharePoint"></a> 裝載平台  
 Microsoft 有多種方法可用來裝載資料、應用程式、報表和共同作業。 在本節中，我們將討論有關各種裝載平台的 Analysis Services 互通性。  
  
|**平台**|**說明**|  
|------------------|---------------------|  
|Microsoft Azure|您可以在 Azure 虛擬機器上執行任何支援的 Analysis Services 版本。 相較於 Azure SQL Database 這個可提供內部部署關聯式資料庫引擎所提供的大多數相同功能的 Azure 服務，Analysis Services 在 Azure 上並沒有相同的東西。 在 Azure VM 中安裝、設定及執行 Analysis Services 是我們唯一的 Azure 架構選項。|  
|Office 365|Office 365 中的 Excel Online 支援遠端連接到在內部部署中執行的表格式和多維度模型。|  
|Office 365 中的 Power BI 網站|在 Power BI 網站中，Power View 報表可以連接到在內部部署中執行的表格式資料模型。|  
|在內部部署伺服器 (SharePoint 和 SQL Server 執行個體)|內部部署資料庫伺服器 (也就是已安裝 Analysis Services 的 SQL Server 執行個體) 仍然是讓報表和用戶端應用程式可以使用 Analysis Services 資料的主要方式。 表格式、多維度和資料採礦解決方案會在網路上的 Analysis Services 執行個體中執行，不需取決於 SharePoint。<br /><br /> SQL Server 藉由新增 PowerPivot 資料存取和表格式資料存取的支援來與 SharePoint 整合。 當您將每一個產品中使用的功能數目最大化時，SharePoint 和 SQL Server 整合的投資也會增加。 如果您有 SharePoint，您可以安裝 SQL Server PowerPivot for SharePoint 來啟用 PowerPivot 資料存取，並取得用來存取表格式資料庫的 PowerPivot .bism 連接檔案，該資料庫會在網路伺服器上的外部 Analysis Services 執行個體中執行。<br /><br /> 如果您同時有 SharePoint 和 SQL Server，則可支援下列服務與應用程式的組合：<br /><br /> Analysis Services 模型 (表格式或多維度)<br /><br /> 中間層 SharePoint 服務 (Excel Services、SharePoint 中的 Reporting Services、PerformancePoint Services)<br /><br /> 瀏覽器用戶端或豐富型用戶端 (Excel)，以進行更深層的資料分析和探索。|  
  
##  <a name="bkmk_Next"></a> 下一個步驟：建立解決方案  
 現在您對於解決方法的比較已經有了基本了解，請試試以下的教學課程，以了解建立每一個解決方案的步驟。 以下連結會帶領您前往說明步驟的教學課程。  
  
-   使用[表格式模型化 &#40;Adventure Works 教學課程&#41;](tabular-modeling-adventure-works-tutorial.md) 建置表格式模型。  
  
-   使用[多維度模型化 &#40;Adventure Works 教學課程&#41;](multidimensional-modeling-adventure-works-tutorial.md) 建置多維度模型。  
  
-   使用＜ [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md)＞建立資料採礦模型。  
  
-   使用 [PowerPivot for Excel 教學課程](http://go.microsoft.com/fwlink/?LinkId=251135)建立 PowerPivot 模型。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 執行個體管理](instances/analysis-services-instance-management.md)   
 [新功能 Analysis Services 和 Business Intelligence](what-s-new-in-analysis-services.md)   
 [最新消息&#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md)   
 [在 PowerPivot 中最新消息](http://go.microsoft.com/fwlink/?LinkId=238141)   
 [適用於 SQL Server 2012 PowerPivot 說明](http://go.microsoft.com/fwlink/?LinkID=220946)   
 [PowerPivot BI 語意模型連接&#40;.bism&#41;](power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [建立和管理共用資料來源 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
  