---
title: 表格式模型資料存取 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6ae74a8b-0025-450d-94a5-4e601831d420
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: af892b5d3fe0c05572c4c9abe8e0176051e313a2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="tabular-model-data-access"></a>表格式模型資料存取
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Analysis Services 中的表格式模型資料庫可由您用來擷取多維度模型中之資料或中繼資料的大部分相同用戶端、介面和語言所存取。 如需詳細資訊，請參閱[多維度模型資料存取 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)。  
  
 本文說明用戶端、 查詢語言和程式設計介面，使用表格式模型。  
  
## <a name="clients"></a>用戶端  
 下列 Microsoft 用戶端應用程式支援 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格式模型資料庫的原生連接。  
  
### <a name="power-bi"></a>Power BI
您可以從 [Power BI](https://powerbi.microsoft.com/)連接到內部部署 Analysis Services 表格式模型資料庫。 Power BI 是一套商業分析工具，可分析資料以及共用見解。 

### <a name="excel"></a>Excel  
 您可以使用 Excel 中的資料視覺效果與分析功能，從 Excel 連接至表格式模型資料庫，以處理您的資料。 若要存取資料，您要定義 Analysis Services 資料連接、指定在表格式伺服器模式下執行的伺服器，然後選擇您要使用的資料庫。 如需詳細資訊，請參閱＜ [連接到 SQL Server Analysis Services 或是從中匯入資料](http://go.microsoft.com/fwlink/?linkID=215150)＞。  
  
 Excel 也是在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中瀏覽表格式模型的建議應用程式。 這個工具包含 [在 Excel 中進行分析] 選項，此選項可啟動新的 Excel 執行個體、建立 Excel 活頁簿，並開啟活頁簿與模型工作空間資料庫之間的資料連接。 在 Excel 中瀏覽表格式模型資料時，請注意 Excel 會使用 Excel 樞紐分析表用戶端，針對模型發出查詢。 因此，Excel 活頁簿中的作業會導致 MDX 查詢傳送給工作空間資料庫，而不是 DAX 查詢。 如果您要使用 SQL Profiler 或其他監視工具來監視查詢，您預期可以在 Profiler 追蹤內看到 MDX 而非 DAX。 如需在 excel 中進行分析的詳細資訊，請參閱[在 Excel 中的進行分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)。  
  
### <a name="power-view"></a>Power View  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 是一個在 SharePoint 2010 環境下執行的 Reporting Services 報告用戶端應用程式。 它可將資料瀏覽、查詢設計和簡報配置結合成整合式的隨選報表體驗。 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 可以使用表格式模型當做資料來源，不論此模型是否裝載於以表格式模式執行的 Analysis Services 執行個體上，或者是否使用 DirectQuery 模式從關聯式資料存放區擷取模型資料。 若要連接至 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]中的表格式模型，您必須建立一個包含伺服器位置和資料庫名稱的連接檔案。 您可以在 SharePoint 中建立 Reporting Services 共用資料來源或 BI 語意模型連接檔案。 如需 BI 語意模型連接的詳細資訊，請參閱 [Power Pivot BI 語意模型連接 &#40;.bism&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)。  
  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 用戶端會藉由傳送要求給指定的資料來源來判斷指定之模型的結構，該資料來源會傳回可由用戶端使用的結構描述，以便針對資料來源形式的模型建立查詢，並執行以資料為根據的作業。 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 使用者介面中用來篩選資料、執行計算或彙總及顯示相關資料的後續作業是由用戶端所控制，而且無法以程式設計方式操作。  
  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 用戶端傳送給模型的查詢會當做 DAX 陳述式發出，您可以在模型上設定追蹤來加以監視。  在初始結構描述定義中，用戶端也會發出要求給伺服器，該定義是根據概念結構定義語言 (CSDL) 而呈現。 如需詳細資訊，請參閱 [商業智慧的 CSDL 註解 &#40;CSDLBI&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
### <a name="sql-server-management-studio"></a>Transact-SQL  
 您可使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來管理裝載表格式模型的執行個體及查詢其中的中繼資料和資料。 您可以處理模型或模型中的物件、建立及管理資料分割，以及設定可用於管理資料存取的安全性。 如需詳細資訊，請參閱下列主題：  
  
-   [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
-   [連接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
-   [監視 Analysis Services 執行個體](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用 MDX 和 XMLA 查詢視窗兩者，從表格式模型資料庫中擷取資料和中繼資料。 不過，請注意以下限制：  
  
-   已經在 DirectQuery 模式下部署的模型並不支援使用 MDX 和 DMX 的陳述式；因此，如果您需要針對 DirectQuery 模式中的表格式模型建立查詢，您應該改用 [XMLA 查詢] 視窗。  
  
-   在您開啟 [查詢] 視窗之後，便無法變更 [XMLA 查詢] 視窗的資料庫內容。 因此，如果您需要傳送查詢到不同的資料庫或不同的執行個體，您必須使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 開啟該資料庫或執行個體，並在該內容中開啟新的 [XMLA 查詢] 視窗。  
  
 您可以針對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格式模型建立追蹤，就像多維度方案一樣。 在這個版本中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會提供可用來追蹤記憶體使用量、查詢和處理作業與檔案使用狀況的許多新的事件。 如需詳細資訊，請參閱 [Analysis Services 追蹤事件](../../analysis-services/trace-events/analysis-services-trace-events.md)。  
  
> [!WARNING]  
>  如果您將追蹤放在表格式模型資料庫上，您可能會看到分類為 DMX 查詢的某些事件。 但是，表格式模型資料上並不支援資料採礦，而且資料庫上所執行的 DMX 查詢受限於模型中繼資料上的 SELECT 陳述式。 這些事件只會分類為 DMX，因為 MDX 會使用相同的剖析器架構。  
  
## <a name="query-languages"></a>查詢語言  
 Analysis Services 表格式模型可支援為了存取多維度模型所提供的大部分相同的查詢語言。 例外情況是已經在 DirectQuery 模式下部署的表格式模型，這些模型不會從 Analysis Services 資料存放區擷取資料，而是會直接從 SQL Server 資料來源擷取資料。 您不能使用 MDX 查詢這些模型，但是必須使用可支援將 DAX 運算式轉換為 Transact-SQL 陳述式的用戶端，例如 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 用戶端。  
  
### <a name="dax"></a>DAX  
 您可以在所有種類的表格式模型中使用 DAX 來建立運算式和公式，不論該模型是當做具有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]功能的 Excel 活頁簿儲存在 SharePoint 上還是儲存在 Analysis Services 執行個體上。  
  
 此外，您也可以在 XMLA EXECUTE 命令陳述式的內容中使用 DAX 運算式，將查詢傳送給已在 DirectQuery 模式下部署的表格式模型。  
  
 如需使用 DAX 查詢表格式模型的範例，請參閱 [DAX 查詢語法參考](http://msdn.microsoft.com/en-us/4dd0cf0e-191d-411d-987c-f606813fc39e)。  
  
### <a name="mdx"></a>MDX  
 您可以針對使用記憶體中快取當做慣用查詢方法的表格式模型 (也就是尚未在 DirectQuery 模式下部署的模型) 來使用 MDX 建立查詢。 雖然類似 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 的用戶端會使用 DAX 來建立彙總以及以資料來源的形式查詢模型，但是如果您很熟悉 MDX，它就可以成為在 MDX 中建立範例查詢的捷徑，請參閱 [在 MDX 中建立量值](../../analysis-services/multidimensional-models/mdx/mdx-building-measures.md)。  
  
### <a name="csdl"></a>CSDL  
 概念結構定義語言本身並不是查詢語言，但是可用來擷取有關模型和模型中繼資料的資訊，該資訊之後可用來建立報表或是針對模型建立查詢。  
  
 如需如何在表格式模型中使用 CSDL 的詳細資訊，請參閱 [商業智慧的 CSDL 註解 &#40;CSDLBI&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)。  
  
## <a name="programmatic-interfaces"></a>程式設計介面  
 用來與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格式模型互動的主要介面為結構描述資料列集、XMLA 及 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]所提供的查詢用戶端和查詢工具。  
  
### <a name="data-and-metadata"></a>資料和中繼資料  
 您可以在 Managed 應用程式中使用 ADOMD.NET 從表格式模型擷取資料和中繼資料。 
  
-   [使用動態管理檢視 & #40; Dmv & #41;監視 Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
 您可以在 Unmanaged 用戶端應用程式中使用 Analysis Services 9.0 OLE DB 提供者支援 OLE DB 存取表格式模型。 需要更新版本的 Analysis Services OLE DB 提供者來啟用表格式模型存取。 如需與表格式模型搭配使用之提供者的詳細資訊，請參閱 [在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859) 。  
  
 您也可以直接從 Analysis Services 執行個體擷取 XML 架構格式的資料。 您可以使用 DISCOVER_CSDL_METADATA 資料列集來擷取表格式模型的結構描述，或者搭配現有的 ASSL 元素、物件或屬性使用 EXECUTE 或 DISCOVER 命令。 자세한 내용은 다음 리소스를 참조하십시오.  
  
-   [商業智慧的 CSDL 註解 &#40;CSDLBI&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
### <a name="manipulate-analysis-services-objects"></a>操作 Analysis Services 物件  
 您可以利用 XMLA 命令或 AMO 來建立、修改、刪除和處理表格式模型以及模型中的物件，其中包括資料表、資料行、檢視方塊、量值和資料分割。 AMO 和 XMLA 都已更新，可支援表格式模型中所使用的其他屬性，以增強報告和模型化功能。  
  
  
### <a name="schema-rowsets"></a>結構描述資料列集  
 用戶端應用程式可以使用結構描述資料列集來檢查表格式模型的中繼資料，並從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器擷取支援和監視資訊。 在這個版本的 SQL Server 中，已加入新的結構描述資料列集，並擴充現有的結構描述資料列集來支援與表格式模型有關的功能及增強 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中的監視和效能分析。  
  
-   [DISCOVER_CALC_DEPENDENCY 資料列集](../../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md)  
  
     表格式模型中為了追蹤資料行與參考之間之相依性的新結構描述資料列集  
  
-   [DISCOVER_CSDL_METADATA 資料列集](../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)  
  
     為了取得表格式模型之 CSDL 表示法的新結構描述資料列集  
  
-   [DISCOVER_XEVENT_TRACE_DEFINITION 資料列集](http://msdn.microsoft.com/library/e1ce2d2d-f994-4318-801a-ee0385aecd84)  
  
     為了監視 SQL Server 擴充事件的新結構描述資料列集 如需詳細資訊，請參閱 [使用 SQL Server 擴充事件監視 Analysis Services](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)。  
  
-   [DISCOVER_TRACES 資料列集](../../analysis-services/schema-rowsets/xml/discover-traces-rowset.md)  
  
     新的 [類型] 資料行可讓您依據類別目錄篩選追蹤。 如需詳細資訊，請參閱[建立 Profiler 追蹤以重新執行 &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)。  
  
-   [MDSCHEMA_HIERARCHIES 資料列集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)  
  
     新的 **STRUCTURE_TYPE** 列舉可支援在表格式模型中建立之使用者定義階層的識別。 如需詳細資訊，請參閱[階層](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)。  
  
 這個版本中的 OLE DB for Data Mining 結構描述資料列集沒有更新。  
  
> [!WARNING]  
>  您不能在已經於 DirectQuery 模式下部署的資料庫中使用 MDX 或 DMX 查詢；因此，如果您需要使用結構描述資料列集來針對 DirectQuery 模式執行查詢，您應該使用 XMLA 而不是關聯的 DMV。 如果是整體會傳回伺服器結果的 DMV，例如來自 $system.DBSCHEMA_CATALOGS 或 DISCOVER_TRACES 的 SELECT *，您可以在快取模式中部署的資料庫內容中執行查詢。  
  
## <a name="see-also"></a>另請參閱  
 [連接到表格式模型資料庫 ](../../analysis-services/tabular-models/connect-to-a-tabular-model-database-ssas.md)   
 [Power Pivot 資料存取](../../analysis-services/power-pivot-sharepoint/power-pivot-data-access.md)   
 [連接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
