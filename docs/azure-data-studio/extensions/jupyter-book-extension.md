---
title: 建立 Jupyter Book 延伸模組
description: 了解如何使用延伸模組產生器將 Jupyter Book 封裝成延伸模組。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 5d9138a5d02008cc173bc7f0b64d354d67112d3b
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364085"
---
# <a name="create-a-jupyter-book-extension"></a>建立 Jupyter Book 延伸模組

本教學課程會示範如何建立新的 Jupyter Book Azure Data Studio 延伸模組。 延伸模組隨附可在 Azure Data Studio 中開啟的範例 Jupyter Book。

在本文中，您將了解如何：

> [!div class="checklist"]
> - 建立延伸模組專案。
> - 安裝延伸模組產生器。
> - 建立您的 Jupyter Book 延伸模組。
> - 執行您的延伸模組。
> - 封裝您的延伸模組。
> - 將延伸模組發佈到市集。

## <a name="apis-used"></a>所使用的 API

- `bookTreeView.openBook`

### <a name="extension-use-cases"></a>延伸模組使用案例

您可能會基於幾個不同原因而建立 Jupyter Book 延伸模組：

- 共用組織和分節互動文件
- 共用完整的書籍 (與電子書類似，但透過 Azure Data Studio 散發)
- 版本控制及追蹤 Jupyter Book 更新

Jupyter Book 和筆記本延伸模組之間的差異是 Jupyter Book 可提供組織。 您可將數十個筆記本分成 Jupyter Book 中的不同章節，但筆記本延伸模組的目的是傳遞少量的個別筆記本。

## <a name="prerequisites"></a>先決條件

Azure Data Studio 建置在與 Visual Studio Code 相同的架構上，因此 Azure Data Studio 的延伸模組是使用 Visual Studio Code 所建立。 若要開始進行，您需要下列元件：

- `$PATH` 中已安裝並可供使用的 [Node.js](https://nodejs.org)。 Node.js 包含 Node.js 套件管理員 [npm](https://www.npmjs.com/)，可用來安裝延伸模組產生器。
- [Visual Studio Code](https://code.visualstudio.com)，以對延伸模組進行任何變更及針對延伸模組進行偵錯。
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

1. 從延伸模組類型清單中選擇 [新增 Jupyter Book]。

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-extension-generator.png" alt-text="顯示延伸模組產生器的螢幕擷取畫面。":::

1. 依照下列步驟填入延伸模組名稱。 在本教學課程中，請使用「測試書籍」。 然後，填入發行者名稱。 在本教學課程中，請使用 **Microsoft**。 最後，新增描述。

您可選取提供現有的 Jupyter Book、使用範例書籍，或建立新的 Jupyter Book。 三個選項都會顯示。

### <a name="provide-an-existing-book"></a>提供現有書籍

如果您想要傳遞已建立的書籍，請提供書籍內容所在資料夾的絕對檔案路徑。 您接著即會準備好繼續了解延伸模組及傳遞延伸模組的過程。

:::image type="content" source="media/jupyter-book-extension/jupyter-book-existing-book.png" alt-text="顯示現有書籍的螢幕擷取畫面。":::

### <a name="use-the-sample-book"></a>使用範例書籍

若您沒有現有的書籍或筆記本，可以使用產生器中提供的範例。

:::image type="content" source="media/jupyter-book-extension/jupyter-book-sample-path.png" alt-text="顯示範例 Jupyter Book 的螢幕擷取畫面。":::

範例書籍會展示簡易 Jypyter Book 的外觀。 如果您想要了解如何自訂 Jypyter Book，請參閱下一節與如何使用現有筆記本建立新書籍有關的內容。

### <a name="create-a-new-book"></a>建立新書籍

如果您有想要封裝成 Jypyter Book 的筆記本，則可執行這項操作。 產生器會詢問您是否要在書籍中包含章節、要包含多少章節，以及各章節的標題。 您可在這裡查看選取程序。 使用空格鍵可選取您要放入各章節中的筆記本。

:::image type="content" source="media/jupyter-book-extension/jupyter-book-create-book.png" alt-text="顯示建立 Jupyter Book 的螢幕擷取畫面。":::

完成先前步驟會建立包含全新 Jypyter Book 的新資料夾。 在 Visual Studio Code 中開啟資料夾後，您便已準備好傳遞 Jypyter Book 延伸模組。

## <a name="understand-your-extension"></a>了解您的延伸模組

這是專案目前看起來的樣子：

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-file-structure-generator.png" alt-text="顯示延伸模組檔案結構的螢幕擷取畫面。":::

`vsc-extension-quickstart.md` 檔案提供重要檔案的參考。 您可以在 `README.md` 檔案中提供新延伸模組的文件。 請注意 `package.json`、`jupyter-book.ts`、`content` 和 `toc.yml` 檔案。 `content` 資料夾保存所有筆記本或 Markdown 檔案。 `toc.yml` 會構成 Jupyter Book 的結構，且會在選擇透過延伸模組產生器建立自訂 Jupyter Book 時自動產生。

若使用產生器並選擇書籍中的章節來建立書籍，則資料夾結構可能會有些不同。 Markdown 和 Jupyter Notebook 檔案會保存在對應到針對章節所選標題的子資料夾中，而非 `content` 資料夾內。

若您有任何不想要發佈的檔案或資料夾，可以在 `.vscodeignore` 檔案中包含這些檔案或資料夾的名稱。

讓我們看一下 `jupyter-book.ts` 來了解新構成的延伸模組正在執行什麼工作。

```javascript
// This function is called when you run the command `Launch Book: Test Book` from the
// command palette in Azure Data Studio. If you want any additional functionality
// to occur when you launch the book, add it to the activate function.
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand('launchBook.test-book', () => {
        processNotebooks();
    }));

    // Add other code here if you want to register another command.
}
```

`activate` 函式是延伸模組的主要動作。 任何所要註冊的命令都應出現在 `activate` 函式中，與 `launchBook.test-book` 命令相似。 在 `processNotebooks` 函式中，我們會尋找保存 Jupyter Book 的延伸模組資料夾，並使用延伸模組的資料夾作為參數來呼叫 `bookTreeView.openBook`。

`package.json` 檔案在註冊延伸模組命令的過程中也扮演重要角色。

```json
"activationEvents": [
        "onCommand:launchBook.test-book"
    ],
    "main": "./out/notebook.js",
    "contributes": {
        "commands": [
            {
                "command": "launchBook.test-book",
                "title": "Launch Book: Test Book"
            }
        ]
    }
```

啟用事件 `onCommand` 會在叫用命令時觸發註冊的函式。 還有一些其他的啟用事件可能可提供其他自訂。 如需詳細資訊，請參閱[啟用事件](https://code.visualstudio.com/api/references/activation-events)。

## <a name="package-your-extension"></a>封裝您的延伸模組

若要與其他人共用，則需要將延伸模組封裝成單一檔案。 您的延伸模組可發佈到 Azure Data Studio 延伸模組市集，或與小組或社群共用。 若要執行此步驟，您必須從命令列安裝另一個 npm 套件。

```console
`npm install -g vsce`
```

依據您的喜好編輯 `README.md` 檔案。 然後，移至延伸模組的基底目錄，並執行 `vsce package`。 您可選擇將存放庫與延伸模組連結，或在不連結的情況下繼續。 若要新增，請將類似的一行新增到 `package.json` 檔案。

```json
"repository": {
    "type": "git",
    "url": "https://github.com/laurajjiang/testbook.git"
}
```

新增這幾行之後，`my test-book-0.0.1.vsix` 檔案即已建立，並可安裝在 Azure Data Studio 中。

## <a name="run-your-extension"></a>執行延伸模組

若要執行和測試延伸模組，請開啟 Azure Data Studio，然後選取 **Ctrl+Shift+P** 以開啟命令選擇區。 尋找命令 [Extensions:從 VSIX 安裝]，然後移至包含新延伸模組的資料夾。 其現在應該會顯示在 Azure Data Studio 中延伸模組面板上。

   :::image type="content" source="media/jupyter-book-extension/install-vsix.png" alt-text="顯示安裝 VSIX 的螢幕擷取畫面。":::

再次開啟命令選擇區，然後尋找已註冊的命令 [Launch Book:Test Notebook] \(啟動 Notebook: 測試 Notebook\) 時呼叫。 執行時，其應該會開啟我們使用延伸模組所封裝的 Jupyter Book。

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-launch-ads.png" alt-text="顯示筆記本命令的螢幕擷取畫面。":::

恭喜！ 您已建置且可傳遞第一個 Jupyter Book 延伸模組。 如需 Jupyter Book 的詳細資訊，請參閱 [Book with Jupyter](https://jupyterbook.org/intro.html) (使用 Jupyter 撰寫書籍)。

## <a name="publish-your-extension-to-the-marketplace"></a>將延伸模組發佈到 Marketplace

Azure Data Studio 延伸模組市集正在建構中。 若要發佈，請在某個位置裝載延伸模組 VSIX，例如 GitHub 發行頁面。 提交提取要求，以使用您的延伸模組資訊更新[此 JSON 檔案](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：
> [!div class="checklist"]
> - 建立延伸模組專案。
> - 安裝延伸模組產生器。
> - 建立您的 Jupyter Book 延伸模組。
> - 封裝您的延伸模組。
> - 將延伸模組發佈到市集。

我們希望在閱讀完本文後，您會對想要和 Azure Data Studio 社群分享的 Jupyter Book 有些想法。

如果您有些想法，但不確定如何著手，請提出問題或透過 [azuredatastudio](https://twitter.com/azuredatastudio) 對小組推文。

[Visual Studio Code 延伸模組指南](https://code.visualstudio.com/docs/extensions/overview)涵蓋了所有現有的 API 和模式，可供您取得詳細資訊。
