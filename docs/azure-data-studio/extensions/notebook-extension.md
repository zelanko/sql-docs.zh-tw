---
title: 建立 Jupyter Notebook 延伸模組
description: 了解如何使用延伸模組產生器將筆記本封裝成延伸模組。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: e2996b583cd1005e26e4334c9934fff79c321ee4
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364045"
---
# <a name="create-a-jupyter-notebook-extension"></a>建立 Jupyter Notebook 延伸模組

本教學課程示範如何建立新的 Jupyter Notebook Azure Data Studio 延伸模組。 延伸模組隨附可在 Azure Data Studio 中開啟的範例 Jupyter Notebook。

在本文中，您將了解如何：

> [!div class="checklist"]
> - 建立延伸模組專案。
> - 安裝延伸模組產生器。
> - 建立筆記本延伸模組。
> - 執行您的延伸模組。
> - 封裝您的延伸模組。
> - 將延伸模組發佈到市集。

## <a name="apis-used"></a>所使用的 API

- `azdata.nb.showNotebookDocument`

### <a name="extension-use-cases"></a>延伸模組使用案例

您可能會基於幾個不同原因而建立筆記本延伸模組：
- 共用互動式文件
- 儲存並持續存取該筆記本
- 提供程式碼問題以供使用者追蹤
- 版本控制及追蹤筆記本更新

## <a name="prerequisites"></a>先決條件

Azure Data Studio 建置在與 Visual Studio Code 相同的架構上，因此 Azure Data Studio 的延伸模組是使用 Visual Studio Code 所建立。 若要開始進行，您需要下列元件：

- `$PATH` 中已安裝並可供使用的 [Node.js](https://nodejs.org)。 Node.js 包含 Node.js 套件管理員 [npm](https://www.npmjs.com/)，可用來安裝延伸模組產生器。
- 用來偵錯延伸模組的 [Visual Studio Code](https://code.visualstudio.com)。
- 確定 `azuredatastudio` 在您的 PATH 中。 針對 Windows，請務必選擇 setup.exe 中的 [新增至路徑] 選項。 若是 Mac 或 Linux，請執行 [Install 'azuredatastudio' command in PATH] \(在 PATH 中安裝 'azuredatastudio' 命令\)**** 選項。

## <a name="install-the-extension-generator"></a>安裝延伸模組產生器

為了簡化建立延伸模組的程序，我們使用 Yeoman 建置了[延伸模組產生器](https://www.npmjs.com/package/generator-azuredatastudio)。 若要安裝，請從命令提示字元執行下列命令：

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-extension"></a>建立您的延伸模組

若要建立延伸模組：

1. 使用下列命令啟動延伸模組產生器：

   `yo azuredatastudio`

2. 從延伸模組類型清單中選擇 [新增筆記本 (個別)]。

   :::image type="content" source="media/notebook-extension/notebook-extension-generator.png" alt-text="Notebook 延伸模組產生器":::

3. 依照下列步驟填入延伸模組名稱。 在本教學課程中，請使用「測試筆記本」。 然後，填入發行者名稱。 在本教學課程中，請使用 **Microsoft**。 最後，新增描述。

現在，這就是某些分支所在的位置。 您可新增已建立的 Jupyter Notebook，或使用透過產生器提供給您的範例筆記本。

在本教學課程中，我們將使用範例 Python 筆記本：

   :::image type="content" source="media/notebook-extension/notebook-sample-generator.png" alt-text="選取 Python 範例":::

如果您有想要傳遞的筆記本，請回答您有想要傳遞的現有筆記本。 提供所有筆記本或 Markdown 檔案所在的絕對檔案路徑。

完成先前步驟會建立包含範例筆記本的新資料夾。 在 Visual Studio Code 中開啟資料夾後，您即已準備好傳遞新的筆記本延伸模組。

## <a name="understand-your-extension"></a>了解您的延伸模組

這是專案目前看起來的樣子：

   :::image type="content" source="media/notebook-extension/notebook-file-structure-generator.png" alt-text="延伸模組檔案結構":::

`vsc-extension-quickstart.md` 檔案提供重要檔案的參考。 您可以在 `README.md` 檔案中提供新延伸模組的文件。 請注意 `package.json`、`notebook.ts` 和 `pySample.ipynb` 檔案。

若您有任何不想要發佈的檔案或資料夾，可以在 `.vscodeignore` 檔案中包含這些檔案或資料夾的名稱。

讓我們看一下 `notebook.ts` 來了解新構成的延伸模組正在執行什麼工作。

```javascript
// This function is called when you run the command `Launch Notebooks: Test Notebook` from the
// command palette in Azure Data Studio. If you want any additional functionality
// to occur when you launch the book, add it to the activate function.
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand('launchNotebooks.test-notebook', () => {
        let notebooksToDisplay: Array<string> = processNotebooks();
        notebooksToDisplay.forEach(name => {
            azdata.nb.showNotebookDocument(vscode.Uri.file(name));
        });
    }));

    // Add other code here if you want to register another command.
}
```

這是 `notebook.ts` 中的主要函式，會在透過下列命令執行延伸模組時呼叫：[Launch Notebooks:Test Notebook] \(啟動 Notebook: 測試 Notebook\) 時呼叫。 我們使用 `vscode.commands.registerCommand` API 來建立新的命令。 下列位於括弧內的定義是我們每次呼叫命令時所執行的程式碼。 針對每個從 `processNotebooks` 函式中找到的筆記本，我們會使用 `azdata.nb.showNotebookDocument` 在 Azure Data Studio 中加以開啟。

`package.json` 檔案在註冊下列命令時也扮演重要角色：[Launch Notebooks:Test Notebook] \(啟動 Notebook: 測試 Notebook\) 時呼叫。

```json
"activationEvents": [
        "onCommand:launchNotebooks.test-notebook"
    ],
    "main": "./out/notebook.js",
    "contributes": {
        "commands": [
            {
                "command": "launchNotebooks.test-notebook",
                "title": "Launch Notebooks: Test Notebook"
            }
        ]
    }
```

我們擁有一個命令的啟用事件，此外也新增了特定的貢獻點。 這些貢獻點會在發佈延伸模組的延伸模組市集中，在使用者尋找延伸模組時顯示。 若想要新增更多命令，請務必將這些命令新增至 `activationEvents` 欄位。 如需更多選項，請參閱[啟用事件](https://code.visualstudio.com/api/references/activation-events)。

## <a name="package-your-extension"></a>封裝您的延伸模組

若要與其他人共用，則需要將延伸模組封裝成單一檔案。 您的延伸模組可發佈到 Azure Data Studio 延伸模組市集，或與小組或社群共用。 若要執行此步驟，您必須從命令列安裝另一個 npm 套件。

```console
`npm install -g vsce`
```

依據您的喜好編輯 `README.md` 檔案。 然後，移至延伸模組的基底目錄，並執行 `vsce package`。 您可選擇將存放庫與延伸模組連結，或在不連結的情況下繼續。 若要新增，請將類似的一行新增到 `package.json` 檔案。

```json
"repository": {
    "type": "git",
    "url": "https://github.com/laurajjiang/testnotebook.git"
}
```

新增這幾行之後，`my test-notebook-0.0.1.vsix` 檔案即已建立，可供安裝並與任何人共用。

## <a name="run-your-extension"></a>執行延伸模組

若要執行和測試延伸模組，請開啟 Azure Data Studio，然後選取 **Ctrl+Shift+P** 以開啟命令選擇區。 尋找命令 [Extensions:從 VSIX 安裝]，然後移至包含新延伸模組的資料夾。

   :::image type="content" source="media/notebook-extension/install-vsix.png" alt-text="安裝 VSIX":::

您的延伸模組現在應該會顯示在 Azure Data Studio 中的延伸模組面板上。 再次開啟命令選擇區，您即會找到使用延伸模組所建立的新命令 [Launch Book:Test Book] \(啟動書籍: 測試書籍\)。 執行時，其應該會開啟我們使用延伸模組所封裝的 Jupyter Book。

   :::image type="content" source="media/notebook-extension/notebook-launch-ads.png" alt-text="Notebook-命令":::

恭喜！ 您已建置且可傳遞第一個 Jupyter Notebook 延伸模組。

## <a name="publish-your-extension-to-the-marketplace"></a>將您的延伸模組發佈到市集

Azure Data Studio 延伸模組市集正在建構中。 若要發佈，請在某個位置裝載延伸模組 VSIX，例如 GitHub 發行頁面。 然後，提交提取要求，以使用您的延伸模組資訊更新[此 JSON 檔案](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：
> [!div class="checklist"]
> - 建立延伸模組專案。
> - 安裝延伸模組產生器。
> - 建立筆記本延伸模組。
> - 建立您的延伸模組。
> - 封裝您的延伸模組。
> - 將延伸模組發佈到市集。

我們希望本文可為您帶來啟發，進而建置自己的 Azure Data Studio 延伸模組。

如果您有些想法，但不確定如何著手，請提出問題或透過 [azuredatastudio](https://twitter.com/azuredatastudio) 對小組推文。

[Visual Studio Code 延伸模組指南](https://code.visualstudio.com/docs/extensions/overview)涵蓋了所有現有的 API 和模式，可供您取得詳細資訊。