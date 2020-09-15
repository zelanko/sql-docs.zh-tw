---
title: 建立儀表板延伸模組
description: 本教學課程會示範如何建立儀表板延伸模組，將自訂功能新增到 Azure Data Studio。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.reviewer: alayu, maghan
ms.topic: how-to
author: yualan
ms.author: alayu
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: b28b3cd043d6564da7d644bb44469671c9ffa147
ms.sourcegitcommit: c5f0c59150c93575bb2bd6f1715b42716001126b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/02/2020
ms.locfileid: "89392141"
---
# <a name="create-an-azure-data-studio-dashboard-extension"></a>建立 Azure Data Studio 儀表板延伸模組

本教學課程會示範如何建立新的 **Azure Data Studio 儀表板延伸模組**。 延伸模組會提供 Azure Data Studio 連線儀表板，其可供透過使用者能輕鬆看到的方式來延伸 Azure Data Studio 功能。

在本教學課程中，您將了解如何：
> [!div class="checklist"]
> - 安裝延伸模組產生器
> - 建立您的延伸模組
> - 在延伸模組中提供儀表板
> - 測試您的延伸模組
> - 封裝您的延伸模組
> - 將您的延伸模組發佈到市集

## <a name="prerequisites"></a>先決條件

Azure Data Studio 建置在與 Visual Studio Code 相同的架構上，因此 Azure Data Studio 的延伸模組是使用 Visual Studio Code 所建立。 若要開始進行，您需要下列元件：

- `$PATH` 中已安裝並可供使用的 [Node.js](https://nodejs.org)。 Node.js 包含 Node.js 套件管理員 [npm](https://www.npmjs.com/)，可用來安裝延伸模組產生器。
- 用來偵錯延伸模組的 [Visual Studio Code](https://code.visualstudio.com)。
- Azure Data Studio [偵錯延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug) (選擇性)。 讓您不需要將延伸模組封裝並安裝到 Azure Data Studio 中，即可進行測試。
- 確定 `azuredatastudio` 在您的 PATH 中。 若是 Windows，請務必選擇 setup.exe 中的 [`Add to Path`] 選項。 若是 Mac 或 Linux，請執行 [Install 'azuredatastudio' command in PATH] \(在 PATH 中安裝 'azuredatastudio' 命令\)** 選項。

## <a name="install-the-extension-generator"></a>安裝延伸模組產生器

為了簡化建立延伸模組的程序，我們使用 Yeoman 建置了[延伸模組產生器](https://code.visualstudio.com/docs/extensions/yocode)。 若要加以安裝，請從命令提示字元執行下列命令：

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-dashboard-extension"></a>建立儀表板延伸模組

### <a name="introduction-to-the-dashboard"></a>儀表板簡介

Azure Data Studio 連線儀表板是一種強大的工具，其可摘要和提供使用者連線的見解。

儀表板有兩種變化：摘要整個伺服器的「伺服器儀表板」，以及摘要個別資料庫的「資料庫儀表板」。 您可在 Azure Data Studio [Connections] \(連線\) Viewlet 中以滑鼠右鍵按一下伺服器或資料庫，並按一下 [Manage] \(管理\) 來存取這兩種儀表板：

:::image type="content" source="media/dashboard-extension/dashboard-summary.gif" alt-text="儀表板簡介":::

延伸模組有 3 個貢獻點，可將功能新增至儀表板：

1. **[Full Dashboard] \(完整儀表板\) 索引標籤**：延伸模組儀表板中的個別索引標籤。 可新增至伺服器或資料庫儀表板。 可使用小工具、工具列和導覽區段進行自訂。
2. **Homepage Actions (首頁動作)** ：位於連線工具列頂端的 [Action] \(動作\) 按鈕。
3. **Widgets (小工具)** ：針對 SQL Server 執行的圖表。

:::image type="content" source="media/dashboard-extension/dashboard-contrib-points.png" alt-text="貢獻點":::

### <a name="run-the-extension-generator"></a>執行延伸模組產生器

若要建立延伸模組：

1. 使用下列命令啟動延伸模組產生器：

   `yo azuredatastudio`

2. 從延伸模組類型清單選擇 [New Dashboard] \(新增儀表板\)。

3. 填寫提示，如下所示。 這會建立延伸模組，其為伺服器儀表板提供索引標籤。

:::image type="content" source="media/dashboard-extension/dashboard-generator.png" alt-text="延伸模組產生器":::

由於有許多提示，因此以下提供每個問題所代表意義的部分詳細資訊：

:::image type="content" source="media/dashboard-extension/dashboard-flowchart.png" alt-text="儀表板流程圖":::

完成上述步驟會建立新的資料夾。 在 Visual Studio Code 中開啟資料夾，即可建立自己的儀表板延伸模組！

### <a name="run-the-extension"></a>執行延伸模組

讓我們執行延伸模組來查看儀表板範本所提供的內容。 在執行前，請先確認已在 Visual Studio Code 中安裝 **Azure Data Studio 偵錯延伸模組**。

請在 VS Code 中選取 **F5** 來以偵錯模式啟動執行延伸模組的 Azure Data Studio。 然後，您即可檢視此預設範本為儀表板貢獻的方式。

接下來，我們將探討如何修改這個預設儀表板。

### <a name="develop-the-dashboard"></a>開發儀表板

開始進行延伸模組開發的最重要檔案便是 `package.json`。 這是資訊清單檔，其中註冊了儀表板的貢獻。 請注意 `dashboard.tabs`、`dashboard.insights` 和 `dashboard.containers` 區段。

以下是一些可嘗試的變更：

- 嘗試見解類型，包括 'bar'、'horizontalBar'、'timeSeries'
- 撰寫自己的查詢來針對 SQL Server 連線執行
- 請參閱此[範例見解教學課程](../tutorial-qds-sql-server.md)或[本教學課程](../tutorial-table-space-sql-server.md)來取得特定的見解教學課程

## <a name="package-your-extension"></a>封裝您的延伸模組

若要分享給其他人，您必須將延伸模組封裝成單一檔案。 此檔案可發佈到 Azure Data Studio 延伸模組市集，或是在您的小組或社群分享。 若要執行這項操作，您必須從命令列安裝另一個 npm 套件：

```console
`npm install -g vsce`
```

請依照需求編輯 `README.md`，然後巡覽至延伸模組的基礎目錄，並執行 `vsce package`。 您可選擇將存放庫與延伸模組連結，或在不連結的情況下繼續。 若要新增，請將類似的一行新增到 `package.json` 檔案。

```json
"repository": {
    "type": "git",
    "url": "https://github.com/anjalia/my-test-extension.git"
}
```

在新增這些行後，my-test-extension-0.0.1.vsix 即已建立，並已準備好在 Azure Data Studio 中安裝。

:::image type="content" source="media/dashboard-extension/install-vsix.png" alt-text="安裝 VSIX":::

## <a name="publish-your-extension-to-the-marketplace"></a>將您的延伸模組發佈到市集

Azure Data Studio 延伸模組市集尚未完全實行，目前的程序是在其他地方 (例如 GitHub 版本頁面) 裝載延伸模組 VSIX，然後提交 PR 並將[此 JSON 檔案](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)更新為您的延伸模組資訊。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：
> [!div class="checklist"]
> - 安裝延伸模組產生器
> - 建立您的延伸模組
> - 在延伸模組中提供儀表板
> - 測試您的延伸模組
> - 封裝您的延伸模組
> - 將您的延伸模組發佈到市集

希望藉由閱讀本文，可激發您的靈感，建置自己的 Azure Data Studio 延伸模組。 我們支援儀表板深入解析 (針對 SQL Server 執行的精美圖表)、一些 SQL 特定的 API，以及從 Visual Studio Code 繼承的一組龐大現有擴充點。

如果您有些想法，但不確定如何著手，請提出問題或對 [azuredatastudio](https://twitter.com/azuredatastudio) 小組推文。

您可以隨時參考 [Visual Studio Code 延伸模組指南](https://code.visualstudio.com/docs/extensions/overview)，因為指南涵蓋了所有現有的 API 和模式。

若要了解如何在 Azure Data Studio 中使用 T-SQL，請完成 T-SQL 編輯器教學課程：

> [!div class="nextstepaction"]
> [使用 Transact-SQL 編輯器建立資料庫物件](../tutorial-sql-editor.md)。
