---
title: 建立儀表板延伸模組
description: 本教學課程會示範如何建立儀表板延伸模組，將自訂功能新增到 Azure Data Studio。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: c7402c8dd0d2d85d38536a0bcfea3ce8cd780657
ms.sourcegitcommit: 7f76975c29d948a9a3b51abce564b9c73d05dcf0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2020
ms.locfileid: "96900871"
---
# <a name="create-an-azure-data-studio-dashboard-extension"></a>建立 Azure Data Studio 儀表板延伸模組

本教學課程示範如何建立新的 Azure Data Studio 儀表板延伸模組。 延伸模組會提供 Azure Data Studio 連線儀表板，其可供透過使用者能輕鬆看到的方式來延伸 Azure Data Studio 功能。

在本文中，您將了解如何：

> [!div class="checklist"]
> - 安裝延伸模組產生器。
> - 建立您的延伸模組。
> - 參與延伸模組儀表板的編輯。
> - 測試您的延伸模組。
> - 封裝您的延伸模組。
> - 將延伸模組發佈到市集。

## <a name="prerequisites"></a>先決條件

Azure Data Studio 建置在與 Visual Studio Code 相同的架構上，因此 Azure Data Studio 的延伸模組是使用 Visual Studio Code 所建立。 若要開始進行，您需要下列元件：

- `$PATH` 中已安裝並可供使用的 [Node.js](https://nodejs.org)。 Node.js 包含 Node.js 套件管理員 [npm](https://www.npmjs.com/)，可用來安裝延伸模組產生器。
- 用來偵錯延伸模組的 [Visual Studio Code](https://code.visualstudio.com)。
- Azure Data Studio [偵錯延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug) (選擇性)。 偵錯延伸模組讓您無須將延伸模組封裝並安裝到 Azure Data Studio 中，即可測試延伸模組。
- 確定 `azuredatastudio` 在您的 PATH 中。 針對 Windows，請務必選擇 setup.exe 中的 [新增至路徑] 選項。 若是 Mac 或 Linux，請執行 [Install 'azuredatastudio' command in PATH] \(在 PATH 中安裝 'azuredatastudio' 命令\) 選項。

## <a name="install-the-extension-generator"></a>安裝延伸模組產生器

為了簡化建立延伸模組的程序，我們使用 Yeoman 建置了[延伸模組產生器](https://code.visualstudio.com/docs/extensions/yocode)。 若要安裝，請從命令提示字元執行下列命令：

```console
npm install -g yo generator-azuredatastudio
```

## <a name="create-your-dashboard-extension"></a>建立儀表板延伸模組

### <a name="introduction-to-the-dashboard"></a>儀表板簡介

Azure Data Studio 連線儀表板是一種強大的工具，其可摘要和提供使用者連線的見解。

儀表板有兩種變化。 *伺服器儀表板* 會摘要整個伺服器，*資料庫儀表板* 則會摘要個別資料庫。 您可在 Azure Data Studio 的 [連線] Viewlet 中以滑鼠右鍵按一下伺服器或資料庫，並選取 [管理]，以存取其中一個儀表板。

:::image type="content" source="media/dashboard-extension/dashboard-summary.gif" alt-text="顯示儀表板簡介的螢幕擷取畫面。":::

延伸模組有三個貢獻點，可將功能新增至儀表板：

1. **完整儀表板索引標籤**：延伸模組儀表板中的個別索引標籤。 可新增至伺服器或資料庫儀表板。 可使用小工具、工具列和導覽區段進行自訂。
2. **Homepage Actions (首頁動作)** ：位於連線工具列頂端的 [Action] \(動作\) 按鈕。
3. **Widgets (小工具)** ：針對 SQL Server 執行的圖表。

   :::image type="content" source="media/dashboard-extension/dashboard-contrib-points.png" alt-text="顯示貢獻點的螢幕擷取畫面。":::

### <a name="run-the-extension-generator"></a>執行延伸模組產生器

若要建立延伸模組：

1. 使用下列命令啟動延伸模組產生器：

   `yo azuredatastudio`

1. 從延伸模組類型清單選擇 [New Dashboard] \(新增儀表板\)。

1. 填入提示 (如下所示) 以建立延伸模組，為伺服器儀表板提供索引標籤。

   :::image type="content" source="media/dashboard-extension/dashboard-generator.png" alt-text="顯示延伸模組產生器的螢幕擷取畫面。":::

   由於有許多提示，以下提供一些資訊來說明每個問題的涵義：

   :::image type="content" source="media/dashboard-extension/dashboard-flowchart.png" alt-text="顯示儀表板流程圖的螢幕擷取畫面。":::

完成上述步驟會建立新的資料夾。 在 Visual Studio Code 中開啟資料夾，即可建立自己的儀表板延伸模組。

### <a name="run-the-extension"></a>執行延伸模組

讓我們執行延伸模組來查看儀表板範本所提供的內容。 在執行前，請先確認您已在 Visual Studio Code 中安裝 **Azure Data Studio 偵錯延伸模組**。

在 VS Code 中選取 **F5**，以偵錯模式啟動執行延伸模組的 Azure Data Studio。 然後，您可以查看此預設範本對儀表板有何貢獻。

接下來，我們將探討如何修改這個預設儀表板。

### <a name="develop-the-dashboard"></a>開發儀表板

開始進行延伸模組開發時，最重要的檔案是 `package.json`。 此檔案是資訊清單檔，其中註冊了儀表板貢獻。 請注意 `dashboard.tabs`、`dashboard.insights` 和 `dashboard.containers` 區段。

以下是一些可嘗試的變更：

- 試著使用各種深入解析類型，包括 bar、horizontalBar 和 timeSeries。
- 自行撰寫要對 SQL Server 連線執行的查詢。
- 請參閱此[範例深入解析教學課程](../tutorial-qds-sql-server.md)或[本教學課程](../tutorial-table-space-sql-server.md)，以取得特定的深入解析教學課程。

## <a name="package-your-extension"></a>封裝您的延伸模組

若要與其他人共用，則需要將延伸模組封裝成單一檔案。 您的延伸模組可發佈到 Azure Data Studio 延伸模組市集，或與小組或社群共用。 若要執行此步驟，您必須從命令列安裝另一個 npm 套件。

```console
npm install -g vsce
```

依據您的喜好編輯 `README.md` 檔案。 然後，移至延伸模組的基底目錄，並執行 `vsce package`。 您可選擇將存放庫與延伸模組連結，或在不連結的情況下繼續。 若要新增，請將類似的一行新增到 `package.json` 檔案。

```json
"repository": {
    "type": "git",
    "url": "https://github.com/anjalia/my-test-extension.git"
}
```

新增這幾行之後，`my-test-extension-0.0.1.vsix` 檔案即已建立，並可安裝在 Azure Data Studio 中。

:::image type="content" source="media/dashboard-extension/install-vsix.png" alt-text="顯示安裝 VSIX 的螢幕擷取畫面。":::

## <a name="publish-your-extension-to-the-marketplace"></a>將您的延伸模組發佈到市集

Azure Data Studio 延伸模組市集正在建構中。 目前的程序是在某個位置裝載延伸模組 VSIX，例如 GitHub 發行頁面。 然後，請提交提取要求，以使用您的延伸模組資訊更新[此 JSON 檔案](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：
> [!div class="checklist"]
> - 安裝延伸模組產生器。
> - 建立您的延伸模組。
> - 參與延伸模組儀表板的編輯。
> - 測試您的延伸模組。
> - 封裝您的延伸模組。
> - 將延伸模組發佈到市集。

我們希望本文可為您帶來啟發，進而建置自己的 Azure Data Studio 延伸模組。 我們支援儀表板深入解析 (針對 SQL Server 執行的精美圖表)、一些 SQL 特定的 API，以及從 Visual Studio Code 繼承的一組龐大現有擴充點。

如果您有些想法，但不確定如何著手，請提出問題或透過 [azuredatastudio](https://twitter.com/azuredatastudio) 對小組推文。

[Visual Studio Code 延伸模組指南](https://code.visualstudio.com/docs/extensions/overview)涵蓋了所有現有的 API 和模式，可供您取得詳細資訊。

若要了解如何在 Azure Data Studio 中使用 T-SQL，請完成 T-SQL 編輯器教學課程：

> [!div class="nextstepaction"]
> [使用 Transact-SQL 編輯器建立資料庫物件](../tutorial-sql-editor.md)
