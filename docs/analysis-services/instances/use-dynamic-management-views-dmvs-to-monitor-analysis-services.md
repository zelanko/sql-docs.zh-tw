---
title: Analysis Services 中使用動態管理檢視 (Dmv) |Microsoft Docs
ms.date: 09/25/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 24dd1bce8d7433f55ba64eecb1e7a08396b9e548
ms.sourcegitcommit: 38076f423663bdbb42f325e3d0624264e05beda1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/06/2018
ms.locfileid: "52984099"
---
# <a name="dynamic-management-views-dmvs"></a>動態管理檢視 (DMV) 

[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

Analysis Services 動態管理檢視 (DMV) 會傳回模型物件、 伺服器作業和伺服器健全狀況的相關資訊的查詢。 查詢中，SQL，基礎是介面*結構描述資料列集*。 結構描述資料列集是 predescribed 包含 Analysis Services 物件和伺服器狀態，包括資料庫結構描述、 使用中工作階段、 連接、 命令及伺服器執行的作業資訊的資料表。

DMV 查詢是執行 XML/A Discover 命令的替代方法。 對於大部分的系統管理員，撰寫 DMV 查詢比較簡單，因為語法以 SQL 為基礎。 此外，可以更輕鬆地讀取和複製以資料表格式傳回結果。 
  
大多數 DMV 查詢會使用 **選取** 陳述式並 **$System** 結構描述搭配 XML/A 結構描述資料列集的範例：  
  
```  
SELECT * FROM $System.<schemaRowset>  
```  
  
 DMV 查詢會傳回伺服器和物件狀態資訊時執行查詢。 若要監視在即時的方式，使用改用追蹤的作業。 若要深入了解即時監視使用追蹤，請參閱[使用 SQL Server Profiler 監視 Analysis services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)。  
  
## <a name="query-syntax"></a>查詢語法

DMV 的查詢引擎是資料採礦剖析器。 DMV 查詢語法會根據 SELECT &#40;DMX&#41;陳述式。 雖然 DMV 查詢語法以 SQL SELECT 陳述式為基礎，但不支援 SELECT 陳述式的完整語法。 特別是，JOIN、GROUP BY、LIKE、CAST 和 CONVERT 也不受支援。  
  
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
  
有限制的結構描述資料列，查詢必須包含 SYSTEMRESTRICTSCHEMA 函數。 下列範例會傳回約 1103年相容性層級表格式模型的 CSDL 中繼資料。 請注意 CATALOG_NAME 會區分大小寫：  
  
```  
Select * from SYSTEMRESTRICTSCHEMA ($System.Discover_csdl_metadata, [CATALOG_NAME] = 'Adventure Works DW')  
```  

## <a name="examples-and-scenarios"></a>範例和案例

DMV 查詢有助於回答有關使用中工作階段和連接的問題，以及哪些物件在特定時間點耗用最多 CPU 或記憶體的問題。 例如：
  
 `Select * from $System.discover_object_activity`  
自上次啟動服務後，此查詢會報告的物件活動。 
  
 `Select * from $System.discover_object_memory_usage`  
物件，將此查詢報告記憶體耗用量。  
  
 `Select * from $System.discover_sessions`  
此查詢報告使用中工作階段，包括工作階段使用者和持續時間。  
  
 `Select * from $System.discover_locks`   
此查詢會傳回在特定時間點所用的時間鎖定的快照集。  


## <a name="tools-and-permissions"></a>工具與權限

您可以使用任何支援 MDX 或 DMX 查詢的用戶端應用程式。 在大部分情況下，最好是使用 SQL Server Management Studio。 您必須具有伺服器系統管理員權限才能查詢 DMV 的執行個體上。  
  
 **若要從 SQL Server Management Studio 執行 DMV 查詢**

1. 連線到伺服器，您想要查詢的模型物件。 
2. 以滑鼠右鍵按一下伺服器或資料庫物件 >**新的查詢** > **MDX**。
3. 輸入您的查詢，然後按一下**Execute**，或按 F5。
  
## <a name="schema-rowsets"></a>結構描述資料列集

並不是所有結構描述資料列集都有 DMV 介面。 若要傳回可透過 DMV 查詢之所有結構描述資料列集的清單，請使用下列查詢。  
 
```  
SELECT * FROM $System.DBSchema_Tables   
WHERE TABLE_TYPE = 'SCHEMA'   
ORDER BY TABLE_NAME ASC  
```  
  
如果 DMV 不適用於給定的資料列集，伺服器就會傳回錯誤：`The <schemarowset> request type was not recognized by the server.` 所有其他錯誤指出語法問題。  

結構描述資料列是以兩種 SQL Server Analysis Services 通訊協定所述：   

[[MS-SSAS-T]:SQL Server Analysis Services 表格式通訊協定](https://msdn.microsoft.com/library/mt719260)-描述 1200年及以上的相容性層級的表格式模型的結構描述資料列。

[[MS-SSAS]:SQL Server Analysis Services 通訊協定](https://msdn.microsoft.com/library/ee320606)-描述多維度模型和表格式模型 1100年和 1103年相容性層級的結構描述資料列集。

### <a name="rowsets-described-in-the-ms-ssas-t-sql-server-analysis-services-tabular-protocol"></a>[MS-SSAS-T] 中所述的資料列集：SQL Server Analysis Services 表格式通訊協定

|資料列集  |描述  |
|---------|---------|
|[TMSCHEMA_ANNOTATIONS](https://msdn.microsoft.com/library/mt704370)|提供模型中的註釋物件的相關資訊。|
|[TMSCHEMA_ATTRIBUTE_HIERARCHIES](https://msdn.microsoft.com/library/mt704362)     |   提供資料行與 AttributeHierarchy 物件的相關資訊。      |
|[TMSCHEMA_COLUMNS](https://msdn.microsoft.com/library/mt704373)    |  提供每個資料表中的資料行物件的相關資訊。       |
|[TMSCHEMA_COLUMN_PERMISSIONS](https://msdn.microsoft.com/library/mt842440)|提供 ColumnPermission 物件中每個資料表權限的相關資訊。|
|[TMSCHEMA_CULTURES](https://msdn.microsoft.com/library/mt719125)|提供模型中的文化特性物件的相關資訊。|
|[TMSCHEMA_DATA_SOURCES](https://msdn.microsoft.com/library/mt719191)   |   提供模型中的資料來源物件的相關資訊。      |
|[TMSCHEMA_DETAIL_ROWS_DEFINITIONS](https://msdn.microsoft.com/library/mt825017)|提供模型中的 DetailRowsDefinition 物件的相關資訊。|
|[TMSCHEMA_EXPRESSIONS](https://msdn.microsoft.com/library/mt825015)|提供運算式物件模型中的相關資訊。|
|[TMSCHEMA_EXTENDED_PROPERTIES](https://msdn.microsoft.com/library/mt842451)|提供模型中的 ExtendedProperty 物件的相關資訊。|
|[TMSCHEMA_HIERARCHIES](https://msdn.microsoft.com/library/mt719136)    |    提供每個資料表中的階層物件的相關資訊。     |
|[TMSCHEMA_KPIS](https://msdn.microsoft.com/library/mt719002)     |    提供模型中的 KPI 物件的相關資訊。     |
|[TMSCHEMA_LEVELS](https://msdn.microsoft.com/library/mt719038)     |   提供在每個階層層級物件的相關資訊。      |
|[TMSCHEMA_LINGUISTIC_METADATA](https://msdn.microsoft.com/library/mt719169)|提供模型中的特定文化特性的物件的同義字的相關資訊|
|[TMSCHEMA_MEASURES](https://msdn.microsoft.com/library/mt719218)     |    提供每個資料表中的量值物件的相關資訊。     |
|[TMSCHEMA_MODEL](https://msdn.microsoft.com/library/mt719042)    |  指定資料庫中的模型物件。       |
|[TMSCHEMA_OBJECT_TRANSLATIONS](https://msdn.microsoft.com/library/mt719119)|提供文化特性的不同物件的翻譯的相關資訊。|
|[TMSCHEMA_PARTITIONS](https://msdn.microsoft.com/library/mt704375)     |     提供每個資料表中的資料分割物件的相關資訊。    |
|[TMSCHEMA_PERSPECTIVE_COLUMNS](https://msdn.microsoft.com/library/mt719164)     |   提供 PerspectiveColumn 物件中每個 PerspectiveTable 物件的相關資訊。      |
|[TMSCHEMA_PERSPECTIVE_HIERARCHIES](https://msdn.microsoft.com/library/mt719104)     |  提供 PerspectiveHierarchy 物件中每個 PerspectiveTable 物件的相關資訊。       |
|[TMSCHEMA_PERSPECTIVE_MEASURES](https://msdn.microsoft.com/library/mt719135)     |    提供 PerspectiveMeasure 物件中每個 PerspectiveTable 物件的相關資訊。     |
|[TMSCHEMA_PERSPECTIVE_TABLES](https://msdn.microsoft.com/library/mt719272)     |    提供在檢視方塊資料表物件的相關資訊。     |
|[TMSCHEMA_PERSPECTIVES](https://msdn.microsoft.com/library/mt704340)     |     提供模型中的檢視方塊物件的相關資訊。    |
|[TMSCHEMA_RELATIONSHIPS](https://msdn.microsoft.com/library/mt704355)     |    提供模型中的關聯性物件的相關資訊。     |
|[TMSCHEMA_ROLE_MEMBERSHIPS](https://msdn.microsoft.com/library/mt704584)     |  提供每個角色中的 RoleMembership 物件的相關資訊。      |
|[TMSCHEMA_ROLES](https://msdn.microsoft.com/library/mt719267)    |   提供模型中的角色物件的相關資訊。      |
|[TMSCHEMA_TABLE_PERMISSIONS](https://msdn.microsoft.com/library/mt704347)    |    提供每個角色中的 TablePermission 物件的相關資訊。     |
|[TMSCHEMA_TABLES](https://msdn.microsoft.com/library/mt719250)     |   提供模型中的資料表物件的相關資訊。      |
|[TMSCHEMA_VARIATIONS](https://msdn.microsoft.com/library/mt825008)|提供每個資料行中的變化物件的相關資訊。|

### <a name="rowsets-described-in-the-ms-ssas-sql-server-analysis-services-protocol"></a>[MS-SSAS] 中所述的資料列集：SQL Server Analysis Services 通訊協定

|資料列集|描述|  
|------------|-----------------|  
|[DBSCHEMA_CATALOGS](https://msdn.microsoft.com/library/ee302115)|描述可在伺服器存取的目錄。|  
|[DBSCHEMA_COLUMNS](https://msdn.microsoft.com/library/ee301789)|傳回每個量值、 每個 cube 維度屬性，以及每個結構描述資料列集資料行，公開為資料行的資料列。|  
|[DBSCHEMA_PROVIDER_TYPES](https://msdn.microsoft.com/library/ee301696)|識別伺服器所支援的 （基底） 的資料類型。|  
|[DBSCHEMA_TABLES](https://msdn.microsoft.com/library/ee320843)|傳回維度、 量值群組或公開為資料表的結構描述資料列。|  
|[DISCOVER_CALC_DEPENDENCY](https://msdn.microsoft.com/library/hh770226)| 傳回物件中的表格式資料庫或表格式資料庫執行的 DAX 查詢中指定的計算相依性的相關資訊。 |  
|[DISCOVER_COMMAND_OBJECTS](https://msdn.microsoft.com/library/ee320662)|提供參考命令使用中之物件的資源使用量與活動的有關資訊。|  
|[DISCOVER_COMMANDS](https://msdn.microsoft.com/library/ee320715)|提供在伺服器上已開啟的連接中，目前執行或是上次執行的命令之資源使用量與活動資訊。|  
|[DISCOVER_CONNECTIONS](https://msdn.microsoft.com/library/ee301889)|提供有關伺服器上目前已開啟的連接之資源使用量與活動資訊。|  
|[DISCOVER_CSDL_METADATA](https://msdn.microsoft.com/library/gg587670)|傳回記憶體中資料庫的資料庫中繼資料的相關資訊。|  
|[DISCOVER_DATASOURCES](https://msdn.microsoft.com/library/ee320285)|傳回伺服器上可用的資料來源的清單。|
|[DISCOVER_DB_CONNECTIONS](https://msdn.microsoft.com/library/ee320467)|提供有關目前從伺服器到資料庫之間已開啟之連接的資源使用量與活動資訊。|  
|[DISCOVER_DIMENSION_STAT](https://msdn.microsoft.com/library/ee320284)|傳回指定之維度的統計資料。|  
|[DISCOVER_ENUMERATORS](https://msdn.microsoft.com/library/ee302012)|針對特定的資料來源，傳回 XMLA 所支援之列舉值 (Enumerator) 的名稱、資料類型和列舉 (Enumeration) 值的清單。|  
|[DISCOVER_INSTANCES](https://msdn.microsoft.com/library/ee320541)|描述伺服器上的執行個體。|  
|[DISCOVER_JOBS](https://msdn.microsoft.com/library/ee320363)|提供在伺服器上執行之作用中作業的相關資訊。 作業是代表該命令執行特定工作之命令的一部分。|  
|[DISCOVER_KEYWORDS &#40;XMLA&#41;](https://msdn.microsoft.com/library/ee301719)|傳回 XMLA 伺服器所保留的關鍵字相關資訊。|  
|[DISCOVER_LITERALS](https://msdn.microsoft.com/library/ee301320)|傳回伺服器所支援的常值的相關資訊。|  
|[DISCOVER_LOCATIONS](https://msdn.microsoft.com/library/ee302024)|傳回備份檔案的內容資訊。 |
|[DISCOVER_LOCKS](https://msdn.microsoft.com/library/ee320398)|提供有關伺服器上目前永久性鎖定的資訊。|  
|[DISCOVER_MASTER_KEY](https://msdn.microsoft.com/library/ee301825)|傳回伺服器的主要加密金鑰。|
|[DISCOVER_MEMORYGRANT](https://msdn.microsoft.com/library/ee320945)|傳回伺服器上目前執行作業所使用之內部記憶體配額授權的清單。|  
|[DISCOVER_MEMORYUSAGE](https://msdn.microsoft.com/library/ee320910)|傳回伺服器所配置之各種物件的 DISCOVER_MEMORYUSAGE 統計資料。|  
|[DISCOVER_OBJECT_ACTIVITY](https://msdn.microsoft.com/library/ee320661)|提供每個物件自從服務啟動之後的資源使用量資訊。|  
|[DISCOVER_OBJECT_MEMORY_USAGE](https://msdn.microsoft.com/library/ee320910)|傳回伺服器所配置之各種物件的 DISCOVER_MEMORYUSAGE 統計資料。|  
|[DISCOVER_PARTITION_DIMENSION_STAT](https://msdn.microsoft.com/library/ee320268)|傳回與資料分割相關之維度的統計資料。|  
|[DISCOVER_PARTITION_STAT](https://msdn.microsoft.com/library/ee320483)|傳回特定資料分割中彙總的相關統計資料。|  
|[DISCOVER_PERFORMANCE_COUNTERS](https://msdn.microsoft.com/library/ee320809)|傳回一個或多個指定之效能計數器的值。 |  
|[DISCOVER_PROPERTIES](https://msdn.microsoft.com/library/ee320589)|傳回指定的資料來源伺服器所支援的屬性相關資訊及值的清單。|  
|[DISCOVER_RING_BUFFERS](https://msdn.microsoft.com/library/mt719204)|在伺服器上，傳回目前的 XEvent 信號緩衝區的相關資訊。|
|[DISCOVER_SCHEMA_ROWSETS](https://msdn.microsoft.com/library/ee320478)|傳回名稱、 限制、 描述和所有的探索要求的其他資訊。|  
|[DISCOVER_SESSIONS](https://msdn.microsoft.com/library/ee301962)|提供伺服器上目前已開啟的工作階段之資源使用量與活動的有關資訊。|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS](https://msdn.microsoft.com/library/ee320710)|傳回用來儲存資料的記憶體中資料表的資料行區段的相關資訊。|  
|[DISCOVER_STORAGE_TABLE_COLUMNS](https://msdn.microsoft.com/library/ee302101)|包含用來表示記憶體中資料表的資料行的資料行的相關資訊。|  
|[DISCOVER_STORAGE_TABLES](https://msdn.microsoft.com/library/ee302014)|傳回伺服器可用的記憶體中資料表的統計資料。|  
|[DISCOVER_TRACE_COLUMNS](https://msdn.microsoft.com/library/ee301342)||  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO](https://msdn.microsoft.com/library/ee301342)|包含 DISCOVER_TRACE_COLUMNS 結構描述資料列集。|  
|[DISCOVER_TRACE_EVENT_CATEGORIES](https://msdn.microsoft.com/library/ee320442)|包含 DISCOVER_TRACE_EVENT_CATEGORIES 結構描述資料列集。|  
|[DISCOVER_TRACES](https://msdn.microsoft.com/library/ee301643)|包含 DISCOVER_TRACES 結構描述資料列集。|  
|[DISCOVER_TRANSACTIONS](https://msdn.microsoft.com/library/ee301363)|傳回系統上目前的暫止交易集。|  
|[DISCOVER_XEVENT_TRACE_DEFINITION](https://msdn.microsoft.com/library/mt704568)|提供在伺服器目前使用中 XEvent 追蹤的相關資訊。|  
|[DISCOVER_XEVENT_PACKAGES](https://msdn.microsoft.com/library/mt704569)|在伺服器上提供說明的 XEvent 封裝的相關資訊。|
|[DISCOVER_XEVENT_OBJECTS](https://msdn.microsoft.com/library/mt704543)|在伺服器上提供 XEvent 物件所描述的相關資訊。|
|[DISCOVER_XEVENT_OBJECT_COLUMNS](https://msdn.microsoft.com/library/mt719352)|在伺服器上提供 XEvent 物件所描述的結構描述的資訊。|
|[DISCOVER_XEVENT_SESSIONS](https://msdn.microsoft.com/library/mt704397)|在伺服器上，提供目前的 XEvent 工作階段的相關資訊。|
|[DISCOVER_XEVENT_SESSION_TARGETS](https://msdn.microsoft.com/library/mt704564)|在伺服器上，提供目前的 XEvent 工作階段目標的相關資訊。|
|[DISCOVER_XML_METADATA](https://msdn.microsoft.com/library/ee301560)|傳回一個資料列與一個資料行的資料列集。 |
|[DMSCHEMA_MINING_COLUMNS](https://msdn.microsoft.com/library/ee301664)|描述伺服器上的所有描述的資料採礦模型所部署的個別資料行。|  
|[DMSCHEMA_MINING_FUNCTIONS](https://msdn.microsoft.com/library/ee320415)|描述執行 Analysis Services 伺服器可用的資料採礦演算法所支援的資料採礦函數。|  
|[DMSCHEMA_MINING_MODEL_CONTENT](https://msdn.microsoft.com/library/ee302124)|可讓用戶端應用程式，瀏覽定型的資料採礦模型的內容。|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML](https://msdn.microsoft.com/library/ee320692)|傳回採礦模型的 XML 結構。 XML 字串的格式會遵循 PMML 2.1 標準。|  
|[DMSCHEMA_MINING_MODEL_XML](https://msdn.microsoft.com/library/ee301916)|傳回採礦模型的 XML 結構。 XML 字串的格式會遵循 PMML 2.1 標準。|  
|[DMSCHEMA_MINING_MODELS](https://msdn.microsoft.com/library/ee320603)|列舉在伺服器上部署的資料採礦模型。|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS](https://msdn.microsoft.com/library/ee320378)|提供參數清單，這些參數可用以設定每個安裝在伺服器上的資料採礦演算法之行為。|  
|[DMSCHEMA_MINING_SERVICES](https://msdn.microsoft.com/library/ee320487)|提供伺服器支援每個資料採礦演算法的相關資訊。|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS](https://msdn.microsoft.com/library/ee320277)|描述在伺服器上部署之所有採礦結構的個別資料行。|  
|[DMSCHEMA_MINING_STRUCTURES](https://msdn.microsoft.com/library/ee320704)|列舉在目前目錄中之採礦結構的有關資訊。|  
|[MDSCHEMA_ACTIONS](https://msdn.microsoft.com/library/ee320890)|描述可供用戶端應用程式的動作。|
|[MDSCHEMA_CUBES](https://msdn.microsoft.com/library/ee301304)|描述資料庫內 Cube 的結構。 檢視方塊也會傳回在這個結構描述。|
|[MDSCHEMA_DIMENSIONS](https://msdn.microsoft.com/library/ee301366)|描述資料庫內的維度。|  
|[MDSCHEMA_FUNCTIONS](https://msdn.microsoft.com/library/mt719467)|傳回目前可供使用的 DAX 和 MDX 語言中的函式的相關資訊。|
|[MDSCHEMA_HIERARCHIES](https://msdn.microsoft.com/library/ee320250)|描述特定維度中的每個階層。|  
|[MDSCHEMA_INPUT_DATASOURCES](https://msdn.microsoft.com/library/ee301386)|描述在資料庫中所述的資料來源物件。|  
|[MDSCHEMA_KPIS](https://msdn.microsoft.com/library/ee320406)|描述資料庫內的 Kpi。|  
|[MDSCHEMA_LEVELS](https://msdn.microsoft.com/library/ee320746)|描述特定階層內的每個層級。|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS](https://msdn.microsoft.com/library/ee320977)|列舉量值群組的維度。|  
|[MDSCHEMA_MEASUREGROUPS](https://msdn.microsoft.com/library/ee320601)|描述資料庫內的量值群組。|  
|[MDSCHEMA_MEASURES](https://msdn.microsoft.com/library/ee301871)|描述每個量值。|  
|[MDSCHEMA_MEMBERS](https://msdn.microsoft.com/library/ee320960)|描述資料庫內的成員。|  
|[MDSCHEMA_PROPERTIES](https://msdn.microsoft.com/library/ee320393)|描述成員的屬性和資料格屬性。|  
|[MDSCHEMA_SETS](https://msdn.microsoft.com/library/ee301356)|說明目前在資料庫中，包括工作階段範圍集所述的任何集合。|  

> [!NOTE]
> 儲存體 Dmv 沒有通訊協定中所述的結構描述資料列集。