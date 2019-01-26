---
title: 快速存取深入解析和一般工作
titleSuffix: Azure Data Studio
description: 深入了解 Azure Data Studio 中的資料庫儀表板上顯示小工具。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 26e93209e2cbd9809d607f90c7eff4da32d2cd98
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2019
ms.locfileid: "55045027"
---
# <a name="dashboards-in-includename-sosincludesname-sos-shortmd"></a>儀表板 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

若要檢視儀表板，以滑鼠右鍵按一下伺服器或資料庫，然後選取**管理**。

![範例儀表板](media/dashboards/sample-dashboard.png)

**伺服器屬性**包含對伺服器的內容，包括版本、 版本、 電腦名稱和作業系統版本。

**工作**包含 commons 工作，例如還原和新的查詢。

**搜尋資料庫**輕鬆查閱儲存在伺服器上，包括資料表的現有資料庫。

**備份狀態**輕鬆查閱現有資料庫的備份狀態。

## <a name="configuring-insight-widgets"></a>設定的深入解析小工具
強烈建議您遵循教學課程中的，設定您儀表板，您可以找到[此處](tutorial-build-custom-insight-sql-server.md)。

此外，請確定簽出[上設定的深入解析小工具使用說明]()。

之後遵循此教學課程中，繼續閱讀以深入了解本教學課程未涵蓋的特定小工具。

## <a name="insight-detail"></a>了解詳細資料
了解詳細資料飛出視窗上提供相關的深入解析小工具的更詳細的資訊。 
- 深入解析小工具會呈現在摘要的摘要檢視計數、 線條、 圖表等等。 
- 深入解析的詳細資料飛出視窗上提供 「 向內切入 」 的詳細資訊，列出每個項目的高層級的深入解析小工具中所列的更深入資料深入解析。 
  - 使用不同的 SQL 查詢，以主要小工具的查詢定義的詳細資料飛出視窗內容。

沒有集合需求的深入解析 」 詳細資料查詢，但配置是標準。
- 檢視的上半部一律是 2 資料行"的 summary"檢視。 若要使用哪些資料行是由 JSON 設定的 「 標籤 」 和 「 值 」 屬性定義
- 方法是按一下 [摘要] 表格中的資料列，底部飛出視窗的下半部會列出一組完整的資料列的資料行資訊。

### <a name="insight-detail-configuration-in-packagejson"></a>在 package.json 中的深入解析詳細資料設定

飛出視窗上設定的範例深入解析的詳細資料
```json
"details": {
    "queryFile": "./relative_path_to_sqlfile_from_package_json_file.sql",
    "label": {
        "icon": "database",
        "column": "first_column_name_for_summary_list_view",
        "state": [
            {
                "condition": {
                    "if": "equals",
                    "equals": "0"
                },
                "color": "red"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "1"
                },
                "color": "orange"
            },
            {
                "condition": {
                    "if": "equals",
                    "equals": "2"
                },
                "color": "green"
            }
        ]
    },
    "value": "second_column_and_condition_check_value_column_for_summary_list_view",
```

|屬性|型別|value|預設值|description|comment|
|:---|:---|:---|:---|:---|:---|
|詳細資料|json 物件|||必要的屬性，來定義其結構內了解詳細資料定義||
|queryFile|string|||了解詳細資料的 sql 查詢檔案路徑和相對於位置的 package.json 檔案名稱||
|標籤|json 物件|||必要的屬性，以定義摘要清單檢視中的每個明細項目|在未來，變更例如 'summaryList' 這個屬性的名稱|
|圖示|string|||表示針對每個摘要清單檢視項目呈現的圖示名稱。|會記錄支援的圖示清單 (tbd)|
|column|string|||指出在從查詢結果集的摘要清單 檢視中的第一個資料行名稱|這個屬性的名稱會在未來變更為更具直覺性的名稱|
|value|string|||指出在從查詢結果集的摘要清單 檢視中的第二個資料行名稱。 這個資料行的值用來檢查條件，並設定每個摘要清單檢視項目色彩點的色彩|這個屬性的名稱會在未來變更為更具直覺性的項目|
|condition (條件)|json 物件|||定義資料行值的條件檢查，並決定每個摘要清單檢視項目色彩||
|if|string|一律，equals、 notEquals、 greaterThan、 lessThan、 greaterThanOrEquals、 lessThanOrEquals||條件檢查運算子|在未來的屬性名稱會變更為運算子|
|equals|string|||條件檢查值|在未來的這個屬性名稱會變更為 'value'|

## <a name="insight-actions"></a>了解動作
透過深入解析小工具與深入解析的詳細資料，您可以輕鬆地提供行動計畫來減輕問題，或管理。 比方說，您會把執行 DBCC CHECKDB、 讀取錯誤記錄檔或還原資料庫，當資料庫處於復原暫止。 或者，它可以是任何您想要執行的動作。

使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]的深入解析動作組態，您可以將對應內建動作，例如還原，或攜帶您自己的 sql 指令碼以定義的動作。

> 使用 sql 指令碼的自訂動作的設定正在開發，它尚未可用的私人預覽組建中。

## <a name="sample-insight-action-definition"></a>範例深入解析動作定義中

```"actions"{}``` 定義的深入解析動作。 動作可以定義特定的範圍這類```"server"```，```"database"```等和[!INCLUDE[name-sos](../includes/name-sos-short.md)]將目前的連接內容資訊傳遞至動作。

比方說，當您啟動 WideWorldImporters 資料庫還原動作時，才```"database": "${Database}"```定義會表示要傳遞```Database```您還原動作的查詢結果中的資料行值。 然後還原動作會啟動資料庫。 ```"types"``` json 陣列且陣列中可以列出多個動作。 它基本上會變成操作功能表該使用者可以在深入解析的詳細資料 對話方塊上按一下，並執行的動作。 

> [!INCLUDE[name-sos](../includes/name-sos-short.md)] 預覽 0.17.1 已啟用 「 備份 」、 「 還原 」、 [新增查詢] 和 [新的資料庫] 為動作類型。

```json
"details": {
    "queryFile": "./sql/database_state_detail.sql",
    "label": {...},
    "value": "state",
    "actions": {
        "database": "${Database}",
        "types": ["restore"]
    }
}
```
