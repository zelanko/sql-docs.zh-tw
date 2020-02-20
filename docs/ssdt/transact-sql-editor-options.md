---
title: Transact-SQL 編輯器選項
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.RESULTS_TO_GRID
- sql.data.tools.SqlExecutionAdvancedSettingsOption
- sql.data.tools.SqlExecutionAnsiSettingsDlg
- sql.data.tools.SqlResultToTextSettingsDlg
- sql.data.tools.SqlExecutionGeneralSettingsDlg
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.GENERAL
- sql.data.tools.unittesting.tsqleditor
- sql.data.tools.SqlResultsToGridSettingsDlg
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.EDITOR_TAB_AND_STATUS_BAR
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.RESULTS_TO_TEXT
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.ANSI
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.ONLINE_EDITING
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.ADVANCED
ms.assetid: fa9a250f-7feb-433e-91bd-a09779d74c8b
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 0b91be419419d7dab1904068b1600def88106023
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75256325"
---
# <a name="transact-sql-editor-options"></a>Transact-SQL 編輯器選項

本主題包含 Transact-SQL 編輯器部分選項的相關資訊。 若要設定這些選項，請透過 [工具\選項]  功能表巡覽至 [選項]  對話方塊。  
  
[查詢執行](#QueryExecution)  
  
[查詢結果](#QueryResults)  
  
## <a name="QueryExecution"></a>查詢執行  
  
|屬性|描述|  
|------------|---------------|  
|**SET ROWCOUNT**|預設值 0 表示 SQL Server 將等候結果，直到所有結果都收到為止。 如果您要 SQL Server 在取得指定的資料列數後停止查詢，請提供大於 0 的值。 若要關閉此選項 (以便傳回所有資料列)，請指定 SET ROWCOUNT 0。|  
|**SET TEXTSIZE**|2,147,483,647 個位元組的預設值表示 SQL Server 將提供完整的資料欄位，直到 text、ntext、nvarchar(max) 及 varchar(max) 資料欄位的上限。 這不會影響 XML 資料類型。 提供較小的數值，即可在有大量數值時，限制傳回的結果數量。 資料行若大於提供的數值，就會被截斷。|  
|**執行逾時**|指出取消查詢之前要等候的秒數。 值為 0 表示無盡的等候，或沒有逾時。|  
|**預設會以 SQLCMD 模式開啟新查詢**|選取此核取方塊，即可以 SQLCMD 模式開啟新查詢。 只有在透過 [工具] 功能表開啟此對話方塊時，才可以看見此核取方塊。<br /><br />當您選取此選項時，請注意以下限制：<br /><br />-   資料庫引擎查詢編輯器中的 IntelliSense 會關閉。<br />-   由於查詢編輯器不會從命令列執行，所以您無法傳入命令列參數 (如變數)。<br />-   由於查詢編輯器無法回應作業系統提示，所以您必須非常小心，不要執行互動式陳述式。|  
|**SET NOCOUNT**|停止在結果中傳回指出 Transact-SQL 陳述式所影響之資料列數的訊息。 如需詳細資訊，請參閱 [SET NOCOUNT](https://go.microsoft.com/fwlink/?LinkID=238731)。|  
|**SET NOEXEC**|若為 **ON**，則告知 Microsoft® SQL Server™ 編譯 Transact-SQL 陳述式的每個批次，但不要執行它們。 若為 **OFF**，則告知 Microsoft® SQL Server™ 在編譯之後執行所有批次。如需詳細資訊，請參閱 [SET NOEXEC](https://go.microsoft.com/fwlink/?LinkId=238770)。|  
|**SET PARSEONLY**|檢查每個 Transact-SQL 陳述式的語法，且會在未編譯或執行陳述式的情況下，傳回任何錯誤訊息。 如需詳細資訊，請參閱 [SET PARSEONLY](https://go.microsoft.com/fwlink/?LinkId=238734)。|  
|**SET CONCAT_NULL_YIELDS_NULL**|控制是否將串連結果視為 Null 或空字串值。如需詳細資訊，請參閱 [SET CONCAT_NULL_YIELDS_NULL](https://go.microsoft.com/fwlink/?LinkId=238733)。|  
|**SET ARITHABORT**|查詢執行過程中發生溢位或除以零的錯誤時終止查詢。 如需詳細資訊，請參閱  [SET ARITHABORT](https://msdn.microsoft.com/library/aa259212(v=SQL.80).aspx) \(英文\)。|  
|**SET SHOWPLAN_TEXT**|使 Microsoft® SQL Server™ 不執行 Transact-SQL 陳述式。 相反地，SQL Server 會傳回如何執行這些陳述式的詳細資訊。 如需詳細資訊，請參閱 [SET SHOWPLAN_TEXT](https://go.microsoft.com/fwlink/?LinkID=238737)。|  
|**SET STATISTICS TIME**|顯示剖析、編譯和執行每個陳述式所需要的毫秒數。|  
|**SET STATISTICS IO**|使 Microsoft® SQL Server™ 顯示 Transact-SQL 陳述式所產生之磁碟活動量的相關資訊。|  
|**SET TRANSACTION ISOLATION LEVEL**|控制連接所發出之所有 Microsoft® SQL Server™ **SELECT** 陳述式的預設交易鎖定行為。 如需詳細資訊，請參閱  [SET TRANSACTION ISOLATION LEVEL](https://go.microsoft.com/fwlink/?LinkId=238730)。|  
|**SET LOCK_TIMEOUT**|指定陳述式等待鎖定釋出的毫秒數。 如需詳細資訊，請參閱 [SET LOCK_TIMEOUT](https://go.microsoft.com/fwlink/?LinkId=238747)|  
|**SET QUERY_GOVERNOR_COST_LIMIT**|覆寫目前針對目前連接所設定的值。 如需詳細資訊，請參閱 [SET QUERY_GOVERNOR_COST_LIMIT](https://go.microsoft.com/fwlink/?LinkId=238749)。|  
|**SET ANSI_DEFAULTS**|控制一組共同指定某些 SQL-92 標準行為的 Microsoft® SQL Server™ 設定。 如需詳細資訊，請參閱 [SET ANSI_DEFAULTS](https://go.microsoft.com/fwlink/?LinkId=238750)。|  
|**SET QUOTED_IDENTIFIER**|在分隔識別碼和常值字串的引號方面，使 Microsoft® SQL Server™ 遵照 SQL-92 規則。 以雙引號分隔的識別碼可能是 Transact-SQL 的保留關鍵字，或是包含通常識別碼的 Transact-SQL 語法規則不允許的字元。如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER](https://go.microsoft.com/fwlink/?LinkId=238751)。|  
|**SET ANSI_NULL_DFLT_ON**|當資料庫的 ANSI null default 選項是 false 時，改變工作階段的行為來覆寫新資料行的預設 Null 屬性。 如需詳細資訊，請參閱 [SET ANSI_NULL_DFLT_ON](https://go.microsoft.com/fwlink/?LinkID=238752)。|  
|**SET IMPLICIT_TRANSACTIONS**|若為 **ON**，則將連接設定為隱含交易模式。 若為 **OFF**，則讓連接返回自動認可交易模式。 如需詳細資訊，請參閱 [SET IMPLICIT_TRANSACTIONS](https://go.microsoft.com/fwlink/?LinkId=238753)。|  
|**SET CURSOR_CLOSE_ON_COMMIT**|控制是否要在認可交易時關閉資料指標。 如需詳細資訊，請參閱 [SET CURSOR_CLOSE_ON_COMMIT](https://go.microsoft.com/fwlink/?LinkId=238754)。|  
|**SET ANSI_PADDING**|控制資料行如何儲存比資料行的定義大小還短的值，以及如何儲存 **char**、 **varchar**、 **binary**和 **varbinary** 資料含有尾端空格的值。 如需詳細資訊，請參閱 [SET ANSI_PADDING](https://go.microsoft.com/fwlink/?LinkId=238755)。|  
|**SET ANSI_WARNINGS**|指定數個錯誤狀況的 SQL-92 標準行為。如需詳細資訊，請參閱 [SET ANSI_WARNINGS](https://go.microsoft.com/fwlink/?LinkId=238758)。|  
|**SET ANSI_NULLS**|等於 ( **=** ) 和不等於 ( **<>** ) 比較運算子搭配 Null 值一起使用時，指定符合 SQL-92 規範的行為。如需詳細資訊，請參閱 [SET ANSI_NULLS](https://go.microsoft.com/fwlink/?LinkId=238759)。|  
  
## <a name="QueryResults"></a>查詢結果  
  
|屬性|描述|  
|------------|---------------|  
|**在結果集裡包含查詢**|將查詢的文字當成結果集的一部分傳回。|  
|**複製或儲存結果時包含資料行標頭**|將結果複製到剪貼簿或儲存在檔案中時，請包含資料行標頭 (標題)。 如果您不想將結果資料儲存或複製為只有資料而沒有資料行標題，請清除此核取方塊。|  
|**執行之後捨棄結果**|在螢幕顯示已收到查詢結果後，將查詢結果捨棄以釋放記憶體。|  
|**在其他索引標籤中顯示結果**|在新的文件視窗中顯示結果集，而非在查詢文件視窗的下方顯示。|  
|**執行查詢後，切換至結果索引標籤**|自動將螢幕焦點設定為結果集。|  
|**已擷取的最大字元數**|非 XML 資料：<br /><br />輸入從 1 到 65535 的數字，來指定每個資料格中會顯示的最大字元數。 **注意：** 指定大量字元可能造成結果集內顯示的資料截斷。 每個資料格中所顯示的最大字元數，會視字型大小而定。 若傳回了大量的結果集，且此方塊中所設定的值較大，就可能會造成 SQL Server Management Studio 的可用記憶體不足而降低系統的效能。<br /><br />XML 資料：<br /><br />選取 1 MB、2 MB 或 5 MB。 選取 [無限制] 以擷取所有字元。|  
|**輸出格式**|根據預設，輸出會顯示在以空格填補結果所建立的資料行中。 其他選項包括使用逗號、索引標籤，或空格來分隔資料行。 選取 **[自訂分隔符號]** 核取方塊，即可在 **[自訂分隔符號]** 方塊中指定不同的分隔字元。|  
|**自訂分隔符號**|指定您要用來分隔資料行的字元。 只有當您在 [ **輸出格式** ] 方塊中選取了 [ **自訂分隔符號** ] 核取方塊時，才能使用此選項。|  
|**在結果集內包含資料行標頭**|如果您不希望每個資料行均標示資料行標題，請清除此核取方塊。|  
|**收到結果時捲動**|選取此核取方塊，即可將顯示焦點保持在最近傳回的底部記錄上。 清除此核取方塊，即可將作用中的顯示保持為接收到的第一組資料列。|  
|**數值靠右對齊**|選取此核取方塊，即可將數值靠資料行的右邊對齊。 此選項可讓您更輕易地檢閱具有固定小數位數的數字。|  
|**執行查詢之後捨棄結果**|在螢幕上顯示查詢結果之後即將其捨棄，以釋放記憶體。|  
|**在其他索引標籤中顯示結果**|選取此核取方塊，即可在新的文件視窗中顯示結果集，而非在查詢文件視窗的下方顯示。|  
|**執行查詢後，切換至結果索引標籤**|按一下以自動將螢幕焦點設定為結果集。|  
|**每個資料行中顯示的最大字元數**|這個值預設為 256。 增加這個值即可顯示較大的結果集而不會截斷。|  
|**重設為預設值**|將此頁面上的所有值重設為原始預設值。|  
  
