---
title: 在 SQL Server Management Studio 中使用 Analysis Services 範本 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 54ad1954-22e2-4628-b334-8fad8e9433b8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1c8daa38dd1bda5c23d60478394cd1f6450d41ff
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543740"
---
# <a name="use-analysis-services-templates-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中使用 Analysis Services 範本
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供一組範本，協助您快速建立 XMLA 指令碼、DMX 或 MDX 查詢、在 Cube 或表格式模型中建立 KPI、編寫備份與還原作業的指令碼，以及執行許多其他工作。 範本位於 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的範本總管****。

 此主題包含用於多維度模型和表格式模型之範本的清單，並提供如何使用中繼資料總管和範本總管建立 MDX 查詢和 XMLA 陳述式的範例。

 這個主題包括下列各節：

 [開啟 Analysis Services 範本](#bkmk_usingTE)

 [使用範本在表格式模型上建立及執行 MDX 查詢](#BKMK_Building_Queries)

 [從範本建立 XMLA 腳本](#bkmk_backup)

 [使用 XMLA 範本產生架構資料列集查詢](#bkmk_schemarowset)

 [Analysis Services 範本參考](#bkmk_Ref)

 本主題未涵蓋 DMX 範本。 如需如何使用範本建立資料採礦查詢的範例，請參閱 [在 SQL Server Management Studio 中建立 DMX 查詢](../data-mining/create-a-dmx-query-in-sql-server-management-studio.md) 或 [根據範本建立單一預測查詢](../data-mining/create-a-singleton-prediction-query-from-a-template.md)。

##  <a name="open-an-analysis-services-template"></a><a name="bkmk_usingTE"></a> 開啟 Analysis Services 範本
 Database Engine 查詢和 Analysis Services 查詢與命令的所有範本都是在範本總管中存取。

 若要開啟範本總管，請選取 [檢視]**** 功能表上的 [範本總管]****。 接著按一下 Cube 圖示，查看 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的可用範本清單。

 ![範本總管，針對 Analysis Services 進行篩選](../media/ssas-templateexplorer.gif "範本總管，針對 Analysis Services 進行篩選")

 若要開啟範本，以滑鼠右鍵按一下範本名稱，然後選取 [開啟]****，或將範本拖曳至已開啟的查詢視窗。 在查詢視窗開啟之後，您可以使用工具列或 [查詢] 功能表上的命令，建立陳述式：

-   若要檢查查詢的語法，請按一下 [剖析]****。

-   若要執行查詢，請按一下 [執行]****。

     若要停止執行中的查詢，請按一下 [取消執行查詢]****。

-   檢視畫面底端的 [結果]**** 索引標籤中的查詢結果。

     切換至 [訊息]**** 索引標籤，查看所傳回的記錄數目、與查詢執行相關聯的錯誤、查詢陳述式和任何其他訊息。 例如，如果對處於 DirectQuery 模式的模型執行 DAX 陳述式，您會看到 xVelocity 記憶體中分析引擎 (VertiPaq) 所產生的 Transact-SQL 陳述式。

##  <a name="build-and-run-an-mdx-query-on-a-tabular-model-using-a-template"></a><a name="BKMK_Building_Queries"></a> 使用範本在表格式模型上建立及執行 MDX 查詢
 這個範例示範如何將表格式模型資料庫做為資料來源，在 SQL Server Management Studio 中建立 MDX 查詢。 若要在電腦上重複此範例，您可以 [下載 Adventureworks 表格式模型範例專案](https://go.microsoft.com/fwlink/?LinkId=231183)。

> [!WARNING]
>  您不能對 DirectQuery 模式下部署的表格式模型使用 MDX 查詢。 但是，可透過將 DAX 資料表查詢搭配 EVALUATE 命令使用，傳送對等查詢。 如需詳細資訊，請參閱[DAX 查詢的參數](https://msdn.microsoft.com/library/gg492200(v=sql.120).aspx)。

#### <a name="create-an-mdx-query-from-a-template"></a>從範本建立 MDX 查詢

1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟包含所要查詢之表格式模型的執行個體。 以滑鼠右鍵按一下資料庫圖示，選取 [新增查詢]****，然後選取 [MDX]****。

2.  在範本瀏覽器中，開啟 [Analysis Services 範本] 中的 [MDX]****，然後開啟 [查詢]****。 將 [基本查詢]**** 拖曳至查詢視窗。

3.  使用中繼資料總管****，將下列欄位和量值拖曳至查詢範本：

    1.  取代 \<row_axis, mdx_set> 為 **[產品類別目錄]. [產品類別名稱]**。

    2.  取代 \<column_axis, mdx_set> 為 **[Date]. [行事歷年度]。[行事歷年度]**。

    3.  取代 \<from_clause, mdx_name> 為 **[網際網路銷售]**。

    4.  取代 \<where_clause, mdx_set> 為 **[量值]. [網際網路總銷售額]**。

4.  您可以直接執行原有的查詢，但可能要進行某些變更，例如加入函數以傳回特定成員。 例如，輸入 `.members` **[Product Category]. [產品類別名稱]**。 如需詳細資訊，請參閱 [使用成員運算式](/sql/mdx/using-member-expressions)。

##  <a name="create-xmla-script-from-a-template"></a><a name="bkmk_backup"></a> 從範本建立 XMLA 指令碼
 範本總管隨附的 XMLA 命令範本可用於建立監視及更新 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的指令碼，不論執行個體處於多維度和資料採礦模式或表格式模式。 **XMLA** 範本包含下列類型的指令碼範例：

-   備份、還原與同步處理作業

-   取消指定的處理序或命令

-   處理物件

-   探索結構描述資料列集

-   監視伺服器狀態，包括作業、連接、交易、記憶體和效能計數器

#### <a name="create-a-backup-command-script-from-a-template"></a>從範本建立備份命令指令碼

1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟包含所要查詢之資料庫的執行個體。 以滑鼠右鍵按一下資料庫圖示，選取 [新增查詢]****，然後選取 [XMLA]****。

    > [!WARNING]
    >  您不能透過變更限制清單或在連接對話方塊中指定資料庫，設定 XMLA 查詢的內容。 您必須從要查詢的資料庫開啟 XMLA 查詢視窗。

2.  將 `Backup` 範本拖曳至空白查詢視窗。

3.  按兩下元素內的文字 \<DatabaseID> 。

4.  在 [物件總管] 中，選取要備份的資料庫，並將此資料庫拖放在 DatabaseID 元素的角括號內。

5.  按兩下元素內的文字 \<File> 。 輸入備份檔案的名稱，包括 .abf 副檔名。 如果您不使用預設的備份位置，請指定完整檔案路徑。 如需詳細資訊，請參閱[備份、還原和同步處理資料庫 &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)。

##  <a name="generate-a-schema-rowset-query-using-an-xmla-template"></a><a name="bkmk_schemarowset"></a> 使用 XMLA 範本產生結構描述資料列集查詢
 範本總管**** 只包含一個用於結構描述資料列集查詢的範本。 若要使用此範本，您必須熟悉所要使用之個別結構描述資料列集的需求，包括任何必要元素，以及可做為限制的資料行。 如需詳細資訊，請參閱 [Analysis Services 結構描述資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets)。

 請注意，為了簡單起見，許多結構描述資料列集也已公開做為動態管理檢視 (DMV)。 透過使用對應的 DMV，您可以使用類似 Transact-SQL 的語法來查詢結構描述資料列集。 例如，下列查詢傳回相同的結果，但一個是 XML 格式的查詢，一個是表格式查詢。 如需 DMV 的詳細資訊，請參閱[使用動態管理檢視 &#40;DMV&#41; 監視 Analysis Services](use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)。

 DMV，傳回可做為 DMV 的所有結構描述資料列集的清單：

```
SELECT * FROM $system.DISCOVER_SCHEMA_ROWSETS
```

 XMLA 命令，傳回可用結構描述資料列集的清單：

```
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">
<RequestType>DISCOVER_SCHEMA_ROWSETS</RequestType>
    <Restrictions>
<RestrictionList>
</RestrictionList>
</Restrictions>
    <Properties>
<PropertyList>
   </PropertyList>
</Properties>
</Discover>
```

#### <a name="get-a-list-of-data-sources-for-a-tabular-model-using-a-schema-rowset-query"></a>使用結構描述資料列集查詢，取得表格式模型的資料來源清單

1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟包含所要查詢之資料庫的執行個體。 以滑鼠右鍵按一下資料庫圖示，選取 [新增查詢]****，然後選取 [XMLA]****。

    > [!WARNING]
    >  您不能透過變更限制清單或在連接對話方塊中指定資料庫，設定 XMLA 查詢的內容。 您必須從要查詢的資料庫開啟 XMLA 查詢視窗。

2.  開啟範本總管****，並將 [探索結構描述資料列集]**** 範本拖曳至空白查詢視窗中。

3.  在範本中，將[&#40;XMLA&#41;元素的 RequestType 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla)取代為下列文字：`<RequestType>MDSCHEMA_INPUT_DATASOURCES</RequestType>`

4.  按一下 **[執行]** 。

     預期的結果：

    ```
    <CATALOG_NAME>AW Internet Sales Tabular Model_ 24715b71-ea74-4828-aefc-d4c12c15db64</CATALOG_NAME> 
    <DATASOURCE_NAME>SqlServer localhost AdventureWorksDW2012</DATASOURCE_NAME> 
    <DATASOURCE_TYPE>Relational</DATASOURCE_TYPE> 
    <CREATED_ON>2011-10-12T20:27:05.196667</CREATED_ON> 
    <LAST_SCHEMA_UPDATE>2011-10-12T20:27:05.196667</LAST_SCHEMA_UPDATE> 
    <DESCRIPTION /> 
    <TIMEOUT>0</TIMEOUT> 
    <DBMS_NAME>Microsoft SQL Server</DBMS_NAME> 
    <DBMS_VERSION>11.00.1724</DBMS_VERSION>

    ```

##  <a name="analysis-services-template-reference"></a><a name="bkmk_Ref"></a> Analysis Services 範本參考
 下列範本可用於 Analysis Services 資料庫和資料庫物件，包括採礦結構與採礦模型、Cube，以及表格式模型：

|類別|項目範本|Description|
|--------------|-------------------|-----------------|
|DMX\模型內容|內容查詢|示範如何使用 DMX SELECT FROM *\<model>* 。CONTENT 語句，用來抓取所指定之採礦模型的採礦模型架構資料列集內容。|
||連續資料行值|示範如何使用 DMX SELECT DISTINCT FROM *\<model>* 語句及 dmx `RangeMin` 和 `RangeMax` 函數，從指定之採礦模型的連續資料行中，抓取指定範圍內的一組值。|
||離散資料行值|示範如何使用 DMX SELECT DISTINCT FROM 語句， *\<model>* 從指定之模型中的離散資料行取得一組完整的值。|
||鑽研查詢|示範如何搭配 DMX IsInNode 函數使用 DMX SELECT * FROM Model.CASES 陳述式來執行鑽研查詢。|
||模型屬性|示範如何使用 DMX System.GetModelAttributes 函數來傳回模型所用的屬性清單。|
||PMML 內容|示範如何使用 DMX SELECT \* FROM *\<model>* 。PMML 語句，可針對支援這項功能的演算法，取得採礦模型的預測模型標記語言（PMML）標記法。|
|DMX\模型管理|加入模型|示範如何使用 DMX ALTER MINING MODEL STRUCTURE 陳述式來加入採礦模型。|
||清除模型|示範如何使用 DMX DELETE * FROM MINING MODEL 陳述式來刪除指定之採礦模型的內容。|
||清除結構案例|示範如何使用 DMX DELETE FROM MINING STRUCTURE 陳述式來清除採礦模型結構案例。|
||清除結構|示範如何使用 DMX DELETE FROM MINING STRUCTURE 陳述式來清除採礦模型結構。|
||從 PMML 建立|展示如何使用 DMX CREATE MINING MODEL 陳述式和 FROM PMML 子句，從 PMML 表示法建立採礦模型。|
||建立巢狀結構|示範如何搭配巢狀資料行定義清單使用 DMX CREATE MINING STRUCTURE 陳述式來建立含有巢狀資料行的採礦模型。|
||建立結構|示範如何使用 DMX CREATE MINING STRUCTURE 陳述式來建立採礦模型。|
||卸除模型|展示如何使用 DMX DROP MINING MODEL 陳述式，來刪除現有的採礦模型。|
||卸除結構|示範如何使用 DMX DROP MINING STRUCTURE 陳述式來刪除現有的採礦結構。|
||匯出模型|示範如何使用具有 WITH DEPENDENCIES 和 PASSWORD 子句的 DMX EXPORT MINING MODEL 陳述式將採礦模型匯出至檔案，其中包括採礦模型所相依的資料來源和資料來源檢視。|
||匯出結構|示範如何使用具有 WITH DEPENDENCIES 子句的 DMX EXPORT MINING STRUCTURE 陳述式將採礦結構匯出至檔案，其中包括此採礦結構所包含的所有採礦模型，以及此採礦結構所相依的資料來源和資料來源檢視。|
||匯入|示範如何使用具有 WITH PASSWORD 子句的 DMX IMPORT FROM 陳述式來執行匯入。|
||重新命名模型|示範如何使用 DMX RENAME MINING MODEL 陳述式來重新命名現有的採礦模型。|
||重新命名結構|示範如何使用 DMX RENAME MINING STRUCTRE 陳述式來重新命名現有的採礦結構。|
||定型模型|示範如何使用 DMX INSERT INTO MINING MODEL 陳述式來培訓之前已培訓之結構內的採礦模型。|
||培訓巢狀結構|示範如何結合 DMX INSERT INTO MINING STRUCTURE 陳述式和 SHAPE 來源資料查詢，以便培訓含有巢狀資料行的採礦模型，這些資料行中的資料包含利用查詢從現有資料來源擷取的巢狀資料表。|
||培訓結構|示範如何結合 DMX INSERT INTO MINING STRUCTURE 陳述式和 OPENQUERY 來源資料查詢來培訓採礦結構。|
|DMX\預測查詢|基本預測|示範如何結合 DMX SELECT FROM *\<model>* 預測聯結語句和 OPENQUERY 來源資料查詢，使用現有資料來源中的資料（使用查詢來抓取），針對採礦模型執行預測查詢。|
||巢狀預測|示範如何結合 DMX SELECT FROM *\<model>* 預測聯結語句與 SHAPE 和 OPENQUERY 來源資料查詢，使用包含從現有資料來源取得之嵌套資料表的資料，針對該模型執行預測查詢。|
||巢狀單一預測|示範如何使用 DMX SELECT FROM *\<model>* 自然預測聯結子句，以使用單一值（在預測查詢中明確指定）對採礦模型執行預測查詢，其名稱符合採礦模型中的資料行，而且在使用 UNION 語句所建立的嵌套資料表中包含一組值，而該聯集的名稱也與在採礦模型中的嵌套資料行相符。|
||單一預測|示範如何使用 DMX SELECT FROM \<model> 自然預測聯結語句，針對使用單一值（在預測查詢中明確指定）的資料行，在其名稱符合「採礦模型」中資料行的資料行中，針對採礦模型執行預測查詢。|
||預存程序呼叫|示範如何使用 DMX CALL 陳述式來呼叫預存程序。|
|MDX\運算式|移動平均-固定|展示如何使用 MDX `ParallelPeriod` 和 `CurrentMember` 函數搭配自然已排序集合，來建立導出量值，以提供量值在時間維度階層所包含之固定時間週期上的移動平均。|
||移動平均-變動|展示如何在 `CASE` 函數內使用 MDX `Avg` 陳述式，來建立導出量值，以提供量值在時間維度階層所包含之變動時間週期上的移動平均。|
||至今的期間數|展示如何在導出成員中使用 MDX `PeriodsToDate` 函數。|
||對父系的比率|展示如何使用 MDX `Parent` 函數來建立導出量值，該值代表指定階層中父成員之每一個子系的量值比率百分比。|
||對總計的比率|展示如何使用所有成員來建立導出量值，該值代表指定階層中每一個成員的量值比率百分比。|
|MDX\查詢|基本查詢|展示可以用來建構 MDX 查詢的基本 MDX SELECT 陳述式。|
||KPI 查詢|展示如何在 MDX 查詢中使用 MDX `KPIValue` 和 `KPIGoal` 函數，來擷取關鍵效能指標 (KPI) 資訊。|
||子 SELECT 查詢|展示如何建立 MDX SELECT 陳述式，該陳述式會從另一個 SELECT 陳述式所定義的 Subcube 中擷取資訊。|
||使用導出成員|展示如何在 SELECT 陳述式中使用 MDX WITH 子句，來定義 MDX 查詢的導出成員。|
||使用命名集|展示如何在 SELECT 陳述式中使用 MDX WITH 子句，來定義 MDX 查詢的命名集。|
|XMLA\管理|備份|展示如何使用 XMLA `Backup` 命令，將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫備份至檔案。|
||取消|展示如何使用 XMLA `Cancel` 命令，以取消在目前工作階段 (適用於管理員或伺服器管理員以外的使用者)、資料庫 (適用於管理員) 或執行個體 (適用於伺服器管理員) 上所有正在執行的作業。|
||建立遠端資料分割資料庫|展示如何使用 XMLA `Create` 命令和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL) 資料庫元素，來建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫和資料來源以儲存遠端資料分割。|
||刪除|展示如何使用 XMLA `Delete` 命令，來刪除現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。|
||處理維度|展示如何使用 XMLA `Batch` 命令並結合 `Parallel` 元素和 `Process` 命令，使用平行批次作業來更新維度的屬性。|
||處理資料分割|展示如何使用 XMLA `Batch` 命令並結合 `Parallel` 元素和 `Process` 命令，使用平行批次作業來完整處理資料分割。|
||還原|展示如何使用 XMLA `Restore` 命令，從現有的備份檔案還原 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。|
||同步處理|示範如何使用 XMLA `Synchronize` 命令，利用 SynchronizeSecurity 標記的 SkipMembership 選項將另一個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫與目前的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫同步。|
|XMLA\結構描述資料列集|探索結構描述資料列集|展示如何使用 XMLA `Discover` 方法，來擷取 DISCOVER_SCHEMA_ROWSETS 結構描述資料列集的內容。|
|XMLA\伺服器狀態|連接|展示如何使用 XMLA `Discover` 方法，來擷取 DISCOVER_CONNECTIONS 結構描述資料列集的內容。|
||工作|展示如何使用 XMLA `Discover` 方法，來擷取 DISCOVER_JOBS 結構描述資料列集的內容。|
||位置|展示如何使用 XMLA `Discover` 方法，並指定位置備份檔案的路徑，來擷取 DISCOVER_LOCATIONS 結構描述資料列集的內容。|
||鎖定|展示如何使用 XMLA `Discover` 方法，來擷取 DISCOVER_LOCKS 結構描述資料列集的內容。|
||記憶體授權|展示如何使用 XMLA `Discover` 方法，來擷取 DISCOVER_MEMORYGRANT 結構描述資料列集的內容。|
||效能計數器|展示如何使用 XMLA `Discover` 方法，來擷取 DISCOVER_PERFORMANCE_COUNTERS 結構描述資料列集的內容。|
||工作階段|展示如何使用 XMLA `Discover` 方法，來擷取 DISCOVER_SESSIONS 結構描述資料列集的內容。|
||追蹤|展示如何使用 XMLA `Discover` 方法，來擷取 DISCOVER_TRACES 結構描述資料列集的內容。|
||異動|展示如何使用 XMLA `Discover` 方法，來擷取 DISCOVER_TRANSACTIONS 結構描述資料列集的內容。|

## <a name="see-also"></a>另請參閱
 [&#40;MDX 的多維度運算式&#41; 參考](/sql/mdx/multidimensional-expressions-mdx-reference)[資料採礦延伸模組 &#40;DMX&#41; 參考](/sql/dmx/data-mining-extensions-dmx-reference) [Analysis Services 指令碼語言 &#40;ASSL&#41; 參考](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla) [Analysis Services 指令碼語言 &#40;ASSL&#41; 參考](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)


