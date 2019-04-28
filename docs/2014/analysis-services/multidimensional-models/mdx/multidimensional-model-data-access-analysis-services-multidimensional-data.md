---
title: 多維度模型資料存取 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, data access interfaces
- objects [Analysis Services], data access interfaces
- Analysis Services data access interfaces
- data retrieval [Analysis Services]
- retrieving data
- metadata [Analysis Services]
- data access interfaces [Analysis Services]
- manipulating objects [Analysis Services]
- Analysis Services data access interfaces, about data access interfaces
ms.assetid: 46388efb-3c78-47a2-b5c9-5a69ff394d03
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac889b67dec5c6ff014f18d18899109741a2eef9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725272"
---
# <a name="multidimensional-model-data-access-analysis-services---multidimensional-data"></a>多維度模型資料存取 (Analysis Services - 多維度資料)
  使用本主題中的資訊了解如何使用程式設計方法、指令碼或用戶端應用程式 (其中包含的內建支援可連接至網路上的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器) 存取 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 多維度資料。  
  
 本主題包含下列幾節：  
  
 [用戶端應用程式](#bkmk_clientapps)  
  
 [查詢語言](#bkmk_querylang)  
  
 [程式設計介面](#bkmk_api)  
  
##  <a name="bkmk_clientapps"></a> 用戶端應用程式  
 雖然 Analysis Services 提供的介面可讓您使用程式設計方式建立或整合多維度資料庫，但更常見的方法是使用 Microsoft 以及對 Analysis Services 資料擁有內建資料存取之其他軟體廠商所提供的用戶端應用程式。  
  
 下列 Microsoft 應用程式支援多維度資料的原生連接。  
  
### <a name="excel"></a>[匯出]  
 Analysis Services 多維度資料通常是使用 Excel 活頁簿中的樞紐分析表和樞紐分析圖控制項呈現。 樞紐分析表適用於多維度資料，因為模型中的階層、彙總與導覽建構函式與樞紐分析表的資料摘要功能是絕配。 Analysis Services OLE DB 資料提供者包含在 Excel 安裝中，可以讓資料連接的設定更為容易。 如需詳細資訊，請參閱＜ [連接到 SQL Server Analysis Services 或是從中匯入資料](https://go.microsoft.com/fwlink/?linkID=215150)＞。  
  
### <a name="reporting-services-reports"></a>Reporting Services 報表  
 您可以使用報表產生器或報表設計師建立取用包含分析資料之 Analysis Services 資料庫的報表。 報表產生器和報表設計師都包含一個 MDX 查詢設計工具，您可以使用此查詢設計工具輸入或設計從可用資料來源擷取的 MDX 陳述式。 如需詳細資訊，請參閱 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md) 和 [MDX 的 Analysis Services 連接類型 &#40;SSRS&#41;](../../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)。  
  
### <a name="performancepoint-dashboards"></a>PerformancePoint 儀表板  
 PerformancePoint 儀表板用來在 SharePoint 中建立計分卡，這些計分卡會根據預先定義的量值，傳達商務效能。 PerformancePoint 包含 Analysis Services 多維度資料的資料連接支援。 如需詳細資訊，請參閱 [建立 Analysis Services 資料連接 (PerformancePoint Services)](https://go.microsoft.com/fwlink/?linkid=232471)。  
  
### <a name="sql-server-data-tools"></a>SQL Server Data Tools  
 模型和報表設計師使用 SQL Server Data Tools 建立包含多維度模型的方案。 將方案部署至 Analysis Services 執行個體就是建立您之後從 Excel、Reporting Services 以及其他商業智慧用戶端應用程式連接之資料庫的程序。  
  
 SQL Server Data Tools 建立在 Visual Studio Shell 之上，並使用專案組織與包含模型。 如需詳細資訊，請參閱[使用 SQL Server 資料工具建立多維度模型 &#40;SSDT&#41;](../creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)。  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 對於資料庫管理員，SQL Server Management Studio 是一個整合式的環境，可用來管理 SQL Server 執行個體，包括 Analysis Services 的執行個體與多維度資料庫。 如需詳細資訊，請參閱 [SQL Server Management Studio](../../../ssms/sql-server-management-studio-ssms.md) 和 [連接到 Analysis Services](../../instances/connect-to-analysis-services.md)。  
  
##  <a name="bkmk_querylang"></a> 查詢語言  
 MDX 是一個業界標準查詢與計算語言，可用來擷取 OLAP 資料庫中的資料。 在 Analysis Services 中，MDX 是用來擷取資料的查詢語言，但也支援資料定義與資料操作。 MDX 編輯器內建在 SQL Server Management Studio、Reporting Services 和 SQL Server Data Tools 中。 您可以使用 MDX 編輯器建立特定查詢或可重複使用的指令碼 (如果是可重複的資料作業)。  
  
 有些工具和應用程式 (例如 Excel) 在內部使用 MDX 建構函式來查詢 Analysis Services 資料來源。 您也可以在程式設計上使用 MDX，只要將 MDX 陳述式包含在 XMLA Execute 要求中即可。  
  
 下列連結提供有關 MDX 的詳細資訊：  
  
 [使用 MDX 查詢多維度資料](querying-multidimensional-data-with-mdx.md)  
  
 [MDX 的關鍵概念 &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)  
  
 [MDX 查詢基礎觀念 &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
 [MDX 指令碼基礎觀念 &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)  
  
##  <a name="bkmk_api"></a> 程式設計介面  
 如果您要建立使用多維度資料的自訂應用程式，您存取資料的方法最有可能分成下列其中一個類別：  
  
-   **XMLA**。 當您需要與多種作業系統和通訊協定相容時，請使用 XMLA。 XMLA 提供最大的彈性，但代價是犧牲提升的效能與程式設計的簡易性。  
  
-   **用戶端程式庫**。 當您想要從在 Microsoft Windows 作業系統上執行的用戶端程式使用程式設計方式存取資料時，請使用 Analysis Services 用戶端程式庫 (例如 ADOMD.NET、AMO 和 OLE DB)。 用戶端應用程式會使用提供更好效能的物件模型與最佳化包裝 XMLA。  
  
     ADOMD.NET 和 AMO 用戶端程式庫則供使用 Managed 程式碼撰寫的應用程式使用。 如果您的應用程式是以原生程式碼撰寫，請使用 OLE DB for Analysis Services。  
  
 下表提供連接 Analysis Services 與自訂應用程式所使用之用戶端程式庫的其他詳細資料和連結。  
  
|介面|描述|  
|---------------|-----------------|  
|Analysis Services 管理物件 (AMO)|AMO 是在程式碼中管理 Analysis Services 執行個體與多維度資料庫的主要物件模型。 例如，SQL Server Management Studio 使用 AMO 支援伺服器與資料庫管理。 如需詳細資訊，請參閱[使用分析管理物件 &#40;AMO&#41; 來開發](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)。|  
|ADOMD.NET|ADOMD.NET 是在自訂應用程式中建立與存取多維度資料的主要物件模型。 您可以使用通用的 Microsoft .NET Framework 資料存取介面，在 Managed 用戶端應用程式中使用 ADOMD.NET 來擷取 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資訊。 如需詳細資訊，請參閱 [使用 ADOMD.NET 來開發](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net) 和 [ADOMD.NET 用戶端程式設計](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/adomd-net-client-programming)。|  
|Analysis Services OLE DB 提供者 (MSOLAP.dll)|您可以使用原生 OLE DB 提供者，使用程式設計方式從 Unmanaged API 存取 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 如需詳細資訊，請參閱 [Analysis Services OLE DB 提供者 &#40;Analysis Services - 多維度資料&#41;](../../dev-guide/analysis-services-ole-db-provider-analysis-services-multidimensional-data.md)。|  
|結構描述資料列集|結構描述資料列集資料表是一種資料結構，其中包含有關在伺服器上部署之多維度模型的描述性資訊，以及有關伺服器上目前活動的資訊。 身為程式設計人員，您可以在用戶端應用程式中查詢結構描述資料列集資料表，以檢查儲存在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上的中繼資料，並從其擷取支援和監視資訊。 您可以搭配這些程式設計介面使用結構描述資料列集：OLE DB、 Analysis services OLE DB、 OLE DB 資料採礦或 XMLA。 如需詳細資訊，請參閱 [Analysis Services 結構描述資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets)。<br /><br /> 以下清單說明使用結構描述資料列集的數個方法：<br /><br /> 在 SQL Server Management Studio 或自訂報表中執行 DMV 查詢，以便使用 SQL 語法存取結構描述資料列集。 如需詳細資訊，請參閱[使用動態管理檢視 &#40;DMV&#41; 監視 Analysis Services](../../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)。<br /><br /> 撰寫呼叫結構描述資料列集的 ADOMD.NET 程式碼。<br /><br /> 直接針對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體執行 XMLA `Discover` 方法，以擷取結構描述資料列集資訊。 如需詳細資訊，請參閱 [Discover 方法 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)。|  
|XMLA|XMLA 是提供給 Analysis Services 程式設計人員的最低層級 API，也是做為所有 Analysis Services 資料存取方法的共同分母。 XMLA 是一種業界標準，SOAP 以 XML 通訊協定為基礎，支援通用資料透過 HTTP 連接，對於任何可用之標準多維度資料來源的存取。 它會使用 SOAP 編寫用於多維度資料的要求和回應。 如果您的應用程式在非 Windows 平台上執行，可以使用 XMLA 存取在網路上的 Windows 伺服器上執行的多維度資料庫。 如需詳細資訊，請參閱 [在 Analysis Services 中使用 XMLA 進行開發](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)。|  
|Analysis Services 指令碼語言 (ASSL)|ASSL 是一個適用於 XMLA 通訊協定之 Analysis Services 延伸模組的描述性詞彙。 ASSL 延伸模組可讓 Analysis Services 使用超出通訊協定基本提供範圍的 XMLA 建構函式，以增加資料定義、資料操作以及資料控制支援。  由於 Execute 和 Discover 方法是由 XMLA 通訊協定所描述，因此 ASSL 會加入下列功能：<br /><br /> XMLA 指令碼<br /><br /> XMLA 物件定義<br /><br /> XMLA 命令<br /><br /> <br /><br /> 如需詳細資訊，請參閱＜ [使用 Analysis Services 指令碼語言 &#40;ASSL&#41; 開發](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)＞。|  
  
## <a name="see-also"></a>另請參閱  
 [連接到 Analysis Services](../../instances/connect-to-analysis-services.md)   
 [使用 Analysis Services 指令碼語言 &#40;ASSL&#41; 開發](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [在 Analysis Services 中使用 XMLA 進行開發](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [表格式模型資料存取](../../tabular-models/tabular-model-data-access.md)  
  
  
