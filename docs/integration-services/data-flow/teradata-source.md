---
description: 連線到 Teradata 來源
title: 連線到 Teradata 來源 | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5b4e64c2d7ada0db923f1aa623576e7b2994d8e6
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194700"
---
# <a name="connect-to-the-teradata-source"></a>連線到 Teradata 來源

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Teradata 來源使用下列方法從 Teradata 資料庫擷取資料：
- 資料表或檢視表。
- SQL 陳述式的結果。

來源使用 Teradata 連線管理員連線到 Teradata 來源。 如需詳細資訊，請參閱[使用 Teradata 連線管理員](teradata-connection-manager.md)。

## <a name="troubleshoot-the-teradata-source"></a>針對 Teradata 來源進行疑難排解

您可以記錄 Teradata 來源對 Teradata 平行傳輸器 (TPT) API 所執行的呼叫。 若要這樣做，請啟用套件記錄，然後在套件層級選取 [診斷]**** 事件。

您可以透過啟用開放式資料庫連接 (ODBC) 驅動程式管理員追蹤，記錄 Teradada 來源對 Teradata ODBC 驅動程式所執行的 ODBC 呼叫。 如需詳細資訊，請參閱[如何使用 ODBC 資料來源系統管理員產生 ODBC 追蹤](../../odbc/admin/setting-tracing-options.md) \(部分機器翻譯\)。

## <a name="parallelism"></a>平行處理原則

Teradata 來源支援平行處理原則，亦即匯出作業可以同時存取相同資料表或不同資料表。 稱為 `MaxLoadTasks` 的資料庫變數會設定可同時執行的匯出作業數目限制。 您可以使用 `MaxLoadTasks` 變數來定義此最大數目。

## <a name="teradata-source-custom-properties"></a>Teradata 來源自訂屬性

下表列出 Teradata 來源的自訂屬性。 所有屬性都是可讀寫的。

|屬性名稱|資料類型|描述|
|:-|:-|:-|
|AccessMode|整數 (列舉)|用來存取資料庫的模式。 可能的值為*資料表名稱*與 *SQL 命令*。 預設值為「資料表名稱」**。|
|BlockSize|整數|將資料傳回給用戶端時所使用的區塊大小 (以位元組為單位)。 預設值為 1048576 (1 MB)。 最小值為 256 個位元組。 最大值為 16775168 個位元組。<br> 這個屬性位於 [進階編輯器]**** 窗格中。|
|BufferMaxSize|整數|GetBuffer 函數所傳回資料緩衝區的大小上限。 這個大小必須能容納至少一個資料列，包括資料列標頭、實際資料列，以及緩衝區結尾。 資料緩衝區的預設總大小上限為 16775552 個位元組。 <br>如需詳細資訊，請參閱[使用 GetBuffer 從 Teradata 資料庫匯出資料](https://docs.teradata.com/reader/TvVKKmxaBAoyETJZD8zz_g/oaxiwNJmnCa6UctY4k498w) \(英文\)。|
|BufferMode|Boolean|預設值為 [True]。 如果使用 PutBuffer 功能，值必須為 *True*。 這個屬性位於 [進階編輯器]**** 窗格中。|
|DataEncryption|Boolean|預設值為 [False]。 若值為 *True*，則會使用完整安全性加密。|
|DefaultCodePage|整數|當資料來源沒有字碼頁資訊時，所要使用的字碼頁。 這個屬性位於 [進階編輯器]**** 窗格中。|
|DetailedTracingLevel|整數 (列舉)|選取下列其中一個選項以進行進階追蹤： <br> *Off*：不使用進階記錄。 <br> *一般*：記錄驅動程式特定的活動一般追蹤。 <br> *CLI*：記錄 CLIv2 相關的活動追蹤。 <br> *通知方法*：記錄通知功能相關的活動追蹤。 <br> *通用程式庫*：記錄 Opcommon 程式庫活動追蹤。 <br> *全部*：記錄所有先前的活動追蹤。 <br> 進階追蹤記錄檔定義於 `DetailedTracingFile` 屬性中。 <br> 如果選項不為 *Off*，則您必須設定 `DetailedTracingFile` 屬性。 這個屬性位於 [進階編輯器]**** 窗格中。|
|DetailedTracingFile|String|當 *DetailedTracingLevel* 不為 *Off* 時，會自動產生記錄檔路徑。 這個屬性位於 [進階編輯器]**** 窗格中。|
|DiscardLargeRow|Boolean|預設值為 [False]。 若值為 *True*，則捨棄大型資料列 (大於 64 KB)。|
|ExtendedStringColumnsAllocation|Boolean|若值為 *True*，則會使用「最大傳輸字元配置因數」**。 <br> 如果 Teradata 資料庫的 `Export Width Table ID` 屬性設定為 [最大的預設值]**，則此值應該設定為 *True*。 <br> 預設值為 [False]。|
|JobMaxRowSize|整數|可以支援最大資料列大小。 如果 `DiscardLargeRow` 值為 *True*，則需要此值。<br>有效值： <br>*64* (預設值)：可以支援 2 個位元組的資料列長度。 <br>*1024*：可以支援 4 個位元組的資料列長度。|
|MaxSessions|整數|已登入工作階段的數目上限。 這個值必須大於一。 預設值為每個可用存取模組處理器 (AMP) 的一個工作階段。|
|MinSessions|整數|已登入工作階段的數目下限。 這個值必須大於一。 預設值為每個可用 AMP 的一個工作階段。|
|QueryBandSessInfo|Varchar|連接字串格式的使用者定義工作階段型查詢頻帶運算式。 您可以使用此屬性進行退款監視和治理。 這個屬性位於 [進階編輯器]**** 窗格中。|
|SpoolMode|Varchar|有效值為： <br>*Spool*：使用預設值 *Spool*。 <br> *NoSpool*：不使用 *Spool*。 只有當資料庫伺服器 (DBS) 支援 *NoSpool* 時，這個值才有效。 <br>  *NoSpoolOnly*：在任何情況下都不使用 *Spool*。 如果 DBS 不支援 *NoSpool*，作業將會因錯誤而終止。|
|SqlCommand|String|當 `AccessMode` 設定為 [SQL 命令]** 時要執行的 SQL 命令。|
|TableName|String|當 `AccessMode` 設定為 [資料表名稱]** 時，所要使用包含資料的資料表名稱。|
|TenacityHours|整數|當已在執行載入/匯出作業為最大數目時，TPT 驅動程式嘗試登入的小時數。 預設值為「4 小時」**。 這個屬性位於 [進階編輯器]**** 窗格中。|
|TenacitySleep|整數|當 TPT 驅動程式達到此分鐘數限制時，便暫停嘗試登入。 限制是由 `MaxSessions` 和 `TenacityHours` 屬性定義。 預設值為 6 分鐘。 這個屬性位於 [進階編輯器]**** 窗格中。|
|UnicodePassThrough|Boolean|*Off* (預設值)：停用 Unicode 傳遞。 <br>*於*：啟用 Unicode 穿通。|

## <a name="configure-the-teradata-source"></a>設定 Teradata 來源

您可以用程式設計方式或使用 SQL Server Integration Services (SSIS) 設計工具來設定 Teradata 來源。

下列影像顯示 [Teradata 來源編輯器]**** 窗格。 如需詳細資訊，請移至下列每一個 Teradata 來源編輯器小節：

- [[連線管理員] 窗格](#the-connection-manager-pane)
- [[資料行] 窗格](#the-columns-pane)
- [[錯誤輸出] 窗格](#the-error-output-pane)

![Teradata 來源編輯器](media/teradata-source.png)

[進階編輯器]**** 窗格包含能以程式設計方式設定的屬性。 開啟窗格：
- 在 Integration Services 專案的 [資料流程]**** 頁面上，以滑鼠右鍵按一下 Oracle 來源，然後選取 [顯示進階編輯器]****。

如需可在 [進階編輯器]**** 窗格中設定之屬性的詳細資訊，請參閱 [Teradata 來源自訂屬性](#teradata-source-custom-properties)。

## <a name="the-connection-manager-pane"></a>[連線管理員] 窗格

使用 [連線管理員]**** 窗格選取來源的 Teradata 連線管理員執行個體。 您也可以在此窗格中，從資料庫選取資料表或檢視表。 開啟窗格：

1. 在 SQL Server Data Tools 中，開啟包含 Teradata 來源的 SSIS 套件。

1. 在 [資料流程]**** 索引標籤中，按兩下 Teradata 來源。

1. 在 Teradata 來源編輯器中，選取 [連線管理員]**** 索引標籤。

### <a name="options"></a>選項。

**[ODBC 目的地編輯器]**

* 從清單中選取現有的連線管理員，或選取 [新增]**** 以建立新的 Teradata 連線管理員執行個體。

**新增**

* 選取 [新增]。 [Teradata 連線管理員編輯器]**** 窗格隨即開啟。 您可以從此窗格建立新的連線管理員。

**資料存取模式**

* 選擇從來源選取資料的方法。 下表將顯示這些選項：

    |選項|描述|
    |:-|:-|
    |資料表名稱 - TPT 匯出|從 Teradata 資料來源中的資料表或檢視表擷取資料。 選取此選項後，從清單中選取可用的資料表或檢視，以取得**資料表或檢視的名稱**。|
    |SQL 命令 - TPT 匯出|使用 SQL 查詢從 Teradata 資料來源擷取資料。 當選取此選項時，請用下列其中一種方式輸入查詢： <ul><li>在 **[SQL 命令文字]** 欄位中輸入 SQL 查詢的文字。</li><li>選取 [瀏覽]**** 以從文字檔載入 SQL 查詢。</li><li>選取 [剖析查詢]**** 以驗證查詢文字的語法。</li></ul>|

**預覽**

* 選取 [預覽]****，最多可檢視從所選取資料表或檢視表中擷取的前 200 個資料列。

## <a name="the-columns-pane"></a>[資料行] 窗格

使用 [資料行]**** 窗格可以將輸出資料行對應至每個外部 (來源) 資料行。 開啟窗格：

1. 在 SQL Server Data Tools 中，開啟包含 Teradata 來源的 SSIS 套件。

1. 在 [資料流程]**** 索引標籤中，按兩下 Teradata 來源。

1. 在 Teradata 來源編輯器中，選取 [資料行]**** 索引標籤。

### <a name="options"></a>選項。

**可用的外部資料行**

您可以選取下表列出的可用外部資料行，將它新增到 [外部資料行]**** 清單。 您可以依照您選擇的順序列出資料行。 您無法使用此資料表來新增或刪除資料行。

* 若要選擇所有資料行，請選取 [全選]**** 核取方塊。

**外部資料行**

您所選取的外部 (來源) 資料行會依序列出。 若要變更順序，請先清除 [可用的外部資料行]**** 清單，然後以不同順序選取資料行。

**輸出資料行**

雖然所選外部 (來源) 資料行的名稱是預設輸出名稱，您也可以輸入任何唯一名稱。

>[!NOTE]
>>如果有資料行包含不支援的資料類型，您會收到警告，顯示那些不支援的資料類型，並將相關的資料行從對應資料行中移除。

## <a name="the-error-output-pane"></a>[錯誤輸出] 窗格

使用 [錯誤輸出]**** 窗格可選取錯誤處理選項。 開啟窗格：

1. 在 SQL Server Data Tools 中，開啟包含 Teradata 來源的 SSIS 套件。

1. 在 [資料流程]**** 索引標籤中，按兩下 Teradata 來源。

1. 在 Teradata 來源編輯器中，選取 [錯誤輸出]**** 索引標籤。

### <a name="options"></a>選項。

**錯誤行為**

* 選取 Teradata 來源應該如何處理流程中的錯誤： 
  * 忽略失敗
  * 重新導向資料列
  * 使元件失效

**相關主題**：請參閱[資料中的錯誤處理](error-handling-in-data.md)。

**截斷**

* 選取 Teradata 來源應該如何處理流程中的截斷： 
  * 忽略失敗
  * 重新導向資料列
  * 使元件失效

## <a name="next-steps"></a>後續步驟

- 設定 [Teradata 目的地](teradata-destination.md)。
- 如有任何疑問，請瀏覽[技術社群](https://aka.ms/AA6iwdw) \(英文\)。