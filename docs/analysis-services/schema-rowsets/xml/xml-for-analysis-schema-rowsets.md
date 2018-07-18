---
title: XML for Analysis 結構描述資料列 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f85f7f1a0daa81a549441bff6a386213916f57f1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036089"
---
# <a name="xml-for-analysis-schema-rowsets"></a>XML for Analysis 結構描述資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 提供者所含的結構描述資料列集會傳回有關伺服器狀態、活動和物件的中繼資料。 如果您要開發連接到有可變結構和特性之 Analysis Services 模型的用戶端應用程式，需要擷取中繼資料。  
  
 結構描述資料列集還提供內部處理序和作業的洞察能力，可協助您監視伺服器並解決問題。 若要加強支援特定管理工作，您可以對大多數的結構描述資料列集執行動態管理檢視 (DMV) 查詢。 DMV 查詢會以可讀取、表格格式傳回結果，您可以在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 中檢視它們。  
  
 下表列出並描述每個 XMLA 結構描述資料列集，以及識別傳回資訊是表格式資料模型專屬的。  
  
## <a name="in-this-section"></a>本節內容  
  
|Rowset<sup>1</sup>|Description|  
|------------------------|-----------------|  
|[DISCOVER_CALC_DEPENDENCY 資料列集](../../../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md)|傳回關於資料表、資料行、量值和導出資料行公式間相依性的資訊。<br /><br /> 適用於 Analysis Services 執行個體上部署的表格式模型和[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]在 SharePoint 環境中執行的 Excel 活頁簿中的模型。|  
|[DISCOVER_CONNECTIONS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-connections-rowset.md)|提供有關伺服器上目前已開啟的連接之資源使用量與活動資訊。|  
|[DISCOVER_COMMAND_OBJECTS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-command-objects-rowset.md)|提供參考命令使用中之物件的資源使用量與活動的有關資訊。|  
|[DISCOVER_COMMANDS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-commands-rowset.md)|提供在伺服器上已開啟的連接中，目前執行或是上次執行的命令之資源使用量與活動資訊。|  
|[DISCOVER_CSDL_METADATA 資料列集](../../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)|資料來源的 XML 定義傳回到可以取用表格式用戶端或[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]模型，然後將來源資料呈現為報表的一部分。<br /><br /> 適用於 Analysis Services 執行個體上部署的表格式模型和[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]在 SharePoint 環境中執行的 Excel 活頁簿中的模型。|  
|[DISCOVER_DATASOURCES 資料列集](../../../analysis-services/schema-rowsets/xml/discover-datasources-rowset.md)|傳回可用於伺服器或 Web 服務的 XMLA 提供者資料來源清單。|  
|[DISCOVER_DB_CONNECTIONS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-db-connections-rowset.md)|提供有關目前從伺服器到資料庫之間已開啟之連接的資源使用量與活動資訊。|  
|[DISCOVER_DIMENSION_STAT 資料列集](../../../analysis-services/schema-rowsets/xml/discover-dimension-stat-rowset.md)|傳回指定之維度的統計資料。|  
|[DISCOVER_ENUMERATORS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)|針對特定的資料來源，傳回 XMLA 所支援之列舉值 (Enumerator) 的名稱、資料類型和列舉 (Enumeration) 值的清單。|  
|[DISCOVER_JOBS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-jobs-rowset.md)|提供在伺服器上執行之作用中作業的相關資訊。|  
|[DISCOVER_KEYWORDS 資料列集 & #40;XMLA & #41;](../../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)|傳回 XMLA 提供者所保留關鍵字的相關資訊。|  
|[DISCOVER_LITERALS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)|傳回 XMLA 提供者所支援常值的相關資訊，包括資料類型和值。|  
|[DISCOVER_LOCATIONS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-locations-rowset.md)|傳回備份檔案的內容資訊。|  
|[DISCOVER_LOCKS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-locks-rowset.md)|提供有關伺服器上目前永久性鎖定的資訊。|  
|[DISCOVER_MEMORYGRANT 資料列集](../../../analysis-services/schema-rowsets/xml/discover-memorygrant-rowset.md)|傳回伺服器上目前執行作業所使用之內部記憶體配額授權的清單。|  
|[DISCOVER_MEMORYUSAGE 資料列集](../../../analysis-services/schema-rowsets/xml/discover-memoryusage-rowset.md)|傳回伺服器所配置之各種物件的記憶體使用量統計資料。|  
|[DISCOVER_OBJECT_ACTIVITY 資料列集](../../../analysis-services/schema-rowsets/xml/discover-object-activity-rowset.md)|提供每個物件自從服務啟動之後的資源使用量資訊。|  
|[DISCOVER_OBJECT_MEMORY_USAGE 資料列集](../../../analysis-services/schema-rowsets/xml/discover-object-memory-usage-rowset.md)|提供物件使用之記憶體資源的有關資訊。|  
|[DISCOVER_PARTITION_DIMENSION_STAT 資料列集](../../../analysis-services/schema-rowsets/xml/discover-partition-dimension-stat-rowset.md)|傳回與資料分割相關之維度的統計資料。|  
|[DISCOVER_PARTITION_STAT 資料列集](../../../analysis-services/schema-rowsets/xml/discover-partition-stat-rowset.md)|傳回特定資料分割中彙總的相關統計資料。|  
|[DISCOVER_PERFORMANCE_COUNTERS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-performance-counters-rowset.md)|傳回一個或多個指定之效能計數器的值。|  
|[DISCOVER_PROPERTIES 資料列集](../../../analysis-services/schema-rowsets/xml/discover-properties-rowset.md)|針對指定的資料來源，傳回 XMLA 提供者所支援標準和提供者特定屬性的相關資訊及值清單。|  
|[DISCOVER_SCHEMA_ROWSETS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-schema-rowsets-rowset.md)|傳回 XMLA 提供者所支援之所有列舉值 (Enumeration Value) 以及任何其他的提供者特定列舉值的名稱、限制、描述和其他資訊。|  
|[DISCOVER_SESSIONS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-sessions-rowset.md)|提供伺服器上目前已開啟的工作階段之資源使用量與活動的有關資訊。|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-storage-table-column-segments-rowset.md)|提供有關表格式所使用的儲存體資料表資料行和區段層級的資訊或[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]資料庫。<br /><br /> 適用於 Analysis Services 執行個體上部署的表格式模型和[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]在 SharePoint 環境中執行的 Excel 活頁簿中的模型。|  
|[DISCOVER_STORAGE_TABLE_COLUMNS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-storage-table-columns-rowset.md)|可讓用戶端決定表格式所使用的儲存體資料表之資料行指派或[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]資料庫。<br /><br /> 適用於 Analysis Services 執行個體上部署的表格式模型和[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]在 SharePoint 環境中執行的 Excel 活頁簿中的模型。|  
|[DISCOVER_STORAGE_TABLES 資料列集](../../../analysis-services/schema-rowsets/xml/discover-storage-tables-rowset.md)|傳回模型中所用之資料表的相關資訊。<br /><br /> 適用於 Analysis Services 執行個體上部署的表格式模型和[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]在 SharePoint 環境中執行的 Excel 活頁簿中的模型。|  
|[DISCOVER_TRACE_COLUMNS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-trace-columns-rowset.md)|描述追蹤提供者所提供的追蹤資料行。|  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO 資料列集](../../../analysis-services/schema-rowsets/xml/discover-trace-definition-providerinfo-rowset.md)|傳回有關追蹤提供者的基本資訊，例如其名稱和說明。|  
|[DISCOVER_TRACE_EVENT_CATEGORIES 資料列集](../../../analysis-services/schema-rowsets/xml/discover-trace-event-categories-rowset.md)|描述追蹤提供者所提供的事件類別目錄。|  
|[DISCOVER_TRACES 資料列集](../../../analysis-services/schema-rowsets/xml/discover-traces-rowset.md)|傳回伺服器上執行之追蹤的相關資訊。|  
|[DISCOVER_TRANSACTIONS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-transactions-rowset.md)|傳回系統上目前的暫止交易集。|  
|[DISCOVER_XML_METADATA 資料列集](../../../analysis-services/schema-rowsets/xml/discover-xml-metadata-rowset.md)|傳回描述所要求物件的 XML 文件。|  
  
 <sup>1</sup>此處所列的所有結構描述資料列的 MSOLAP 資料來源提供者支援[!INCLUDE[msCoName](../../../includes/msconame-md.md)]XMLA 提供者。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Analysis Services 中的 XMLA 進行開發](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [使用動態管理檢視&#40;Dmv&#41;監視 Analysis Services](../../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)   
 [從分析資料來源擷取中繼資料](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  
