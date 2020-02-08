---
title: Teradata 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d016a1fed3a60df78a02242a2f42e46cf7184553
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75245096"
---
# <a name="teradata-destination"></a>Teradata 目的地

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Teradata 目的地可將資料大量載入 Teradata 資料庫中。

此目的地使用 Teradata 連線管理員連線到資料來源。 如需詳細資訊，請參閱 [Teradata 連線管理員](teradata-connection-manager.md)。

## <a name="load-options"></a>載入選項

Teradata 目的地支援兩種資料載入模式：

- **TPT 資料流**：此模式使用 TPT API 資料流運算子 (Teradata TPump 通訊協定)。

- **TPT Load** (快速大量載入)：此模式使用 TPT API 載入運算子 (Teradata FastLoad 通訊協定) 以快速地大量載入。

快速載入模式的限制如下：

- Teradata 資料庫的工作階段限制，取決於第一個遇到的任一下列因素：
    - 使用 SESSIONS 命令設定的工作階段限制
    - 每個 AMP 中，一個工作階段的 Teradata 資料庫限制
    - 每個應用程式中，平台對工作階段最大數目的限制：由通訊處理器 (COP) 介面軟體檔案 (CLISPB.DAT) 中的 MaxSess 變數所定義。 您可以使用 TDP SET MAXSESSIONS 命令來指定平台限制。 預設限制為伺服器 MAXSESS。

- 不支援聯結索引。
- 不支援對目標資料表的外部索引鍵參考。
- 不支援以次要索引定義的目標資料表。

如需有關 Teradata 快速載入限制的詳細資訊，請參閱 Teradata 的快速載入參考。

您可以在 [Teradata 目的地編輯器 (連線管理員頁面)](#teradata-destination-editor-connection-manager-page) 中設定模式。

## <a name="error-handling"></a>錯誤處理

載入處理期間傳回的錯誤會寫入至載入處理期間鎖定的暫存錯誤資料表。
您可於進階編輯器中的 [最大錯誤數目 (MaxErrors)]  屬性設定可寫入這些資料表的錯誤數目上限。

如果錯誤數目上限大於零，則會產生具有唯一名稱的錯誤資料表，並將資訊訊息輸出至封裝記錄檔。 錯誤則會透過標準 SSIS 元件錯誤輸出進行擷取。

載入處理完成後，就會卸除暫存資料表。 如果 Teradata 目的地無法讀取時態表，除非您已選取 [永遠卸除錯誤資料表]  屬性，否則將不會卸除這些資料表。  如果載入處理在完成前就停止，您可以視需要手動卸除這些資料表。 這些資料表與目的地資料表位於相同的資料庫中。

當達到**最大錯誤數目**時，目標資料表的狀態會取決於您所使用的模式。

- 在快速載入模式中，無法使用目標資料表。 若要再次執行，您必須截斷或卸除目標資料表，然後重新建立一次。 不支援復原。
- 在 TPT 資料流運算子模式中，Teradata 目的地會透過緩衝的資料列機制來執行。 如果作業失敗，則在失敗時完成的所有變更 (已傳送緩衝區) 將永遠存在於目標資料表中。 無法復原， 且會卸除錯誤資料表。

Teradata 目的地含有錯誤輸出。 如需詳細資訊，請參閱 [Teradata 目的地編輯器 (錯誤輸出頁面)](#teradata-destination-editor-error-output-page)。

## <a name="parallelism"></a>平行處理原則

平行處理原則在快速載入模式中受到限制，多個獨立的快速載入作業無法同時存取相同的資料表。 同時，可並行的快速載入作業數目亦會受限於資料庫變數 **MaxLoadTasks**。

TPT 資料流模式中則沒有平行處理原則的限制。 您可以針對相同的資料表同時執行多個 Teradata 目的地，但這可能會降低每個 Teradata 的效能。 如需詳細資訊，請參閱 Teradata 文件。

## <a name="troubleshooting-the-teradata-destination"></a>針對 Teradata 目的地進行疑難排解

您可以記錄 Teradata 來源對 Teradata 平行傳輸器 API (TPT API) 所執行的呼叫。 您可以啟用封裝記錄，然後在封裝層級選取 [診斷]  事件來記錄呼叫。

您可以藉由啟用 ODBC 驅動程式管理員追蹤，記錄 Teradada 來源對 Teradata ODBC 驅動程式所執行的 ODBC 呼叫。 如需詳細資訊，請參閱 Microsoft 文件集＜如何使用 ODBC 資料來源管理員產生 ODBC 追蹤＞。 

## <a name="teradata-destination-custom-properties"></a>Teradata 目的地自訂屬性

下表說明 Teradata 目的地的自訂屬性。 所有屬性都是可讀寫的。

|屬性名稱|資料類型|描述|
|:-|:-|:-|
|AlwaysDropErrorTable|Boolean|預設值為 **False**。 若設定為 **True**，則即使 Teradata 目的地讀取失敗亦會卸除錯誤資料表。|
|ArraySupport|Boolean|預設值為 **True**。 若設定為 **True**，則 DML 群組會使用 ArraySupport。 僅適用於 TPT 資料流。 這個屬性位於 [進階編輯器]  中。|
|緩衝區|整數|要增加的要求緩衝區數目，可以將值設定為 2 到 64。 僅適用於 TPT 資料流。 這個屬性位於 [進階編輯器]  中。|
|BufferMode|Boolean|預設值為 **True**。 如果使用 PutBuffer 功能，則必須設定為 **True**。 這個屬性位於 [進階編輯器]  中。|
|BufferSize|整數|用於傳送載入包裹的輸出緩衝區大小 (以 KB 為單位)。 預設值為 1024。 僅適用於 TPT 載入。 這個屬性位於 [進階編輯器]  中。|
|DataEncryption|Boolean|預設值為 **False**。 若設定為 **True**，則會使用完整安全性加密。|
|DefaultCodePage|整數|當資料來源沒有字碼頁資訊時，所要使用的字碼頁。 <br>**注意**：這個屬性位於 [進階編輯器]  中。|
|DetailedTracingLevel|整數 (列舉)|選取下列其中一個選項以進行進階追蹤： <br> **Off**：不使用進階記錄。 <br> **一般**：記錄驅動程式特定的活動一般追蹤。 <br> **CLI**：記錄 CLIv2 相關的活動追蹤。 <br> **通知方法**：記錄通知功能相關的活動追蹤。 <br> **通用程式庫**：記錄 Opcommon 程式庫活動追蹤。 <br> **全部**：記錄以上所有的活動追蹤。 <br> 進階追蹤記錄檔定義於 **DetailedTracingFile** 屬性中。 <br> 如果選項不為 Off，則您必須設定 **DetailedTracingFile** 屬性。 <br> 這個屬性位於 [進階編輯器]  中。|
|DetailedTracingFile|String|當 **DetailedTracingLevel** 不為 **Off** 時，則會自動產生的記錄檔路徑。 這個屬性位於 [進階編輯器]  中。|
|DiscardLargeRow|Boolean|預設值為 **False**。 若設定為 **True**，則捨棄大型資料列 (大於 64K)|
|ErrorTableName|String|錯誤資料表名稱。 預設值為目標資料表名稱|
|ExtendedStringColumnsAllocation|Boolean|若設定為 **True**，則會使用**最大傳輸字元配置因數**。 <br> 如果 Teradata 資料庫的 [匯出寬度資料表識別碼]  屬性設定為 [最大的預設值]  ，則此值應該設定為 **True**。 <br> 預設值為 **False**。|
|FastLoad|Boolean|若設定為 **True**，則會使用快速載入。 預設值為 **false**。 這項功能也可以在 [Teradata 目的地編輯器 (連線管理員頁面)](#teradata-destination-editor-connection-manager-page) 中設定。|
|MaxErrors|整數|停止資料流程之前可以發生的錯誤數目。 預設值為 **0**，表示沒有錯誤數目的限制。<br> 如果已在 [錯誤處理]  頁面中選取 [重新導向流程]  。 在達到錯誤數目限制之前，所有錯誤都會在錯誤輸出中傳回。 如需詳細資訊，請參閱 [Teradata 目的地編輯器 (錯誤輸出頁面)](#teradata-destination-editor-error-output-page)。|
|MaxSessions|整數|已登入的工作階段數目上限。 這個值必須大於一。 預設值為每個可用 AMP 的一個工作階段。|
|MinSessions|整數|已登入的工作階段數目下限。 這個值必須大於一。 預設值為每個可用 AMP 的一個工作階段。|
|Pack|整數|要壓縮為多重陳述式要求的陳述式數目。 預設值為 20，允許的上限為 2400。 僅適用於 TPT 資料流。 這個屬性位於 [進階編輯器]  中。|
|PackMaximum|Boolean|若設定為 **True**，則會自動判斷目前資料流作業的最大壓縮因素。 僅適用於 TPT 資料流。 這個屬性位於 [進階編輯器]  中。|
|QueryBandSessInfo|Varchar|為使用者定義、並以工作階段為基礎的查詢頻帶運算式，可讓您進行退款監視和治理。 這個屬性必須為連接字串格式。 這個屬性位於 [進階編輯器]  中。|
|ReplicationOveride|整數 (列舉)|選項： <br> **預設值**：不將 SET SESSION OVERRIDE REPLICATION 陳述式傳送到資料庫。 使用資料庫的預設設定。 <br> **於**：覆寫一般複寫服務控制項。 <br> **Off**：使用一般複寫服務控制項。 <br> 這個屬性只適用於 TPT 資料流。 <br> 這個屬性位於 [進階編輯器]  中。|
|Robust|Boolean|若設定為 **True**，則使用強固重新啟動邏輯以復原並重新啟動作業。 這個屬性只適用於 **TPT 資料流**。 這個屬性位於 [進階編輯器]  中。|
|TableName|String|包含所要使用之資料的資料表名稱。|
|TenacityHours|整數|當已在執行載入/匯出作業的最大數目時，TPT 驅動程式嘗試登入的小時數。 預設值為 4 小時。 這個屬性位於 [進階編輯器]  中|
|TenacitySleep|整數|在達到限制時，TPT 驅動程式在嘗試登入前暫停的分鐘數。 限制是由 **MaxSessions** 與 **TenacityHours** 屬性所定義。 預設值為 6 分鐘。 這個屬性位於 [進階編輯器]  中|
|UnicodePassThrough|Boolean|Off (預設值)：停用 Unicode 通過。 <br>On：啟用 Unicode 通過。|

## <a name="configuring-the-teradata-destination"></a>設定 Teradata 目的地

Teradata 目的地可以透過程式設計的方式或 SSIS 設計工具來設定。

下圖中顯示 [Teradata 目的地編輯器]。 它包含 [連線管理員] 頁面、[對應] 頁面與 [錯誤輸出] 頁面。

如需詳細資訊，請參閱下列其中一個主題：

- [Teradata 目的地編輯器 (連線管理員頁面)](#teradata-destination-editor-connection-manager-page)
- [Teradata 目的地編輯器 (對應頁面)](#teradata-destination-editor-mappings-page)
- [Teradata 目的地編輯器 (錯誤輸出頁面)](#teradata-destination-editor-error-output-page)

![目的地編輯器](media/teradata-destination.png)

**[進階編輯器]** 對話方塊包含可以程式設計方式設定的屬性。
若要開啟 **[進階編輯器]** 對話方塊：

- 在 Integration Services 專案的 [資料流程]  畫面中，以滑鼠右鍵按一下 [Teradata 目的地]，然後選取 [顯示進階編輯器]  。

如需有關可在 [進階編輯器] 對話方塊中設定之屬性的詳細資訊，請參閱 [Teradata 目的地自訂屬性](#teradata-destination-custom-properties)。

## <a name="teradata-destination-editor-connection-manager-page"></a>Teradata 目的地編輯器 (連線管理員頁面)

使用 [Teradata 目的地編輯器]  對話方塊的 [連線管理員]  頁面，即可選取目的地的 Teradata 連線管理員。 這個頁面也可以讓您從資料庫中選取資料表或檢視。

若要開啟Teradata 目的地編輯器連線管理員頁面

- 在 SQL Server Data Tools 中，開啟具有 Teradata 目的地的 SQL Server Integration Services (SSIS) 套件。

- 在 [資料流程] 索引標籤中，按兩下 [Teradata 目的地]。

- 在 [Teradata 目的地編輯器] 中，按一下 [連線管理員]。

### <a name="options"></a>選項。

**[ODBC 目的地編輯器]**

從清單中選取現有的連線管理員，或按一下 [新增]  以建立新的 Teradata 連線管理員。

**新增**

按一下 **[新增]** 。 [Teradata 連線管理員編輯器]  對話方塊隨即開啟，讓您能夠建立新的連線管理員。

**資料存取模式**

選取從來源中選取資料的方法。 下表將顯示這些選項：

|選項|描述|
|:-|:-|
|資料表名稱 - TPT 資料流|使用 TPT 資料流運算子的累加模式。 <br>**資料表或檢視表的名稱**：從清單中選取現有的資料表或檢視表。 這份清單只會顯示前 1000 個資料表。 您可以輸入資料表名稱前置詞，或使用名稱的任何部分加上 (*) 萬用字元，以列出您要使用的資料表。|
|資料表名稱 - TPL 載入|使用 TPT API 載入運算子 (Teradata FastLoad 通訊協定) 的快速 (直接路徑) 載入模式，其要求目標資料表必須是空的。 <br>**資料表或檢視表的名稱**：從清單中選取現有的資料表或檢視表。 這份清單只會顯示前 1000 個資料表。 您可以輸入資料表名稱前置詞，或使用名稱的任何部分加上 (*) 萬用字元，以列出您要使用的資料表。|

**資料加密**，啟用資料加密的核取方塊。 預設為未選取。

**永遠卸除錯誤資料表**，將錯誤資料表置放於所有執行個體中的核取方塊。

**錯誤資料表**，寫入錯誤之資料表的名稱。

**最小工作階段數目**，已登入的工作階段數目下限。 預設值為每個可用 AMP 的一個工作階段。 這個值必須大於 1。

**最大工作階段數目**，已登入的工作階段數目上限。 預設值為每個可用 AMP 的一個工作階段。 這個值必須大於 1。

**最大錯誤數目**，在停止或重新導向資料流之前，可傳回的錯誤數目上限。 

## <a name="teradata-destination-editor-mappings-page"></a>Teradata 目的地編輯器 (對應頁面)

使用 [Teradata 目的地編輯器]  對話方塊的 [對應]  頁面，將輸入資料行對應至目的地資料行。

若要開啟 Teradata 目的地編輯器對應頁面

- 在 SQL Server Data Tools 中，開啟具有 Teradata 目的地的 SQL Server Integration Services (SSIS) 套件。

- 在 [資料流程] 索引標籤中，按兩下 [Teradata 目的地]。

- 在 [Teradata 目的地編輯器] 中，按一下 [對應]。

### <a name="options"></a>選項。

**可用的輸入資料行**

可用輸入資料行的清單。 將輸入資料行拖放至可用的目的地資料行，即可對應資料行。

**可用的目的地資料行**

可用目的地資料行的清單。 將目的地資料行拖放至可用的輸入資料行，即可對應資料行。

**輸入資料行**

檢視所選取的輸入資料行。 您可以選取 [< 忽略 >]  移除對應，將資料行從輸出排除。

**目的地資料行**

檢視所有可用的目的地資料行，包括對應和取消對應的資料行。

>[!NOTE]
>
>具有不支援之資料類型的資料行將從具有警告的對應中刪除。

## <a name="teradata-destination-editor-error-output-page"></a>Teradata 目的地編輯器 (錯誤輸出頁面)
使用 [Teradata 目的地編輯器] 對話方塊的 [錯誤輸出] 頁面，以選取錯誤處理選項。

**若要開啟 Teradata 目的地編輯器錯誤輸出頁面**

- 在 SQL Server Data Tools 中，開啟具有 Teradata 目的地的 SQL Server Integration Services (SSIS) 套件。

- 在 [資料流程] 索引標籤中，按兩下 [Teradata 目的地]。

- 在 [Teradata 目的地編輯器] 中，按一下 [錯誤輸出]。

### <a name="options"></a>選項。

**錯誤行為**

選取 Teradata 目的地應該如何處理流程中的錯誤：忽略失敗、重新導向資料列，或使元件失效。

**相關主題**：[資料中的錯誤處理](https://docs.microsoft.com/sql/integration-services/data-flow/error-handling-in-data?view=sql-server-2017)

**截斷**

選取 Teradata 目的地應該如何處理流程中的截斷：忽略失敗、重新導向資料列，或使元件失效。

## <a name="next-steps"></a>後續步驟

- 設定 [Teradata 連線管理員](teradata-connection-manager.md)
- 設定 [Teradata 來源](teradata-source.md)
- 設定 [Teradata 目的地](teradata-destination.md)
- 如有任何疑問，請瀏覽[技術社群](https://aka.ms/AA6iwdw)。
