---
description: Oracle 目的地
title: Oracle 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5c1bb607326233dccdafa8fc57e3ce9d32cf20c9
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "92195360"
---
# <a name="oracle-destination"></a>Oracle 目的地

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Oracle 目的地會將資料大量載入 Oracle Database。

目的地使用 Oracle 連線管理員來連線到資料來源。 如需詳細資訊，請參閱 [Oracle 連線管理員](oracle-connection-manager.md)。

Oracle 目的地包含輸入資料行與目的地資料來源中資料行之間的對應。 您不一定要將輸入資料行對應到所有目的地資料行，但因目的地資料行屬性的不同，如果輸入資料行未對應到目的地資料行，則可能發生錯誤。 例如，如果目的地資料行不允許 Null 值，則輸入資料行必須對應到該資料行。 此外，如果輸入資料與目的地資料行類型不相容，在執行階段會發生錯誤。 根據錯誤行為設定，錯誤將會被忽略、導致失敗，或者資料列會重新導向至錯誤輸出。

Oracle 目的地具有一個規則輸入和一個錯誤輸出。

在對應之前，會從具有警告的資料行中刪除具有不支援之資料類型的資料行。
如需詳細資訊，請參閱[資料類型支援](oracle-data-type-support.md)。

## <a name="load-options"></a>載入選項

支援兩種存取載入模式。 您可以在 [Oracle 目的地編輯器 (連線管理員頁面)](#oracle-destination-editor-connection-manager-page) 中設定模式。 兩種模式為：

- 批次載入：此模式是以批次方式將資料載入 Oracle 資料表，而且整個批次是在相同的交易之下插入的。
有關如何設定此模式的詳細資料，請參閱 [Oracle 目的地編輯器 (連線管理員頁面)](#oracle-destination-editor-connection-manager-page) 與 [Oracle 目的地自訂屬性](#oracle-destination-custom-properties)。

- 使用直接路徑的快速載入：此模式是使用驅動程式的直接路徑模式來載入 Oracle 資料表。 使用此模式時有一些限制，請參閱 Oracle 文件以取得詳細資料。  
有關如何設定此模式的詳細資料，請參閱 [Oracle 目的地編輯器 (連線管理員頁面)](#oracle-destination-editor-connection-manager-page) 與 [Oracle 目的地自訂屬性](#oracle-destination-custom-properties)。

## <a name="error-handling"></a>錯誤處理

Oracle 目的地有錯誤輸出。 此元件的錯誤輸出包含下列輸出資料行：

- **錯誤碼**：代表目前錯誤之錯誤類型的數字。 錯誤碼可能是來自：
    - Oracle 伺服器。 請參閱 Oracle 資料庫文件中的詳細錯誤描述。
    - SSIS 執行階段。 如需 SSIS 錯誤碼清單，請參閱＜SSIS 錯誤碼和訊息參考＞。
- **錯誤資料行**：導致轉換錯誤的來源欄編號。

- **錯誤資料欄**：造成錯誤的資料。

載入程序中受支援的輸出錯誤類型為：資料轉換、截斷或條件約束違規等等。 請參閱 [Oracle 目的地編輯器 (錯誤輸出頁面)](#oracle-destination-editor-error-output-page)。

[錯誤數目上限 (MaxErrors)] 屬性可設定可能發生的錯誤數目上限。 當達到數目上限時，執行會停止並傳回錯誤。 而且，只有在達到數目上限之前的執行記錄才會包含在目標資料表中。 如需詳細設定，請參閱 [Oracle 目的地編輯器 (連線管理員頁面)](#oracle-destination-editor-connection-manager-page)。

## <a name="parallelism"></a>平行處理原則

在批次載入模式中，平行執行的設定沒有限制，但效能可能會受到標準記錄鎖定機制的影響。 效能損失的幅度取決於資料和資料表組織。

在直接路徑通訊協定 (快速載入) 中，只能將一個 Oracle 目的地設定為同時對相同的資料表執行，但是可以使用平行模式。

平行直接路徑允許多個直接路徑載入，可以將多個 Oracle 目的地設定為同時針對相同的資料表執行。 Oracle 不會以獨佔方式鎖定目標資料表以用於快速載入工作階段，這可讓您執行額外的快速載入目的地元件，以平行方式載入相同的目標資料表。
平行直接路徑的限制更多，使用任何平行處理原則都應事先規劃。

沒有理由使用單一平行工作階段。

請參閱 Oracle 文件中有關使用平行直接路徑載入的限制。

如需詳細資訊，請參閱 [Oracle 目的地自訂屬性](#oracle-destination-custom-properties)。

## <a name="troubleshooting-the-oracle-destination"></a>針對 Oracle 目的地進行疑難排解

您可以記錄 Oracle 來源對 Oracle 資料來源進行的 ODBC 呼叫，以針對資料匯出進行疑難排解。 若要記錄 ODBC 來源對 Oracle 資料來源進行的 ODBC 呼叫，請啟用 ODBC 驅動程式管理員追蹤。 如需詳細資訊，請參閱 Microsoft 文件集＜如何使用 ODBC 資料來源管理員產生 ODBC 追蹤＞。 

## <a name="oracle-destination-custom-properties"></a>Oracle 目的地自訂屬性

下表描述 Oracle 目的地的自訂屬性。 所有屬性都是可讀寫的。

|屬性名稱|資料類型|描述|載入模式|
|:-|:-|:-|:-|
|BatchSize|整數|大量載入的批次大小。 這是當做批次載入的資料列數目。|只能在批次模式中使用。|
|DefaultCodePage|整數|當資料來源沒有字碼頁資訊時，所要使用的字碼頁。 <br>**注意**：這個屬性僅由 [進階編輯器] 設定。|用於這兩種模式。|
|FastLoad|布林值|是否使用快速載入。 預設值為 **false**。 這也可以在 [Oracle 目的地編輯器 (連線管理員頁面)](#oracle-destination-editor-connection-manager-page) 中設定。 |用於這兩種模式。|
|MaxErrors|整數|停止資料流程之前可以發生的錯誤數目。 預設值為 **0**，表示沒有錯誤數目的限制。<br> 如果已在 [錯誤處理] 頁面中選取 [重新導向流程]。 在達到錯誤數目限制之前，所有錯誤都會在錯誤輸出中傳回。 如需詳細資訊，請參閱[錯誤處理](#error-handling)。|只能在「快速載入」模式中使用。|
|NoLogging|布林值|資料庫記錄是否已停用。 預設值為 **False**，表示記錄已啟用。|用於這兩種模式。|
|平行|布林值|是否允許平行載入。 **True** 表示允許其他載入工作階段針對相同的目標資料表執行。<br> 如需詳細資訊，請參閱[平行處理原則](#parallelism)。|只能在「快速載入」模式中使用。|
|TableName|String|包含所要使用之資料的資料表名稱。|用於這兩種模式。|
|TableSubName|String|subname 或 subpartition。 此為選用值。<br> **注意**：此屬性只能在 [進階編輯器] 中設定。|只能在「快速載入」模式中使用。|
|TransactionSize|整數|單一交易中可以進行的插入數目。 預設值為 **BatchSize**。|只能在批次模式中使用。|
|TransferBufferSize|整數|傳輸緩衝區的大小。 預設值為 64 KB。|只能在「快速載入」模式中使用。|

## <a name="configuring-the-oracle-destination"></a>設定 Oracle 目的地

Oracle 目的地可以透過程式設計方式或 SSIS 設計工具來設定。

下圖中顯示 [Oracle 目的地編輯器]。 它包含 [連線管理員] 頁面、[對應] 頁面與 [錯誤輸出] 頁面。

如需詳細資訊，請參閱下列其中一節：

- [Oracle 目的地編輯器 (連線管理員頁面)](#oracle-destination-editor-connection-manager-page)
- [Oracle 目的地編輯器 (對應頁面)](#oracle-destination-editor-mappings-page)
- [Oracle 目的地編輯器 (錯誤輸出頁面)](#oracle-destination-editor-error-output-page)

![Oracle 目的地](media/oracle-destination.png)

**[進階編輯器]** 對話方塊包含可以程式設計方式設定的屬性。
若要開啟 **[進階編輯器]** 對話方塊：

- 在 Integration Services 專案的 [資料流程] 畫面中，以滑鼠右鍵按一下 Oracle 目的地，然後選取 [顯示進階編輯器]。

如需有關可在 [進階編輯器] 對話方塊中設定之屬性的詳細資訊，請參閱 [Oracle 目的地自訂屬性](#oracle-destination-custom-properties)。

## <a name="oracle-destination-editor-connection-manager-page"></a>Oracle 目的地編輯器 (連線管理員頁面)

使用 [Oracle 目的地編輯器] 對話方塊的 [連線管理員] 頁面，即可選取目的地的 Oracle 連線管理員。 這個頁面也可以讓您從資料庫中選取資料表或檢視。

**開啟 Oracle 目的地編輯器的連線管理員頁面**

- 在 SQL Server Data Tools 中，開啟具有 Oracle 目的地的 SQL Server Integration Services (SSIS) 套件。

- 在 [資料流程] 索引標籤中，按兩下 Oracle 目的地。

- 在 [Oracle 目的地編輯器] 中，按一下 [連線管理員]。

### <a name="options"></a>選項。

**[ODBC 目的地編輯器]**

從清單中選取現有的連線管理員，或按一下 [新增] 以建立新的 Oracle 連線管理員。

**新增**

按一下 **[新增]** 。 [Oracle 連線管理員編輯器] 對話方塊隨即開啟，讓您能夠建立新的連線管理員。

**資料存取模式**

選取從來源中選取資料的方法。 下表將顯示這些選項：

|選項|描述|
|:-|:-|
|資料表名稱|設定 Oracle 目的地以批次模式工作。 選項：<br><br> **資料表或檢視的名稱**：從清單的資料庫中選取可用的資料表或檢視表。<br><br> **交易大小**：輸入單一交易中可以進行的插入數目。 預設值為 **BatchSize**。<br><br> **批次大小**：輸入大量載入的批次大小 (載入的資料列數目)。
|資料表名稱 – 快速載入|設定 Oracle 目的地以快速 (直接路徑) 載入模式工作。 <br><br>可用的選項如下：<br><br> **資料表或檢視的名稱**：從清單的資料庫中選取可用的資料表或檢視表。<br><br> **平行載入**：是否啟用平行載入。 如需詳細資訊，請參閱[平行處理原則](#parallelism)。<br><br> **不記錄**：此核取方塊可停用資料庫記錄。 此記錄是針對復原目的所使用的 Oracle 資料庫，與追蹤無關。<br><br> **最大錯誤數目**：停止資料流程之前可以發生的最大錯誤數目。 預設值為 0，表示沒有數目限制。<br><br> 錯誤輸出中會傳回所有錯誤。<br><br> **傳輸緩衝區大小 (KB)** ：輸入傳輸緩衝區的大小。 預設大小為 64 KB。|

**檢視現有的資料**

按一下 [檢視現有的資料]，最多可檢視您所選取之資料表的 200 個資料列。

## <a name="oracle-destination-editor-mappings-page"></a>Oracle 目的地編輯器 (對應頁面)

使用 [Oracle 目的地編輯器] 對話方塊的 [對應] 頁面，將輸入資料行對應至目的地資料行。

**開啟 Oracle 目的地編輯器的對應頁面**

- 在 SQL Server Data Tools 中，開啟具有 Oracle 目的地的 SQL Server Integration Services (SSIS) 套件。

- 在 [資料流程] 索引標籤中，按兩下 Oracle 目的地。

- 在 [Oracle 目的地編輯器] 中，按一下 [對應]。

### <a name="options"></a>選項。

**可用的輸入資料行**

可用輸入資料行的清單。 將輸入資料行拖放至可用的目的地資料行，即可對應資料行。

**可用的目的地資料行**

可用目的地資料行的清單。 將目的地資料行拖放至可用的輸入資料行，即可對應資料行。

**輸入資料行**

檢視所選取的輸入資料行。 您可以選取 [< 忽略 >] 移除對應，將資料行從輸出排除。

**目的地資料行**

檢視所有可用的目的地資料行，包括對應和取消對應的資料行。

> [!NOTE]
>
>具有不支援之資料類型的資料行將從具有警告的對應中刪除。

## <a name="oracle-destination-editor-error-output-page"></a>Oracle 目的地編輯器 (錯誤輸出頁面)

使用 [Oracle 目的地編輯器] 對話方塊的 [錯誤輸出] 頁面，以選取錯誤處理選項。

**開啟 Oracle 目的地編輯器的錯誤輸出頁面**

- 在 SQL Server Data Tools 中，開啟具有 Oracle 目的地的 SQL Server Integration Services (SSIS) 套件。

- 在 [資料流程] 索引標籤中，按兩下 Oracle 目的地。

- 在 [Oracle 目的地編輯器] 中，按一下 [錯誤輸出]。

### <a name="options"></a>選項。

**錯誤行為**

選取 Oracle 來源應該如何處理流程中的錯誤：忽略失敗、重新導向資料列，或使元件失效。
**相關小節**：[資料中的錯誤處理](./error-handling-in-data.md?view=sql-server-2017)

**截斷**

選取 Oracle 來源應該如何處理流程中的截斷：忽略失敗、重新導向資料列，或使元件失效。

## <a name="next-steps"></a>後續步驟

- 設定 [Oracle 連線管理員](oracle-connection-manager.md)。
- 設定 [Oracle 來源](oracle-source.md)。
- 設定 [Oracle 目的地](oracle-destination.md)。
- 如有任何疑問，請瀏覽 [TechCommunity](https://aka.ms/AA5u35j) \(英文\)。