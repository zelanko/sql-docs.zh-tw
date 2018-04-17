---
title: 建立指令碼檔案 (SybaseToSQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Configuring Settings
- Sybase Console,Script Commands
- Sybase Console,Script File Validation
- Sybase Console,Server Connection Parameters
ms.assetid: e6baf106-abbd-4200-b3de-33b4b4f1b294
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9639d7527d910e61cd799ab616f10eb20b5262e4
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="creating-script-files-sybasetosql"></a>建立指令碼檔案 (SybaseToSQL)
第一個步驟之前啟動 SSMA 主控台應用程式。 若要建立指令碼檔案，並在必要時建立的變數值的檔案和伺服器連接檔案。  
  
指令碼檔案可以分成三個區段，viz..,:  
  
1.  **config:**可讓使用者設定的主控台應用程式的組態參數。  
  
2.  **伺服器：**可讓使用者設定來源/目標伺服器定義。 這也可以在不同的伺服器連接檔案中。  
  
3.  **指令碼命令：**可讓使用者執行 SSMA 工作流程命令。  
  
下面將詳細說明每個區段：  
  
## <a name="configuring-sybase-console-settings"></a>Sybase 主控台設定  
指令碼的組態會顯示在主控台指令碼檔案。  
  
如果有任何項目會指定 [設定] 節點中，它們會設定為全域的設定也就它們是適用於所有的指令碼命令。 這些組態項目也可以設定每個命令中的指令碼命令區段中如果使用者想要覆寫全域設定。  
  
使用者可設定選項包括：  
  
1.  **輸出視窗提供者：**如果隱藏訊息屬性設為 'true'，命令指定不要不取得在主控台上顯示訊息。 屬性描述如下所示：  
  
    -   目的地： 指定是否需要取得列印到檔案或 stdout 輸出。 這是預設為 false。  
  
    -   檔案名稱: （選擇性） 檔案的路徑。  
  
    -   隱藏訊息： 不顯示在主控台上的訊息。 這是預設的 ' false'。  
  
    **範例：**  
  
    ```xml  
    <output-providers>  
  
      <output-window  
  
        suppress-messages="<true/false>"   (optional)  
  
        destination="<file/stdout>"        (optional)  
  
        file-name="<file-name>"            (optional)  
  
       />  
  
    </output-providers>  
    ```  
    *或*  
  
    ```xml  
    <…All commands…>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </…All commands…>  
    ```  
  
2.  **資料移轉連接提供者：**這指定哪一個來源/目標伺服器會被視為資料移轉。  來源-使用-上次使用時，表示上次使用的來源伺服器用於資料移轉。 同樣地目標-使用-上次使用，表示上次使用的目標伺服器，用於資料移轉。 使用者也可以指定使用屬性的來源伺服器或目標伺服器的伺服器 （來源或目標）。  
  
    可以也就使用一部或其他指定的屬性：  
  
    -   來源-使用-上次使用 ="true"（預設值） 或來源伺服器 ="source_servername"  
  
    -   target-use-last-used="true" (default) or target-server="target_servername"  
  
    **範例：**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection   source-use-last-used="true"  
  
                                   target-server="<target-server-unique-name>"/>  
  
    </output-providers>  
    ```  
    *或*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="<source-server-unique-name>"  
  
                                   target-use-last-used="true"/>  
  
    </migrate-data>  
    ```  
  
3.  **使用者輸入快顯視窗：**這樣的錯誤，處理物件從資料庫載入時。 使用者提供的輸入的模式，並發生錯誤，主控台會繼續為使用者指定。  
  
    模式包括：  
  
    -   **詢問使用者-**會提示使用者 continue('yes') 或 out ('no') 的錯誤。  
  
    -   **錯誤-**主控台會顯示錯誤並暫停執行。  
  
    -   **繼續-**主控台會繼續執行。  
  
    預設模式是**錯誤**。  
  
    **範例：**  
  
    ```xml  
    <output-providers>  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </output-providers>  
    ```  
    *或*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="<target-server-unique-name>">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **重新連線提供者：**這可讓使用者設定重新連線設定忙線的連接失敗。 這可以設定來源和目標伺服器。  
  
    重新連線的模式包括：  
  
    -   重新連線至最後一個-使用-伺服器： 如果連接不在作用中，它會嘗試重新連線到最後一個伺服器使用最多 5 次。  
  
    -   產生的-錯誤： 如果連接不在作用中，會產生錯誤。  
  
    預設模式是**產生的-錯誤**。  
  
    **範例：**  
  
    ```xml  
    <output-providers>  
  
      <reconnect-manager  on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
                          on-target-reconnect="<reconnect-to-last-used-server/generate-an-error>"/>  
  
    </output-providers>  
    ```  
    *或*  
  
    ```xml  
    <!--synchronization-->  
  
    <synchronize-target>  
  
      <reconnect-manager on-target-reconnect="reconnect-to-last-used-server"/>  
  
    </synchronize-target>  
    ```  
    *或*  
  
    ```xml  
    <!--data migration-->  
  
    <migrate-data server="<target-server-unique-name>">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **轉換器覆寫提供者：**這可讓使用者處理已存在於目標物件 metabase。 可能的動作包括：  
  
    -   錯誤： 主控台會顯示錯誤並暫停執行。  
  
    -   覆寫： 覆寫現有的物件值。 依預設，進行此動作。  
  
    -   略過： 主控台略過資料庫上的已存在的物件  
  
    -   詢問使用者： 提示使用者輸入 ('yes '/' 沒有')  
  
    **範例：**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </output-providers>  
    ```  
    *或*  
  
    ```xml  
    <convert-schema object-name="<object-name>">  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **失敗的必要元件提供者：**這可讓使用者處理所需的處理命令的任何先決條件。 根據預設，strict 模式為 'false'。 如果設定為 'true'，例外狀況會產生符合必要條件失敗。  
  
    **範例：**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true/false>"/>  
  
    </output-providers>  
    ```  
  
7.  **停止作業：**中間作業期間，如果使用者想要停止作業，然後**' Ctrl + C'**快速鍵可用。 SSMA for Sybase 主控台將會等到作業完成，並終止主控台執行。  
  
    如果使用者想要停止執行，然後**' Ctrl + C'**快速鍵可以按下一次的 SSMA 主控台應用程式突然終止  
  
8.  **進度的提供者：**通知每個主控台命令的進度。 預設為停用。 進度報告的屬性組成：  
  
    -   關閉  
  
    -   每隔 1%  
  
    -   每隔 2%  
  
    -   每隔 5%  
  
    -   每隔 10%  
  
    -   每隔 20%  
  
    **範例：**  
  
    ```xml  
    <output-providers>  
  
      <progress-reporting enable="<true/false>"           (optional)  
  
                          report-messages="<true/false>"  (optional)  
  
                          report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off" (optional)/>  
  
    </output-providers>  
    ```  
    *或*  
  
    ```xml  
    <…All commands…>  
  
      <progress-reporting  
  
        enable="<true/false>"          (optional)  
  
        report-messages="<true/false>" (optional)  
  
        report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off (optional)/>  
  
    </…All commands…>  
    ```  
  
9. **記錄器詳細等級：**集合記錄的詳細資訊層級。 這等同於在 UI 中的所有類別目錄選項使用。 根據預設，記錄檔的詳細資訊層級會是 「 錯誤 」。  
  
    記錄器層級的選項包括：  
  
    -   嚴重錯誤： 只有嚴重錯誤訊息記錄。  
  
    -   錯誤： 僅錯誤和嚴重錯誤訊息會記錄。  
  
    -   警告： 偵錯和資訊訊息以外的所有層級會記錄。  
  
    -   資訊： 除了偵錯訊息會記錄所有的層級。  
  
    -   偵錯： 所有層級的記錄的訊息。  
  
    > [!NOTE]  
    > 必要的訊息會記錄在任何層級。  
  
    **範例：**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </output-providers>  
    ```  
    *或*  
  
    ```xml  
    <…All commands…>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </…All commands…>  
    ```  
  
10. **覆寫加密密碼：**如果 'true'，純文字密碼指定伺服器連接檔案的伺服器定義區段中，或在指令碼檔案中，覆寫儲存在加密的密碼保護的儲存體，如果存在。 如果沒有指定密碼以純文字，系統會提示使用者輸入的密碼。  
  
    以下兩種情況下發生：  
  
    1.  如果覆寫選項是**false**，搜尋的順序是受保護儲存體-&gt;指令碼檔案-&gt;伺服器連線檔案-&gt;提示使用者。  
  
    2.  如果覆寫選項是**true**，搜尋的順序是指令碼檔案-&gt;伺服器連線檔案-&gt;提示使用者。  
  
    **範例：**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
不可設定的選項是：  
  
-   **重新連接嘗試次數上限：**時建立的連接逾時或因網路失敗而中斷，則需要重新連線的伺服器。 最多允許重新連線嘗試**5**重試次數之後，主控台會自動執行重新連線。 自動重新連線功能會減少您在重新執行指令碼的工作。  
  
## <a name="server-connection-parameters"></a>伺服器連接參數  
伺服器連接參數可以在指令碼檔案或伺服器連接檔案中定義。 請參閱[伺服器連線檔案建立&#40;SybaseToSQL&#41; ](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md) > 一節以取得詳細資料  
  
## <a name="script-commands"></a>指令碼命令  
指令碼檔案包含一連串的移轉工作流程命令，以 XML 格式。 SSMA 主控台應用程式會處理指令碼檔案中出現的命令順序移轉。  
  
Sybase 資料庫中特定資料表的一般資料移轉，例如，如下的階層： 資料庫-&gt;結構描述-&gt;資料表。  
  
當指令碼檔案中的所有命令都執行成功時，SSMA 主控台應用程式結束，並將控制權傳回給使用者。 指令碼檔案的內容會更多或較少的靜態變數的資訊包含在[變數值的檔案](http://msdn.microsoft.com/en-us/395be464-4b19-44f7-91e5-b8876d6743dc)或變數值的指令碼檔案中的個別區段中。  
  
**範例：**  
  
```xml  
<!--Sample of script file commands -->  
  
<ssma-script-file>  
  
  <script-commands>  
  
    <create-new-project project-folder="<project-folder>"  
  
                        project-name="<project-name>"  
  
                        overwrite-if-exists="<true/false>"/>  
  
    <connect-source-database server="<source-server-unique-name>"/>  
  
    <save-project/>  
  
    <close-project/>  
  
  </script-commands>  
  
</ssma-script-file>  
```  
範本包含 3 個指令碼檔案 （適用於執行各種案例），變數值的檔案，與伺服器連接檔案提供產品目錄的範例主控台 Scripts 資料夾中：  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
在變更參數，其中顯示的資訊之後，您可以執行範本 （檔案）。  
  
指令碼命令的完整清單位於[執行 SSMA 主控台&#40;SybaseToSQL&#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md)  
  
## <a name="script-file-validation"></a>指令碼檔案驗證  
使用者可以輕鬆地驗證自己的指令碼檔案對結構描述定義檔**'S2SSConsoleScriptSchema.xsd'**可用 '結構描述' 資料夾中  
  
## <a name="next-step"></a>下一個步驟  
在操作主控台的下一個步驟是[建立變數值的檔案&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[建立變數值的檔案&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
