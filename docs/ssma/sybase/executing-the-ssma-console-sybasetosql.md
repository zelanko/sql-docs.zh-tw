---
title: "執行 SSMA 主控台 (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Database Connection Commands
- Sybase Console,Manageability Commands
- Sybase Console,Migration Commands
- Sybase Console,Migration Preparation Command
- Sybase Console,Project Commands
- Sybase Console,Report Commands
- Sybase Console,Script File Commands
- Sybase Console,Script Generation Commands
ms.assetid: ea8950b7-fabc-4aa4-89f8-9573a2617d70
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0df634087870db32ed0357c97b1211d4fc1ddcba
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="executing-the-ssma-console-sybasetosql"></a>執行 SSMA 主控台 (SybaseToSQL)
Microsoft 提供一組強大的指令碼檔案命令來執行及控制 SSMA 活動。 這可確保各節詳細說明相同。  
  
## <a name="script-file-commands"></a>指令碼檔案命令  
主控台應用程式會使用某些標準的指令碼檔案命令做為列舉這一節。  
  
## <a name="project-commands"></a>專案命令  
建立專案、 開啟、 儲存及結束專案專案的命令控制代碼。  
  
### <a name="create-new-project"></a>建立新專案間的  
建立新的 SSMA 專案  
  
-   `project-folder`表示取得建立之專案的資料夾。  
  
-   `project-name`表示專案的名稱。 {string}  
  
-   `overwrite-if-exists`選擇性屬性會表示是否應該覆寫現有的專案。 {布林值。  
  
-   `project-type:`選擇性屬性。 指出專案類型也就是 「 sql-server 2005 的 「 專案或"sql-server-2008"專案或 「 sql-server 2012 的 「 專案或 「 sql-server 2014 的 「 專案或"sql azure"專案。 預設值為"sql-server-2008"。  
  
**範例：**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>" (optional)  
  
   project-type=”<sql-server-2008/sql-server-2005/sql-server-2012/sql-server-2014/sql-azure>”  
/>  
```  
屬性 '覆寫-if-存在' **false**預設。  
  
屬性 '專案型別' **sql server 2008**預設。  
  
### <a name="open-project"></a>開啟專案  
  
-   `project-folder`表示取得建立之專案的資料夾。 如果指定的資料夾不存在，則命令會失敗。  {string}  
  
-   `project-name`表示專案的名稱。 如果指定的專案不存在，則命令會失敗。  {string}  
  
**語法範例：**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> SSMA for Sybase 主控台應用程式支援回溯相容性。 您可以開啟 建立的前一版的 SSMA 專案。  
  
### <a name="save-project"></a>儲存專案  
儲存移轉專案  
  
**語法範例：**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>關閉專案  
關閉移轉專案  
  
**語法範例：**  
  
```xml  
<close-project   
  if-modified="<save/error/ignore>"   (optional)  
/>  
```  
「 如果修改 ' 屬性是選擇性的**忽略**預設。  
  
## <a name="database-connection-commands"></a>資料庫連線命令  
資料庫連接命令，協助連接至資料庫。  
  
> [!NOTE]  
> 1.  **瀏覽**主控台中不支援功能的 ui。  
> 2.  如需有關建立指令碼檔的詳細資訊，請參閱[建立指令碼檔案 &#40;SybaseToSQL &#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
### <a name="connect-source-database"></a>連接來源資料庫  
  
-   執行來源資料庫的連接，並載入高的層級中繼資料的來源資料庫，而非全部的中繼資料。  
  
-   如果無法建立來源的連接，則會產生錯誤並停止進一步執行主控台應用程式。  
  
從伺服器連線檔案或指令碼檔案的每個連線伺服器區段中定義的名稱屬性，擷取伺服器定義。  
  
**語法範例：**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>強制載入-來源/目標的資料庫  
  
-   載入來源的中繼資料。  
  
-   適用於離線移轉專案。  
  
-   如果無法建立來源/目標的連接，則會產生錯誤並停止進一步執行主控台應用程式。  
  
需要一或數個 metabase 節點做為命令列參數。  
  
**語法範例：**  
  
```xml  
<force-load metabase=”<source/target>” >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>重新連接來源資料庫  
  
-   重新連線到來源資料庫，但不會載入與不同的是連接來源資料庫命令的任何中繼資料。  
  
-   如果 (re) 與來源的連接無法建立，則會產生錯誤，主控台應用程式會停止進一步執行。  
  
**語法範例：**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>連接目標資料庫  
  
-   連接到目標 SQL Server 資料庫，並完全載入目標資料庫的高的層級中繼資料，但不是中繼資料。  
  
-   如果無法連線到目標，則會產生錯誤，主控台應用程式會停止進一步執行。  
  
伺服器定義會從伺服器連線檔案或指令碼檔案的每個連線伺服器區段中定義的名稱屬性  
  
**語法範例：**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>重新連線目標資料庫  
  
-   重新連線到目標資料庫，但不會載入任何中繼資料，不同於連接目標資料庫命令。  
  
-   （重新） 連線至目標無法建立，則會產生錯誤，主控台應用程式會停止進一步執行。  
  
**語法範例：**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>報表命令  
報表命令產生各種 SSMA 主控台活動的效能上的報表。  
  
### <a name="generate-assessment-report"></a>產生評估報告  
  
-   產生的來源資料庫上的評估報告。  
  
-   如果來源資料庫連接不會再執行此命令執行，則會產生錯誤，並在主控台應用程式結束。  
  
-   無法連線至來源資料庫伺服器，在命令執行時，也會產生結束主控台應用程式中。  
  
-   `conversion-report-folder:`指定評估報表可以儲存在其中的資料夾。（選擇性的屬性）  
  
-   `object-name:`指定評估報表產生 （可以有 indivdual 物件名稱或群組的物件名稱） 被視為物件。  
  
-   `object-type:`指定的屬性中指定的物件名稱 （如果指定物件類別，則物件類型將會是 「 類別目錄 」） 的物件類型。  
  
-   `conversion-report-overwrite:`指定是否要覆寫評估報表資料夾已經存在。  
  
    **預設值：** false。 （選擇性的屬性）  
  
-   `write-summary-report-to:`指定要產生報表的路徑。  
  
    如果只提及的資料夾路徑，然後檔案名稱**AssessmentReport&lt;n&gt;。XML**建立。 （選擇性的屬性）  
  
    報表建立具有兩個其他的子類別：  
  
    -   `report-errors`（="true/false"，預設值為"false"（選擇性的屬性））  
  
    -   `verbose`（="true/false"，預設值為"false"（選擇性的屬性））  
  
**語法範例：**  
  
```xml  
<generate-assessment-report  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>”             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  assessment-report-folder="<folder-name>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
或  
  
```xml  
<generate-assessment-report  
  
  assessment-report-folder="<folder-name>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
<metabase-object object-name="<object-name>"  
  
        object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-commands"></a>移轉命令  
移轉命令來源結構描述轉換成目標資料庫結構描述，並將資料移轉到目標伺服器。  
  
### <a name="convert-schema"></a>轉換結構描述  
  
-   執行從來源到目標結構描述的結構描述轉換。  
  
-   如果來源或目標資料庫的連接不會再執行此命令執行或在命令執行期間的來源或目標資料庫伺服器的連線失敗，則會產生錯誤，則主控台應用程式結束。  
  
-   `conversion-report-folder:`指定評估報表可以儲存在其中的資料夾。（選擇性的屬性）  
  
-   `object-name:`指定來源物件視為轉換結構描述 （可能有 indivdual 物件名稱或群組的物件名稱）。  
  
-   `object-type:`指定的屬性中指定的物件名稱 （如果指定物件類別，則物件類型將會是 「 類別目錄 」） 的物件類型。  
  
-   `conversion-report-overwrite:`指定是否要覆寫評估報表資料夾已經存在。  
  
    **預設值：** false。 （選擇性的屬性）  
  
-   `write-summary-report-to:`指定產生的摘要報告所在的路徑。  
  
    如果只提及的資料夾路徑，然後檔案名稱**SchemaConversionReport&lt;n&gt;。XML**建立。 （選擇性的屬性）  
  
    報表建立具有兩個其他的子類別：  
  
    -   `report-errors`（="true/false"，預設值為"false"（選擇性的屬性））  
  
    -   `verbose`（="true/false"，預設值為"false"（選擇性的屬性））  
  
**語法範例：**  
  
```xml  
<convert-schema  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  write-summary-report-to="<file-name/folder-name>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder-name>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
或  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder-name>"         (optional)  
  
  conversion-report-overwrite="<true/false>"> (optional)  
  
  <metabase-object object-name="<object-name>"  
  
    object-type="<object-category>"/>  
  
</convert-schema>  
```  
  
### <a name="migrate-data"></a>移轉資料  
將來源資料移轉到目標。  
  
-   `object-name:`指定來源物件視為移轉 （可能有 indivdual 物件名稱或群組的物件名稱） 的資料。  
  
-   `object-type:`指定的屬性中指定的物件名稱 （如果指定物件類別，則物件類型將會是 「 類別目錄 」） 的物件類型。  
  
-   `write-summary-report-to:`指定要產生報表的路徑。  
  
    如果只提及的資料夾路徑，然後檔案名稱**DataMigrationReport&lt;n&gt;。XML**建立。 （選擇性的屬性）  
  
    報表建立具有兩個其他的子類別：  
  
    -   `report-errors`（="true/false"，預設值為"false"（選擇性的屬性））  
  
    -   `verbose`（="true/false"，預設值為"false"（選擇性的屬性））  
  
**語法範例：**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>">  
  
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
  
  report-errors="<true/false>" verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-command"></a>移轉準備命令  
開始結構描述對應來源和目標資料庫之間的移轉準備命令。  
  
> [!NOTE]  
> 預設的主控台輸出設定移轉命令是 'Full' 輸出報表不報告詳細的錯誤： 只有摘要的來源物件樹狀結構根節點。  
  
### <a name="map-schema"></a>對應結構描述  
目標結構描述的來源資料庫的結構描述對應。  
  
-   `source-schema`指定我們想要移轉的來源結構描述。  
  
-   `sql-server-schema`指定我們想要移轉的目標結構描述。  
  
**語法範例：**  
  
```xml  
<map-schema source-schema="<source-schema>"  
  
sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-commands"></a>管理性命令  
管理性命令可以幫助與來源資料庫同步處理目標資料庫物件。  
  
> [!NOTE]  
> 預設的主控台輸出設定移轉命令是 'Full' 輸出報表不報告詳細的錯誤： 只有摘要的來源物件樹狀結構根節點。  
  
### <a name="synchronize-target"></a>同步處理目標  
  
-   目標物件會同步處理目標資料庫。  
  
-   如果針對來源資料庫執行此命令時，發生錯誤。  
  
-   如果目標資料庫連接不會再執行此命令執行，或在目標資料庫伺服器的連線失敗命令執行期間，會產生錯誤，則主控台應用程式結束。  
  
-   `object-name:`指定同步處理目標資料庫 （可以有 indivdual 物件名稱或群組的物件名稱） 被視為目標物件。  
  
-   `object-type:`指定的屬性中指定的物件名稱 （如果指定物件類別，則物件類型將會是 「 類別目錄 」） 的物件類型。  
  
-   `on-error:`指定是否要指定同步處理錯誤視為警告或錯誤。 在錯誤的可用選項：  
  
    -   報表-總計-為-警告  
  
    -   報表-每個-為-警告  
  
    -   失敗指令碼  
  
-   `report-errors-to:`同步處理作業 （選擇性的屬性） 如果只指定資料夾路徑，然後檔案依名稱指定的錯誤報表位置**TargetSynchronizationReport.XML**建立。  
  
**語法範例：**  
  
```xml  
<synchronize-target  
  
object-name="<object-name>"  
  
on-error="<report-total-as-warning/  
  
report-each-as-warning/  
  
fail-script>" (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
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
  
### <a name="refresh-from-database"></a>從資料庫重新整理  
  
-   重新整理資料庫中的來源物件。  
  
-   如果針對目標資料庫執行此命令時，會產生錯誤。  
  
需要一或數個 metabase 節點做為命令列參數。  
  
-   `object-name:`指定來源物件視為重新整理從來源資料庫 （可以有 indivdual 物件名稱或群組的物件名稱）。  
  
-   `object-type:`指定的屬性中指定的物件名稱 （如果指定物件類別，則物件類型將會是 「 類別目錄 」） 的物件類型。  
  
-   `on-error:`指定是否要指定重新整理錯誤視為警告或錯誤。 在錯誤的可用選項：  
  
    -   報表-總計-為-警告  
  
    -   報表-每個-為-警告  
  
    -   失敗指令碼  
  
-   `report-errors-to:`重新整理作業 （選擇性的屬性） 如果只指定資料夾路徑，然後檔案依名稱指定的錯誤報表位置**SourceDBRefreshReport.XML**建立。  
  
**語法範例：**  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  on-error="<report-total-as-warning/  
  
             report-each-as-warning/  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
或  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  object-type="<object-category>" />  
```  
或  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-commands"></a>指令碼產生命令  
產生指令碼命令執行雙重工作： 它們協助節省主控台輸出在指令碼檔案中;並記錄 T-SQL 輸出到主控台或檔案，根據您指定的參數。  
  
### <a name="save-as-script"></a>儲存為指令碼  
用來將物件的指令碼儲存至檔案，當提到 metabase = 目標，這是同步處理命令，在我們取得的指令碼並在目標資料庫上執行相同的替代方式。  
  
需要一或數個 metabase 節點做為命令列參數。  
  
-   `object-name:`指定的指令碼要儲存的物件。 （可以有 indivdual 物件名稱或群組的物件名稱）  
  
-   `object-type:`指定的屬性中指定的物件名稱 （如果指定物件類別，則物件類型將會是 「 類別目錄 」） 的物件類型。  
  
-   `metabase:`指定是否它 ithe 來源或目標 metabase。  
  
-   `destination:`指定的路徑或指令碼之儲存，如果檔案名稱中未指定然後檔案名稱格式 （object_name 屬性值）.out 的資料夾  
  
-   `overwrite:`如果為 true 然後它會覆寫相同的檔案名稱。 它可以包含值 (true/false)。  
  
**語法範例：**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  destination="<file-name/folder-name>"  
  
  overwrite="<true/false>"   (optional)  
  
/>  
```  
或  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file-name/folder-name>"  
  
    <metabase-object object-name="<object-name>"  
  
                     object-type="<object-category>"/>  
  
</save-as-script>  
```  
  
### <a name="convert-sql-statement"></a>轉換 sql 陳述式  
  
-   `context`指定的結構描述名稱。  
  
-   `destination`指定是否要將輸出儲存在檔案中。  
  
    如果未指定此屬性，則已轉換的 T-SQL 陳述式會顯示在主控台上。 （選擇性的屬性）  
  
-   `conversion-report-folder`指定評估報表可以儲存在其中的資料夾。（選擇性的屬性）  
  
-   `conversion-report-overwrite`指定是否要覆寫評估報表資料夾已經存在。  
  
    **預設值：** false。 （選擇性的屬性）  
  
-   `write-converted-sql-to`指定的檔案 （或） 儲存已轉換的 T-SQL 的資料夾路徑。 與指定的資料夾路徑時`sql-files`屬性，每個來源檔案將會有對應的目標 T-SQL 檔案的指定資料夾底下建立。 與指定的資料夾路徑時`sql`屬性，已轉換的 T-SQL 寫入 Result.out 為指定的資料夾下的檔案。  
  
-   `sql`指定要轉換一或多個陳述式的 Sybase sql 陳述式可以分隔使用";"  
  
-   `sql-files`指定已轉換成 T-SQL 程式碼的 sql 檔案的路徑。  
  
-   `write-summary-report-to`指定產生的摘要報告所在的路徑。 如果只提及的資料夾路徑，然後檔案名稱**ConvertSQLReport.XML**建立。 （選擇性的屬性）  
  
    建立具有子類別，取得進一步的 viz 2 的摘要報告..,:  
  
    -   報告錯誤 （="true/false"，預設值為"false"（選擇性的屬性））。  
  
    -   詳細資訊 （="true/false"，預設值為"false"（選擇性的屬性））。  
  
需要一或數個 metabase 節點做為命令列參數。  
  
**語法範例：**  
  
```  
<convert-sql-statement  
  
       context="<database-name>.<schema-name>"  
  
        conversion-report-folder="<folder-name>"  
  
        conversion-report-overwrite="<true/false>"  
  
        write-summary-report-to="<file-name/folder-name>"   (optional)  
  
        verbose="<true/false>"   (optional)  
  
        report-errors="<true/false>"   (optional)  
  
        destination="<stdout/file>"   (optional)  
  
        write-converted-sql-to ="<file-name/folder-name>"  
  
        sql="SELECT 1 FROM DUAL;">  
  
    <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
或  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         write-summary-report-to="<file-name/folder-name>"   (optional)  
  
         verbose="<true/false>"   (optional)  
  
         report-errors="<true/false>"   (optional)  
  
         destination="<stdout/file>"   (optional)  
  
         write-converted-sql-to ="<file-name/folder-name>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
或  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-step"></a>下一個步驟  
如需命令列選項的資訊，請參閱[SSMA 主控台 &#40; 中的命令列選項SybaseToSQL &#41;](../../ssma/sybase/command-line-options-in-ssma-console-sybasetosql.md) .  
  
如需範例主控台指令碼檔案的資訊，請參閱[使用範例主控台指令碼檔案 &#40;SybaseToSQL &#41;](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)  
  
下一個步驟取決於您的專案需求：  
  
-   指定的密碼或匯出 / 匯入的密碼，請參閱[管理密碼 &#40;SybaseToSQL &#41;](../../ssma/sybase/managing-passwords-sybasetosql.md).  
  
-   產生報告，請參閱[產生報表 &#40;SybaseToSQL &#41;](../../ssma/sybase/generating-reports-sybasetosql.md).  
  
-   如需疑難排解主控台中的問題，請參閱[疑難排解 &#40;SybaseToSQL &#41;](../../ssma/sybase/troubleshooting-sybasetosql.md).  
  

