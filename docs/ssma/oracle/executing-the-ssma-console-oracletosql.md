---
description: 執行 SSMA 主控台 (OracleToSQL)
title: 執行 SSMA 主控台 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Oracle SSMA Console
- Script File Commands, Script Generation Commands,Manageability Commands
- Script File Commands,Project Commands
ms.assetid: 7228ccba-c69f-4b4c-8664-01a2750183c5
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 554012e73716a828e3bf54a8384c84b1d8a4cb66
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497703"
---
# <a name="executing-the-ssma-console-oracletosql"></a>執行 SSMA 主控台 (OracleToSQL)
Microsoft 為您提供一組健全的腳本檔案命令，來執行和控制 SSMA 活動。 主控台應用程式會使用特定的標準腳本檔案命令，如本節中所列舉。  
  
## <a name="project-script-file-commands"></a>專案腳本檔案命令  
專案命令會處理建立專案、開啟、儲存和結束專案的工作。  
  
**命令**  
  
create-new-project  
                  ：建立新的 SSMA 專案。  
  
**指令碼**  
  
-   `project-folder` 指出建立專案的資料夾。  
  
-   `project-name` 表示專案的名稱。 {string}  
  
-   `overwrite-if-exists`選擇性屬性會指出是否應覆寫現有的專案。 布林  
  
-   `project-type:`選擇性屬性。 指出專案類型，也就是 "sql-server-2005" 專案或 "sql-server-2008" 專案或 "sql-server-2012" 專案或 "sql-server-2014" 專案或 "sql-azure"。 預設值為 "sql-server-2014"。  
  
**範例︰**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014>"   (optional)  
  
/>  
```  
依預設，屬性「覆寫-存在」為 **false** 。  
  
屬性 ' project-type ' 預設為 **sql-server-2008** 。  
  
**命令**  
  
開啟專案：開啟現有的專案。  
  
**指令碼**  
  
-   `project-folder` 指出建立專案的資料夾。 如果指定的資料夾不存在，命令就會失敗。  {string}  
  
-   `project-name` 表示專案的名稱。 如果指定的專案不存在，命令就會失敗。  {string}  
  
**語法範例：**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
SSMA for Oracle 主控台應用程式支援回溯相容性。 您將能夠開啟舊版 SSMA 所建立的專案。  
  
**命令**  
  
save-project  
  
儲存遷移專案。  
  
**指令碼**  
  
**語法範例：**  
  
```xml  
<save-project/>  
```  
**命令**  
  
關閉專案  
  
關閉遷移專案。  
  
**指令碼**  
  
**語法範例：**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
  
## <a name="database-connection-script-file-commands"></a>資料庫連接指令檔命令  
資料庫連接命令可協助連接至資料庫。  
  
-   主控台不支援 UI 的 **流覽** 功能。  
  
-   如需有關「建立腳本檔案」的詳細資訊，請參閱 [建立腳本檔 &#40;OracleToSQL&#41;](../../ssma/oracle/creating-script-files-oracletosql.md)。  
  
**命令**  
  
連接-來源-資料庫  
  
-   執行與源資料庫的連接，並載入源資料庫的高層級中繼資料，但不載入所有中繼資料。  
  
-   如果無法建立與來源的連線，則會產生錯誤，而主控台應用程式會停止進一步執行  
  
**指令碼**  
  
伺服器定義是從伺服器連接檔案或腳本檔案的 [伺服器] 區段中，針對每個連接所定義的名稱屬性來抓取。  
  
**語法範例：**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**命令**  
  
強制載入-來源/目標資料庫  
  
-   載入來源中繼資料。  
  
-   適用于離線處理遷移專案。  
  
-   如果無法建立與來源/目標的連線，則會產生錯誤，而主控台應用程式會停止進一步執行  
  
**指令碼**  
  
需要一或多個多個元資料庫節點作為命令列參數。  
  
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
**命令**  
  
重新連接-來源-資料庫  
  
-   重新連接至源資料庫，但不會載入任何中繼資料，而不像連接來源資料庫命令一樣。  
  
-   如果無法建立與來源之間的 () 連接，則會產生錯誤，而主控台應用程式會停止執行。  
  
**指令碼**  
  
**語法範例：**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**命令**  
  
連接-目標-資料庫  
  
-   連接到目標 SQL Server 資料庫，並載入目標資料庫的高層級中繼資料，但不會完全載入中繼資料。  
  
-   如果無法建立與目標的連線，則會產生錯誤，而主控台應用程式會停止進一步執行。  
  
**指令碼**  
  
伺服器定義是從伺服器連接檔案或腳本檔案的 [伺服器] 區段中為每個連接定義的名稱屬性抓取  
  
**語法範例：**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**命令**  
  
重新連接-目標-資料庫  
  
-   重新連接到目標資料庫，但不會載入任何中繼資料，與連接目標資料庫命令不同。  
  
-   如果無法建立與目標 (的) 連接，則會產生錯誤，而主控台應用程式會停止執行。  
  
**指令碼**  
  
**語法範例：**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file--commands"></a>報表指令檔命令  
報告命令會產生各種 SSMA 主控台活動的效能報告。  
  
**命令**  
  
產生-評量-報告  
  
-   在源資料庫上產生評量報告。  
  
-   如果在執行此命令之前未執行源資料庫連接，則會產生錯誤並結束主控台應用程式。  
  
-   在命令執行期間無法連線到源資料庫伺服器，也會導致終止主控台應用程式。  
  
**指令碼**  
  
-   `conversion-report-folder:` 指定可儲存評定報告的資料夾。 (選用屬性)   
  
-   `object-name:` 指定) 考慮產生評定報告的物件 ( (它可以有個別物件名稱或群組物件名稱) 。  
  
-   `object-type:` 指定物件名稱屬性中指定的物件類型 (如果指定了物件類別，則物件類型會是 "category" ) 。  
  
-   `conversion-report-overwrite:` 指定是否要覆寫評量報告資料夾（如果已存在）。  
  
    **預設值：** false。  (選擇性屬性)   
  
-   `write-summary-report-to:` 指定將產生摘要報告的路徑。  
  
    如果只提及資料夾路徑，則依名稱 **AssessmentReport &lt; n &gt; 。建立 XML** 。  (選擇性屬性)   
  
    報表建立有兩個進一步的子類別：  
  
    -   `report-errors` (= "true/false"，預設值為 "false" (選擇性屬性) # A3  
  
    -   `verbose` (= "true/false"，預設值為 "false" (選擇性屬性) # A3  
  
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
  
## <a name="migration-script-file-commands"></a>遷移指令檔命令  
遷移命令會將目標資料庫架構轉換成來源架構，並將資料移轉至目標伺服器。  
  
遷移命令的預設主控台輸出設定為 [完整] 輸出報告，沒有詳細的錯誤報表：只有來源物件樹狀結構根節點的摘要。  
  
**命令**  
  
轉換-架構  
  
-   執行從來源到目標架構的架構轉換。  
  
-   如果在執行此命令之前未執行來源或目標資料庫連接，或在命令執行期間，與來源或目標資料庫伺服器的連接失敗，則會產生錯誤並結束主控台應用程式。  
  
**指令碼**  
  
-   `conversion-report-folder:` 指定可儲存評定報告的資料夾。 (選用屬性)   
  
-   `object-name:` 指定 (s 的來源物件) 考慮轉換架構 (它可以有個別物件名稱或群組物件名稱) 。  
  
-   `object-type:` 指定物件名稱屬性中指定的物件類型 (如果指定了物件類別，則物件類型會是 "category" ) 。  
  
-   `conversion-report-overwrite:` 指定是否要覆寫評量報告資料夾（如果已存在）。  
  
    **預設值：** false。  (選擇性屬性)   
  
-   `write-summary-report-to:` 指定將產生摘要報告的路徑。  
  
    如果只提及資料夾路徑，則依名稱 **SchemaConversionReport &lt; n &gt; 。建立 XML** 。  (選擇性屬性)   
  
    報表建立有兩個進一步的子類別：  
  
    -   `report-errors` (= "true/false"，預設值為 "false" (選擇性屬性) # A3  
  
    -   `verbose` (= "true/false"，預設值為 "false" (選擇性屬性) # A3  
  
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
**命令**  
  
遷移-資料  
  
將源資料移轉至目標。  
  
**指令碼**  
  
-   `conversion-report-folder:` 指定可儲存評定報告的資料夾。 (選用屬性)   
  
-   `object-name:` 指定) 考慮用來遷移資料的來源物件 (s (它可以有個別物件名稱或) 的群組物件名稱。  
  
-   `object-type:` 指定物件名稱屬性中指定的物件類型 (如果指定了物件類別，則物件類型會是 "category" ) 。  
  
-   `conversion-report-overwrite:` 指定是否要覆寫評量報告資料夾（如果已存在）。  
  
    **預設值：** false。  (選擇性屬性)   
  
-   `write-summary-report-to:` 指定將產生摘要報告的路徑。  
  
    如果只提及資料夾路徑，則依名稱 **DataMigrationReport &lt; n &gt; 。建立 XML** 。  (選擇性屬性)   
  
    報表建立有兩個進一步的子類別：  
  
    -   `report-errors` (= "true/false"，預設值為 "false" (選擇性屬性) # A3  
  
    -   `verbose` (= "true/false"，預設值為 "false" (選擇性屬性) # A3  
  
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
  
## <a name="migration-preparation-script-file-commands"></a>遷移準備指令檔命令  
「遷移準備」命令會在來源和目標資料庫之間起始架構對應。  
  
**命令**  
  
對應架構  
  
源資料庫與目標架構的架構對應。  
  
將源資料移轉至目標。  
  
**指令碼**  
  
-   `source-schema` 指定我們想要遷移的來源架構。  
  
-   `sql-server-schema` 指定要在其中遷移的目標架構。  
  
**語法範例：**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>管理性腳本檔案命令  
管理性命令可協助同步處理目標資料庫物件與源資料庫。 遷移命令的預設主控台輸出設定為 [完整] 輸出報告，沒有詳細的錯誤報表：只有來源物件樹狀結構根節點的摘要。  
  
**命令**  
  
同步處理-目標  
  
-   將目標物件與目標資料庫進行同步處理。  
  
-   如果針對源資料庫執行此命令，就會發生錯誤。  
  
-   如果在執行此命令之前未執行目標資料庫連接，或在命令執行期間連接到目標資料庫伺服器失敗，則會產生錯誤並結束主控台應用程式。  
  
**指令碼**  
  
-   `object-name:` 指定) 考慮與目標資料庫進行同步處理的目標物件 ( (它可以有個別物件名稱或) 的群組物件名稱。  
  
-   `object-type:` 指定物件名稱屬性中指定的物件類型 (如果指定了物件類別，則物件類型會是 "category" ) 。  
  
-   `on-error:` 指定是否將同步處理錯誤指定為警告或錯誤。 錯誤的可用選項：  
  
    -   報告-總為警告  
  
    -   報告-每個警告  
  
    -   失敗-腳本  
  
-   `report-errors-to:` 指定同步處理作業的錯誤報表位置 (選擇性屬性) 如果僅指定資料夾路徑，則會建立依名稱 **TargetSynchronizationReport.XML** 的檔案。  
  
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
**命令**  
  
從資料庫重新整理  
  
-   從資料庫重新整理來源物件。  
  
-   如果對目標資料庫執行此命令，就會產生錯誤。  
  
**指令碼**  
  
需要一或多個多個元資料庫節點作為命令列參數。  
  
-   `object-name:` 指定) 考慮從源資料庫重新整理 (s 的來源物件 (它可以有個別物件名稱或) 的群組物件名稱。  
  
-   `object-type:` 指定物件名稱屬性中指定的物件類型 (如果指定了物件類別，則物件類型會是 "category" ) 。  
  
-   `on-error:` 指定是否將重新整理錯誤指定為警告或錯誤。 錯誤的可用選項：  
  
    -   報告-總為警告  
  
    -   報告-每個警告  
  
    -   失敗-腳本  
  
-   `report-errors-to:` 指定重新整理作業的錯誤報表位置 (選擇性屬性) 如果僅提供資料夾路徑，則會建立依名稱 **SourceDBRefreshReport.XML** 的檔案。  
  
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
  
## <a name="script-generation-script-file-commands"></a>腳本產生指令檔命令  
腳本產生命令會執行兩項工作：它們有助於將主控台輸出儲存在腳本檔案中。並根據您指定的參數，將 T-sql 輸出記錄到主控台或檔案中。  
  
**命令**  
  
另存新檔-腳本  
  
用來將物件的腳本儲存至在 database = target 時所提到的檔案，這是同步處理命令的替代方式，在中，我們會取得腳本，並在目標資料庫上執行相同的作業。  
  
**指令碼**  
  
需要一或多個多個元資料庫節點作為命令列參數。  
  
-   `object-name:` 指定要儲存其腳本的) 物件 (s。  (可以有個別的物件名稱或群組物件名稱)   
  
-   `object-type:` 指定物件名稱屬性中指定的物件類型 (如果指定了物件類別，則物件類型會是 "category" ) 。  
  
-   `metabase:` 指定它是否 ithe 來源或目標元資料庫。  
  
-   `destination:` 指定必須儲存腳本的路徑或資料夾，如果未提供檔案名，則會使用格式 (object_name 屬性值) 的檔案名。  
  
-   `overwrite:` 若為 true，則會覆寫是否存在相同的檔案名。 它可以將值 (true/false) 。  
  
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
**命令**  
  
convert-sql 語句  
  
-   `context` 指定架構名稱。  
  
-   `destination` 指定是否應將輸出儲存在檔案中。  
  
    如果未指定此屬性，則會在主控台上顯示轉換的 T-sql 語句。  (選擇性屬性)   
  
-   `conversion-report-folder` 指定可儲存評定報告的資料夾。 (選用屬性)   
  
-   `conversion-report-overwrite` 指定是否要覆寫評量報告資料夾（如果已存在）。  
  
    **預設值：** false。  (選擇性屬性)   
  
-   `write-converted-sql-to` 指定要儲存已轉換 T-sql 的檔案 (或) 資料夾路徑。 當資料夾路徑與屬性一起指定時 `sql-files` ，每個原始程式檔都會有一個對應的目標 t-sql 檔案，該檔案會在指定的資料夾下建立。 當資料夾路徑與屬性一起指定時 `sql` ，會將已轉換的 t-sql 寫入至名為 **Result** 的檔案，在指定的資料夾下。  
  
-   `sql` 指定要轉換的 Oracle sql 語句，可以使用 ";" 分隔一或多個語句。  
  
-   `sql-files` 指定必須轉換成 T-sql 程式碼的 sql 檔案路徑。  
  
-   `write-summary-report-to` 指定將產生報告的路徑。 如果只提及資料夾路徑，則會建立依名稱 **ConvertSQLReport.XML** 的檔案。  (選擇性屬性)   
  
    建立報表還有2個子類別：視覺效果。  
  
    -   報表-錯誤 (= "true/false"，預設值為 "false" (選擇性屬性) # A3。  
  
    -   verbose (= "true/false"，預設值為 "false" (選擇性屬性) # A3。  
  
**指令碼**  
  
需要一或多個多個元資料庫節點作為命令列參數。  
  
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
  
## <a name="next-step"></a>後續步驟  
如需命令列選項的詳細資訊，請參閱 [SSMA 主控台中的命令列選項 &#40;OracleToSQL&#41;](../../ssma/oracle/command-line-options-in-ssma-console-oracletosql.md) 。  
  
如需範例主控台腳本檔案的詳細資訊，請參閱 [使用範例主控台腳本檔 &#40;OracleToSQL&#41;](../../ssma/oracle/working-with-the-sample-console-script-files-oracletosql.md)  
  
下一步取決於您的專案需求：  
  
-   如需指定密碼或匯出/匯入密碼，請參閱 [管理密碼 &#40;OracleToSQL&#41;](../../ssma/oracle/managing-passwords-oracletosql.md)。  
  
-   若要產生報表，請參閱 [&#40;OracleToSQL&#41;產生報表 ](../../ssma/oracle/generating-reports-oracletosql.md)。  
  
-   如需疑難排解主控台中的問題，請參閱 [&#40;OracleToSQL&#41;的疑難排解 ](../../ssma/oracle/troubleshooting-oracletosql.md)。  
  
