---
title: 快速存取 insights 和 SQL 作業 Studio （預覽） 中的一般工作 |Microsoft 文件
description: 深入了解具洞察力的 widget 顯示 SQL 作業 Studio （預覽） 中。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad7fcbab5a01828cccd855da2d65ba3199e0b41b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="dashboards-in-includename-sosincludesname-sos-shortmd"></a>儀表板 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

若要檢視儀表板，以滑鼠右鍵按一下伺服器或資料庫，並選取**管理**。

![範例儀表板](media/dashboards/sample-dashboard.png)

**伺服器屬性**包含伺服器，包括版本、 版本、 電腦名稱和作業系統版本的內容。

**工作**包含 commons 工作，例如還原和新的查詢。

**搜尋資料庫**輕鬆地查詢儲存在伺服器上，包括資料表的現有資料庫。

**備份狀態**輕鬆地查詢現有的資料庫備份狀態。

## <a name="configuring-insight-widgets"></a>設定 深入了解 Widget
強烈建議您依照教學課程中的，設定您儀表板，您可以找到[這裡](tutorial-build-custom-insight-sql-server.md)。

此外，請確定簽出[如何設定深入了解 widget]()。

之後進行本教學課程中，閱讀，以深入了解特定未涵蓋在本教學課程中的 widget。

## <a name="insight-detail"></a>深入了解詳細資料
深入了解詳細資料彈出式視窗提供相關的深入解析小工具的詳細的資訊。 
- 深入了解 widget 會呈現在摘要的摘要檢視計數、 線條、 圖表等。 
- 深入了解詳細資料彈出式視窗提供 」 向下切入 」 詳細資料，列出每個項目列在 [高階] widget 中深入了解資料的深入解析。 
  - 詳細資料彈出式視窗內容被定義與另一個主要的 widget 查詢的 SQL 查詢。 

沒有集合需要深入了解詳細資料查詢，但標準配置。
- 檢視的上半部一律為 2 欄 「 摘要 」 檢視。 若要使用哪些資料行定義"label"和"value"屬性的 JSON 組態
- 按一下 [摘要] 表格中的資料列，底部彈出式視窗的下半部會列出一組完整的資料列的資料行資訊。

### <a name="insight-detail-configuration-in-packagejson"></a>Package.json 中深入了解詳細組態

深入了解詳細資料彈出式視窗組態範例
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
|詳細資料|json 物件|||若要定義深入了解詳細定義其結構中的強制 proerty||
|queryFile|string|||深入了解詳細的 sql 查詢檔案路徑和 package.json 的位置相對的檔名||
|標籤|json 物件|||必要的屬性定義摘要清單檢視中的每個明細項目|在未來，變更例如 'summaryList' 這個屬性的名稱|
|圖示|string|||表示每個摘要清單檢視項目至 reder 的圖示名稱。|將記錄 (tbd) 支援圖示清單|
|column|string|||指出在從查詢結果集的摘要清單檢視中的第一個資料行名稱|這個屬性的名稱將在未來變更為更具直覺性的名稱|
|value|string|||指出在從查詢結果集的摘要清單檢視中的第二個資料行的名稱。 此資料行的值用來檢查條件，並設定每個摘要清單檢視項目的色彩點的色彩|這個屬性的名稱會在未來變更為更具直覺性的項目|
|condition (條件)|json 物件|||定義資料行值的條件檢查，並判斷每個摘要清單檢視項目的色彩||
|if|string|永遠，能等於 notEquals、 greaterThan、 lessThan、 greaterThanOrEqauls、 lessThanOrEquals||條件檢查運算子|在未來的屬性名稱會變更為運算子|
|equals|string|||條件的核取值|在未來的這個屬性名稱會變更為 'value'|

## <a name="insight-actions"></a>深入了解動作
深入了解 widget 和深入了解詳細資料，您可以輕鬆地出現行動計畫來減輕問題或管理。 比方說，您將會考慮執行 DBCC CHECKDB、 讀取錯誤記錄檔或還原資料庫時資料庫處於復原暫止。 或者可以是任何您想要執行的動作。

使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]的深入了解動作設定中，您可以將對應內建動作，例如還原或攜帶您自己的 sql 指令碼以定義的動作。

> 使用 sql 指令碼的自訂動作的設定正在開發，它尚未提供私人預覽組建中。

## <a name="sample-insight-action-definition"></a>深入了解動作定義範例

```"actions"{}``` 定義的深入解析 」 動作。 動作可以定義在特定範圍例如```"server"```，```"database"```等和[!INCLUDE[name-sos](../includes/name-sos-short.md)]將目前的連接內容資訊傳遞至動作。 

例如，還原動作啟動時 WideWorldImporters 資料庫```"database": "${Database}"```定義表示傳遞```Database```您要還原動作的查詢結果中的資料行值。 接著還原動作，啟動資料庫。 ```"types"``` json 陣列，陣列中可以列出多個動作。 它基本上會成為快顯功能表在深入了解詳細資料 對話方塊上，該使用者可以按一下並執行的動作。 

> [!INCLUDE[name-sos](../includes/name-sos-short.md)] 預覽 0.17.1 已啟用 「 備份 」、 「 還原 」、 [新增查詢] 和 [新的資料庫] 做為動作類型。

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
