---
title: 查詢設計工具的報表設計工具的 SQL Server Data Tools (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- graphical query designer [Reporting Services]
- MDX query designer [Reporting Services]
- text-based query designer [Reporting Services]
- DMX [Reporting Services]
- query designers [Reporting Services]
- generic query designer See text-based query designer
- Reporting Services, query designers
- semantic queries [Reporting Services]
- Report Model Query Designer
ms.assetid: a8139a9d-4aeb-4e64-96f3-564edf60479f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a7b952414a86a647655a7a0c0dbc2754b352e671
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107179"
---
# <a name="query-design-tools-in-report-designer-sql-server-data-tools-ssrs"></a>SQL Server 資料工具中報表設計師的查詢設計工具 (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供各種查詢設計工具，您可以在報表設計師中利用這些工具來建立資料集查詢。 您使用的資料來源類型會決定特定查詢設計工具的可用性。 此外，某些查詢設計工具還提供替代模式，讓您能夠選擇使用視覺化模式或直接使用查詢語言。 本主題簡介每個工具，並描述每個工具支援的資料來源類型。 本主題將描述下列工具：  
  
-   [以文字為基礎的查詢設計工具](#Textbased)  
  
-   [圖形化查詢設計工具](#Graphical)  
  
-   [報表模型查詢設計工具](#Model)  
  
-   [MDX 查詢設計工具](#MDX)  
  
-   [DMX 查詢設計工具](#DMX)  
  
-   [SapNetWeaver BI 查詢設計工具](#SAPBW)  
  
-   [Hyperion Essbase 查詢設計工具](#Hyperion)  
  
 當您使用報表伺服器專案範本或報表伺服器精靈專案範本時，所有的查詢設計工具都會在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的資料設計環境中執行。 如需使用查詢設計工具的詳細資訊，請參閱 [Reporting Services 查詢設計工具](../reporting-services-query-designers.md)。  
  
##  <a name="Textbased"></a> 以文字為基礎的查詢設計工具  
 以文字為基礎的查詢設計工具是預設的查詢建立工具，它適用於大部分支援的關聯式資料來源，包括 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、Oracle、Teradata、OLE DB、XML 和 ODBC。 相較於圖形化查詢設計工具，此查詢設計工具在查詢設計期間並不會驗證查詢語法。 下圖說明以文字為基礎的查詢設計工具。  
  
 ![關聯式資料查詢的一般查詢設計工具](../../analysis-services/media/rsqd-dsaw-sql-generic.gif "關聯式資料查詢的一般查詢設計工具")  
  
 建議您利用以文字為基礎的查詢設計工具來建立複雜的查詢、使用預存程序、查詢 XML 資料，以及撰寫動態查詢。 根據資料來源，您可能可以切換工具列上的 [當成文字編輯]  按鈕，以便在圖形化查詢設計工具和以文字為基礎的查詢設計工具之間切換。 如需詳細資訊，請參閱 [以文字為基礎的查詢設計工具使用者介面](../text-based-query-designer-user-interface.md)。  
  
##  <a name="Graphical"></a> 圖形化查詢設計工具  
 圖形化查詢設計工具用於建立或修改根據關聯式資料庫執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢。 此查詢設計工具可用於數種 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 產品以及其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 元件。 根據資料來源類型，它支援文字模式、StoredProcedure 模式和 TableDirect 模式。 下圖說明圖形化查詢設計工具。  
  
 ![SQL 查詢適用的圖形化查詢設計工具](../media/rsqd-dsaw-sql.gif "SQL 查詢適用的圖形化查詢設計工具")  
  
 您可以切換工具列上的 [當成文字編輯]  按鈕，以便在圖形化查詢設計工具和以文字為基礎的查詢設計工具之間切換。 如需詳細資訊，請參閱 [圖形化查詢設計工具使用者介面](graphical-query-designer-user-interface.md)。  
  
##  <a name="Model"></a> 報表模型查詢設計工具  
 報表模型查詢設計工具是用於建立或修改針對已發行至報表伺服器的 SMDL 報表模型所執行的查詢。 針對模型執行的報表支援 clickthrough 資料瀏覽。 查詢會在執行階段判斷資料瀏覽的路徑。 下圖說明報表模型查詢設計工具。  
  
 ![語意模型查詢設計工具 UI](../media/rsqd-dsawmodel-smql.gif "語意模型查詢設計工具 UI")  
  
 若要使用報表模型查詢設計工具，您必須定義指向已發行模型的資料來源。 當您定義資料來源的資料集時，您可以在報表模型查詢設計工具中開啟資料集查詢。 報表模型查詢設計工具可用於圖形化模式或以文字為基礎的模式。 您可以切換工具列上的 [當成文字編輯]  按鈕，以便在圖形化查詢設計工具和以文字為基礎的查詢設計工具之間切換。 如需詳細資訊，請參閱 [報表模型查詢設計工具使用者介面](report-model-query-designer-user-interface.md)。  
  
##  <a name="MDX"></a> MDX 查詢設計工具  
 多維度運算式 (MDX) 查詢設計工具用於建立或修改針對包含多維度 Cube 之 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料來源所執行的查詢。 下圖說明定義查詢和篩選之後的 MDX 查詢設計工具。  
  
 ![Analysis Services MDX 查詢設計工具，設計檢視](../../analysis-services/media/rsqd-dsawas-mdx-designmode.gif "Analysis Services MDX 查詢設計工具，設計檢視")  
  
 若要使用 MDX 查詢設計工具，您定義的資料來源必須包含有效而且已經經過處理的可用 Analysis Services Cube。 當您定義資料來源的資料集時，您可以在 MDX 查詢設計工具中開啟查詢。 必要時，使用工具列上的 MDX 和 DMX 按鈕，在 MDX 與 DMX 模式之間切換。 如需詳細資訊，請參閱 [Analysis Services MDX 查詢設計工具使用者介面](analysis-services-mdx-query-designer-user-interface.md)。  
  
##  <a name="DMX"></a> DMX 查詢設計工具  
 資料採礦預測運算式 (DMX) 查詢設計工具用於建立或修改針對包含採礦模型之 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料來源所執行的查詢。 下圖說明選取模型和輸入資料表之後的 DMX 查詢設計工具。  
  
 ![Analysis Services DMX 查詢設計工具，設計檢視](../media/rsqd-dsawas-dmx-designmode.gif "Analysis Services DMX 查詢設計工具，設計檢視")  
  
 若要使用 DMX 查詢設計工具，您定義的資料來源必須已經包含有效的可用資料採礦模型。 當您定義資料來源的資料集時，您可以在 DMX 查詢設計工具中開啟查詢。 必要時，使用工具列上的 MDX 和 DMX 按鈕，在 MDX 與 DMX 模式之間切換。 選取模型之後，您可以建立資料採礦預測查詢，提供資料給報表。 如需詳細資訊，請參閱 [Analysis Services MDX 查詢設計工具使用者介面](analysis-services-dmx-query-designer-user-interface.md)。  
  
##  <a name="SAPBW"></a> Sap NetWeaver BI 查詢設計工具  
 [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] 查詢設計工具用於擷取 [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] 資料庫中的資料。 若要使用此查詢設計工具，您所具備的 [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] 資料來源必須至少已經定義一個 InfoCube、MultiProvider 或 Web 查詢。 下圖說明 [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] 查詢設計工具。  
  
 ![在設計模式下使用 MDX 的查詢設計工具](../media/rsqd-dssapbw-mdx-designmode.gif "在設計模式下使用 MDX 的查詢設計工具")  
  
##  <a name="Hyperion"></a> Hyperion Essbase 查詢設計工具  
 [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] 查詢設計工具是用來擷取 [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] 資料庫與應用程式中的資料。 下圖說明 [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] 查詢設計工具。  
  
 ![Hyperion Essbase 資料來源的查詢設計工具](../media/rsqd-dshyperionessbase-mdx-designmode.gif "Hyperion Essbase 資料來源的查詢設計工具")  
  
 若要使用此查詢設計工具，您所具備的 [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] 資料來源必須至少擁有一個資料庫。 如需詳細資訊，請參閱 [SAP Netweaver BI 查詢設計工具使用者介面](sap-netweaver-bi-query-designer-user-interface.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 工具](../tools/reporting-services-tools.md)   
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-datasets-ssrs.md)   
 [資料連接、 資料來源和 Reporting Services 中的連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Reporting Services 教學課程 &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)   
 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [建立內嵌或共用資料來源 &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)  
  
  
