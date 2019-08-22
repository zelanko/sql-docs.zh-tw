---
title: Oracle 來源 | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7444c5710663eb601aa3c8ce2287869a8083f814
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553207"
---
# <a name="oracle-source"></a>Oracle 來源

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Oracle 來源會使用下列模式從 Oracle Database 擷取資料：

- 資料表或檢視。

- SQL 陳述式的結果。

來源會使用 Oracle 連線管理員來連線到 Oracle 來源。 如需詳細資訊，請參閱 [Oracle 連線管理員](oracle-connection-manager.md)。

## <a name="error-output"></a>錯誤輸出

錯誤輸出包含下列欄：  

- **錯誤碼**：代表目前錯誤之錯誤類型的數字。 錯誤碼可能是來自：
    - Oracle 伺服器。 請參閱 Oracle 資料庫文件中的詳細錯誤描述。
    - SSIS 執行階段。 如需 SSIS 錯誤碼清單，請參閱＜SSIS 錯誤碼和訊息參考＞。
- **錯誤資料行**：導致轉換錯誤的來源欄編號。

- **錯誤資料欄**：造成錯誤的資料。

Oracle 來源會在錯誤輸出中傳回載入和擷取程序期間發生的錯誤。 如需詳細資訊，請參閱 [Oracle 來源編輯器 (錯誤輸出頁面)](#oracle-source-editor-error-output-page)。

## <a name="troubleshooting-the-oracle-source"></a>針對 Oracle 來源進行疑難排解

您可以記錄 Oracle 來源對 Oracle 資料來源進行的 ODBC 呼叫，以針對資料匯出進行疑難排解。 若要記錄 ODBC 來源對 Oracle 資料來源進行的 ODBC 呼叫，請啟用 ODBC 驅動程式管理員追蹤。 如需詳細資訊，請參閱 Microsoft 文件集＜如何使用 ODBC 資料來源管理員產生 ODBC 追蹤＞。 

## <a name="oracle-source-custom-properties"></a>Oracle 來源自訂屬性

Oracle 來源的自訂屬性如下所示。 所有屬性都是可讀寫的。

|屬性名稱|資料類型|描述|
|:-|:-|:-|
|AccessMode|整數 (列舉)|用來存取資料庫的模式。 可能的值為**資料表名稱**與 **SQL 命令**。 預設值為**資料表名稱**。|
|BatchSize|整數|大量載入的批次大小。 這是當做陣列擷取的記錄數目。 <br>這個屬性僅由 [進階編輯器]  設定|
|DefaultCodePage|整數|當資料來源沒有字碼頁資訊時，所要使用的字碼頁。 <br>這個屬性僅由 [進階編輯器]  設定。|
|PreFetchCount|整數|預先提取 (查閱) 資料列的數目。 <br>這個屬性僅由 [進階編輯器]  設定。|
|SqlCommand|字串|當 AccessMode 設為 [SQL 命令] 時要執行的 SQL 命令。|
|TableName|字串|當 AccessMode 設定為 [資料表名稱] 時所使用之資料的資料表名稱。|

## <a name="configuring-the-oracle-source"></a>設定 Oracle 來源

您可以透過程式設計方式或 SSIS 設計工具來設定 Oracle 來源。

下圖中顯示 [Oracle 來源編輯器]。 它包含 [連線管理員] 頁面、[資料行] 頁面和 [錯誤輸出] 頁面。

如需詳細資訊，請參閱下列其中一節：

- [Oracle 來源編輯器 (連線管理員頁面)](#oracle-source-editor-connection-manager-page)
- [Oracle 來源編輯器 (資料行頁面)](#oracle-source-editor-columns-page)
- [Oracle 來源編輯器 (錯誤輸出頁面)](#oracle-source-editor-error-output-page)

![](media/oracle-source.png)

[進階編輯器]  對話方塊包含能以程式設計方式設定的屬性。

若要開啟 [進階編輯器]  對話方塊：

- 在 Integration Services 專案的 [資料流程]  畫面中，以滑鼠右鍵按一下 Oracle 來源，然後選取 [顯示進階編輯器]  。

如需有關可在 [進階編輯器]  對話方塊中設定之屬性的詳細資訊，請參閱 [Oracle 來源自訂屬性](#oracle-source-custom-properties)。

## <a name="oracle-source-editor-connection-manager-page"></a>Oracle 來源編輯器 (連線管理員頁面)

在 [連線管理員]  頁面上，[Oracle 來源編輯器]  對話方塊中是用來從資料庫中選取 Oracle Database 作為來源、資料表或檢視。

**開啟 Oracle 來源編輯器的連線管理員頁面**

- 在 SQL Server Data Tools 中，開啟具有 Oracle 來源的 SQL Server Integration Services (SSIS) 套件。

- 在 [資料流程] 索引標籤上，按兩下 Oracle 來源。
### <a name="options"></a>選項

**[ODBC 目的地編輯器]**

從清單中選取現有的連線管理員，或按一下 [新增]  來建立新的 Oracle 連線管理員。

**新增**

按一下 [新增]  。 [Oracle 連線管理員編輯器]  對話方塊隨即開啟，讓您能夠建立新的連線管理員。

**資料存取模式**

選取從來源中選取資料的方法。 下表將顯示這些選項：

|選項|描述|
|:-|:-|
|資料表或檢視|從 Oracle 資料來源中的資料表或檢視表擷取資料。 選取此選項後，從清單中選取可用的資料表或檢視，以取得**資料表或檢視的名稱**。|
|SQL (命令)|使用 SQL 查詢從 Oracle 資料來源擷取資料。 當選取此選項時，請用下列其中一種方式輸入查詢： <br>在 [SQL 命令文字]  欄位中輸入 SQL 查詢的文字。 <br>按一下 [瀏覽]  ，從文字檔載入 SQL 查詢。 <br>按一下 [剖析查詢]  驗證查詢文字的語法。|

**預覽**

按一下 [預覽]  ，最多可檢視從所選取之資料表或檢視表中擷取的前 200 個資料列。

## <a name="oracle-source-editor-columns-page"></a>Oracle 來源編輯器 (資料行頁面)

在 [資料行]  頁面上，可使用 [Oracle 來源編輯器]  對話方塊將輸出資料行對應至每個外部 (來源) 資料行。

**開啟 Oracle 來源編輯器的資料行頁面**

- 在 SQL Server Data Tools 中，開啟具有 Oracle 來源的 SQL Server Integration Services (SSIS) 套件。

- 在 [資料流程] 索引標籤上，按兩下 Oracle 來源。

- 在 [Oracle 來源編輯器]中，按一下 [資料行]。

### <a name="options"></a>選項

**可用的外部資料行**

可用的外部資料行清單，您可以選取這些資料行，依選取的順序加入 [外部資料行]  清單。 無法使用此資料表來加入或刪除資料行。

選取 [全選]  核取方塊以選取所有資料行。

**外部資料行**

您所選取的外部 (來源) 資料行會依序列出。
若要變更順序，請先清除 [可用的外部資料行] 清單，然後以不同的順序選取資料行。

**輸出資料行**

選取之外部 (來源) 資料行的名稱是預設的輸出名稱。 雖然您可以輸入任何唯一名稱。
> [!NOTE]
>
>如果有資料行具有不支援的資料類型，將會出現警告，指出不支援資料類型，而且會從對應資料行中移除相關的資料行。

## <a name="oracle-source-editor-error-output-page"></a>Oracle 來源編輯器 (錯誤輸出頁面)

使用 [Oracle 來源編輯器]  對話方塊的 [錯誤輸出]  頁面，即可選取錯誤處理選項。

**開啟 Oracle 來源編輯器的錯誤輸出頁面**

- 在 SQL Server Data Tools 中，開啟具有 Oracle 來源的 SQL Server Integration Services (SSIS) 套件。

- 在 [資料流程] 索引標籤上，按兩下 Oracle 來源。

- 在 [Oracle 來源編輯器] 中，按一下 [錯誤輸出]。

### <a name="options"></a>選項

**錯誤行為**

選取 Oracle 來源應該如何處理流程中的錯誤：忽略失敗、重新導向資料列，或使元件失效。
**相關小節**：[資料中的錯誤處理](https://docs.microsoft.com/en-us/sql/integration-services/data-flow/error-handling-in-data?view=sql-server-2017)

**截斷**

選取 Oracle 來源應該如何處理流程中的截斷：忽略失敗、重新導向資料列，或使元件失效。

## <a name="next-steps"></a>後續步驟

- 設定 [Oracle 目的地](oracle-destination.md)。
- 如有任何疑問，請瀏覽 [TechCommunity](https://aka.ms/AA5u35j) \(英文\)。
