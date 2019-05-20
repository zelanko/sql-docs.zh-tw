---
title: 轉換自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Slowly Changing Dimension transformation
- Import Column transformation [Integration Services]
- Sort transformation
- Unpivot transformation
- Merge Join transformation
- Data Mining Query transformation
- Fuzzy Grouping transformation
- Data Conversion transformation
- Fuzzy Lookup transformation
- Term Extraction transformation
- Row Count transformation custom properties [Integration Services]
- transformations [Integration Services], properties
- Pivot transformation
- Lookup transformation
- Percentage Sampling transformation
- Export Column transformation [Integration Services]
- Row Sampling transformation
- Conditional Split transformation custom properties [Integration Services]
- custom properties [Integration Services]
- Audit transformation
- Term Lookup transformation
- Script Component transformation custom properties [Integration Services]
- Derived Column transformation
- OLE DB Command transformation
- Copy Column transformation custom properties [Integration Services]
- Character Map transformation custom properties [Integration Services]
ms.assetid: 56f5df6a-56f6-43df-bca9-08476a3bd931
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d075bdbd593d450cbeef18162da5e8329d4ea850
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725800"
---
# <a name="transformation-custom-properties"></a>轉換自訂屬性

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  除了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 物件模型中大部分資料流程物件通用的屬性以外，許多資料流程物件都具有物件特有的自訂屬性。 這些自訂屬性只能在執行階段使用，而且不會記錄在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] Managed 程式設計參考文件集中。  
  
 本主題將列出並描述各種資料流程轉換的自訂屬性。 如需大部分資料流程物件通用之屬性的詳細資訊，請參閱 [通用屬性](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)。  
  
 您可以使用屬性運算式來設定轉換的某些屬性。 如需詳細資訊，請參閱 [可以使用運算式設定的資料流程屬性](https://msdn.microsoft.com/library/cd0e171a-08be-45d6-81dc-ed94f37698b8)。  
  
## <a name="transformations-with-custom-properties"></a>含有自訂屬性的轉換  
  
||||  
|-|-|-|  
|[Aggregate](#aggregate)|[匯出資料行](#extract)|[資料列計數](#rowcount)|  
|[稽核](#audit)|[模糊群組 (Fuzzy Grouping)](#fgroup)|[資料列取樣](#rowsamp)|  
|[快取轉換](#cachetransform)|[模糊查閱](#flookup)|[指令碼元件](#script)|  
|[字元對應](#charmap)|[匯入資料行](#insert)|[緩時變維度](#scd)|  
|[條件式分割](#condsplit)|[查閱](#lookup)|[排序](#sort)|  
|[複製資料行](#copymap)|[合併聯結](#mjoin)|[詞彙擷取](#textract)|  
|[資料轉換](#dataconv)|[OLE DB 命令](#oledbcmd)|[詞彙查閱](#tlookup)|  
|[資料採礦查詢](#dmquery)|[百分比取樣](#percent)|[取消樞紐](#unpivot)|  
|[衍生的資料行](#derived)|[樞紐](#pivot)||  
  
### <a name="transformations-without-custom-properties"></a>不含自訂屬性的轉換  
 下列轉換在元件、輸入或輸出層級沒有自訂屬性︰[合併轉換](../../../integration-services/data-flow/transformations/merge-transformation.md)、[多點傳送轉換](../../../integration-services/data-flow/transformations/multicast-transformation.md)和[全部聯集轉換](../../../integration-services/data-flow/transformations/union-all-transformation.md)。 它們只會使用所有資料流程元件通用的屬性。  
  
##  <a name="aggregate"></a> 彙總轉換自訂屬性  
 彙總轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是彙總轉換的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|AutoExtendFactor|Integer|介於 1 到 100 之間的值，指定記憶體於彙總期間可以擴充的百分比。 這個屬性的預設值為 **25**。|  
|CountDistinctKeys|Integer|一個值，指定彙總可寫入之相異計數的確切數目。 如果您指定了 CountDistinctScale 值，就會優先使用 CountDistinctKeys 中的值。|  
|CountDistinctScale|整數 (列舉)|一個值，描述彙總可以在資料行中計算之相異值的近似數目。 此屬性可以有下列其中一個值：<br /><br /> **低** (1) - 表示最多 500,000 個索引鍵值<br /><br /> **中** (2) - 表示最多 5 百萬個索引鍵值<br /><br /> **高** (3) - 表示多於 2 千 5 百萬個索引鍵值。<br /><br /> **未指定** (0) - 表示未使用 CountDistinctScale 值。 使用 **未指定** (0) 選項可能會影響在大型資料集中的效能。|  
|索引鍵|Integer|一個值，指定彙總寫入之群組依據索引鍵的確切數目。 如果您指定了 KeyScale 值，就會優先使用 Keys 中的值。|  
|KeyScale|整數 (列舉)|一個值，描述彙總可寫入之群組依據索引鍵值的近似數目。 此屬性可以有下列其中一個值：<br /><br /> **低** (1) - 表示最多 500,000 個索引鍵值。<br /><br /> **中** (2) - 表示最多 5 百萬個索引鍵值。<br /><br /> **高** (3) - 表示多於 2 千 5 百萬個索引鍵值。<br /><br /> **未指定** (0) - 表示未使用 KeyScale 值。|  
  
 下表描述的是彙總轉換之輸出的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|索引鍵|Integer|一個值，指定彙總可寫入之群組依據索引鍵的確切數目。 如果您指定了 KeyScale 值，就會優先使用 Keys 中的值。|  
|KeyScale|整數 (列舉)|一個值，描述彙總可寫入之群組依據索引鍵值的近似數目。 此屬性可以有下列其中一個值：<br /><br /> **低** (1) - 表示最多 500,000 個索引鍵值，<br /><br /> **中** (2) - 表示最多 5 百萬個索引鍵值，<br /><br /> **高** (3) - 表示多於 2 千 5 百萬個索引鍵值。<br /><br /> **未指定** (0) - 表示未使用 KeyScale 值。|  
  
 下表描述的是彙總轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|AggregationColumnId|Integer|參與 GROUP BY 或彙總函式之資料行的 **LineageID** 。|  
|AggregationComparisonFlags|Integer|一個值，指定彙總轉換如何比較資料行中的字串資料。 如需詳細資訊，請參閱 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。|  
|AggregationType|整數 (列舉)|一個值，指定要在資料行上執行的彙總作業。 此屬性可以有下列其中一個值：<br /><br /> **群組依據** (0)<br /><br /> **計數** (1)<br /><br /> **全部計數** (2)<br /><br /> **相異計數** (3)<br /><br /> **總和** (4)<br /><br /> **平均** (5)<br /><br /> **最大值** (7)<br /><br /> **最小值** (6)|  
|CountDistinctKeys|Integer|當彙總類型為 [相異計數] 時，就是指定彙總可寫入之索引鍵確切數目的值。 如果您指定了 CountDistinctScale 值，就會優先使用 CountDistinctKeys 中的值。|  
|CountDistinctScale|整數 (列舉)|當彙總類型為 [相異計數] 時，就是描述彙總可寫入之索引鍵值近似數目的值。 此屬性可以有下列其中一個值：<br /><br /> **低** (1) - 表示最多 500,000 個索引鍵值，<br /><br /> **中** (2) - 表示最多 5 百萬個索引鍵值，<br /><br /> **高** (3) - 表示多於 2 千 5 百萬個索引鍵值。<br /><br /> **未指定** (0) - 表示未使用 CountDistinctScale 值。|  
|IsBig|布林|一個值，指出資料行包含大於 40 億的值，或有效位數超過雙精確度浮點數值的值。 此值可能是 0 或 1。 0 表示 IsBig 為 **False** 而且資料行不包含大數值或精確值。 這個屬性的預設值為 1。|  
  
 彙總轉換的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [彙總轉換](../../../integration-services/data-flow/transformations/aggregate-transformation.md)。  
  
##  <a name="audit"></a> 稽核轉換自訂屬性  
 稽核轉換只有元件層級上所有資料流程元件通用的屬性。  
  
 下表描述的是稽核轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|LineageItemSelected|整數 (列舉)|針對輸出選取的稽核項目。 此屬性可以有下列其中一個值：<br /><br /> **執行執行個體 GUID** (0)<br /><br /> **執行開始時間** (4)<br /><br /> **電腦名稱** (5)<br /><br /> **封裝識別碼** (1)<br /><br /> **封裝名稱** (2)<br /><br /> **工作識別碼** (8)<br /><br /> **工作名稱** (7)<br /><br /> **使用者名稱** (6)<br /><br /> **版本識別碼** (3)|  
  
 稽核轉換的輸入、輸入資料行和輸出沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [稽核轉換](../../../integration-services/data-flow/transformations/audit-transformation.md)。  
  
##  <a name="cachetransform"></a> 快取轉換轉換自訂屬性  
 快取轉換轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是快取轉換轉換的屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|Connectionmanager|String|指定連接管理員的名稱。|  
|ValidateExternalMetadata|布林|指出快取轉換是否在設計階段使用外部資料來源進行驗證。 如果此屬性設定為 [False]，就會在執行階段根據外部資料來源進行驗證。<br /><br /> 預設值為 [True]。|  
|AvailableInputColumns|String|可用輸入資料行的清單。|  
|InputColumns|String|選取之輸入資料行的清單。|  
|CacheColumnName|String|指定對應至選取之輸入資料行的資料行名稱。<br /><br /> CacheColumnName 屬性中的資料行名稱必須與快取連接管理員編輯器之 [資料行] 頁面上所列的對應資料行名稱相符。<br /><br /> 如需詳細資訊，請參閱 [快取連接管理員編輯器](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md)|  
  
##  <a name="charmap"></a> 字元對應轉換自訂屬性  
 字元對應轉換只有元件層級上所有資料流程元件通用的屬性。  
  
 下表描述的是字元對應轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Integer|一個值，指定屬於輸出資料行來源之輸入資料行的 **LineageID** 。|  
|MapFlags|整數 (列舉)|一個值，指定字元對應轉換在資料行上執行的字串作業。 此屬性可以有下列其中一個值：<br /><br /> **位元組反轉** (2)<br /><br /> **全形** (6)<br /><br /> **半形** (5)<br /><br /> **平假名** (3)<br /><br /> **片假名** (4)<br /><br /> **語言大小寫** (7)<br /><br /> **小寫** (0)<br /><br /> **簡體中文** (8)<br /><br /> **繁體中文**(9)<br /><br /> **大寫** (1)|  
  
 字元對應轉換的輸入、輸入資料行和輸出沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [字元對應轉換](../../../integration-services/data-flow/transformations/character-map-transformation.md)。  
  
##  <a name="condsplit"></a> 條件式分割轉換自訂屬性  
 條件式分割轉換只有元件層級上所有資料流程元件通用的屬性。  
  
 下表描述的是條件式分割轉換之輸出的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|EvaluationOrder|Integer|一個值，指定條件清單中條件式分割轉換所評估之條件 (與輸出相關聯) 的位置。 這些條件會依據最低至最高值的順序進行評估。|  
|運算式|String|代表條件式分割轉換所評估之條件的運算式。 資料行是由歷程識別碼所代表。|  
|FriendlyExpression|String|代表條件式分割轉換所評估之條件的運算式。 資料行是由它們的名稱所代表。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
|IsDefaultOut|布林|一個值，指出輸出是否為預設輸出。|  
  
 條件式分割轉換的輸入、輸入資料行和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)。  
  
##  <a name="copymap"></a> 複製資料行轉換自訂屬性  
 複製資料行轉換只有元件層級上所有資料流程元件通用的屬性。  
  
 下表描述的是複製資料行轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|copyColumnId|Integer|從中複製輸出資料行之輸入資料行的 **LineageID** 。|  
  
 複製資料行轉換的輸入、輸入資料行和輸出沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [複製資料行轉換](../../../integration-services/data-flow/transformations/copy-column-transformation.md)。  
  
##  <a name="dataconv"></a> 資料轉換自訂屬性  
 資料轉換只有元件層級上所有資料流程元件通用的屬性。  
  
 下表描述的是資料轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|FastParse|布林|一個值，指出資料行會使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 所提供之速度更快但不區分地區設定的快速剖析常式，還是區分地區設定的標準剖析常式。 此屬性的預設值為 **False**。 如需詳細資訊，請參閱 [快速剖析](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) 和 [標準剖析](https://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)。 。<br /><br /> 注意:雖然您無法在 [資料轉換編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|SourceInputColumnLineageId|Integer|屬於輸出資料行來源之輸入資料行的 **LineageID** 。|  
  
 資料轉換的輸入、輸入資料行和輸出沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)。  
  
##  <a name="dmquery"></a> 資料採礦查詢轉換自訂屬性  
 資料採礦查詢轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是資料採礦查詢轉換的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|連接物件的唯一識別碼。|  
|ASConnectionString|String|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 專案或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫的連接字串。|  
|CatalogName|String|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫的名稱。|  
|ModelName|String|資料採礦模型的名稱。|  
|ModelStructureName|String|採礦結構的名稱。|  
|ObjectRef|String|可識別轉換所使用之資料採礦結構的 XML 標記。|  
|QueryText|String|轉換所使用的預測查詢陳述式。|  
  
 資料採礦查詢轉換的輸入、輸入資料行、輸出和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [資料採礦查詢轉換](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md)。  
  
##  <a name="derived"></a> 衍生的資料行轉換自訂屬性  
 衍生的資料行轉換只有元件層級上所有資料流程元件通用的屬性。  
  
 下表描述的是衍生的資料行轉換之輸入資料行和輸出資料行的自訂屬性。 當您選擇要加入衍生的資料行當做新資料行時，這些自訂屬性會套用至新的輸出資料行。當您選擇要使用衍生的結果來取代現有輸入資料行的內容時，這些自訂屬性會套用至現有的輸入資料行。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|運算式|String|代表條件式分割轉換所評估之條件的運算式。 資料行是由資料行的 **LineageID** 屬性所代表。|  
|FriendlyExpression|String|代表條件式分割轉換所評估之條件的運算式。 資料行是由它們的名稱所代表。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
  
 衍生的資料行轉換的輸入和輸出沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [衍生的資料行轉換](../../../integration-services/data-flow/transformations/derived-column-transformation.md)。  
  
##  <a name="extract"></a> 匯出資料行轉換自訂屬性  
 匯出資料行轉換只有元件層級上所有資料流程元件通用的屬性。  
  
 下表描述的是匯出資料行轉換之輸入資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|AllowAppend|布林|一個值，指定轉換是否將資料附加至現有的檔案。 此屬性的預設值為 **False**。|  
|ForceTruncate|布林|一個值，指定轉換是否在寫入資料之前截斷現有的檔案。 此屬性的預設值為 **False**。|  
|FileDataColumnID|Integer|一個值，可識別包含轉換插入檔案中之資料的資料行。 在擷取資料行上，這個屬性的值為 **0**。在檔案路徑資料行上，這個屬性包含擷取資料行的 **LineageID** 。|  
|WriteBOM|布林|一個值，指定是否要將位元組順序標記 (BOM) 寫入該檔案。|  
  
 匯出資料行轉換的輸入、輸出和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [匯出資料行轉換](../../../integration-services/data-flow/transformations/export-column-transformation.md)。  
  
##  <a name="insert"></a> 匯入資料行轉換自訂屬性  
 匯入資料行轉換只有元件層級上所有資料流程元件通用的屬性。  
  
 下表描述的是匯入資料行轉換之輸入資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|ExpectBOM|布林|一個值，指定匯入資料行轉換是否必須使用位元組順序標記 (BOM)。 BOM 只有在資料的資料類型為 DT_NTEXT 時才需要。|  
|FileDataColumnID|Integer|一個值，可識別包含轉換插入資料流程中之資料的資料行。 在即將插入之資料的資料行上，這個屬性的值為 0。在包含來源檔案路徑的資料行上，這個屬性包含即將插入之資料的資料行 **LineageID** 。|  
  
 匯入資料行轉換的輸入、輸出和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [匯入資料行轉換](../../../integration-services/data-flow/transformations/import-column-transformation.md)。  
  
##  <a name="fgroup"></a> 模糊群組轉換自訂屬性  
 模糊群組轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是模糊群組轉換的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|Delimiters|String|轉換所使用的 Token 分隔符號。 預設分隔符號包括下列字元：空格 ( )、逗號 (,)、句號 (.)、分號 (;)、冒號 (:)、連字號 (-)、雙引號 (")、單引號 (')、& 符號、正斜線 (/)、反斜線 (\\)、@ 符號、驚嘆號 (!)、問號 (?)、左括弧 (()、右括弧 ())、小於 (\<)、大於 (>)、左方括弧 ([)、右方括弧 (])、左大括弧 ({)、右大括弧 (})、縱線字元 (&#124;)、數字符號 (#)、星號 (*)、插入號 (^) 和百分比 (%)。|  
|Exhaustive|布林|一個值，指定每個輸入資料錄是否會與其他每個輸入資料錄比較。 **True** 值大部分用於偵錯目的。 此屬性的預設值為 **False**。<br /><br /> 注意:雖然您無法在 [模糊群組轉換編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|MaxMemoryUsage|Integer|可供轉換使用的記憶體數量上限。 此屬性的預設值為 **0**，表示啟用動態記憶體使用量。<br /><br /> 此屬性的值可以使用屬性運算式指定。<br /><br /> 注意:雖然您無法在 [模糊群組轉換編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|MinSimilarity|Double|轉換用來識別重複項目的相似度臨界值，表示成介於 0 與 1 之間的值。  這個屬性的預設值為 0.8。|  
  
 下表描述的是模糊群組轉換之輸入資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|ExactFuzzy|整數 (列舉)|一個值，指定轉換會執行模糊比對或完全比對。 有效值為 [Exact] 和 [Fuzzy]。 這個屬性的預設值為 [Fuzzy]。|  
|FuzzyComparisonFlags|整數 (列舉)|一個值，指定轉換如何比較資料行中的字串資料。 此屬性可以有下列其中一個值：<br /><br /> **FullySensitive**<br /><br /> **IgnoreCase**<br /><br /> **IgnoreKanaType**<br /><br /> **IgnoreNonSpace**<br /><br /> **IgnoreSymbols**<br /><br /> **IgnoreWidth**<br /><br /> <br /><br /> 如需詳細資訊，請參閱 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。|  
|LeadingTrailingNumeralsSignificant|整數 (列舉)|一個值，指定數字的重要性。 此屬性可以有下列其中一個值：<br /><br /> **NumeralsNotSpecial** (0) - 數字不重要時使用。<br /><br /> **LeadingNumeralsSignificant** (1) - 開頭數字很重要時使用。<br /><br /> **TrailingNumeralsSignificant** (2) - 尾端數字很重要時使用。<br /><br /> **LeadingAndTrailingNumeralsSignificant** (3) - 開頭和尾端數字都很重要時使用。|  
|MinSimilarity|Double|用於資料行之聯結的相似度臨界值，指定成介於 0 與 1 之間的值。 只有大於臨界值的資料列會判定為相符項目。|  
|ToBeCleaned|布林|一個值，指定此資料行是否用於識別重複項目。亦即，這個資料行是否為您分組所依據的資料行。 此屬性的預設值為 **False**。|  
  
 下表描述的是模糊群組轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|ColumnType|整數 (列舉)|一個值，可識別輸出資料行的類型。 此屬性可以有下列其中一個值：<br /><br /> **Undefined** (0)<br /><br /> **KeyIn** (1)<br /><br /> **KeyOut** (2)<br /><br /> **Similarity** (3)<br /><br /> **ColumnSimilarity** (4)<br /><br /> **PassThru** (5)<br /><br /> **Canonica**l (6)|  
|InputID|Integer|對應輸入資料行的 **LineageID** 。|  
  
 模糊群組轉換的輸入和輸出沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [模糊群組轉換](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)。  
  
##  <a name="flookup"></a> 模糊查閱轉換自訂屬性  
 模糊查閱轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是模糊查閱轉換的自訂屬性。 除了 **ReferenceMetadataXML** 以外的所有屬性都是讀取/寫入。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|CopyReferenceTable|布林|指定是否應該針對模糊查閱索引建構和後續的查閱建立參考資料表的副本。 這個屬性的預設值為 **True**。|  
|Delimiters|String|轉換用來 Token 化資料行值的分隔符號。 預設分隔符號包括下列字元：空格 ( )、逗號 (,)、句號 (.)、分號 (;)、冒號 (:)、連字號 (-)、雙引號 (")、單引號 (')、& 符號、正斜線 (/)、反斜線 (\\)、@ 符號、驚嘆號 (!)、問號 (?)、左括弧 (()、右括弧 ())、小於 (\<)、大於 (>)、左方括弧 ([)、右方括弧 (])、左大括弧 ({)、右大括弧 (})、縱線字元 (&#124;)。 數字符號 (#)、星號 (*)、插入號 (^) 及百分比 (%)。|  
|DropExistingMatchIndex|布林|值，指定是否要在 MatchIndexOptions 未設定為 ReuseExistingIndex 時，刪除 MatchIndexName 中指定的比對索引。 這個屬性的預設值是 [True]。|  
|Exhaustive|布林|一個值，指定每個輸入資料錄是否會與其他每個輸入資料錄比較。 **True** 值大部分用於偵錯目的。 此屬性的預設值為 **False**。<br /><br /> 注意:雖然您無法在 [模糊查閱轉換編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|MatchIndexName|String|相符索引的名稱。 相符索引是轉換用以建立並儲存它所使用之索引的資料表。 若重複使用相符索引，MatchIndexName 會指定要重複使用的索引。 MatchIndexName 必須是有效的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 識別碼名稱。 例如，如果名稱包含空格，此名稱就必須以方括號括住。|  
|MatchIndexOptions|整數 (列舉)|一個值，指定轉換如何管理相符索引。 此屬性可以有下列其中一個值：<br /><br /> **ReuseExistingIndex** (0)<br /><br /> **GenerateNewIndex** (1)<br /><br /> **GenerateAndPersistNewIndex** (2)<br /><br /> **GenerateAndMaintainNewIndex** (3)|  
|MaxMemoryUsage|Integer|查閱資料表的快取大小上限。 此屬性的預設值為 **0**，表示快取大小沒有任何限制。<br /><br /> 此屬性的值可以使用屬性運算式指定。<br /><br /> 注意:雖然您無法在 [模糊查閱轉換編輯器] 中使用這個屬性，但是可以使用 [進階編輯器] 來設定這個屬性。|  
|MaxOutputMatchesPerInput|Integer|轉換可以針對每個輸入資料列傳回的相符項目數上限。 這個屬性的預設值為 **1**。<br /><br /> 注意:您只能使用 [進階編輯器] 來指定大於 100 的值。|  
|MinSimilarity|Integer|轉換在元件層級使用的相似度臨界值，指定成介於 0 與 1 之間的值。 只有大於臨界值的資料列會判定為相符項目。|  
|ReferenceMetadataXML|String|[!INCLUDE[ssInternalOnly](../../../includes/ssinternalonly-md.md)]|  
|ReferenceTableName|String|查閱資料表的名稱。 此名稱必須是有效的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 識別碼名稱。 例如，如果名稱包含空格，此名稱就必須以方括號括住。|  
|WarmCaches|布林|如果它是 True，查閱就會在執行開始之前，將索引和參考資料表部分載入記憶體中。 這可能會強化效能。|  
  
 下表描述的是模糊查閱轉換之輸入資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|FuzzyComparisonFlags|Integer|一個值，指定轉換如何比較資料行中的字串資料。 如需詳細資訊，請參閱 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。|  
|FuzzyComparisonFlagsEx|整數 (列舉)|一個值，指定轉換所使用的擴充比較旗標。 這些值可包括 **MapExpandLigatures、MapFoldCZone**、 **MapFoldDigits**、 **MapPrecomposed**和 **NoMapping**。 **NoMapping** 無法與其他旗標搭配使用。|  
|JoinToReferenceColumn|String|一個值，指定此資料行在參考資料表中所聯結的資料行名稱。|  
|JoinType|Integer|一個值，指定轉換會執行模糊比對或完全比對。 這個屬性的預設值為 [Fuzzy]。 代表完全聯結類型的整數值為 **1**，而代表模糊聯結類型的整數值為 **2**。|  
|MinSimilarity|Double|轉換在資料行層級使用的相似度臨界值，指定成介於 0 與 1 之間的值。 只有大於臨界值的資料列會判定為相符項目。|  
  
 下表描述的是模糊查閱轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
> [!NOTE]  
>  若為包含對應輸入資料行之通過值的輸出資料行，CopyFromReferenceColumn 就是空的，而且 SourceInputColumnLineageID 會包含對應輸入資料行的 **LineageID** 。 若為包含查閱結果的輸出資料行，CopyFromReferenceColumn 會包含查閱資料行的名稱，而且 SourceInputColumnLineageID 是空的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|ColumnType|整數 (列舉)|一個值，可識別轉換加入至輸出之資料行的輸出資料行類型。 此屬性可以有下列其中一個值：<br /><br /> **Undefined** (0)<br /><br /> **Similarity** (1)<br /><br /> **Confidence** (2)<br /><br /> **ColumnSimilarity** (3)|  
|CopyFromReferenceColumn|String|一個值，指定參考資料表中提供輸出資料行之值的資料行名稱。|  
|SourceInputColumnLineageId|Integer|一個值，可識別提供值給這個輸出資料行的輸入資料行。|  
  
 模糊查閱轉換的輸入和輸出沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [模糊查閱轉換](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)。  
  
##  <a name="lookup"></a> 查閱轉換自訂屬性  
 查閱轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是查閱轉換的自訂屬性。 除了 **ReferenceMetadataXML** 以外的所有屬性都是讀取/寫入。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|CacheType|整數 (列舉)|查閱資料表的快取類型。 這些值為 **Full** (0)、 **Partial** (1) 和 **None** (2)。 這個屬性的預設值為 **Full**。|  
|DefaultCodePage|Integer|無法從資料來源中取得字碼頁資訊時要使用的預設字碼頁。|  
|MaxMemoryUsage|Integer|查閱資料表的快取大小上限。 此屬性的預設值為 **25**，表示快取大小沒有任何限制。|  
|MaxMemoryUsage64|Integer|在 64 位元電腦上，查閱資料表的快取大小上限。|  
|NoMatchBehavior|整數 (列舉)|一個值，指定在參考資料集中沒有相符項目的資料列是否會被視為錯誤。<br /><br /> 當此屬性設定為 [將無相符項目的資料列視為錯誤] (0) 時，沒有相符項目的資料列就會被視為錯誤。 您可以使用 [查閱轉換編輯器] 對話方塊的 [錯誤輸出] 頁面來指定發生這種錯誤類型時要採取的動作。 如需詳細資訊，請參閱[查閱轉換編輯器 &#40;錯誤輸出頁面&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)。<br /><br /> 當屬性設定為 [將無相符項目的資料列傳送至無相符結果輸出] (1)，資料列就不會被視為錯誤。<br /><br /> 預設值是 [將無相符項目的資料列視為錯誤] (0)。|  
|ParameterMap|String|歷程識別碼的分號分隔清單，而這些歷程識別碼會對應至 **SqlCommand** 陳述式中使用的參數。|  
|ReferenceMetadataXML|String|轉換從查閱資料表中複製到輸出之資料行的中繼資料。|  
|SqlCommand|String|填入查閱資料表的 SELECT 陳述式。|  
|SqlCommandParam|String|填入查閱資料表的參數化 SQL 陳述式。|  
  
 下表描述的是查閱轉換之輸入資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|CopyFromReferenceColumn|String|在參考資料表中，從中複製資料行的資料行名稱。|  
|JoinToReferenceColumns|String|在參考資料表中，來源資料行所聯結的資料行名稱。|  
  
 下表描述的是查閱轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|CopyFromReferenceColumn|String|在參考資料表中，從中複製資料行的資料行名稱。|  
  
 查閱轉換的輸入和輸出沒有任何自訂屬性。  
  
 如需相關資訊，請參閱 [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)。  
  
##  <a name="mjoin"></a> 合併聯結轉換自訂屬性  
 合併聯結轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是合併聯結轉換的自訂屬性。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|JoinType|整數 (列舉)|指定聯結是內部聯結 (2)、左方外部聯結 (1) 或完整聯結 (0)。|  
|MaxBuffersPerInput|Integer|您再也不必設定 **MaxBuffersPerInput** 屬性的值，因為 Microsoft 已做出變更，降低合併聯結轉換會耗用過多記憶體的風險。 這個問題有時候會發生在合併聯結的多個輸入以不平均的速率產生資料時。|  
|NumKeyColumns|Integer|聯結中使用的資料行數目。|  
|TreatNullsAsEqual|布林|一個值，指定轉換是否要將 Null 值當做相等值處理。 此屬性的預設值為 [True]。 如果此屬性值為 [False]，轉換處理 Null 值的方式就如同 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 一樣。|  
  
 下表描述的是合併聯結轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|InputColumnID|Integer|從中複製資料到這個輸出資料行之輸入資料行的 **LineageID** 。|  
  
 合併聯結轉換的輸入、輸入資料行和輸出沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [合併聯結轉換](../../../integration-services/data-flow/transformations/merge-join-transformation.md)。  
  
##  <a name="oledbcmd"></a> OLE DB 命令轉換自訂屬性  
 OLE DB 命令轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 OLE DB 命令轉換的自訂屬性。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|CommandTimeout|Integer|逾時之前 SQL 命令可以執行的秒數上限。值為 **0** 指出無限的時間。 這個屬性的預設值為 **0**。|  
|DefaultCodePage|Integer|無法從資料來源中取得字碼頁資訊時要使用的字碼頁。|  
|SqlCommand|String|轉換針對資料流程中每個資料列執行的 Transact-SQL 陳述式。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
  
 下表描述的是 OLE DB 命令轉換之外部資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|DBParamInfoFlag|整數 (位元遮罩)|描述參數特定的旗標集。 如需詳細資訊，請參閱 MSDN Library 中 OLE DB 文件集的 DBPARAMFLAGSENUM。|  
  
 OLE DB 命令轉換的輸入、輸入資料行、輸出和輸出資料行沒有任何自訂屬性。  
  
 如需相關資訊，請參閱 [OLE DB Command Transformation](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md)。  
  
##  <a name="percent"></a> 百分比取樣轉換自訂屬性  
 百分比取樣轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是百分比取樣轉換的自訂屬性。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|SamplingSeed|Integer|隨機號碼產生器所使用的種子。 此屬性的預設值為 **0**，表示轉換會使用滴答計數。|  
|SamplingValue|Integer|取樣的大小 (以來源的百分比為單位)。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
  
 下表描述的是百分比取樣轉換之輸出的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|已選取|布林|指定取樣資料列要導向的目標輸出。 在選取的輸出中，Selected 設定為 [True]，在未選取的輸出中，Selected 設定為 [False]。|  
  
 百分比取樣轉換的輸入、輸入資料行和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [百分比取樣轉換](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)。  
  
##  <a name="pivot"></a> 樞紐轉換自訂屬性  
 下表描述樞紐轉換的自訂元件屬性。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|**PassThroughUnmatchedPivotKeyts**|布林|設定為 [True] 時，可將樞紐轉換設定為忽略包含 [樞紐索引鍵] 資料行中未辨識之值的資料列，並在執行封裝時，將所有樞紐索引鍵值輸出至記錄訊息。|  
  
 下表描述的是樞紐轉換之輸入資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|PivotUsage|整數 (列舉)|一個值，指定當資料集進行樞紐處理時，資料行的角色。<br /><br /> **0**:<br />                      資料行未經樞紐，且資料行值已傳送至轉換輸出。<br /><br /> **1**:<br />                      資料行是集索引鍵的一部分，可識別一個集中的一或多個資料列。 具有相同集索引鍵的所有輸入資料列會組合成一個輸出資料列。<br /><br /> **2**:<br />                      資料行為樞紐資料行。 至少應從每個資料行值建立一個資料行。<br /><br /> **3**:<br />                      此資料行的值會置於樞紐後建立的資料行中。|  
  
 下表描述的是樞紐轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|PivotKeyValue|String|資料行的其中一個可能值，此值會由其 PivotUsage 屬性的值標示為樞紐索引鍵。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
|SourceColumn|Integer|包含樞紐值之輸入資料行的 **LineageID** ，或 -1。 值為 -1 表示此資料行不會用於樞紐作業中。|  
  
 如需詳細資訊，請參閱 [樞紐轉換](../../../integration-services/data-flow/transformations/pivot-transformation.md)。  
  
##  <a name="rowcount"></a> 資料列計數轉換自訂屬性  
 資料列計數轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是資料列計數轉換的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|VariableName|String|保存資料列計數之變數的名稱。|  
  
 資料列計數轉換的輸入、輸入資料行、輸出和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [Row Count Transformation](../../../integration-services/data-flow/transformations/row-count-transformation.md)。  
  
##  <a name="rowsamp"></a> 資料列取樣轉換自訂屬性  
 資料列取樣轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是資料列取樣轉換的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|SamplingSeed|Integer|隨機號碼產生器所使用的種子。 此屬性的預設值為 **0**，表示轉換會使用滴答計數。|  
|SamplingValue|Integer|取樣的資料列計數。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
  
 下表描述的是資料列取樣轉換之輸出的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|已選取|布林|指定取樣資料列要導向的目標輸出。 在選取的輸出中，Selected 設定為 [True]，在未選取的輸出中，Selected 設定為 [False]。|  
  
 下表描述的是資料列取樣轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Integer|一個值，指定屬於輸出資料行來源之輸入資料行的 **LineageID** 。|  
  
 資料列取樣轉換的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [資料列取樣轉換](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)。  
  
##  <a name="script"></a> 指令碼元件自訂屬性  
 指令碼元件同時具有自訂屬性以及所有資料流程元件通用的屬性。 不論指令碼元件是當做來源、轉換或目的地，您都可以使用相同的自訂屬性。  
  
 下表描述的是指令碼元件的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|ReadOnlyVariables|String|可供指令碼元件用於唯讀存取之變數的逗號分隔清單。|  
|ReadWriteVariables|String|可供指令碼元件用於可讀寫存取之變數的逗號分隔清單。|  
  
 除非指令碼開發人員為指令碼元件的輸入、輸入資料行、輸出和輸出資料行建立自訂屬性，否則它們沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [指令碼元件](../../../integration-services/data-flow/transformations/script-component.md)。  
  
##  <a name="scd"></a> 緩時變維度轉換自訂屬性  
 緩時變維度轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是緩時變維度轉換的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|CurrentRowWhere|String|SELECT 陳述式中的 WHERE 子句，它會從具有相同商務索引鍵的資料列中選取目前的資料列。|  
|EnableInferredMember|布林|一個值，指定是否要偵測推斷的成員更新。 這個屬性的預設值為 **True**。|  
|FailOnFixedAttributeChange|布林|一個值，指定當含有固定屬性的資料列資料行變更或維度資料表中的查閱失敗時，轉換是否會失敗。 如果您預期傳入資料列會包含新的記錄，請將這個值設定為 [True]，以便在查閱失敗之後繼續進行轉換，因為轉換會使用失敗來識別新的記錄。 此屬性的預設值為 **False**。|  
|FailOnLookupFailure|布林|一個值，指定當現有資料錄的查閱失敗時，轉換是否會失敗。 此屬性的預設值為 **False**。|  
|IncomingRowChangeType|Integer|一個值，指定所有傳入資料列是否都是新的資料列，或轉換是否應該偵測變更的類型。|  
|InferredMemberIndicator|String|推斷的成員的資料行名稱。|  
|SqlCommand|String|用來建立結構描述資料列集的 SQL 陳述式。|  
|UpdateChangingAttributeHistory|布林|一個值，指出歷程記錄屬性更新是否會導向至轉換輸出，以便變更屬性更新。|  
  
 下表描述的是緩時變維度轉換之輸入資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|ColumnType|整數 (列舉)|資料行的更新類型。 這些值為：**變更屬性** (2)、**固定屬性** (4)、**歷程記錄屬性** (3)、**索引鍵** (1) 和**其他** (0)。|  
  
 緩時變維度轉換的輸入、輸出和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [緩時變維度轉換](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)。  
  
##  <a name="sort"></a> 排序轉換自訂屬性  
 排序轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是排序轉換的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|EliminateDuplicates|布林|指定轉換是否會從轉換輸出中移除重複的資料列。 此屬性的預設值為 **False**。|  
|MaximumThreads|Integer|包含轉換可用於排序的執行緒數目上限。 值為 **0** 表示無限的執行緒數目。 這個屬性的預設值為 **0**。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
  
 下表描述的是排序轉換之輸入資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|NewComparisonFlags|整數 (位元遮罩)|一個值，指定轉換如何比較資料行中的字串資料。 如需詳細資訊，請參閱 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。|  
|NewSortKeyPosition|Integer|一個值，指定資料行的排序次序。 值為 0 表示這個資料行的資料不會進行排序。|  
  
 下表描述的是排序轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|SortColumnID|Integer|排序資料行的 **LineageID** 。|  
  
 排序轉換的輸入和輸出沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [排序轉換](../../../integration-services/data-flow/transformations/sort-transformation.md)。  
  
##  <a name="textract"></a> 詞彙擷取轉換自訂屬性  
 詞彙擷取轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是詞彙擷取轉換的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|--------------|-----------------|  
|FrequencyThreshold|Integer|一個數值，指出在擷取某個詞彙之前，它必須出現的次數。 這個屬性的預設值為 **2**。|  
|isCaseSensitive|布林|一個值，指定在擷取名詞和名詞片語時是否要區分大小寫。 此屬性的預設值為 **False**。|  
|MaxLengthOfTerm|Integer|一個數值，指出詞彙的長度上限。 這個屬性只會套用至片語。 這個屬性的預設值為 **12**。|  
|NeedRefenceData|布林|一個值，指定轉換是否會使用儲存在參考資料表中的排除詞彙清單。 此屬性的預設值為 **False**。|  
|OutTermColumn|String|包含排除詞彙之資料行的名稱。|  
|OutTermTable|String|包含具有排除詞彙之資料行的資料表名稱。|  
|ScoreType|Integer|一個值，指定要與詞彙產生關聯的分數類型。 有效的值為 0 (表示頻率) 和 1 (表示 TFIDF 分數)。 TFIDF 分數是「詞彙頻率」和「反向文件頻率」的乘積，定義為：詞彙 T 的 TFIDF = (T 的頻率) \* log( (輸入中的資料列數目) / (有 T 的資料列數目) )。 這個屬性的預設值為 **0**。|  
|WordOrPhrase|Integer|指定詞彙類型的值。 有效的值包括 0 (表示只有字詞)、1 (表示只有名詞片語) 和 2 (表示同時有字詞和名詞片語)。 這個屬性的預設值為 **0**。|  
  
 詞彙擷取轉換的輸入、輸入資料行、輸出和輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [詞彙擷取轉換](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)。  
  
##  <a name="tlookup"></a> 詞彙查閱轉換自訂屬性  
 詞彙查閱轉換同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是詞彙查閱轉換的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|isCaseSensitive|布林|一個值，指定區分大小寫的比較是否會套用至輸入資料行文字和查閱詞彙的相符項目。 此屬性的預設值為 **False**。|  
|RefTermColumn|String|包含查閱詞彙之資料行的名稱。|  
|RefTermTable|String|包含具有查閱詞彙之資料行的資料表名稱。|  
  
 下表描述的是詞彙查閱轉換之輸入資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|InputColumnType|Integer|一個值，指定資料行的使用方式。 有效的值包括 0 (代表通過資料行)、1 (代表查閱資料行) 和 2 (代表同時屬於通過和查閱資料行的資料行)。|  
  
 下表描述的是詞彙查閱轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|CustomLineageID|Integer|對應輸入資料行的 **LineageID** (如果該資料行的 **InputColumnType** 是 0 或 2 的話)。|  
  
 詞彙查閱轉換的輸入和輸出沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [詞彙查閱轉換](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)。  
  
##  <a name="unpivot"></a> 取消樞紐轉換自訂屬性  
 取消樞紐轉換只有元件層級上所有資料流程元件通用的屬性。  
  
> [!NOTE]  
>  本節仰賴於 [取消樞紐轉換](../../../integration-services/data-flow/transformations/unpivot-transformation.md) 中所描述的取消樞紐狀況，來說明此處所描述之選項的使用方式。  
  
 下表描述的是取消樞紐轉換之輸入資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性|資料類型|Description|  
|--------------|---------------|-----------------|  
|DestinationColumn|Integer|輸入資料行所對應之輸出資料行的 **LineageID** 。 值為 -1 表示輸入資料行不會對應至輸出資料行。|  
|PivotKeyValue|String|複製到轉換輸出資料行的值。<br /><br /> 此屬性的值可以使用屬性運算式指定。<br /><br /> 在[取消樞紐轉換](../../../integration-services/data-flow/transformations/unpivot-transformation.md)所描述的取消樞紐狀況中，樞紐值包括 Ham、Coke、Milk、Beer 和 Chips 等文字值。 這些值會在 [樞紐索引鍵值資料行名稱] 選項所指定的新 Product 資料行中顯示成文字值。|  
  
 下表描述的是取消樞紐轉換之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|PivotKey|布林|指出輸入資料行之 **PivotKeyValue** 屬性中的值是否會寫入這個輸出資料行中。<br /><br /> 在 [取消樞紐轉換](../../../integration-services/data-flow/transformations/unpivot-transformation.md)所描述的取消樞紐狀況中，樞紐值資料行名稱為 **Product** ，並且指定 Ham、Coke、Milk、Beer 和 Chips 資料行已取消樞紐的新 **Product** 資料行。|  
  
 取消樞紐轉換的輸入和輸出沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [取消樞紐轉換](../../../integration-services/data-flow/transformations/unpivot-transformation.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [通用屬性](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)   
 [路徑屬性](https://msdn.microsoft.com/library/89b1e347-9579-4f6b-af74-c6519ea08eea)   
 [可以使用運算式設定的資料流程屬性](https://msdn.microsoft.com/library/cd0e171a-08be-45d6-81dc-ed94f37698b8)  
  
  
