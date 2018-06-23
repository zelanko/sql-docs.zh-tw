---
title: 支援 XMLA 屬性 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- properties [XML for Analysis]
- XML for Analysis, properties
- XMLA, properties
ms.assetid: 5745f7b4-6b96-44d5-b77c-f2831a898e5e
caps.latest.revision: 24
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 89293d101513cb2cec07fe69b2ba22e67f55dd21
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136756"
---
# <a name="supported-xmla-properties-xmla"></a>支援的 XMLA 屬性 (XMLA)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支援下表所列的屬性。 使用列出的屬性用於[屬性](properties-element-xmla.md)元素[探索](../xml-elements-methods-discover.md)和[Execute](../xml-elements-methods-execute.md)方法。  
  
|[屬性]|元素|  
|----------|-------------|  
|AxisFormat|*使用方式*<br /> 選擇性的唯寫 `String` 屬性<br /><br /> *描述*<br /> 決定用於格式[MDDataSet](../xml-data-types/mddataset-data-type-xmla.md)結果集中用於描述多維度資料集中的座標軸。 這個屬性可以具有下表中所列的值。|  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*ClusterFormat*|`MDDataSet`軸所組成的一或多個[CrossProduct](crossproduct-element-xmla.md)項目。|  
|*CustomFormat*|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用*TupleFormat*格式，這項設定。|  
|*TupleFormat*|（預設值）`MDDataSet`座標軸包含一個或多個[Tuple](tuple-element-xmla.md)項目。|  
  
 這個屬性可搭配 `Execute` 方法使用。  
  
|[屬性]|元素|  
|----------|-------------|  
|BeginRange|*使用方式*<br /> 選擇性的唯寫 `Integer` 屬性<br /><br /> *描述*<br /> 包含對應至 `CellOrdinal` 屬性值的以零為基底整數值  (`CellOrdinal`屬性屬於[儲存格](cell-element-mddataset-xmla.md)中的項目[CellData](celldata-element-xmla.md)區段`MDDataSet`。)<br /><br /> 與 `EndRange` 屬性一起使用時，用戶端應用程式可以使用這個屬性，將命令傳回的 OLAP 資料集限制為特定資料格範圍。 如果指定為 -1，傳回的所有資料格最多至 `EndRange` 屬性中指定的資料格為止。<br /><br /> 這個屬性的預設值為-1。<br /><br /> 這個屬性可搭配 `Execute` 方法使用。|  
|目錄|*使用方式*<br /> 選擇性的可讀寫 `String` 屬性<br /><br /> *描述*<br /> 使用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體來建立要傳送 XMLA 命令的工作階段時，這個屬性就相當於 OLE DB 屬性 DBPROP_INIT_CATALOG。<br /><br /> 當您在工作階段期間設定這個屬性，以便變更工作階段的目前資料庫時，這個屬性就相當於 OLE DB 屬性 DBPROP_CURRENTCATALOG。<br /><br /> 這個屬性的預設為空字串。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|CatalogLocation|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_CATALOGLOCATION。<br /><br /> 這個屬性的預設值為零 (0)，相當於 DBPROPVAL_CL_START。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|ClientProcessID|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 包含目前工作階段之處理序執行緒的識別碼 (ID)。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|CommitTimeout|*使用方式*<br /> 選擇性的唯寫 `Integer` 屬性<br /><br /> *描述*<br /> 決定在進行回復之前，目前執行中 XMLA 命令之認可階段等候的時間長度 (以秒為單位)。 認可階段對應至 XMLA 命令，例如[陳述式](../xml-elements-commands/statement-element-xmla.md)或[程序](../xml-elements-commands/process-element-xmla.md)。<br /><br /> 值為零 (0) 表示執行個體會永遠等候。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|內容|*使用方式*<br /> 選擇性的唯寫 `String` 屬性<br /><br /> *描述*<br /> 決定從 `Discover` 和 `Execute` 方法傳回的資料類型。 這個屬性可以具有下表中所列的值。|  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*無*|允許驗證命令的結構，但不執行。|  
|*結構描述*|傳回與所要求命令相關的 XML 結構描述。 XML 結構描述會指出資料行和其他資訊。|  
|*資料*|只傳回所要求的資料。|  
|*SchemaData*|(預設值) 傳回結構描述資訊和資料。|  
  
 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。  
  
|[屬性]|元素|  
|----------|-------------|  
|Cube|*使用方式*<br /> 選擇性的唯寫 `String` 屬性<br /><br /> *描述*<br /> 包含設定命令內容之 Cube 的名稱。 如果命令本身包含 cube 名稱，例如 FROM 子句的多維度運算式 (MDX) 中[選取](/sql/mdx/mdx-data-manipulation-select)陳述式，此屬性設定會被忽略。<br /><br /> 這個屬性的預設為空字串。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DataSourceInfo|*使用方式*<br /> 必要的可讀寫 `String` 屬性<br /><br /> *描述*<br /> 包含連接至資料來源所需的資訊，例如執行個體名稱。<br /><br /> 用戶端應該程式不應該建構要傳送至執行個體的 `DataSourceInfo` 屬性內容。 相反地，用戶端應用程式應該會發現使用提供者所支援的資料來源`Discover`方法來擷取[DISCOVER_DATASOURCES](../../schema-rowsets/xml/discover-datasources-rowset.md)資料列集。 然後，用戶端應用程式會針對用戶端從 DISCOVER_DATASOURCES 資料列集中擷取的 `DataSourceInfo` 屬性，傳回相同的值。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropCatalogTerm|*使用方式*<br /> 選擇性的唯讀 `String` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_CATALOGTERM。<br /><br /> 這個屬性的預設值是 "Database"。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropCatalogUsage|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_CATALOGUSAGE。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropColumnDefinition|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_COLUMNDEFINITION。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropConcatNullBehavior|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_CONCATNULLBEHAVIOR。<br /><br /> 這個屬性的預設值為 1，相當於 DBPROPVAL_CB_NULL。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropDataSourceReadOnly|*使用方式*<br /> 選擇性的唯讀 `Boolean` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_DATASOURCEREADONLY。<br /><br /> 這個屬性的預設值是 FALSE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropGroupBy|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_GROUPBY。<br /><br /> 這個屬性的預設值為 2，相當於 DBPROPVAL_GB_EQUALS_SELECT。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropHeterogeneousTables|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_HETEROGENEOUSTABLES。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropIdentifierCase|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_IDENTIFIERCASE。<br /><br /> 這個屬性的預設值為 8，相當於 DBPROPVAL_IC_MIXED。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropInitMode|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_INIT_MODE。<br /><br /> 支援這個屬性的值只有 DB_MODE_READWRITE 和 DB_MODE_READ。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMaxIndexSize|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_MAXINDEXSIZE。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMaxOpenChapters|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_MAXOPENCHAPTERS。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMaxRowSize|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_MAXROWSIZE。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMaxRowSizeIncludeBlob|*使用方式*<br /> 選擇性的唯讀 `Boolean` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_MAXROWSIZEINCLUDESBLOB。<br /><br /> 這個屬性的預設值是 TRUE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMaxTablesInSelect|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_MAXTABLESINSELECT。<br /><br /> 這個屬性的預設值為 1。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMsmdAutoexists|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 決定自動存在的行為。 這個屬性可以具有下表中所列的值。|  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*0*|預設值，與 1 相同。|  
|*1*|為查詢座標軸和命名集套用深層自動存在。 包含 WHERE 子句和子選擇。|  
|*2*|為查詢座標軸套用深層自動存在，並將命名集排除在自動存在之外。 包含 WHERE 子句和子選擇。|  
|*3*|對包含 WHERE 子句的命名集套用無自動存在。 對包含 WHERE 子句的查詢座標軸套用淺層自動存在。 對包含子選擇的查詢座標軸以及包含子選擇的命名集套用深層自動存在。|  
  
 這個屬性的預設值為零或空白。 這是一個工作階段屬性，只能在建立工作階段時設定。  
  
|[屬性]|元素|  
|----------|-------------|  
|DbpropMsmdCacheMode|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMsmdCachePolicy|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMsmdCacheRatio|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMsmdCacheRatio2|*使用方式*<br /> 選擇性的可讀寫 `Double` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMsmdCompareCaseNotSensitiveStringFlags|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 決定區分大小寫字串比較和排序次序功能。 這個屬性會控制如何在不支援大寫和小寫字元的字元集中進行比較，例如日文和印度文。 這個屬性的值設定於處理序執行緒的第一個連接中，而且它會影響該處理序執行緒中的所有後續連接。<br /><br /> 您可以使用下表來決定要使用的旗標。|  
  
|[屬性]|ReplTest1|描述|  
|----------|-----------|-----------------|  
|NORM_IGNORECASE|*0x00000001*|忽略大小寫。|  
|不適用|*0x00000002*|二進位比較。 根據字元集的基礎值而非特定字母中的順序來比較字元。|  
|NORM_IGNORENONSPACE|*0x00000010*|忽略非空格字元。|  
|NORM_IGNORESYMBOLS|*0x00000100*|忽略符號。|  
|NORM_IGNOREKANATYPE|*0x00001000*|平假名與片假名字元之間沒有任何差異。 進行比較時，對應的平假名與片假名字元會被視為相等。|  
|NORM_IGNOREWIDTH|*0x00010000*|相同字元的單一位元組與雙位元組版本之間沒有任何差異。|  
|SORT_STRINGSORT|*0x00100000*|標點符號會被視為與符號相同。|  
  
 如需有關在 OLE DB 中比較字串的詳細資訊，請在 MSDN Library 的 Platform SDK 章節中搜尋 "CompareString"。  
  
 這個屬性沒有預設值。  
  
 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。  
  
|[屬性]|元素|  
|----------|-------------|  
|DbpropMsmdCompareCaseSensitiveStringFlags|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 決定不區分大小寫字串比較和排序順序功能。 這個屬性會控制如何在不支援大寫和小寫字元的字元集中進行比較，例如日文和印度文。 這個屬性的值設定於處理序執行緒的第一個連接中，而且它會影響該處理序執行緒中的所有後續連接。<br /><br /> 您可以使用下表來決定要使用的旗標。|  
  
|[屬性]|ReplTest1|描述|  
|----------|-----------|-----------------|  
|NORM_IGNORECASE|*0x00000001*|忽略大小寫。|  
|不適用|*0x00000002*|二進位比較。 根據字元集的基礎值而非特定字母中的順序來比較字元。|  
|NORM_IGNORENONSPACE|*0x00000010*|忽略非空格字元。|  
|NORM_IGNORESYMBOLS|*0x00000100*|忽略符號。|  
|NORM_IGNOREKANATYPE|*0x00001000*|平假名與片假名字元之間沒有任何差異。 進行比較時，對應的平假名與片假名字元會被視為相等。|  
|NORM_IGNOREWIDTH|*0x00010000*|相同字元的單一位元組與雙位元組版本之間沒有任何差異。|  
|SORT_STRINGSORT|*0x00100000*|標點符號會被視為與符號相同。|  
  
 如需有關在 OLE DB 中比較字串的詳細資訊，請在 MSDN Library 的 Platform SDK 章節中搜尋 "CompareString"。  
  
 這個屬性沒有預設值。  
  
 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。  
  
|[屬性]|元素|  
|----------|-------------|  
|DbpropMsmdDebugMode|*使用方式*<br /> 選擇性的可讀寫 `String` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMsmdDynamicDebugLimit|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMsmdFlattened2|*使用方式*<br /> 選擇性的可讀寫 `Boolean` 屬性<br /><br /> *描述*<br /> 除非針對第 0 軸要求父子式階層，否則便在扁平化結果的單一資料表資料行中輸出父子式階層的所有成員。 系統不會使用輸出資料行的層級範本。<br /><br /> 這個屬性的預設值是 FALSE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMsmdMDXCompatibility|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 決定如何處理不完全或不對稱階層中的預留位置成員。 這個屬性可以具有下表中所列的值。|  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*0*|為了與舊版 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 相容，這個值相當於 1。|  
|*1*|角色扮演維度中的階層收到包含維度名稱和階層名稱的標題。 此標題具有下列格式：<br /><br /> [維度].[階層]<br /><br /> 系統會公開預留位置成員。|  
|*2*|角色扮演維度中的階層收到包含維度名稱和階層名稱的標題。此標題具有下列格式：<br /><br /> [維度].[階層]<br /><br /> 系統不會公開預留位置成員。|  
|*3*|(預設值) 系統不會公開預留位置成員。|  
  
 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。  
  
|[屬性]|元素|  
|----------|-------------|  
|DbpropMsmdMDXUniqueNameStyle|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 決定用於產生維度中成員之唯一名稱的演算法。 這個屬性可以具有下表中所列的值。<br /><br /> 這個屬性的預設值為 6。|  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*0*|為了與舊版 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 相容，這個值相當於 2。|  
|*1*|使用索引鍵路徑演算法：<br /><br /> [dim].&[key1].&[key2]|  
|*2*|使用名稱路徑演算法：<br /><br /> [dim].[name1].&[name2]|  
|*3*|使用保證隨著時間穩定的唯一名稱。|  
  
 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。  
  
|[屬性]|元素|  
|----------|-------------|  
|DbpropMsmdSQLCompatibility|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMsmdSubQueries|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 這是一個位元遮罩，用於決定子查詢的行為。 這個屬性可以具有下表中所列的值。|  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*0*|預設值，與舊版 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 相容。<br /><br /> 不允許在子選擇或 Subcube 中使用導出成員或導出集合。|  
|*1*|允許在子選擇或 Subcube 中使用導出成員或導出集合。 導出成員的上階沒有包含在子選擇或 Subcube 的空間中。|  
|*2*|允許在子選擇或 Subcube 中使用導出成員或導出集合。 導出成員的上階包含在子選擇或 Subcube 的空間中。|  
  
 這個屬性的預設值為零或空白。  
  
 這是一個工作階段屬性，只能在建立工作階段時設定。  
  
 請參閱[子選擇和 Subcube 中導出成員](../../multidimensional-models/mdx/calculated-members-in-subselects-and-subcubes.md)的導出的成員或導出的集合子選擇和 subcube 中的行為的詳細說明。  
  
|[屬性]|元素|  
|----------|-------------|  
|DbpropMsmdUseFormulaCache|*使用方式*<br /> 選擇性的可讀寫 `String` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropMultiTableUpdate|*使用方式*<br /> 選擇性的唯讀 `Boolean` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_MULTITABLEUPDATE。<br /><br /> 這個屬性的預設值是 FALSE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropNullCollation|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_NULLCOLLATION。<br /><br /> 這個屬性的預設值為 4，相當於 DBPROPVAL_NC_LOW。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropOrderByColumnsInSelect|*使用方式*<br /> 選擇性的唯讀 `Boolean` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_ORDERBYCOLUMNSINSELECT。<br /><br /> 這個屬性的預設值是 FALSE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropOutputParameterAvailable|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_OUTPUTPARAMETERAVAILABILITY。<br /><br /> 這個屬性的預設值為 1，相當於 DBPROPVAL_OA_NOTSUPPORTED。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropPersistentIdType|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_PERSISTENTIDTYPE。<br /><br /> 這個屬性的預設值為 4，相當於 DBPROPVAL_PT_NAME。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropPrepareAbortBehavior|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_PREPAREABORTBEHAVIOR。<br /><br /> 這個屬性的預設值為 1，相當於 DBPROPVAL_CB_DELETE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropPrepareCommitBehavior|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_PREPARECOMMITBEHAVIOR。<br /><br /> 這個屬性的預設值為 1，相當於 DBPROPVAL_CB_DELETE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropProcedureTerm|*使用方式*<br /> 選擇性的唯讀 `String` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_PROCEDURETERM。<br /><br /> 這個屬性的預設值為 "Calculated member"。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropQuotedIdentifierCase|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_QUOTEDIDENTIFIERCASE。<br /><br /> 這個屬性的預設值為 8，相當於 DBPROPVAL_IC_MIXED。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropSchemaUsage|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_SCHEMAUSAGE。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropSqlSupport|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_SQLSUPPORT。<br /><br /> 這個屬性的預設值為 512，相當於 DBPROPVAL_SQL_SUBMINIMUM。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropSubqueries|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_SUBQUERIES。<br /><br /> **注意！** 雖然資料採礦延伸模組 (DMX) 支援子查詢，但是這個屬性會參考 SQL 中的子查詢支援。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropSupportedTxnDdl|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_SUPPORTEDTXNDDL。<br /><br /> 這個屬性的預設值為零 (0)，相當於 DBPROPVAL_TC_NONE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropSupportedTxnIsoLevels|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_SUPPORTEDTXNISOLEVELS。<br /><br /> 這個屬性的預設值為 4096，相當於 DBPROPVAL_TI_READCOMMITTED。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropSupportedTxnIsoRetain|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_SUPPORTEDTXNISORETAIN。<br /><br /> 這個屬性的預設值為 292，相當於 DBPROPVAL_TR_ABORT_NO、DBPROPVAL_TR_COMMIT_NO 和 DBPROPVAL_TR_NONE 的組合。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|DbpropTableTerm|*使用方式*<br /> 選擇性的唯讀 `String` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_TABLETERM。<br /><br /> 這個屬性的預設值是 "Cube"。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|Dialect|*使用方式*<br /> 選擇性的可讀寫 `String` 屬性<br /><br /> *描述*<br /> 建立在下列情況中使用的方言：<br /><br /> 層提供者會使用第一的方言時間提供者會嘗試執行查詢。<br />的用於因查詢失敗而導致傳回之執行錯誤方言。<br /><br /> 當您預期大部分查詢使用單一特定方言的頻率超過任何其他方言時，就可以使用 `Dialect` 屬性。<br /><br /> 某些語言方言的查詢語法可能會相同，例如 DMX 和 SQL。 由於語法可能相同，因此 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 可能無法從查詢語法推斷出方言。 如果查詢無法以某個方言執行，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體可能會嘗試以不同的方言再次執行查詢。<br /><br /> 如果您已設定 `Dialect` 屬性，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 就會以具有優先順序的方言傳回查詢執行錯誤，即使提供者嘗試以另一種方言再次執行查詢也一樣。 例如，`Dialect` 屬性設定為 MDGUID_DM。 提供者會先嘗試執行查詢當做資料採礦查詢，但是這個查詢會失敗。 然後，提供者便重新提交查詢當做 SQL 查詢。 不過，這個 SQL 查詢也會失敗。 由於 `Dialect` 屬性的值為 MDGUID_DM，因此 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會傳回資料採礦錯誤訊息，而非 SQL 錯誤訊息。<br /><br /> 如果您沒有設定 `Dialect` 屬性，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 就會以上次使用的方言傳回查詢執行錯誤。 例如，`Dialect` 屬性未設定，而且資料採礦查詢失敗。 然後，提供者便重新提交查詢當做 SQL。 此 SQL 查詢也會失敗。 由於 `Dialect` 屬性未設定，因此提供者會傳回 SQL 錯誤訊息，而非資料採礦錯誤訊息。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。<br /><br /> 適用於這個屬性的方言列於下表中。|  
  
|[屬性]|ReplTest1|描述|  
|----------|-----------|-----------------|  
|DBGUID_SQL|*C8B522D7-5CF3-11CE-ADE5-00AA0044773D*|SQL 剖析器具有優先順序。|  
|MDGUID_DM|*62C58FED-CCA5-44F1-83B6-7B45682B3904*|DMX 剖析器具有優先順序。|  
|MDGUID_MDX|*A07CCCD0-8148-11D0-87BB-00C04FC33942*|MDX 剖析器具有優先順序。|  
  
|[屬性]|元素|  
|----------|-------------|  
|Disable Prefetch Facts|*使用方式*<br /> 選擇性的可讀寫 `Boolean` 屬性<br /><br /> *描述*<br /> 設定為 True 時，引擎就會停止嘗試預先提取工作階段長度的值。<br /><br /> 這個屬性的預設值是`False`。|  
|EffectiveRoles|*使用方式*<br /> 選擇性的唯寫 `String` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|EffectiveUserName|*使用方式*<br /> 選擇性的唯寫 `String` 屬性<br /><br /> *描述*<br /> 指定連接至 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體時要用於覆寫使用者名稱的帳戶名稱。 屬性的值不會正規化，在中，MDX [UserName](/sql/mdx/username-mdx)函式會傳回常值，如果使用這個屬性。 只有伺服器管理員可以使用這個屬性。<br /><br /> 這個屬性支援下列 SID 類型：User、Group、Alias、WellKnownGroup 和 Computer。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|EndRange|*使用方式*<br /> 選擇性的唯寫 `Integer` 屬性<br /><br /> *描述*<br /> 指定對應至 `CellOrdinal` 屬性值的以零為基底整數值  (`CellOrdinal` 屬性屬於 `Cell` 之 `CellData` 區段中 `MDDataSet` 元素的一部分)。<br /><br /> 與 `BeginRange` 屬性一起使用時，用戶端應用程式可以使用這個屬性，將命令傳回的 OLAP 資料集限制為特定資料格範圍。 如果指定為 -1，就會從 `BeginRange` 屬性中指定的資料格開始傳回所有資料格。<br /><br /> 這個屬性的預設值為-1。<br /><br /> 這個屬性可搭配 `Execute` 方法使用。|  
|ExecutionMode|*使用方式*<br /> 選擇性的唯寫 `String` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性的預設值是*Execute*。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|ForceCommitTimeout|*使用方式*<br /> 選擇性的唯寫 `Integer` 屬性<br /><br /> *描述*<br /> 決定在強制先前發出的命令回復之前，目前執行中 XMLA 命令之認可階段等候的時間長度 (以秒為單位)。 認可階段會對應至 XMLA 命令，例如 `Statement` 或 `Process`。<br /><br /> 值為零 (0) 表示執行個體會永遠等候。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|[格式]|*使用方式*<br /> 選擇性的唯寫 `String` 屬性<br /><br /> *描述*<br /> 決定從 `Discover` 和 `Execute` 方法傳回的結果集類型。 這個屬性可以具有下表中所列的值。|  
  
 這個屬性的預設值是*原生*。  
  
 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*表格式*|傳回的結果集使用[資料列集](../xml-data-types/rowset-data-type-xmla.md)資料型別。|  
|*多維度*|傳回資料列集使用[MDDataSet](../xml-data-types/mddataset-data-type-xmla.md)資料型別。|  
|*原生*|沒有明確指定任何格式。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會針對此命令傳回適當的格式。 實際的結果類型是由結果的命名空間加以識別。|  
  
|[屬性]|元素|  
|----------|-------------|  
|ImpactAnalysis|*使用方式*<br /> 選擇性的唯寫 `Boolean` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|LocaleIdentifier|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 讀取或設定 `Discover` 或 `Execute` 方法所使用的地區設定識別碼 (LCID)。 如需語言識別碼的完整十六進位清單，請在 MSDN Library 中搜尋「語言識別碼」。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MaximumRows|*使用方式*<br /> 選擇性的唯寫 `Integer` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropAggregateCellUpdate|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_AGGREGATECELL_UPDATE。<br /><br /> 這個屬性的預設值為 4，相當於 MDPROPVAL_AU_SUPPORTED。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropAxes|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_AXES。<br /><br /> 這個屬性的預設值為 2147483647。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropDrillFunctions|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 判斷伺服器對鑽研函數的支援層級。 下列值用來建立有效的位元遮罩：<br /><br /> MDPROPVAL_MDF_BASIC (0x01)<br /><br /> MDPROPVAL_MDF_ASYMMETRIC (0x02)<br /><br /> MDPROPVAL_MDF_CALC_MEMBERS (0x04)<br /><br /> 預設值是：<br /><br /> 3 代表 SQL Server 2008<br /><br /> 7 代表 SQL Server 2008 R2 和 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropFlatteningSupport|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_FLATTENING_SUPPORT。<br /><br /> 這個屬性的預設值為 1，相當於 MDPROPVAL_FS_FULL_SUPPORT。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxCaseSupport|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_CASESUPPORT。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxDescFlags|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_DESCFLAGS。<br /><br /> 這個屬性的預設值為 7，相當於 MDPROPVAL_MD_BEFORE、MDPROPVAL_MD_AFTER 和 MDPROPVAL_MD_SELF。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxFormulas|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_FORMULAS。<br /><br /> 這個屬性的預設值為 63，相當於 MDPROPVAL_MF_WITH_CALCMEMBERS、MDPROPVAL_MF_WITH_NAMEDSETS、MDPROPVAL_MF_CREATE_CALCMEMBERS、MDPROPVAL_MF_CREATE_NAMEDSETS、MDPROPVAL_MF_SCOPE_SESSION 和 MDPROPVAL_MF_SCOPE_GLOBAL 的組合。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxJoinCubes|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_JOINCUBES。<br /><br /> 這個屬性的預設值為 1，相當於 MDPROPVAL_MJC_SINGLECUBE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxMemberFunctions|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_MEMBER_FUNCTIONS。<br /><br /> 這個屬性的預設值為 15，相當於所有可用 OLE DB 值的組合。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxNamedSets|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 來自下表所列的值的位元遮罩。|  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*0x01*|MDPROPVAL_MNS_BASIC|  
|*0x02*|MDPROPVAL_MNS_DYNAMIC|  
|*0x04*|MDPROPVAL_MNS_DISPLAYFOLDER|  
|*0x08*|MDPROPVAL_MNS_CAPTION|  
  
 這個屬性的預設值為 15。  
  
|[屬性]|元素|  
|----------|-------------|  
|MdpropMdxNonMeasureExpressions|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_NONMEASURE_EXPRESSIONS。<br /><br /> 這個屬性的預設值為零 (0)，相當於 MDPROPVAL_NME_ALLDIMENSIONS。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxNumericFunctions|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_NUMERIC_FUNCTIONS。<br /><br /> 這個屬性的預設值為 2047，相當於 MDPROPVAL_MNF_MEDIAN、MDPROPVAL_MNF_VAR、MDPROPVAL_MNF_STDDEV、MDPROPVAL_MNF_RANK、MDPROPVAL_MNF_AGGREGATE、MDPROPVAL_MNF_COVARIANCE、MDPROPVAL_MNF_CORRELATION、MDPROPVAL_MNF_LINREGSLOPE、MDPROPVAL_MNF_LINREGVARIANCE、MDPROPVAL_MNF_LINREG2 和 MDPROPVAL_MNF_LINREGPOINT 的組合。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxObjQualification|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_OBJQUALIFICATION。<br /><br /> 這個屬性的預設值為 496，相當於 MDPROPVAL_MOQ_DIM_HIER、MDPROPVAL_MOQ_DIMHIER_LEVEL、MDPROPVAL_MOQ_DIMHIER_MEMBER、MDPROPVAL_MOQ_LEVEL_MEMBER 和 MDPROPVAL_MOQ_MEMBER_MEMBER 的組合。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxOuterReference|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_OUTERREFERENCE。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxQueryByProperty|*使用方式*<br /> 選擇性的唯讀 `Boolean` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_QUERYBYPROPERTY。<br /><br /> 這個屬性的預設值是 TRUE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxRangeRowset|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_RANGEROWSET。<br /><br /> 這個屬性的預設值為 4，相當於 MDPROPVAL_RR_UPDATE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxSetFunctions|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_SET_FUNCTIONS。<br /><br /> 這個屬性的預設值為 524287，相當於 MDPROPVAL_MSF_TOPPERCENT、MDPROPVAL_MSF_BOTTOMPERCENT、MDPROPVAL_MSF_TOPSUM、MDPROPVAL_MSF_BOTTOMSUM、MDPROPVAL_MSF_PERIODSTODATE、MDPROPVAL_MSF_LASTPERIODS、MDPROPVAL_MSF_YTD、MDPROPVAL_MSF_QTD、MDPROPVAL_MSF_MTD、MDPROPVAL_MSF_WTD、MDPROPVAL_MSF_DRILLDOWNMEMBER、MDPROPVAL_MSF_DRILLDOWNLEVEL、MDPROPVAL_MSF_DRILLDOWNMEMBERTOP、MDPROPVAL_MSF_DRILLDOWNMEMBERBOTTOM、MDPROPVAL_MSF_DRILLDOWNLEVEL、MDPROPVAL_MSF_DRILLDOWNLEVELTOP、MDPROPVAL_MSF_DRILLDOWNLEVELBOTTOM、MDPROPVAL_MSF_DRILLUPMEMBER、MDPROPVAL_MSF_DRILLUPLEVEL 和 MDPROPVAL_MSF_TOGGLEDRILLSTATE 的組合。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxSlicer|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_SLICER。<br /><br /> 這個屬性的預設值為 2，相當於 MDPROPVAL_MS_SINGLETUPLE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxStringCompop|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_MDX_STRING_COMPOP。<br /><br /> 這個屬性的預設值為 15，相當於 MDPROPVAL_MSC_LESSTHAN、MDPROPVAL_MSC_GREATERTHAN、MDPROPVAL_MSC_LESSTHANEQUAL 和 MDPROPVAL_MSC_GREATERTHANEQUAL 的組合。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdpropMdxSubQueries|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> SQL Server 2014 中這個屬性的預設值為 63。<br /><br /> 在 SQL Server 2008 R2 和 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中，這個屬性的預設值為 31。<br /><br /> SQL Server 2008 中這個屬性的預設值為 15。<br /><br /> 表示 MDX 中的子查詢的支援層級。 來自下表所列的值的位元遮罩。|  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*0x01*|MDPROPVAL_MSQ_BASIC|  
|*0x02*|MDPROPVAL_MSQ_ARBITRARYSHAPE|  
|*0x04*|MDPROPVAL_MSQ_NONVISUAL|  
|*0x08*|MDPROPVAL_MSQ_CALCMEMBERS|  
  
|||  
|-|-|  
|*0x10*|MDPROPVAL_MSQ_CALCMEMBERS2|  
  
|[屬性]|元素|  
|----------|-------------|  
|MdpropNamedLevels|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_NAMED_LEVELS。<br /><br /> 這個屬性的預設值為 3，相當於 MDPROPVAL_NL_NAMEDLEVELS 和 MDPROPVAL_NL_NUMBEREDLEVELS 的組合。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|MdxMissingMemberMode|*使用方式*<br /> 選擇性的唯寫 `String` 屬性<br /><br /> *描述*<br /> 指出是否要在 MDX 陳述式中忽略遺漏的成員。<br /><br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_MDX_MISSING_MEMBER_MODE。<br /><br /> 這個屬性的預設值是*預設*。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。<br /><br /> 這個屬性可以具有下表中所列的值。|  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*預設值*|使用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體所產生的值。|  
|*錯誤*|產生錯誤。|  
|*略過*|永遠忽略遺漏的成員。|  
  
|[屬性]|元素|  
|----------|-------------|  
|MDXSupport|*使用方式*<br /> 選擇性的唯讀 `String` 屬性<br /><br /> *描述*<br /> 指定描述 MDX 支援程度的列舉。<br /><br /> `Value` = *核心*支援所有 MDX 選項。<br /><br /> 目前，唯一的值，其中包含列舉型別是*核心*。 在未來的版本中，將會針對這個列舉定義其他值。<br /><br /> 這個屬性的預設值是*核心*。<br /><br /> 這個屬性可搭配 `Discover` 方法使用。|  
|NonEmptyThreshold|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|[密碼]|**不再支援這個屬性。**<br /><br /> *使用方式*<br /> 選擇性的唯寫 `String` 屬性<br /><br /> *描述*<br /> 為了回溯相容性，當這個屬性與 `Execute` 或 `Discover` 方法搭配使用時，系統會忽略此屬性，但不會產生錯誤。|  
|ProviderName|*使用方式*<br /> 選擇性的唯讀 `String` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_DBMSNAME。<br /><br /> 這個屬性的預設值是 "OLAP Server"。<br /><br /> 這個屬性可搭配 `Discover` 方法使用。|  
|ProviderType|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_DATASOURCE_TYPE。<br /><br /> 這個屬性的預設值為 6。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|ProviderVersion|*使用方式*<br /> 選擇性的唯讀 `String` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_DBMSVER。<br /><br /> 這個屬性的預設值為 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體的版本。<br /><br /> 這個屬性可搭配 `Discover` 方法使用。|  
|ReadOnlySession|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|RealTimeOlap|*使用方式*<br /> 選擇性的可讀寫 `Boolean` 屬性<br /><br /> *描述*<br /> 如果設定為 TRUE，就表示接聽資料表通知的所有資料分割都要進行即時查詢，而略過快取。 這個屬性就相當於 OLE DB 屬性 DBPROP_MSMD_REAL_TIME_OLAP。<br /><br /> 這個屬性的預設值是 FALSE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|ReturnCellProperties|*使用方式*<br /> 選擇性的可讀寫 `Boolean` 屬性<br /><br /> *描述*<br /> 這個屬性的預設值是 FALSE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|角色|*使用方式*<br /> 選擇性的可讀寫 `String` 屬性<br /><br /> *描述*<br /> 指定用戶端應用程式連接至 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體所用之角色名稱的逗號分隔字串。 這個屬性可讓使用者使用目前使用中角色以外的角色進行連接。 例如，伺服器管理員可能會想要以某個角色成員的身分連接至 Cube，以便測試授與該角色的權限。 這位使用者必須是指定之角色的成員，才能使用這個屬性進行連接。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。<br /><br /> **注意！** 角色名稱區分大小寫。 **請勿使用**逗號分隔的角色名稱之間的空格。 否則，受保護之資料格集的查詢可能會傳回錯誤和非預期的結果。|  
|SafetyOptions|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 決定用戶端應用程式是否可以註冊和載入不安全的程式庫。<br /><br /> 這個屬性的值也會決定本機 Cube 中是否允許使用 PASSTHROUGH 關鍵字。 在下列情況中會發生錯誤：<br /><br /> -如果用戶端應用程式嘗試建立本機 cube 搭配 INSERT INTO 陳述式，其中包含使用 PASSTHROUGH 關鍵字。<br />-如果用戶端應用程式會更新本機 cube，其中包含的 INSERT INTO 陳述式使用 PASSTHROUGH 關鍵字。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。<br /><br /> 這個屬性可以具有下表中所列的值。|  
  
|[屬性]|ReplTest1|描述|  
|----------|-----------|-----------------|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_DEFAULT|*0*|這個值會被視為 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE。<br /><br /> 若為本機 Cube 的連接，這個值會取決於是否使用了 CREATECUBE 連接字串屬性。 如果使用了 CREATECUBE 連接字串屬性，這個值就與 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL 相同。 否則，這個值會與 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE 相同。|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL|*1*|這個值會啟用所有使用者定義函數程式庫，但不驗證它們的初始化和指令碼是否安全。 若為本機 Cube 的連接，這個值可讓您使用預存程序以及在 INSERT INTO 陳述式中使用 PASSTHROUGH 關鍵字。<br /><br /> **我們不建議您使用這個選項**。|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE|*2*|這個值會確保特定使用者定義函數程式庫的所有類別都經過檢查，以便確定它們的初始化和指令碼安全無虞。 若為本機 Cube 的連接，這個值會讓您無法在 INSERT INTO 陳述式中使用 PASSTHROUGH 關鍵字以及 PermissionSet 屬性未設定為 Safe 的預存程序。<br /><br /> 這個值也會移除在動作[MDSCHEMA_ACTIONS](../../schema-rowsets/ole-db-olap/mdschema-actions-rowset.md) HTML 值，或是命令在 ACTION_TYPE 資料行，或是有 URL ACTION_TYPE 資料行的值和值並不會在內容資料行中的結構描述資料列以"http://"或"https://"開頭。|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_NONE|*3*|這個值會讓使用者定義函數無法用於工作階段中。 若為本機 Cube 的連接，這個值會讓您無法使用所有預存程序以及在 INSERT INTO 陳述式中使用 PASSTHROUGH 關鍵字。<br /><br /> 此外，這個值也會移除 MDSCHEMA_ACTIONS 結構描述資料列集中的所有動作。|  
  
|[屬性]|元素|  
|----------|-------------|  
|SecuredCellValue|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 指定錯誤碼以及當它嘗試存取受保護的資料格時，系統要傳回之 `Value` 和 `Formatted Value` 資料格屬性的值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。<br /><br /> 這個屬性可以具有下表中所列的值。|  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*0*|（預設值）為了與舊版相容，這個值會是相同*1*。 這個預設值的意義在未來的版本中可能會變更。|  
|*1*|傳回：HRESULT = NO_ERROR<br /><br /> 資料格的 `Value` 屬性會包含結果當做 Variant 資料類型。 `Formatted Value` 屬性中會傳回字串 "#N/A"。|  
|*2*|傳回錯誤當做 HRESULT 的值。|  
|*3*|在 `Value` 和 `Formatted Value` 屬性中都傳回 NULL。|  
|*4*|在 `Value` 屬性中傳回數值零 (0)，而在 `Formatted Value` 屬性中傳回格式化零。 例如，若為 `Formatted Value` 屬性是 "#.##" 的資料格，系統就會在 `Format` 屬性中傳回 0.00。|  
|*5*|在 `Value` 和 `Formatted Value` 屬性中都傳回字串 "#SEC"。|  
  
|[屬性]|元素|  
|----------|-------------|  
|ServerName|*使用方式*<br /> 選擇性的唯讀 `String` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 DBPROP_SERVERNAME。<br /><br /> 這個屬性的預設值為 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體的名稱。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|ShowHiddenCubes|*使用方式*<br /> 選擇性的可讀寫 `Boolean` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性的預設值是 FALSE。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|SQLQueryMode|*使用方式*<br /> 選擇性的可讀寫 `String` 屬性<br /><br /> *描述*<br /> 決定計算是否包含在 SQL 查詢中。<br /><br /> 這個屬性的預設值是*計算*。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。<br /><br /> 這個屬性可以具有下表中所列的值。|  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*資料*|不包含任何計算。|  
|*計算*|系統會傳回計算。|  
|*IncludeEmpty*|系統會傳回計算和空白資料列。|  
  
|[屬性]|元素|  
|----------|-------------|  
|SQLSupport|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性的預設值為 512。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|SspropInitAppName|*使用方式*<br /> 選擇性的可讀寫 `String` 屬性<br /><br /> *描述*<br /> 包含用戶端應用程式的名稱。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|SspropInitPacketsize|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 包含用戶端應用程式的識別碼。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|SspropInitWsid|*使用方式*<br /> 選擇性的可讀寫 `String` 屬性<br /><br /> *描述*<br /> 包含用戶端工作站的識別碼。<br /><br /> 這個屬性沒有預設值。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|StateSupport|*使用方式*<br /> 選擇性的唯讀 `String` 屬性<br /><br /> *描述*<br /> 指定對 Statefulness 的支援程度。<br /><br /> *無* = <br />                        不支援 Statefulness。<br /><br /> *工作階段*= Statefulness 透過工作階段支援所提供。<br /><br /> 如需有關 statefulness 和工作階段支援的詳細資訊，請參閱[管理連接和工作階段&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)。<br /><br /> 這個屬性的預設值是*工作階段*。<br /><br /> 這個屬性可搭配 `Discover` 方法使用。|  
|逾時|*使用方式*<br /> 選擇性的可讀寫 `Integer` 屬性<br /><br /> *描述*<br /> 指定在傳回錯誤之前，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體應該等候要求成功的最大時間 (以秒為單位)。 這個屬性也會決定在傳回錯誤之前，執行個體應該等候回寫資料表之更新成功的最大時間，相當於連接字串屬性 Writeback Timeout。<br /><br /> 這個屬性的預設值為零 (0)。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|TransactionDDL|*使用方式*<br /> 選擇性的唯讀 `Integer` 屬性<br /><br /> *描述*<br /> 保留供日後使用。<br /><br /> 這個屬性的預設值為 0。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
|UserName|這個屬性不再受到支援。<br /><br /> *使用方式*<br /> 選擇性的唯讀 `String` 屬性<br /><br /> *描述*<br /> 指定字串，它會傳回 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體與命令產生關聯所用的使用者名稱。 為了回溯相容性，當這個屬性與 `Execute` 或 `Discover` 方法搭配使用時，系統會忽略此屬性，但不會產生錯誤。 這個屬性就相當於 OLE DB 屬性 DBPROP_USERNAME。<br /><br /> 這個屬性的預設值是開啟目前工作階段或連接的使用者名稱。<br /><br /> 這個屬性可搭配 `Execute` 方法使用。|  
|VisualMode|*使用方式*<br /> 選擇性的唯寫 `Integer` 屬性<br /><br /> *描述*<br /> 這個屬性就相當於 OLE DB 屬性 MDPROP_VISUALMODE。<br /><br /> 這個屬性的預設值為零 (0)，相當於 DBPROPVAL_VISUAL_MODE_DEFAULT。<br /><br /> 這個屬性可搭配 `Discover` 和 `Execute` 方法使用。|  
  
## <a name="see-also"></a>另請參閱  
 [PropertyList 元素&#40;XMLA&#41;](propertylist-element-xmla.md)  
  
  
