---
title: 執行 SQL 工作編輯器 （一般頁面） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.executesqltask.general.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: beb39086-28ce-46af-b6d8-f7b4fb8d9069
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 853586d51aff06012734a677794f29a9e7991878
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145437"
---
# <a name="execute-sql-task-editor-general-page"></a>執行 SQL 工作編輯器 (一般頁面)
  使用 [執行 SQL 工作編輯器] 對話方塊的 [一般] 頁面，即可設定「執行 SQL」工作和提供該工作執行的 SQL 陳述式。  
  
 若要了解這項工作，請參閱[執行 SQL 工作](control-flow/execute-sql-task.md)、[執行 SQL 工作中的參數和傳回碼](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)和[執行 SQL 工作中的結果集](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)。 若要深入了解 Transact-SQL 查詢語言，請參閱 [Transact-SQL 參考 &#40;資料庫引擎&#41;](/sql/t-sql/language-reference)。  
  
## <a name="static-options"></a>靜態選項  
 **名稱**  
 提供唯一的名稱給工作流程中的執行 SQL 工作。 提供的名稱將顯示在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述執行 SQL 工作。 最佳作法是以其用途描述工作，使封裝可以自我記錄並易於維護。  
  
 **TimeOut**  
 指定工作在逾時之前執行的秒數上限。值為 0 指出無限的時間。 預設值是 0。  
  
> [!NOTE]  
>  如果預存程序藉由提供大於 [逾時] 指定的秒數之連接時間與交易完成時間，使預存程序模擬睡眠功能，就不會發生逾時。 不過，執行查詢的預存程序一律會受到 [逾時] 所指定的時間限制。  
  
 **CodePage**  
 指定翻譯變數中的 Unicode 值時要使用的字碼頁。 預設值是本機電腦的字碼頁。  
  
> [!NOTE]  
>  當「執行 SQL」工作使用 ADO 或 ODBC 連線管理員時， **CodePage** 屬性就無法使用。 如果您的方案需要使用字碼頁，請使用 OLE DB 或 ADO.NET 連接管理員搭配執行 SQL 工作。  
  
 **TypeConversionMode**  
 當您將此屬性設定為`Allowed`，「 執行 SQL 」 工作會嘗試將轉換的輸出參數和查詢結果的資料類型變數的結果會指派。 這適用於 [單一資料列] 結果集類型。  
  
 **ResultSet**  
 指定 SQL 陳述式開始執行的預期結果類型。 在 [單一資料列]、[完整結果集]、[XML] 或 [無] 之間選擇。  
  
 **ConnectionType**  
 選擇用來連接到資料來源的連接管理員類型。 可用的連接類型包括 **OLE DB**、 **ODBC**、 **ADO**、 **ADO.NET** 和 **SQLMOBILE**。  
  
 **相關主題** [OLE DB 連線管理員](connection-manager/ole-db-connection-manager.md)、 [ODBC 連線管理員](connection-manager/odbc-connection-manager.md)、 [ADO 連線管理員](connection-manager/ado-connection-manager.md)、 [ADO.NET 連線管理員](connection-manager/ado-net-connection-manager.md)、 [SQL Server Compact Edition 連線管理員](connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **[連接]**  
 從已定義的連接管理員清單中選擇連接。 若要建立新的連線，請選取 [\<新增連線...>]。  
  
 **SQLSourceType**  
 選取工作執行之 SQL 陳述式的來源類型。  
  
 而根據執行 SQL 工作所使用的連接管理員類型，您必須在參數化 SQL 陳述式中使用特定的參數標記。  
  
 **相關主題[：** 執行 SQL 工作](control-flow/execute-sql-task.md)中的＜執行參數化的 SQL 命令＞一節  
  
 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|將來源設定為 Transact-SQL 陳述式。 選取此值會顯示動態選項 [SQLStatement]。|  
|**檔案連接**|選取包含 Transact-SQL 陳述式的檔案。 選取此選項會顯示動態選項 [FileConnection]。|  
|**變數**|將來源設定為定義 Transact-SQL 陳述式的變數。 選取此值會顯示動態選項 [SourceVariable]。|  
  
 **QueryIsStoredProcedure**  
 指出要執行之指定的 SQL 陳述式是否為預存程序。 只有工作使用 ADO 連接管理員時，此屬性才會是讀取/寫入。 否則此屬性是唯讀的，且其值為 `false`。  
  
 **BypassPrepare**  
 指出 SQL 陳述式是否已備妥。  `true` 會略過準備；`false` 會在執行它之前備妥 SQL 陳述式。 只有搭配支援準備的 OLE DB 連接，才能使用此選項。  
  
 **相關主題**  [備妥的執行](../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **瀏覽**  
 使用 [開啟] 對話方塊，以尋找包含 SQL 陳述式的檔案。 選取要將檔案內容以 SQL 陳述式複製到 **SQLStatement** 屬性的檔案。  
  
 **建立查詢**  
 使用 [查詢產生器] 對話方塊建立 SQL 陳述式，它是用來建立查詢的圖形化工具。 當 [SQLSourceType] 選項設定為 [直接輸入] 時，才能使用此選項。  
  
 **剖析查詢**  
 驗證 SQL 陳述式的語法。  
  
## <a name="sqlsourcetype-dynamic-options"></a>SQLSourceType 動態選項  
  
### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = 直接輸入  
 **SQLStatement**  
 在選項方塊中輸入要執行的 SQL 陳述式，或按一下瀏覽按鈕 (…) 在 [輸入 SQL 查詢] 對話方塊中輸入 SQL 陳述式，或按一下 [建立查詢] 使用 [查詢產生器] 對話方塊來撰寫陳述式。  
  
 **相關主題**︰[查詢產生器](../../2014/integration-services/query-builder.md)  
  
### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = 檔案連接  
 **FileConnection**  
 選取現有的檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="sqlsourcetype--variable"></a>SQLSourceType = 變數  
 **SourceVariable**  
 選取現有的變數，或按一下 [\<新增變數...>] 以建立新的變數。  
  
 **相關主題**︰[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[加入變數](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [執行 SQL 工作編輯器&#40;參數對應頁面&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [執行 SQL 工作編輯器&#40;結果集頁面&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
  
