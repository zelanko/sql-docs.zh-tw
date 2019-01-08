---
title: 執行 SSMA 主控台 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ce63f633-067d-4f04-b8e9-e1abd7ec740b
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6750e17b694086cf716e32629fcf3b3f3b48f486
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52395191"
---
# <a name="executing-the-ssma-console-db2tosql"></a>執行 SSMA 主控台 (DB2ToSQL)
Microsoft 提供您使用一組強大的指令碼檔案命令來執行及控制 SSMA 活動。 後續章節將詳細說明相同。 主控台應用程式會使用某些標準的指令碼檔命令為列舉這一節。  
  
## <a name="project-script-file-commands"></a>專案指令碼檔案命令  
建立專案、 開啟、 儲存及結束專案的專案的命令控制代碼。  
  
**Command**  
  
建立新專案間的  
  
建立新的 SSMA 專案。  
  
**指令碼**  
  
-   `project-folder` 表示取得建立之專案的資料夾。  
  
-   `project-name` 表示專案的名稱。 {string}  
  
-   `overwrite-if-exists`選擇性的屬性會指出是否應該覆寫現有的專案。 {布林值}  
  
-   `project-type:`選擇性屬性。 表示專案類型也就是 「 sql-server 2005 的 「 專案或 「 sql-server 2008 的 「 專案或 「 sql-server 2012 的 「 專案或 「 sql-server 2014 的 「 專案或 [sql azure]。 預設值為"sql-server-2014"。  
  
**範例：**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014>"   (optional)  
  
/>  
```  
' 覆寫-if-exists' 屬性是**false**預設。  
  
[專案類型] 屬性是**sql server 2008**預設。  
  
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
SSMA for DB2 主控台應用程式支援回溯相容性。 您可以在 若要開啟建立的前一版的 SSMA 專案。  
  
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
  
## <a name="database-connection-script-file-commands"></a>資料庫連接指令碼檔案命令  
資料庫連接命令可以幫助連接到資料庫。  
  
-   **瀏覽**主控台中不支援的 ui 功能。  
  
-   如需有關建立指令碼檔的詳細資訊，請參閱[建立指令碼檔案&#40;OracleToSQL&#41;](../../ssma/oracle/creating-script-files-oracletosql.md)。  
  
**Command**  
  
connect-source-database  
  
-   會執行來源資料庫的連接，並載入高的層級中繼資料的來源資料庫，而非全部的中繼資料。  
  
-   如果無法建立來源的連接，則會產生錯誤和主控台應用程式會停止進一步執行  
  
**指令碼**  
  
從伺服器連線檔案或指令碼檔案的每個連線伺服器一節中所定義的名稱屬性，擷取伺服器定義。  
  
**語法範例：**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
force-load-source/target-database  
  
-   載入來源的中繼資料。  
  
-   適用於使用離線移轉專案。  
  
-   如果無法建立來源/目標的連線，則會產生錯誤和主控台應用程式會停止進一步執行  
  
**指令碼**  
  
需要一或多個的 metabase 節點做為命令列參數。  
  
**語法範例：**  
  
```xml  
<force-load object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
中的多個  
  
```xml  
<force-load>  
  
   <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Command**  
  
reconnect-source-database  
  
-   重新連線至來源資料庫，但不會載入與連接來源資料庫命令的任何中繼資料。  
  
-   如果 （重新） 與來源的連接無法建立，則會產生錯誤和主控台應用程式會停止進一步執行。  
  
**指令碼**  
  
**語法範例：**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
連線目標資料庫  
  
-   連接到目標 SQL Server 資料庫，並完全載入目標資料庫的高等級的中繼資料，但不是的中繼資料。  
  
-   如果無法連線到目標，則會產生錯誤和主控台應用程式會停止進一步執行。  
  
**指令碼**  
  
伺服器定義會從定義每個連線伺服器一節中的伺服器連線檔案或指令碼檔案的名稱屬性  
  
**語法範例：**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
reconnect-target-database  
  
-   重新連線到目標資料庫，但不會載入任何中繼資料，不同於連接目標資料庫命令。  
  
-   如果 （重新） 連線到目標不能建立，則會產生錯誤和主控台應用程式會停止進一步執行。  
  
**指令碼**  
  
**語法範例：**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>報表指令碼檔案命令  
報表命令產生的各種 SSMA 主控台活動效能的報告。  
  
**Command**  
  
generate-assessment-report  
  
-   會產生來源資料庫上的評估報告。  
  
-   如果執行此命令會產生錯誤，並在主控台應用程式結束之前，不會執行來源資料庫連接。  
  
-   無法連線至來源資料庫伺服器在命令執行時，也會導致終止的主控台應用程式。  
  
**指令碼**  
  
-   `conversion-report-folder:` 指定要儲存評定報表可以在其中的資料夾。（選擇性屬性）  
  
-   `object-name:` 指定考慮用於產生評定報告 （可以有個別的物件名稱或群組的物件名稱） 的物件。  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果已指定物件類別，則物件類型會是 「 類別 」） 的物件型別。  
  
-   `conversion-report-overwrite:` 指定是否要覆寫評估報告資料夾，如果已經存在。  
  
    **預設值：** ，則為 false。 （選擇性屬性）  
  
-   `write-summary-report-to:` 指定的路徑會產生摘要的報表。  
  
    如果只提及，資料夾路徑，然後檔案名稱**AssessmentReport&lt;n&gt;。XML**建立。 （選擇性屬性）  
  
    報表建立具有兩個其他的子類別：  
  
    -   `report-errors` （="true/false"，預設值為"false"（也就是選擇性屬性））  
  
    -   `verbose` （="true/false"，預設值為"false"（也就是選擇性屬性））  
  
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
中的多個  
  
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
[移轉] 命令將目標資料庫結構描述轉換成來源結構描述，並將資料移轉到目標伺服器。 [移轉] 命令設定預設的主控台輸出會是 'Full' 輸出報表不詳細的錯誤報告：只有在來源物件樹狀結構根節點的摘要。  
  
**Command**  
  
convert-schema  
  
-   執行從來源到目標結構描述的結構描述轉換。  
  
-   如果來源或目標資料庫連接不會執行此命令之前執行，或在來源或目標的 「 資料庫 」 伺服器的連線失敗命令執行期間，會產生錯誤，並在主控台應用程式結束。  
  
**指令碼**  
  
-   `conversion-report-folder:` 指定要儲存評定報表可以在其中的資料夾。（選擇性屬性）  
  
-   `object-name:` 指定來源物件視為轉換 （可以有個別的物件名稱或群組的物件名稱） 的結構描述。  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果已指定物件類別，則物件類型會是 「 類別 」） 的物件型別。  
  
-   `conversion-report-overwrite:` 指定是否要覆寫評估報告資料夾，如果已經存在。  
  
    **預設值：** ，則為 false。 （選擇性屬性）  
  
-   `write-summary-report-to:` 指定的路徑會產生摘要的報表。  
  
    如果只提及，資料夾路徑，然後檔案名稱**SchemaConversionReport&lt;n&gt;。XML**建立。 （選擇性屬性）  
  
    報表建立具有兩個其他的子類別：  
  
    -   `report-errors` （="true/false"，預設值為"false"（也就是選擇性屬性））  
  
    -   `verbose` （="true/false"，預設值為"false"（也就是選擇性屬性））  
  
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
中的多個  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Command**  
  
移轉資料：將來源資料移轉至目標。  
  
**指令碼**  
  
-   `conversion-report-folder:` 指定要儲存評定報表可以在其中的資料夾。（選擇性屬性）  
  
-   `object-name:` 指定視為要移轉的來源物件 （可以有個別的物件名稱或群組的物件名稱） 的資料。  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果已指定物件類別，則物件類型會是 「 類別 」） 的物件型別。  
  
-   `conversion-report-overwrite:` 指定是否要覆寫評估報告資料夾，如果已經存在。  
  
    **預設值：** ，則為 false。 （選擇性屬性）  
  
-   `write-summary-report-to:` 指定的路徑會產生摘要的報表。  
  
    如果只提及，資料夾路徑，然後檔案名稱**DataMigrationReport&lt;n&gt;。XML**建立。 （選擇性屬性）  
  
    報表建立具有兩個其他的子類別：  
  
    -   `report-errors` （="true/false"，預設值為"false"（也就是選擇性屬性））  
  
    -   `verbose` （="true/false"，預設值為"false"（也就是選擇性屬性））  
  
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
中的多個  
  
```xml  
<migrate-data  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>移轉準備指令碼檔案命令  
開始在來源和目標資料庫之間的結構描述對應的移轉準備命令。  
  
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
管理能力命令可以幫助與來源資料庫同步處理目標資料庫物件。  
  
[移轉] 命令設定預設的主控台輸出會是 'Full' 輸出報表不詳細的錯誤報告：只有在來源物件樹狀結構根節點的摘要。  
  
**Command**  
  
同步處理目標  
  
-   會使用目標資料庫，同步處理的目標物件。  
  
-   如果針對來源資料庫執行此命令時，發生錯誤。  
  
-   如果目標資料庫連接不會再執行此命令執行，或在目標資料庫伺服器的連線失敗命令執行期間，會產生錯誤，則主控台應用程式結束。  
  
**指令碼**  
  
-   `object-name:` 指定目標物件視為與 （可以有個別的物件名稱或群組的物件名稱） 的目標資料庫同步處理。  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果已指定物件類別，則物件類型會是 「 類別 」） 的物件型別。  
  
-   `on-error:` 指定是否要指定同步處理錯誤視為警告或錯誤。 錯誤的可用選項：  
  
    -   報表-總計-為-警告  
  
    -   報表-每個-為-警告  
  
    -   失敗指令碼  
  
-   `report-errors-to:` 同步處理作業 （也就是選擇性屬性） 如果只指定資料夾路徑，然後檔案儲存依名稱指定的錯誤報表的位置**TargetSynchronizationReport.XML**建立。  
  
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
**Command**  
  
從資料庫重新整理  
  
-   重新整理資料庫的來源物件。  
  
-   如果針對目標資料庫執行此命令時，會產生錯誤。  
  
**指令碼**  
  
需要一或多個的 metabase 節點做為命令列參數。  
  
-   `object-name:` 指定的來源物件，視為可重新整理從來源資料庫 （可以有個別的物件名稱或群組的物件名稱）。  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果已指定物件類別，則物件類型會是 「 類別 」） 的物件型別。  
  
-   `on-error:` 指定是否要指定重新整理錯誤視為警告或錯誤。 錯誤的可用選項：  
  
    -   報表-總計-為-警告  
  
    -   報表-每個-為-警告  
  
    -   失敗指令碼  
  
-   `report-errors-to:` 重新整理作業 （也就是選擇性屬性） 如果只指定資料夾路徑，然後檔案儲存依名稱指定的錯誤報表的位置**SourceDBRefreshReport.XML**建立。  
  
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
中的多個  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
中的多個  
  
```xml  
<refresh-from-database>  
  
   <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>指令碼產生指令碼檔案命令  
產生指令碼命令會執行雙重工作：它們有助於節省主控台輸出在指令碼檔案中;和 T-SQL 的輸出記錄到主控台] 或 [根據您指定的參數檔案。  
  
**Command**  
  
save-as-script  
  
用來儲存物件的指令碼至檔案中所述當 metabase target，這是替代同步處理命令，在我們取得的指令碼並執行相同目標資料庫。  
  
**指令碼**  
  
需要一或多個的 metabase 節點做為命令列參數。  
  
-   `object-name:` 指定的指令碼是儲存的物件。 （可以有個別的物件名稱或群組的物件名稱）  
  
-   `object-type:` 指定的屬性中指定的物件名稱 （如果已指定物件類別，則物件類型會是 「 類別 」） 的物件型別。  
  
-   `metabase:` 指定是否在來源或目標 metabase。  
  
-   `destination:` 指定的路徑或其中的指令碼必須儲存，如果檔案名稱中未指定則檔案名稱格式 （object_name 屬性值）.out 的資料夾  
  
-   `overwrite:` 如果為 true 則它會覆寫相同的檔案名稱。 它可以有值 (true/false)。  
  
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
中的多個  
  
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
  
-   `destination` 指定輸出是否應該儲存在檔案中。  
  
    如果未指定此屬性，則已轉換的 T-SQL 陳述式會顯示在主控台上。 （選擇性屬性）  
  
-   `conversion-report-folder` 指定要儲存評定報表可以在其中的資料夾。（選擇性屬性）  
  
-   `conversion-report-overwrite` 指定是否要覆寫評估報告資料夾，如果已經存在。  
  
    **預設值：** ，則為 false。 （選擇性屬性）  
  
-   `write-converted-sql-to` 指定的檔案 （或） 要儲存已轉換的 T-SQL 所在的資料夾路徑。 與指定的資料夾路徑時`sql-files`屬性，每個原始程式檔會有對應的目標指定的資料夾下建立的 T-SQL 檔案。 與指定的資料夾路徑時`sql`屬性，名為的檔案寫入已轉換的 T-SQL **Result.out**底下指定的資料夾。  
  
-   `sql` 指定要轉換的 DB2 sql 陳述式可以分隔一或多個陳述式，使用 「; 」  
  
-   `sql-files` 指定必須轉換到 T-SQL 程式碼的 sql 檔案的路徑。  
  
-   `write-summary-report-to` 指定會產生報表的路徑。 如果只提及，資料夾路徑，然後檔案名稱**ConvertSQLReport.XML**建立。 （選擇性屬性）  
  
    建立具有上來進一步子類別，2 的報表。。，：  
  
    -   報告錯誤 （="true/false"，預設值為"false"（也就是選擇性屬性））。  
  
    -   詳細資訊 （="true/false"，預設值為"false"（也就是選擇性屬性））。  
  
**指令碼**  
  
需要一或多個的 metabase 節點做為命令列參數。  
  
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
中的多個  
  
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
中的多個  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
  
## <a name="next-step"></a>下一個步驟  
如需命令列選項的資訊，請參閱[SSMA 主控台中的命令列選項&#40;DB2ToSQL&#41; ](../../ssma/db2/command-line-options-in-ssma-console-db2tosql.md) 。  
  
如需範例主控台指令碼檔的資訊，請參閱[使用範例主控台指令碼檔&#40;DB2ToSQL&#41;](../../ssma/db2/working-with-the-sample-console-script-files-db2tosql.md)  
  
下一個步驟取決於您的專案需求：  
  
-   指定的密碼或匯出 / 匯入的密碼，請參閱 <<c0> [ 管理的密碼&#40;DB2ToSQL&#41;](../../ssma/db2/managing-passwords-db2tosql.md)。</c0>  
  
-   要產生報表，請參閱[產生的報表&#40;DB2ToSQL&#41;](../../ssma/db2/generating-reports-db2tosql.md)。  
  
-   如需疑難排解主控台中的問題，請參閱[疑難排解&#40;DB2ToSQL&#41;](../../ssma/db2/troubleshooting-db2tosql.md)。  
  
