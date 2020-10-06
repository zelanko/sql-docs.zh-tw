---
title: Azure Data Studio 中的 Kusto 核心筆記本
description: 本教學課程說明如何建立及執行 Kusto 筆記本。
ms.topic: how-to
ms.prod: azure-data-studio
ms.technology: azure-data-studio
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: a8379e10e8c3e3af64381e9a4536b253e203964e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725122"
---
# <a name="create-and-run-a-kusto-kql-notebook-preview"></a>建立並執行 Kusto (KQL) 筆記本 (預覽)

本文說明如何使用連線至 Azure 資料總管叢集的 [Kusto (KQL) 延伸模組](../extensions/kusto-extension.md)，來建立並執行 [Azure Data Studio 筆記本](./notebooks-guidance.md)。

透過 Kusto (KQL) 延伸模組，您可以將核心選項變更為 **Kusto**。

此功能目前為預覽狀態。

## <a name="prerequisites"></a>必要條件

如果您沒有 Azure 訂用帳戶，請在開始前建立[免費 Azure 帳戶](https://azure.microsoft.com/free/)。

- [Azure 資料總管叢集，其中包含您可以連線的資料庫](/azure/data-explorer/create-cluster-database-portal)。
- [Azure Data Studio](../download-azure-data-studio.md)。
- [適用於 Azure Data Studio 的 Kusto (KQL) 延伸模組](../extensions/kusto-extension.md)。

## <a name="create-a-kusto-kql-notebook"></a>建立 Kusto (KQL) 筆記本

下列步驟說明如何在 Azure Data Studio 中建立筆記本檔案：

1. 在 Azure Data Studio 中，連線至您的 Azure 資料總管叢集。

2. 瀏覽至 [連線] 窗格，在 [伺服器] 視窗底下，以滑鼠右鍵按一下 Kusto 資料庫，然後選取 [新增筆記本]。 您也可以移至 [檔案] > [新增筆記本]。

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-new-notebook.png" alt-text="開啟筆記本":::

3. 針對 [核心] 選取 [Kusto]。 確認 [附加至] 功能表已設定為叢集名稱和資料庫。 在本文中，我們會使用 help.kusto.windows.net 叢集來處理範例資料庫資料。

   :::image type="content" source="media/notebooks-kusto-kernel/set-kusto-kernel.png" alt-text="開啟筆記本":::

您可從 [檔案] 功能表使用 [儲存] 或 [另存新檔...] 命令來儲存筆記本。

若要開啟筆記本，您可從 [檔案] 功能表使用 [開啟檔案...] 命令，在 [歡迎使用] 頁面上選取 [開啟檔案]，或從命令選擇區使用 [檔案:開啟] 命令。

## <a name="change-the-connection"></a>變更連線

若要變更筆記本的 Kusto 連線：

1. 選取筆記本工具列中的 [附加至]  功能表，然後選取 [變更連線]  。

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-select-attach-to-change-connections.png" alt-text="開啟筆記本":::

   > [!Note]
   > 確定已填入資料庫值。 Kusto 筆記本必須已指定資料庫。

2. 您現在可以選取最近的連線伺服器，或輸入新的連線詳細資料來連線。

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-change-connection-cluster.png" alt-text="開啟筆記本":::

   > [!Note]
   > 指定不含 `https://` 的叢集名稱。

## <a name="run-a-code-cell"></a>執行程式碼資料格

您可以建立資料格，並在其中納入可藉由在資料格左側選取 [執行資料格] 按鈕就地執行的 KQL 查詢。 資料格執行後，會在筆記本中顯示結果。

例如：

1. 選取工具列中的 [+程式碼]  命令來新增程式碼儲存格。

   :::image type="content" source="media/notebooks-kusto-kernel/kusto-kernel-code.png" alt-text="開啟筆記本":::

2. 將下列範例複製並貼到資料格中，然後選取 [執行資料格]。 此範例會查詢 StormEvents 資料以尋找特定事件類型。

   ```kusto
    StormEvents
    | where EventType == "Waterspout"
   ```

   :::image type="content" source="media/notebooks-kusto-kernel/run-kusto-notebook-cell.png" alt-text="開啟筆記本":::

## <a name="save-the-result-or-show-chart"></a>儲存結果或顯示圖表

如果執行會傳回結果的指令碼，則可使用結果上方所顯示的工具列，將該結果儲存為不同的格式。

- 另存為 CSV
- 另存為 Excel
- 另存為 JSON
- 另存為 XML
- 顯示圖表

```kusto
    StormEvents
    | limit 10
```

:::image type="content" source="media/notebooks-kusto-kernel/run-notebook-save-results.png" alt-text="開啟筆記本":::

## <a name="known-issues"></a>已知問題

| 詳細資料 | 因應措施 |
|---------|------------|
| [查詢結果只會顯示的資料行標題](https://github.com/microsoft/azuredatastudio/issues/12565)。 | N/A |

您可以提出[功能要求](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=feature_request.md&title=)，以提供意見反應給產品小組。  
您可以提出[錯誤 (bug)](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=bug_report.md&title=)，以提供意見反應給產品小組。

## <a name="next-steps"></a>後續步驟

深入了解筆記本：

- [適用於 Azure Data Studio 的 Kusto (KQL) 延伸模組](../extensions/kusto-extension.md)
- [如何在 Azure Data Studio 中使用筆記本](./notebooks-guidance.md)
- [建立及執行 Python 筆記本](./notebooks-python-kernel.md)
- [建立並執行 SQL Server 筆記本](./notebooks-sql-kernel.md)