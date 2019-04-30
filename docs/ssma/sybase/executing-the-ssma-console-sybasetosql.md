---
title: 執行 SSMA 主控台 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6cbdd0a1394114e3fdef0511c7ed14658f7dd9b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126301"
---
# <a name="executing-the-ssma-console-sybasetosql"></a>執行 SSMA 主控台 (SybaseToSQL)
Microsoft 提供您使用一組強大的指令碼檔案命令來執行及控制 SSMA 活動。 後續章節將詳細說明相同。  
  
## <a name="script-file-commands"></a>指令碼檔案命令  
主控台應用程式會使用某些標準的指令碼檔命令為列舉這一節。  
  
## <a name="project-commands"></a>專案命令  
建立專案、 開啟、 儲存及結束專案的專案的命令控制代碼。  
  
### <a name="create-new-project"></a>create-new-project  
此命令會建立新的 SSMA 專案。  
  
-   `project-folder` 表示取得建立之專案的資料夾。  
  
-   `project-name` 表示專案的名稱。 {string}  
  
-   `overwrite-if-exists`選擇性的屬性會指出是否應該覆寫現有的專案。 {布林值}  
  
-   `project-type:`選擇性屬性。 表示專案類型，「 sql-server 2005 的 「 專案或 「 sql-server 2008 的 「 專案或 「 sql-server 2012 的 「 專案或 「 sql-server 2014 的 「 專案或 [sql azure] 專案。 預設值是 「 sql server-2008 年。 」  
  
**語法範例：**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>" (optional)  
  
   project-type="<sql-server-2008/sql-server-2005/sql-server-2012/sql-server-2014/sql-azure>"  
/>  
```  
' 覆寫-if-exists' 屬性是**false**預設。  
  
[專案類型] 屬性是**sql server 2008**預設。  
  
### <a name="open-project"></a>開啟專案  
此命令會開啟專案。

-   `project-folder` 表示取得建立之專案的資料夾。 如果指定的資料夾不存在，則命令會失敗。  {string}  
  
-   `project-name` 表示專案的名稱。 如果指定的專案不存在，則命令會失敗。  {string}  
  
**語法範例：**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> SSMA for SAP ASE 主控台應用程式支援回溯相容性。 您可以使用它來開啟 建立的前一版的 SSMA 專案。  
  
### <a name="save-project"></a>save-project  
此命令會將儲存移轉專案。  
  
**語法範例：**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>關閉專案  
此命令會關閉移轉專案。  
  
**語法範例：**  
  
```xml  
<close-project   
  if-modified="<save/error/ignore>"   (optional)  
/>  
```  
「 如果修改 」 的屬性是選擇性的**忽略**預設。  
  
## <a name="database-connection-commands"></a>資料庫連線命令  
資料庫連接命令可以幫助連接到資料庫。  
  
> [!NOTE]  
> - **瀏覽**主控台中不支援的 ui 功能。  
> - 如需有關建立指令碼檔的詳細資訊，請參閱[建立指令碼檔案&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md)。  
  
### <a name="connect-source-database"></a>connect-source-database  
此命令會執行來源資料庫的連接，並載入高層級的中繼資料的來源資料庫，而非全部的中繼資料。
  
如果無法建立來源的連接，則會產生錯誤和主控台應用程式會停止進一步執行。
  
從伺服器連線檔案或指令碼檔案的每個連線伺服器一節中所定義的名稱屬性，擷取伺服器定義。  
  
**語法範例：**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>force-load-source/target-database  
此命令會載入來源的中繼資料，且有助於處理離線移轉專案。  
  
如果無法建立來源/目標的連線，則會產生錯誤和主控台應用程式會停止進一步執行。  
  
此命令需要一個或多個的 metabase 節點做為命令列參數。  
  
**語法範例：**  
  
```xml  
<force-load metabase="<source/target>" >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>reconnect-source-database  
此命令會重新連線至來源資料庫，但不會載入與連接來源資料庫命令的任何中繼資料。  
  
如果 （重新） 與來源的連接無法建立，則會產生錯誤和主控台應用程式會停止進一步執行。  
  
**語法範例：**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>connect-target-database  
此命令會連線到目標 SQL Server 資料庫，並完全載入目標資料庫的高層級的中繼資料，但不是中繼資料。  
  
如果無法連線到目標，則會產生錯誤和主控台應用程式會停止進一步執行。  
  
從伺服器連線檔案或指令碼檔案的每個連線伺服器一節中所定義的名稱屬性，擷取伺服器定義。  
  
**語法範例：**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>reconnect-target-database  
  
此命令會重新連線到目標資料庫，但不會載入任何中繼資料，不同於連接目標資料庫命令。  
  
如果 （重新） 連線到目標不能建立，則會產生錯誤和主控台應用程式會停止進一步執行。  
  
**語法範例：**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>報表命令  
報表命令產生的各種 SSMA 主控台活動效能的報告。  
  
### <a name="generate-assessment-report"></a>generate-assessment-report  
  
此命令會產生來源資料庫上的評估報告。  
  
如果執行此命令會產生錯誤，並在主控台應用程式結束之前，不會執行來源資料庫連接。  
  
無法連線至來源資料庫伺服器在命令執行時，也會導致終止的主控台應用程式。  
  
-   `conversion-report-folder:` 指定可以儲存評定報表的資料夾。 （選擇性屬性）  
  
-   `object-name:` 指定考慮用於評估報表產生 （支援個別的物件名稱或群組物件名稱） 的物件。  
  
-   `object-type:` 指定物件中所呼叫的物件名稱屬性 （如果已指定物件類別，則物件類型會是 「 類別 」） 的類型。  
  
-   `conversion-report-overwrite:` 指定是否要覆寫評估報告資料夾，如果已經存在。  
  
    **預設值：** ，則為 false。 （選擇性屬性）  
  
-   `write-summary-report-to:` 指定將產生報告的路徑。  
  
    如果只提及，資料夾路徑，然後檔案名稱**AssessmentReport&lt;n&gt;。XML**建立。 （選擇性屬性）  
  
    報表建立具有兩個其他的子類別目錄：  
  
    -   `report-errors` （="true/false"，預設值為"false"（也就是選擇性屬性））  
  
    -   `verbose` （="true/false"，預設值為"false"（也就是選擇性屬性））  
  
**語法範例：**  
  
```xml  
<generate-assessment-report  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  assessment-report-folder="<folder-name>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
中的多個  
  
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
[移轉] 命令將目標資料庫結構描述轉換成來源結構描述，並將資料移轉到目標伺服器。  
  
### <a name="convert-schema"></a>convert-schema  
此命令會執行從來源到目標結構描述的結構描述轉換。  
  
如果來源或目標資料庫連接不會執行此命令之前執行，或在來源或目標的 「 資料庫 」 伺服器的連線失敗命令執行期間，會產生錯誤，並在主控台應用程式結束。  
  
-   `conversion-report-folder:` 指定可以在儲存評定報表的資料夾。 （選擇性屬性）  
  
-   `object-name:` 指定來源物件視為轉換結構描述 （支援個別的物件名稱或群組物件名稱）。  
  
-   `object-type:` 指定物件中所呼叫的物件名稱屬性 （如果已指定物件類別，則物件類型會是 「 類別 」） 的類型。  
  
-   `conversion-report-overwrite:` 指定是否要覆寫評估報告資料夾，如果已經存在。  
  
    **預設值：** ，則為 false。 （選擇性屬性）  
  
-   `write-summary-report-to:` 指定產生的摘要報告的路徑。  
  
    如果只提及，資料夾路徑，然後檔案名稱**SchemaConversionReport&lt;n&gt;。XML**建立。 （選擇性屬性）  
  
    報表建立具有兩個其他的子類別目錄：  
  
    -   `report-errors` （="true/false"，預設值為"false"（也就是選擇性屬性））  
  
    -   `verbose` （="true/false"，預設值為"false"（也就是選擇性屬性））  
  
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
中的多個  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder-name>"         (optional)  
  
  conversion-report-overwrite="<true/false>"> (optional)  
  
  <metabase-object object-name="<object-name>"  
  
    object-type="<object-category>"/>  
  
</convert-schema>  
```  
  
### <a name="migrate-data"></a>migrate-data  
此命令會將來源資料移轉至目標。  
  
-   `object-name:` 指定來源物件視為移轉資料 （支援個別的物件名稱或群組物件名稱）。  
  
-   `object-type:` 指定物件中所呼叫的物件名稱屬性 （如果已指定物件類別，則物件類型會是 「 類別 」） 的類型。  
  
-   `write-summary-report-to:` 指定將產生報告的路徑。  
  
    如果只提及，資料夾路徑，然後檔案名稱**DataMigrationReport&lt;n&gt;。XML**建立。 （選擇性屬性）  
  
    報表建立具有兩個其他的子類別目錄：  
  
    -   `report-errors` （="true/false"，預設值為"false"（也就是選擇性屬性））  
  
    -   `verbose` （="true/false"，預設值為"false"（也就是選擇性屬性））  
  
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
中的多個  
  
```xml  
<migrate-data  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-command"></a>移轉準備命令  
開始在來源和目標資料庫之間的結構描述對應的移轉準備命令。  
  
> [!NOTE]  
> [移轉] 命令設定預設的主控台輸出會是 'Full' 輸出報表不詳細的錯誤報告：只有在來源物件樹狀結構根節點的摘要。  
  
### <a name="map-schema"></a>map-schema  
這個命令會提供結構描述對應到目標結構描述的來源資料庫。  
  
-   `source-schema` 指定要移轉的來源結構描述。  
  
-   `sql-server-schema` 指定將會移轉的來源結構描述的目標結構描述。  
  
**語法範例：**  
  
```xml  
<map-schema source-schema="<source-schema>"  
  
sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-commands"></a>管理命令  
管理能力命令可以幫助與來源資料庫同步處理目標資料庫物件。  
  
> [!NOTE]  
> [移轉] 命令設定預設的主控台輸出會是 'Full' 輸出報表不詳細的錯誤報告：只有在來源物件樹狀結構根節點的摘要。  
  
### <a name="synchronize-target"></a>synchronize-target  
此命令會使用目標資料庫，同步處理的目標物件。  
 
如果針對來源資料庫執行此命令時，發生錯誤。  
  
如果目標資料庫連接不會再執行此命令執行，或在目標資料庫伺服器的連線失敗命令執行期間，會產生錯誤，則主控台應用程式結束。  
  
-   `object-name:` 指定同步處理目標資料庫 （支援個別的物件名稱或群組物件名稱） 被視為目標物件。  
  
-   `object-type:` 指定物件中所呼叫的物件名稱屬性 （如果已指定物件類別，則物件類型會是 「 類別 」） 的類型。  
  
-   `on-error:` 指定是否要指定同步處理錯誤視為警告或錯誤。 錯誤的可用選項：  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
-   `report-errors-to:` 指定同步處理作業 （也就是選擇性屬性） 的錯誤報表的位置。 如果只指定資料夾路徑，然後檔案名稱**TargetSynchronizationReport.XML**建立。  
  
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
中的多個  
  
```xml  
<synchronize-target  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"/>  
```  
中的多個  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
  
### <a name="refresh-from-database"></a>refresh-from-database  
此命令會重新整理資料庫的來源物件。  
  
如果針對目標資料庫執行此命令時，會產生錯誤。  
  
此命令需要一個或多個的 metabase 節點做為命令列參數。  
  
-   `object-name:` 指定的來源物件，視為可重新整理從來源資料庫 （支援個別的物件名稱或群組物件名稱）。  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果已指定物件類別，則物件類型會是 「 類別 」） 的物件型別。  
  
-   `on-error:` 指定是否要呼叫重新整理錯誤視為警告或錯誤。 錯誤的可用選項：  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
-   `report-errors-to:` 指定的錯誤報表重新整理作業 （也就是選擇性屬性） 的位置。 如果只指定資料夾路徑，然後檔案名稱**SourceDBRefreshReport.XML**建立。  
  
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
中的多個  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  object-type="<object-category>" />  
```  
中的多個  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-commands"></a>指令碼產生命令  
產生指令碼命令執行雙重工作： 它們說明將主控台輸出指令碼檔案的儲存及它們 T-SQL 輸出記錄至主控台或檔案，根據您指定的參數。  
  
### <a name="save-as-script"></a>save-as-script  
此命令用來儲存到檔案物件的指令碼所述當 metabase target。 我們取得的指令碼，並在目標資料庫上執行相同，這是替代同步處理命令。  
  
此命令需要一個或多個的 metabase 節點做為命令列參數。  
  
-   `object-name:` 指定的物件的指令碼是儲存 （支援個別的物件名稱或群組物件名稱）。  
  
-   `object-type:` 指定物件中所呼叫的物件名稱屬性 （如果已指定物件類別，則物件類型會是 「 類別 」） 的類型。  
  
-   `metabase:` 指定是否在來源或目標 metabase。  
  
-   `destination:` 指定的路徑或指令碼必須儲存所在的資料夾。 如果未指定檔案名稱，則將提供格式 （object_name 屬性值）.out 中的檔案名稱。
  
-   `overwrite:` 如果為 true，則它會覆寫相同的檔案名稱若有的話。 它可以有值 (true/false)。  
  
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
中的多個  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file-name/folder-name>"  
  
    <metabase-object object-name="<object-name>"  
  
                     object-type="<object-category>"/>  
  
</save-as-script>  
```  
  
### <a name="convert-sql-statement"></a>convert-sql-statement
此命令會將轉換的 SQL 陳述式。  
  
-   `context` 指定的結構描述名稱。  
  
-   `destination` 指定輸出是否應該儲存在檔案中。  
  
    如果未指定此屬性，則已轉換的 T-SQL 陳述式會顯示在主控台上。 （選擇性屬性）  
  
-   `conversion-report-folder` 指定可以儲存評定報表的資料夾。 （選擇性屬性）  
  
-   `conversion-report-overwrite` 指定是否要覆寫評估報告資料夾，如果已經存在。  
  
    **預設值：** ，則為 false。 （選擇性屬性）  
  
-   `write-converted-sql-to` 應該儲存已轉換的 T-SQL 中指定的檔案 （或） 資料夾路徑。 與指定的資料夾路徑時`sql-files`屬性，每個原始程式檔有對應的目標指定的資料夾下建立的 T-SQL 檔案。 與指定的資料夾路徑時`sql`屬性，指定的資料夾下名為 Result.out 檔案寫入已轉換的 T-SQL。  
  
-   `sql` 指定要轉換的 Sybase sql 陳述式可以分隔一或多個陳述式，使用 「; 」  
  
-   `sql-files` 指定必須轉換到 T-SQL 程式碼的 sql 檔案的路徑。  
  
-   `write-summary-report-to` 指定的路徑會產生摘要的報表。 如果只提及，資料夾路徑，然後檔案名稱**ConvertSQLReport.XML**建立。 （選擇性屬性）  
  
    建立摘要報表會有兩個其他的子類別，也就是：  
  
    -   報告錯誤 （="true/false"，預設值為"false"（也就是選擇性屬性））。  
  
    -   詳細資訊 （="true/false"，預設值為"false"（也就是選擇性屬性））。  
  
此命令需要一個或多個的 metabase 節點做為命令列參數。  
  
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
中的多個  
  
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
中的多個  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-steps"></a>後續步驟  
如需命令列選項的資訊，請參閱[SSMA 主控台 (AccessToSQL) 中的命令列選項](../access/command-line-options-in-ssma-console-accesstosql.md)。  
  
如需範例主控台指令碼檔案資訊，請參閱[使用範例主控台指令碼檔&#40;SybaseToSQL&#41;](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)  
  
下一個步驟取決於您的專案需求：  
  
-   指定的密碼或匯出 / 匯入的密碼，請參閱 <<c0> [ 管理的密碼&#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md)。</c0>  
  
-   要產生報表，請參閱[產生的報表&#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md)。  
  
-   如需疑難排解主控台中的問題，請參閱[疑難排解&#40;SybaseToSQL&#41;](../../ssma/sybase/troubleshooting-sybasetosql.md)。  
  
