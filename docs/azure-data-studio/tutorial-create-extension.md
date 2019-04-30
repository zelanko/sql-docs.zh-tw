---
title: 教學課程：建立延伸模組
titleSuffix: Azure Data Studio
description: 本教學課程會示範如何建立自訂功能加入 Azure Data Studio 的擴充功能。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: kevcunnane
ms.author: kcunnane
manager: craigg
ms.openlocfilehash: 8389cbad7e5124c1c20c2e076df34fc97306d8ef
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309467"
---
# <a name="tutorial-create-an-azure-data-studio-extension"></a>教學課程：建立 Azure Data Studio 擴充功能

本教學課程會示範如何建立新的 Azure Data Studio 擴充功能。 延伸模組會建立在 Azure 資料 Studio 中熟悉 SSMS 的索引鍵繫結。

在本教學課程期間您會了解如何：
> [!div class="checklist"]
> * 建立擴充功能專案
> * 安裝延伸模組產生器
> * 建立您的延伸模組
> * 測試您的延伸模組
> * 封裝您的延伸模組
> * 將您的延伸模組發佈至 marketplace

## <a name="prerequisites"></a>先決條件

Azure Data Studio 是內建為 Visual Studio Code 中，在同一架構上，因此使用 Visual Studio Code 建置適用於 Azure Data Studio 擴充功能。 若要開始，您需要下列元件：

- [Node.js](https://nodejs.org)已安裝，而且可在您`$PATH`。 包含 Node.js [npm](https://www.npmjs.com/)，Node.js 套件管理員，用來安裝延伸模組產生器。
- [Visual Studio Code](https://code.visualstudio.com)偵錯擴充功能。
- Azure Data Studio[偵錯延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug)（選擇性）。 這可讓您測試您的延伸模組，而不需要封裝，然後將它安裝到 Azure Data Studio。
- 請確定`azuredatastudio`是在您的路徑。 針對 Windows，請確定您選擇`Add to Path`在 setup.exe 的選項。 適用於 Mac 或 Linux，執行*安裝路徑中的 'azuredatastudio' 命令*選項。


## <a name="install-the-extension-generator"></a>安裝延伸模組產生器

若要簡化建立延伸模組的程序，我們已建置[延伸模組產生器](https://code.visualstudio.com/docs/extensions/yocode)使用 Yeoman。 若要安裝它，從命令提示字元執行下列命令：

`npm install -g yo generator-azuredatastudio`

## <a name="create-your-extension"></a>建立您的延伸模組

若要建立擴充功能：

1. 啟動延伸模組產生器，使用下列命令：

   `yo azuredatastudio`

2. 選擇**新的快速鍵**從延伸模組類型的清單：

   ![延伸模組產生器](./media/tutorial-create-extension/extension-generator.png)

3. 遵循步驟來填入 延伸模組名稱 (本教學課程中，使用**ssmskeymap2**)，並且加入的描述。

完成上述步驟建立新的資料夾。 開啟 Visual Studio Code 和您的資料夾已準備好建立您自己的索引鍵繫結延伸模組 ！


### <a name="add-a-keyboard-shortcut"></a>將鍵盤快速鍵

**步驟 1：尋找要取代的快速鍵**

既然我們已經準備好了我們延伸模組，新增一些 SSMS 鍵盤快速鍵 （或按鍵組合） 至 Azure 資料 Studio。 我使用了[Andy Mallon 速查表](https://am2.co/2018/02/updated-cheat-sheet/)和靈感 RedGate 的鍵盤快速鍵清單。

我看到遺失的最上層項目所示：

- 執行查詢與啟用的實際執行計畫。 這是**Ctrl + M**在 SSMS 中，在 Azure Data Studio 沒有繫結。
- 擁有**CTRL + SHIFT + E**作為執行查詢的第二個方法。 使用者意見反應指出這是遺漏。
- 擁有**ALT + F1**執行`sp_help`。 我們已將此 Azure Data Studio 中加入，但因為該繫結已在使用中，我們會對應到**ALT + F2**改。
- 切換全螢幕 (**SHIFT + ALT + ENTER**)。
- **F8**以顯示**物件總管 中** / **Servers 檢視**。

很容易尋找和取代這些按鍵繫結。 執行*開啟的鍵盤快速鍵*以顯示**鍵盤快速鍵**索引標籤中 Azure Data Studio，搜尋*查詢*，然後選擇 **變更索引鍵繫結**. 一旦您完成變更按鍵繫結關係，您可以看到更新的對應 keybindings.json 檔案中 (執行*開啟的鍵盤快速鍵*看到它)。

![鍵盤快速鍵](./media/tutorial-create-extension/keyboard-shortcuts.png)

![keybindings.json 延伸模組](./media/tutorial-create-extension/keybindings-json.png)


**步驟 2：將捷徑新增至延伸模組**

若要加入延伸模組中的快速鍵，請開啟*package.json*檔案 （副檔名），並取代`contributes`有下列區段：

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

請確定`azuredatastudio`藉由在 Azure Data Studio 中的 [路徑] 命令執行安裝 azuredatastudio 命令是在您的路徑。

確定 Azure 資料 Studio 偵錯延伸模組已安裝 Visual Studio Code 中。

選取  **F5**使用來啟動 Azure Data Studio 處於偵錯模式執行的擴充功能：

![安裝擴充功能](./media/tutorial-create-extension/install-extension.png)

![測試擴充功能](./media/tutorial-create-extension/test-extension.png)

索引鍵的對應是其中一個最快速的延伸模組，若要建立，因此您新的延伸模組現在應該可以順利運作，並準備好共用。

## <a name="package-your-extension"></a>封裝您的延伸模組

若要與其他人共用，您需要封裝到單一檔案的延伸模組。 這可以是發佈至 Azure Data Studio 擴充功能 marketplace，或在您的團隊或社群之間共用。 若要這樣做，您需要從命令列安裝另一個的 npm 套件：

`npm install -g vsce`

瀏覽至 延伸模組的基底目錄，然後執行`vsce package`。 我將在幾個額外的線路，以停止*vsce*從抱怨的工具：

```json
"repository": {
    "type": "git",
    "url": "https://github.com/kevcunnane/ssmskeymap.git"
},
"bugs": {
    "url": "https://github.com/kevcunnane/ssmskeymap/issues"
},
```

這項作業完成之後, 我 ssmskeymap 0.1.0.vsix 檔案已建立並準備好安裝，並與全世界分享 ！

![安裝擴充功能](./media/tutorial-create-extension/extensions.png)


## <a name="publish-your-extension-to-the-marketplace"></a>將您的延伸模組發佈至 marketplace

Azure Data Studio 擴充功能 marketplace 完全尚未實作，但目前的處理序裝載的延伸模組的 VSIX 某處 （例如，GitHub 版本頁面） 然後提交提取要求更新[此 JSON 檔案](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)與您擴充功能資訊。


## <a name="next-steps"></a>後續步驟

在本教學課程中，您將了解如何：
> [!div class="checklist"]
> * 建立擴充功能專案
> * 安裝延伸模組產生器
> * 建立您的延伸模組
> * 測試您的延伸模組
> * 封裝您的延伸模組
> * 將您的延伸模組發佈至 marketplace


我們希望閱讀您將充滿靈感來建置您自己的延伸模組適用於 Azure 資料 Studio 這個之後。 我們支援儀表板深入解析 （針對您的 SQL Server 執行的美化圖形）、 數個特定的 SQL Api 和現有無數的繼承自 Visual Studio Code 的擴充點。

如果您有任何想法，但不確定如何開始使用，請開啟問題或在小組的推文： [azuredatastudio](https://twitter.com/azuredatastudio)。

您一律可以參考[Visual Studio Code 擴充功能指南](https://code.visualstudio.com/docs/extensions/overview)因為它涵蓋所有現有的 Api 和模式。


若要了解如何使用 Azure Data Studio 中的 T-SQL，完成 T-SQL 編輯器教學課程：

> [!div class="nextstepaction"]
> [使用 TRANSACT-SQL 編輯器來建立資料庫物件](tutorial-sql-editor.md)。
