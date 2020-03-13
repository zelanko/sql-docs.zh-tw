---
title: 使用動態管理檢視（Dmv）來監視 Analysis Services |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 22b82b2d-867f-4ebf-9288-79d1cdd62f18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1827cf0acf8e600c58efca82bb3223a00efb3e41
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79217114"
---
# <a name="use-dynamic-management-views-dmvs-to-monitor-analysis-services"></a>使用動態管理檢視 (DMV) 監視 Analysis Services
  Analysis Services 動態管理檢視 (DMV) 是公開本機伺服器作業和伺服器健全狀況相關資訊的查詢結構。 查詢結構是傳回 Analysis Services 執行個體中繼資料和監視資訊之結構描述資料列集的介面。  
  
 對於大多數 DMV 查詢，都是將 `SELECT` 陳述式和 `$System` 結構描述搭配 XML/A 結構描述資料列集使用。  
  
```  
SELECT * FROM $System.<schemaRowset>  
```  
  
 DMV 查詢傳回查詢執行當時的伺服器狀態資訊。 若要即時監視作業，請改用追蹤。 如需詳細資訊，請參閱 [Use SQL Server Profiler to Monitor Analysis Services](use-sql-server-profiler-to-monitor-analysis-services.md)。  
  
 這個主題包括下列各節：  
  
 [使用 DMV 查詢的優點](#bkmk_ben)  
  
 [範例和案例](#bkmk_ex)  
  
 [查詢語法](#bkmk_syn)  
  
 [工具和許可權](#bkmk_tools)  
  
 [DMV 參考](#bkmk_ref)  
  
##  <a name="bkmk_ben"></a>使用 DMV 查詢的優點  
 DMV 查詢所傳回的作業和資源耗用資訊，無法透過其他方式提供。  
  
 DMV 查詢是執行 XML/A Discover 命令的替代方法。 對於大多數系統管理員，撰寫 DMV 查詢比較簡單，因為查詢語法以 SQL 為基礎。 此外，結果集是以表格格式傳回，更易於讀取和複製。  
  
##  <a name="bkmk_ex"></a>範例和案例  
 DMV 查詢有助於回答有關使用中工作階段和連接的問題，以及哪些物件在特定時間點耗用最多 CPU 或記憶體的問題。 本節提供最常使用 DMV 查詢的案例範例。 您也可以檢閱＜ [SQL Server 2008 R2 Analysis Services 作業指南](https://go.microsoft.com/fwlink/?LinkID=225539&clcid=0x409) ＞，以取得使用 DMV 查詢監視伺服器執行個體的其他見解。  
  
 
  `Select * from $System.discover_object_activity` /** 此查詢報告自上次啟動服務後的物件活動。 如需以此 DMV 為基礎的範例查詢，請參閱 [新的 System.Discover_Object_Activity](https://go.microsoft.com/fwlink/?linkid=221322)。  
  
 
  `Select * from $System.discover_object_memory_usage` /** 此查詢依物件來報告記憶體耗用量。  
  
 
  `Select * from $System.discover_sessions` /** 此查詢報告使用中工作階段，包括工作階段使用者和持續時間。  
  
 
  `Select * from $System.discover_locks` /** 此查詢傳回在特定時間點所用鎖定的快照集。  
  
##  <a name="bkmk_syn"></a>查詢語法  
 DMV 的查詢引擎是資料採礦剖析器。 DMV 查詢語法以 [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx) 陳述式為基礎。  
  
 雖然 DMV 查詢語法以 SQL SELECT 陳述式為基礎，但不支援 SELECT 陳述式的完整語法。 特別是，JOIN、GROUP BY、LIKE、CAST 和 CONVERT 也不受支援。  
  
```  
SELECT [DISTINCT] [TOP <n>] <select list>  
FROM $System.<schemaRowset>  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
 下列的 DISCOVER_CALC_DEPENDENCY 範例示範如何使用 WHERE 子句提供查詢的參數：  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY  
WHERE OBJECT_TYPE = 'ACTIVE_RELATIONSHIP'  
```  
  
 另外，對於有限制的結構描述資料列集，查詢必須包含 SYSTEMRESTRICTSCHEMA 函數。 下列範例會傳回有關在表格式模式伺服器上執行之表格式模型的 CSDL 中繼資料。 請注意 CATALOG_NAME 會區分大小寫：  
  
```  
Select * from SYSTEMRESTRICTSCHEMA ($System.Discover_csdl_metadata, [CATALOG_NAME] = 'Adventure Works DW')  
```  
  
##  <a name="bkmk_tools"></a>工具和許可權  
 您必須具有 Analysis Services 執行個體的系統管理員權限，才能查詢 DMV。  
  
 您可以使用任何支援 MDX 或 DMX 查詢的用戶端應用程式，包括 SQL Server Management Studio、Reporting Services 報表或 PerformancePoint 儀表板。  
  
 若要從 Management Studio 執行 DMV 查詢，請連接到您要查詢的執行個體，然後按一下 **[新增查詢]**。 可從 MDX 或 DMX 查詢視窗執行查詢。  
  
##  <a name="bkmk_ref"></a>DMV 參考  
 並不是所有結構描述資料列集都有 DMV 介面。 若要傳回可透過 DMV 查詢之所有結構描述資料列集的清單，請使用下列查詢。  
  
```  
SELECT * FROM $System.DBSchema_Tables   
WHERE TABLE_TYPE = 'SCHEMA'   
ORDER BY TABLE_NAME ASC  
```  
  
> [!NOTE]  
>  如果指定的資料列集無法使用 DMV，伺服器會傳回下列錯誤：「伺服器無法辨識\<schemarowset> 要求類型」。 所有其他錯誤都指向語法問題。  
  
|資料列集|描述|  
|------------|-----------------|  
|[DBSCHEMA_CATALOGS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db/dbschema-catalogs-rowset)|傳回目前連接上 Analysis Services 資料庫的清單。|  
|[DBSCHEMA_COLUMNS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db/dbschema-columns-rowset)|傳回目前資料庫中所有資料行的清單。 您可以使用此清單來建構 DMV 查詢。|  
|[DBSCHEMA_PROVIDER_TYPES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db/dbschema-provider-types-rowset)|傳回 OLE DB 資料提供者所支援之基底資料型別的相關屬性。|  
|[DBSCHEMA_TABLES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db/dbschema-tables-rowset)|傳回目前資料庫中所有資料表的清單。 您可以使用此清單來建構 DMV 查詢。|  
|[DISCOVER_CALC_DEPENDENCY 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-calc-dependency-rowset)|傳回模型中所用資料行和資料表的清單，而這些有其他資料行和資料表的相依性。|  
|[DISCOVER_COMMAND_OBJECTS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-command-objects-rowset)|提供所參考命令使用中之物件的資源使用量與活動資訊。|  
|[DISCOVER_COMMANDS 資料列集](https://docs.microsoft.com/analysis-services/instances/analysis-services-schema-rowsets)|提供有關目前執行中命令的資源使用量和活動資訊。|  
|[DISCOVER_CONNECTIONS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-connections-rowset)|提供有關 Analysis Services 開啟連接之資源使用量與活動資訊。|  
|[DISCOVER_CSDL_METADATA 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-csdl-metadata-rowset)|傳回表格式模型的相關資訊。<br /><br /> 需要加入 SYSTEMRESTRICTSCHEMA 和其他參數。|  
|[DISCOVER_DB_CONNECTIONS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-db-connections-rowset)|提供從 Analysis Services 到外部資料來源的開啟連接 (例如處理或匯入期間) 的資源使用量與活動資訊。|  
|[DISCOVER_DIMENSION_STAT 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-dimension-stat-rowset)|傳回維度中的屬性或資料表中的資料行，視模型類型而定。|  
|[DISCOVER_ENUMERATORS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-enumerators-rowset)|傳回有關特定資料來源所支援之列舉值的中繼資料。|  
|[DISCOVER_INSTANCES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/discover-instances-rowset)|傳回指定之執行個體的相關資訊。<br /><br /> 需要加入 SYSTEMRESTRICTSCHEMA 和其他參數。|  
|[DISCOVER_JOBS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-jobs-rowset)|傳回目前作業的相關資訊。|  
|[DISCOVER_KEYWORDS 資料列集 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-keywords-rowset-xmla)|傳回保留關鍵字的清單。|  
|[DISCOVER_LITERALS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-literals-rowset)|傳回 XMLA 所支援常值的清單，包括資料類型和值。|  
|[DISCOVER_LOCKS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-locks-rowset)|傳回在特定時間點所用鎖定的快照集。|  
|[DISCOVER_MEMORYGRANT 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-memorygrant-rowset)|傳回 Analysis Services 在啟動時所配置記憶體的相關資訊。|  
|[DISCOVER_MEMORYUSAGE 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-memoryusage-rowset)|顯示特定物件的記憶體使用量。|  
|[DISCOVER_OBJECT_ACTIVITY 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-object-activity-rowset)|報告自上次啟動服務後的物件活動。|  
|[DISCOVER_OBJECT_MEMORY_USAGE 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-object-memory-usage-rowset)|依物件來報告記憶體耗用量。|  
|[DISCOVER_PARTITION_DIMENSION_STAT 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-partition-dimension-stat-rowset)|提供有關維度屬性的資訊。<br /><br /> 需要加入 SYSTEMRESTRICTSCHEMA 和其他參數。|  
|[DISCOVER_PARTITION_STAT 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-partition-stat-rowset)|提供有關維度、資料表或量值群組之分割區的資訊。<br /><br /> 需要加入 SYSTEMRESTRICTSCHEMA 和其他參數。|  
|[DISCOVER_PERFORMANCE_COUNTERS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-performance-counters-rowset)|列出效能計數器所用的資料行。<br /><br /> 需要加入 SYSTEMRESTRICTSCHEMA 和其他參數。|  
|[DISCOVER_PROPERTIES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-properties-rowset)|傳回有關 XMLA 支援用於指定資料來源之屬性的資訊。|  
|[DISCOVER_SCHEMA_ROWSETS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-schema-rowsets-rowset)|傳回 XMLA 所支援之所有列舉值的名稱、限制、描述和其他資訊。|  
|[DISCOVER_SESSIONS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-sessions-rowset)|報告使用中工作階段，包括工作階段使用者和持續時間。|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-storage-table-column-segments-rowset)|提供在資料行和區段層級中，有關表格式或 SharePoint 模式下執行 Analysis Services 資料庫所用儲存體資料表的資訊。|  
|[DISCOVER_STORAGE_TABLE_COLUMNS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-storage-table-columns-rowset)|允許用戶端決定在表格式或 SharePoint 模式下執行之 Analysis Services 資料庫所用的儲存體資料表之資料行指派。|  
|[DISCOVER_STORAGE_TABLES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-storage-tables-rowset)|傳回有關表格式模型資料庫中用於模型儲存之資料表的資訊。|  
|[DISCOVER_TRACE_COLUMNS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-trace-columns-rowset)|傳回追蹤中可用資料行的 XML 描述。|  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-trace-definition-providerinfo-rowset)|傳回提供者的名稱和版本資訊。|  
|[DISCOVER_TRACE_EVENT_CATEGORIES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-trace-event-categories-rowset)|傳回可用類別目錄的清單。|  
|[DISCOVER_TRACES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-traces-rowset)|傳回目前連接上正在執行之追蹤的清單。|  
|[DISCOVER_TRANSACTIONS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-transactions-rowset)|傳回目前連接上正在執行之交易的清單。|  
|[DISCOVER_XEVENT_TRACE_DEFINITION 資料列集](../dev-guide/discover-xevent-trace-definition-rowset.md)|傳回目前連接上正在執行之 XEvent 追蹤的清單。|  
|[DMSCHEMA_MINING_COLUMNS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-columns-rowset)|列出目前連接上所有可用採礦模型的個別資料行。|  
|[DMSCHEMA_MINING_FUNCTIONS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-functions-rowset)|傳回伺服器上資料採礦演算法所支援之函數的清單。|  
|[DMSCHEMA_MINING_MODEL_CONTENT 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)|傳回由描述目前模型之資料行組成的資料列集。|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset)|傳回由描述目前 PMML 格式模型之資料行組成的資料列集。|  
|[DMSCHEMA_MINING_MODEL_XML 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-xml-rowset)|傳回由描述目前 PMML 格式模型之資料行組成的資料列集。|  
|[DMSCHEMA_MINING_MODELS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-models-rowset)|傳回目前資料庫之採礦模型的清單。|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset)|傳回伺服器上演算法參數的清單。|  
|[DMSCHEMA_MINING_SERVICES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset)|提供伺服器上可用資料採礦演算法的清單。|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset)|傳回目前連接上所有可用採礦模型的所有資料行的清單。|  
|[DMSCHEMA_MINING_STRUCTURES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-structures-rowset)|列出目前連接中可用的採礦結構。|  
|[MDSCHEMA_CUBES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-cubes-rowset)|傳回目前資料庫所定義之 Cube 的相關資訊。|  
|[MDSCHEMA_DIMENSIONS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-dimensions-rowset)|傳回目前資料庫所定義之維度的相關資訊。|  
|[MDSCHEMA_FUNCTIONS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-functions-rowset)|傳回可用於與資料庫相連接的用戶端應用程式之函數的清單。|  
|[MDSCHEMA_HIERARCHIES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset)|傳回目前資料庫所定義之階層的相關資訊。|  
|[MDSCHEMA_INPUT_DATASOURCES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset)|傳回目前資料庫所定義之資料來源物件的相關資訊。|  
|[MDSCHEMA_KPIS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-kpis-rowset)|傳回目前資料庫所定義之 KPI 的相關資訊。|  
|[MDSCHEMA_LEVELS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-levels-rowset)|傳回目前資料庫所定義之階層層級的相關資訊。|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS 資料列集](https://docs.microsoft.com/openspecs/sql_server_protocols/ms-ssas/e6399481-a289-41f3-94d2-e081bf29e094)|列出量值群組的維度。|  
|[MDSCHEMA_MEASUREGROUPS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-measuregroups-rowset)|傳回目前連接中量值群組的清單。|  
|[MDSCHEMA_MEASURES 資料列集](https://docs.microsoft.com/openspecs/sql_server_protocols/ms-ssas/ab8e721f-9b9c-4ba1-b105-37a5f200d67c)|傳回目前連接中量值的清單。|  
|[MDSCHEMA_MEMBERS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-members-rowset)|傳回目前連接上所有成員的清單，依資料庫、Cube 和維度列出。|  
|[MDSCHEMA_PROPERTIES 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-properties-rowset)|傳回每個屬性的完整名稱，以及屬性類型、資料類型和其他中繼資料。|  
|[MDSCHEMA_SETS 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-sets-rowset)|傳回目前連接所定義之集合的清單。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2008 R2 Analysis Services 操作指南](https://go.microsoft.com/fwlink/?LinkID=225539&clcid=0x409)   
 [新增 System. Discover_Object_Activity](https://go.microsoft.com/fwlink/?linkid=221322)   
 [限制資料列集和 Dmv 的新 SYSTEMRESTRICTEDSCHEMA 函數](https://go.microsoft.com/fwlink/?LinkId=231885)  
  
  
