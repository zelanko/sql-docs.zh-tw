---
title: 執行 SSMA 主控台 (DB2ToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ce63f633-067d-4f04-b8e9-e1abd7ec740b
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 816c37c3ac9c26c80d0f3a95ed27af135b9e874c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="executing-the-ssma-console-db2tosql"></a>執行 SSMA 主控台 (DB2ToSQL)
Microsoft 提供一組強大的指令碼檔案命令來執行及控制 SSMA 活動。 這可確保各節詳細說明相同。 主控台應用程式會使用某些標準的指令碼檔案命令做為列舉這一節。  
  
## <a name="project-script-file-commands"></a>專案的指令碼檔案命令  
建立專案、 開啟、 儲存及結束專案專案的命令控制代碼。  
  
**Command**  
  
建立新專案間的  
  
建立新的 SSMA 專案。  
  
**指令碼**  
  
-   `project-folder` 表示取得建立之專案的資料夾。  
  
-   `project-name` 表示專案的名稱。 {string}  
  
-   `overwrite-if-exists`選擇性屬性會表示是否應該覆寫現有的專案。 {布林值。  
  
-   `project-type:`選擇性屬性。 指出專案類型也就是 「 sql-server 2005 的 「 專案或"sql-server-2008"的專案或 「 sql-server 2012 的 「 專案或 「 sql-server 2014 的 「 專案或"sql azure"。 預設值為"2014-sql-伺服器 」。  
  
**範例：**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014>"   (optional)  
  
/>  
```  
屬性 '覆寫-if-存在' **false**預設。  
  
屬性 '專案型別' **sql server 2008**預設。  
  
**Command**  
  
開啟專案  
  
開啟現有的專案。  
  
**指令碼**  
  
-   `project-folder` 表示取得建立之專案的資料夾。 如果指定的資料夾不存在，則命令會失敗。  {string}  
  
-   `project-name` 表示專案的名稱。 如果指定的專案不存在，則命令會失敗。  {string}  
  
**語法範例：**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
DB2 主控台應用程式的 SSMA 支援回溯相容性。 您可以開啟 建立的前一版的 SSMA 專案。  
  
**Command**  
  
儲存專案  
  
儲存移轉的專案。  
  
**指令碼**  
  
**語法範例：**  
  
```xml  
<save-project/>  
```  
**Command**  
  
關閉專案  
  
關閉移轉專案。  
  
**指令碼**  
  
**語法範例：**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
  
## <a name="database-connection-script-file-commands"></a>資料庫連線指令碼檔案命令  
資料庫連接命令，協助連接至資料庫。  
  
-   **瀏覽**主控台中不支援功能的 ui。  
  
-   如需有關建立指令碼檔的詳細資訊，請參閱[建立指令碼檔&#40;OracleToSQL&#41;](../../ssma/oracle/creating-script-files-oracletosql.md)。  
  
**Command**  
  
connect-source-database  
  
-   執行來源資料庫的連接，並載入高的層級中繼資料的來源資料庫，而非全部的中繼資料。  
  
-   如果無法建立來源的連接，則會產生錯誤並停止進一步執行主控台應用程式。  
  
**指令碼**  
  
從伺服器連線檔案或指令碼檔案的每個連線伺服器區段中定義的名稱屬性，擷取伺服器定義。  
  
**語法範例：**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
force-load-source/target-database  
  
-   載入來源的中繼資料。  
  
-   適用於離線移轉專案。  
  
-   如果無法建立來源/目標的連接，則會產生錯誤並停止進一步執行主控台應用程式。  
  
**指令碼**  
  
需要一或數個 metabase 節點做為命令列參數。  
  
**語法範例：**  
  
```xml  
<force-load object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
或  
  
```xml  
<force-load>  
  
   <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Command**  
  
reconnect-source-database  
  
-   重新連線到來源資料庫，但不會載入與不同的是連接來源資料庫命令的任何中繼資料。  
  
-   如果 (re) 與來源的連接無法建立，則會產生錯誤，主控台應用程式會停止進一步執行。  
  
**指令碼**  
  
**語法範例：**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
連接目標資料庫  
  
-   連接到目標 SQL Server 資料庫，並完全載入目標資料庫的高的層級中繼資料，但不是中繼資料。  
  
-   如果無法連線到目標，則會產生錯誤，主控台應用程式會停止進一步執行。  
  
**指令碼**  
  
伺服器定義會從伺服器連線檔案或指令碼檔案的每個連線伺服器區段中定義的名稱屬性  
  
**語法範例：**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
reconnect-target-database  
  
-   重新連線到目標資料庫，但不會載入任何中繼資料，不同於連接目標資料庫命令。  
  
-   （重新） 連線至目標無法建立，則會產生錯誤，主控台應用程式會停止進一步執行。  
  
**指令碼**  
  
**語法範例：**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>報表指令碼檔案命令  
報表命令產生各種 SSMA 主控台活動的效能上的報表。  
  
**Command**  
  
generate-assessment-report  
  
-   產生的來源資料庫上的評估報告。  
  
-   如果來源資料庫連接不會再執行此命令執行，則會產生錯誤，並在主控台應用程式結束。  
  
-   無法連線至來源資料庫伺服器，在命令執行時，也會產生結束主控台應用程式中。  
  
**指令碼**  
  
-   `conversion-report-folder:` 指定評估報表可以儲存在其中的資料夾。（選擇性的屬性）  
  
-   `object-name:` 指定評估報表產生 （可以有 indivdual 物件名稱或群組的物件名稱） 被視為物件。  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果指定物件類別，則物件類型將會是 「 類別目錄 」） 的物件類型。  
  
-   `conversion-report-overwrite:` 指定是否要覆寫評估報表資料夾已經存在。  
  
    **預設值：** false。 （選擇性的屬性）  
  
-   `write-summary-report-to:` 指定產生的摘要報告所在的路徑。  
  
    如果只提及的資料夾路徑，然後檔案名稱**AssessmentReport&lt;n&gt;。XML**建立。 （選擇性的屬性）  
  
    報表建立具有兩個其他的子類別：  
  
    -   `report-errors` （="true/false"，預設值為"false"（選擇性的屬性））  
  
    -   `verbose` （="true/false"，預設值為"false"（選擇性的屬性））  
  
**語法範例：**  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   assessment-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
或  
  
```xml  
<generate-assessment-report  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
>  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>移轉指令碼檔案命令  
移轉命令來源結構描述轉換成目標資料庫結構描述，並將資料移轉到目標伺服器。 預設的主控台輸出設定移轉命令是 'Full' 輸出報表不報告詳細的錯誤： 只有摘要的來源物件樹狀結構根節點。  
  
**Command**  
  
convert-schema  
  
-   執行從來源到目標結構描述的結構描述轉換。  
  
-   如果來源或目標資料庫的連接不會再執行此命令執行或在命令執行期間的來源或目標資料庫伺服器的連線失敗，則會產生錯誤，則主控台應用程式結束。  
  
**指令碼**  
  
-   `conversion-report-folder:` 指定評估報表可以儲存在其中的資料夾。（選擇性的屬性）  
  
-   `object-name:` 指定來源物件視為轉換結構描述 （可能有 indivdual 物件名稱或群組的物件名稱）。  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果指定物件類別，則物件類型將會是 「 類別目錄 」） 的物件類型。  
  
-   `conversion-report-overwrite:` 指定是否要覆寫評估報表資料夾已經存在。  
  
    **預設值：** false。 （選擇性的屬性）  
  
-   `write-summary-report-to:` 指定產生的摘要報告所在的路徑。  
  
    如果只提及的資料夾路徑，然後檔案名稱**SchemaConversionReport&lt;n&gt;。XML**建立。 （選擇性的屬性）  
  
    報表建立具有兩個其他的子類別：  
  
    -   `report-errors` （="true/false"，預設值為"false"（選擇性的屬性））  
  
    -   `verbose` （="true/false"，預設值為"false"（選擇性的屬性））  
  
**語法範例：**  
  
```xml  
<convert-schema  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
或  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Command**  
  
資料移轉： 移轉至目標的來源資料。  
  
**指令碼**  
  
-   `conversion-report-folder:` 指定評估報表可以儲存在其中的資料夾。（選擇性的屬性）  
  
-   `object-name:` 指定來源物件視為移轉 （可能有 indivdual 物件名稱或群組的物件名稱） 的資料。  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果指定物件類別，則物件類型將會是 「 類別目錄 」） 的物件類型。  
  
-   `conversion-report-overwrite:` 指定是否要覆寫評估報表資料夾已經存在。  
  
    **預設值：** false。 （選擇性的屬性）  
  
-   `write-summary-report-to:` 指定產生的摘要報告所在的路徑。  
  
    如果只提及的資料夾路徑，然後檔案名稱**DataMigrationReport&lt;n&gt;。XML**建立。 （選擇性的屬性）  
  
    報表建立具有兩個其他的子類別：  
  
    -   `report-errors` （="true/false"，預設值為"false"（選擇性的屬性））  
  
    -   `verbose` （="true/false"，預設值為"false"（選擇性的屬性））  
  
**語法範例：**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>">  
  
      <metabase-object object-name="<object-name>"/>  
  
      <metabase-object object-name="<object-name>"/>  
  
      <metabase-object object-name="<object-name>"/>  
  
      <data-migration-connection  
  
         source-use-last-used="true"/source-server="<server-unique-name>"  
  
         target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
或  
  
```xml  
<migrate-data  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>移轉準備指令碼檔案命令  
開始結構描述對應來源和目標資料庫之間的移轉準備命令。  
  
**Command**  
  
對應結構描述  
  
目標結構描述的來源資料庫的結構描述對應。  
  
**指令碼**  
  
-   `source-schema` 指定我們想要移轉的來源結構描述。  
  
-   `sql-server-schema` 指定我們想要移轉的目標結構描述。  
  
**語法範例：**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
**Command**  
  
對應結構描述  
  
目標結構描述的來源資料庫的結構描述對應。  
  
**指令碼**  
  
`source-schema` 指定我們想要移轉的來源結構描述。  
  
`sql-server-schema` 指定我們想要移轉的目標結構描述。  
  
**語法範例：**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>管理性指令碼檔案命令  
管理性命令可以幫助與來源資料庫同步處理目標資料庫物件。  
  
預設的主控台輸出設定移轉命令是 'Full' 輸出報表不報告詳細的錯誤： 只有摘要的來源物件樹狀結構根節點。  
  
**Command**  
  
同步處理目標  
  
-   目標物件會同步處理目標資料庫。  
  
-   如果針對來源資料庫執行此命令時，發生錯誤。  
  
-   如果目標資料庫連接不會再執行此命令執行，或在目標資料庫伺服器的連線失敗命令執行期間，會產生錯誤，則主控台應用程式結束。  
  
**指令碼**  
  
-   `object-name:` 指定同步處理目標資料庫 （可以有 indivdual 物件名稱或群組的物件名稱） 被視為目標物件。  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果指定物件類別，則物件類型將會是 「 類別目錄 」） 的物件類型。  
  
-   `on-error:` 指定是否要指定同步處理錯誤視為警告或錯誤。 在錯誤的可用選項：  
  
    -   報表-總計-為-警告  
  
    -   報表-每個-為-警告  
  
    -   失敗指令碼  
  
-   `report-errors-to:` 同步處理作業 （選擇性的屬性） 如果只指定資料夾路徑，然後檔案依名稱指定的錯誤報表位置**TargetSynchronizationReport.XML**建立。  
  
**語法範例：**  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
/>  
```  
或  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
或  
  
```xml  
<synchronize-target>  
  
   <metabase-object object-name="<object-name>"/>  
  
   <metabase-object object-name="<object-name>"/>  
  
   <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
**Command**  
  
從資料庫重新整理  
  
-   重新整理資料庫中的來源物件。  
  
-   如果針對目標資料庫執行此命令時，會產生錯誤。  
  
**指令碼**  
  
需要一或數個 metabase 節點做為命令列參數。  
  
-   `object-name:` 指定來源物件視為重新整理從來源資料庫 （可以有 indivdual 物件名稱或群組的物件名稱）。  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果指定物件類別，則物件類型將會是 「 類別目錄 」） 的物件類型。  
  
-   `on-error:` 指定是否要指定重新整理錯誤視為警告或錯誤。 在錯誤的可用選項：  
  
    -   報表-總計-為-警告  
  
    -   報表-每個-為-警告  
  
    -   失敗指令碼  
  
-   `report-errors-to:` 重新整理作業 （選擇性的屬性） 如果只指定資料夾路徑，然後檔案依名稱指定的錯誤報表位置**SourceDBRefreshReport.XML**建立。  
  
**語法範例：**  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
/>  
```  
或  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
或  
  
```xml  
<refresh-from-database>  
  
   <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>指令碼產生指令碼檔案命令  
產生指令碼命令執行雙重工作： 它們協助節省主控台輸出在指令碼檔案中;並記錄 T-SQL 輸出到主控台或檔案，根據您指定的參數。  
  
**Command**  
  
save-as-script  
  
用來將物件的指令碼儲存至檔案，當提到 metabase = 目標，這是同步處理命令，在我們取得的指令碼並在目標資料庫上執行相同的替代方式。  
  
**指令碼**  
  
需要一或數個 metabase 節點做為命令列參數。  
  
-   `object-name:` 指定的指令碼要儲存的物件。 （可以有個別的物件名稱或群組的物件名稱）  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果指定物件類別，則物件類型將會是 「 類別目錄 」） 的物件類型。  
  
-   `metabase:` 指定是否在來源或目標 metabase。  
  
-   `destination:` 指定的路徑或指令碼之儲存，如果檔案名稱中未指定然後檔案名稱格式 （object_name 屬性值）.out 的資料夾  
  
-   `overwrite:` 如果為 true 然後它會覆寫相同的檔案名稱。 它可以包含值 (true/false)。  
  
**語法範例：**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file/folder>"  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
或  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file/folder>"  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Command**  
  
convert-sql-statement  
  
-   `context` 指定的結構描述名稱。  
  
-   `destination` 指定是否要將輸出儲存在檔案中。  
  
    如果未指定此屬性，則已轉換的 T-SQL 陳述式會顯示在主控台上。 （選擇性的屬性）  
  
-   `conversion-report-folder` 指定評估報表可以儲存在其中的資料夾。（選擇性的屬性）  
  
-   `conversion-report-overwrite` 指定是否要覆寫評估報表資料夾已經存在。  
  
    **預設值：** false。 （選擇性的屬性）  
  
-   `write-converted-sql-to` 指定的檔案 （或） 儲存已轉換的 T-SQL 的資料夾路徑。 與指定的資料夾路徑時`sql-files`屬性，每個來源檔案將會有對應的目標 T-SQL 檔案的指定資料夾底下建立。 與指定的資料夾路徑時`sql`屬性，名為的檔案寫入已轉換的 T-SQL **Result.out**底下指定的資料夾。  
  
-   `sql` 指定要轉換的 DB2 sql 陳述式可以分隔一或多個陳述式，使用";"  
  
-   `sql-files` 指定已轉換成 T-SQL 程式碼的 sql 檔案的路徑。  
  
-   `write-summary-report-to` 指定要產生報表的路徑。 如果只提及的資料夾路徑，然後檔案名稱**ConvertSQLReport.XML**建立。 （選擇性的屬性）  
  
    報表建立了 2 子類別，取得進一步的 viz..,:  
  
    -   報告錯誤 （="true/false"，預設值為"false"（選擇性的屬性））。  
  
    -   詳細資訊 （="true/false"，預設值為"false"（選擇性的屬性））。  
  
**指令碼**  
  
需要一或數個 metabase 節點做為命令列參數。  
  
**語法範例：**  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   file-name="<file-name>"  
  
   sql="SELECT 1 FROM DUAL;">  
  
   <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
或  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>" (optional)  
  
   verbose="<true/false>" (optional)  
  
   report-errors="<true/false>"  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
或  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
  
## <a name="next-step"></a>下一個步驟  
如需命令列選項的資訊，請參閱[SSMA 主控台中的命令列選項&#40;DB2ToSQL&#41; ](../../ssma/db2/command-line-options-in-ssma-console-db2tosql.md) 。  
  
如需範例主控台指令碼檔案的資訊，請參閱[使用範例主控台指令碼檔案&#40;DB2ToSQL&#41;](../../ssma/db2/working-with-the-sample-console-script-files-db2tosql.md)  
  
下一個步驟取決於您的專案需求：  
  
-   指定的密碼或匯出 / 匯入的密碼，請參閱[管理密碼&#40;DB2ToSQL&#41;](../../ssma/db2/managing-passwords-db2tosql.md)。  
  
-   產生報告，請參閱[產生報表&#40;DB2ToSQL&#41;](../../ssma/db2/generating-reports-db2tosql.md)。  
  
-   如需疑難排解主控台中的問題，請參閱[疑難排解&#40;DB2ToSQL&#41;](../../ssma/db2/troubleshooting-db2tosql.md)。  
  
