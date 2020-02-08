---
title: 教學課程：建立延伸模組
titleSuffix: Azure Data Studio
description: 本教學課程示範如何建立延伸模組，將自訂功能新增至 Azure Data Studio。
ms.custom: seodec18
ms.date: 12/10/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: rothja
ms.author: jroth
ms.openlocfilehash: a8a8481653f7161b39cc752878f4544f98751261
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75241758"
---
# <a name="tutorial-create-an-azure-data-studio-extension"></a>教學課程：建立 Azure Data Studio 延伸模組

本教學課程示範如何建立新的 Azure Data Studio 延伸模組。 此延伸模組會在 Azure Data Studio 中建立熟悉的 SSMS 按鍵繫結關係。

在本教學課程中，您將了解如何：
> [!div class="checklist"]
> * 建立延伸模組專案
> * 安裝延伸模組產生器
> * 建立您的延伸模組
> * 測試您的延伸模組
> * 封裝您的延伸模組
> * 將您的延伸模組發佈到市集

## <a name="prerequisites"></a>Prerequisites

Azure Data Studio 建置在與 Visual Studio Code 相同的架構上，因此 Azure Data Studio 的延伸模組是使用 Visual Studio Code 所建立。 若要開始進行，您需要下列元件：

- `$PATH` 中已安裝並可供使用的 [Node.js](https://nodejs.org)。 Node.js 包含 Node.js 套件管理員 [npm](https://www.npmjs.com/)，可用來安裝延伸模組產生器。
- 用來偵錯延伸模組的 [Visual Studio Code](https://code.visualstudio.com)。
- Azure Data Studio [偵錯延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug) (選擇性)。 讓您不需要將延伸模組封裝並安裝到 Azure Data Studio 中，即可進行測試。
- 確定 `azuredatastudio` 在您的 PATH 中。 若是 Windows，請務必選擇 setup.exe 中的 [`Add to Path`] 選項。 若是 Mac 或 Linux，請執行 [Install 'azuredatastudio' command in PATH] \(在 PATH 中安裝 'azuredatastudio' 命令\)  選項。


## <a name="install-the-extension-generator"></a>安裝延伸模組產生器

為了簡化建立延伸模組的程序，我們使用 Yeoman 建置了[延伸模組產生器](https://code.visualstudio.com/docs/extensions/yocode)。 若要加以安裝，請從命令提示字元執行下列命令：

`npm install -g yo generator-azuredatastudio`

## <a name="create-your-extension"></a>建立您的延伸模組

若要建立延伸模組：

1. 使用下列命令啟動延伸模組產生器：

   `yo azuredatastudio`

2. 從延伸模組類型清單選擇 [New Keymap] \(新增按鍵對應\)  ：

   ![延伸模組產生器](./media/tutorial-create-extension/extension-generator.png)

3. 遵循步驟填入延伸模組名稱 (在本教學課程中，使用 **ssmskeymap2**)，並新增描述。

完成上述步驟會建立新的資料夾。 在 Visual Studio Code 中開啟資料夾，即可建立您自己的按鍵繫結關係延伸模組！


### <a name="add-a-keyboard-shortcut"></a>新增鍵盤快速鍵

**步驟 1：尋找要取代的快速鍵**

現在我們已準備好延伸模組，請將一些 SSMS 鍵盤快速鍵 (或按鍵繫結關係) 新增至 Azure Data Studio。 我使用 [Andy Mallon 的速查表](https://am2.co/2018/02/updated-cheat-sheet/)和 RedGate 的鍵盤快速鍵清單來激發靈感。

我發現遺漏了下列重要項目：

- 在啟用實際執行計畫的情況下執行查詢。 這在 SSMS 中是 **Ctrl+M**，但在 Azure Data Studio 中沒有繫結關係。
- 以 **CTRL+SHIFT+E** 作為執行查詢的第二個方法。 使用者意見反應指出遺漏此項目。
- 讓 **ALT+F1** 執行 `sp_help`。 我們已在 Azure Data Studio 中新增此項目，但因為該繫結關係已經在使用，所以我們改為對應至 **ALT+F2**。
- 切換全螢幕 (**SHIFT+ALT+ENTER**)。
- **F8** 顯示物件總管   / [伺服器檢視]  。

尋找及取代這些按鍵繫結關係很容易。 執行 [開啟鍵盤快速鍵]  ，在 Azure Data Studio 中顯示 [鍵盤快速鍵]  索引標籤，搜尋 *query*，然後選擇 [Change Key binding] \(變更按鍵繫結關係\)  。 完成變更按鍵繫結關係之後，您可以在 keybindings.json 檔案中查看更新的對應 (執行 [開啟鍵盤快速鍵]  即可查看)。

![鍵盤快速鍵](./media/tutorial-create-extension/keyboard-shortcuts.png)

![keybindings.json 延伸模組](./media/tutorial-create-extension/keybindings-json.png)


**步驟 2：將快速鍵新增至延伸模組**

若要將快速鍵新增至延伸模組，請開啟延伸模組中的 *package.json* 檔案，然後將 `contributes` 區段取代為下列內容：

```json
"contributes": {
  "keybindings": [
    {
      "key": "shift+cmd+e",
      "command": "runQueryKeyboardAction"
    },
    {
      "key": "ctrl+cmd+e",
      "command": "workbench.view.explorer"
    },
    {
      "key": "alt+f1",
      "command": "workbench.action.query.shortcut1"
    },
    {
      "key": "shift+alt+enter",
      "command": "workbench.action.toggleFullScreen"
    },
    {
      "key": "f8",
      "command": "workbench.view.connections"
    },
    {
      "key": "ctrl+m",
      "command": "runCurrentQueryWithActualPlanKeyboardAction"
    }
  ]
}
```

## <a name="test-your-extension"></a>測試您的延伸模組

在 Azure Data Studio 中執行 [Install azuredatastudio command in PATH] \(在 PATH 中安裝 azuredatastudio 命令\) 的命令，確定 `azuredatastudio` 在您的 PATH 中。

確定已在 Visual Studio Code 中安裝 Azure Data Studio 偵錯延伸模組。

選取 **F5**，在偵錯模式中啟動 Azure Data Studio 並執行延伸模組：

![安裝延伸模組](./media/tutorial-create-extension/install-extension.png)

![測試延伸模組](./media/tutorial-create-extension/test-extension.png)

按鍵對應是可最快速建立的延伸模組之一，因此您的新延伸模組現在應該會成功運作並可供分享。

## <a name="package-your-extension"></a>封裝您的延伸模組

若要分享給其他人，您必須將延伸模組封裝成單一檔案。 此檔案可發佈到 Azure Data Studio 延伸模組市集，或是在您的小組或社群分享。 若要執行這項操作，您必須從命令列安裝另一個 npm 套件：

`npm install -g vsce`

巡覽至延伸模組的基底目錄，然後執行 `vsce package`。 我必須新增幾行額外的程式碼，以停止 *vsce* 工具回報問題：

```json
"repository": {
    "type": "git",
    "url": "https://github.com/kevcunnane/ssmskeymap.git"
},
"bugs": {
    "url": "https://github.com/kevcunnane/ssmskeymap/issues"
},
```

完成此作業之後，我的 ssmskeymap-0.1.0.vsix 檔案便已建立，可供安裝並與全世界分享！

![安裝延伸模組](./media/tutorial-create-extension/extensions.png)


## <a name="publish-your-extension-to-the-marketplace"></a>將您的延伸模組發佈到市集

Azure Data Studio 延伸模組市集尚未完全實行，目前的程序是在其他地方 (例如 GitHub 版本頁面) 裝載延伸模組 VSIX，然後提交 PR 並將[此 JSON 檔案](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)更新為您的延伸模組資訊。


## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：
> [!div class="checklist"]
> * 建立延伸模組專案
> * 安裝延伸模組產生器
> * 建立您的延伸模組
> * 測試您的延伸模組
> * 封裝您的延伸模組
> * 將您的延伸模組發佈到市集


希望藉由閱讀本文，可激發您的靈感，建置自己的 Azure Data Studio 延伸模組。 我們支援儀表板深入解析 (針對 SQL Server 執行的精美圖表)、一些 SQL 特定的 API，以及從 Visual Studio Code 繼承的一組龐大現有擴充點。

如果您有些想法，但不確定如何著手，請提出問題或對 [azuredatastudio](https://twitter.com/azuredatastudio) 小組推文。

您可以隨時參考 [Visual Studio Code 延伸模組指南](https://code.visualstudio.com/docs/extensions/overview)，因為指南涵蓋了所有現有的 API 和模式。


若要了解如何在 Azure Data Studio 中使用 T-SQL，請完成 T-SQL 編輯器教學課程：

> [!div class="nextstepaction"]
> [使用 Transact-SQL 編輯器建立資料庫物件](tutorial-sql-editor.md)。
