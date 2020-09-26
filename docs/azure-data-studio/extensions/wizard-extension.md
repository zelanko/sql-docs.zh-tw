---
title: 建立精靈延伸模組
description: 本教學課程示範如何建立精靈延伸模組，將自訂功能新增至 Azure Data Studio。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 50440aca120dad6cfd165262bd4bfd2e139393cf
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364055"
---
# <a name="create-an-azure-data-studio-wizard-extension"></a>建立 Azure Data Studio 精靈延伸模組

本教學課程示範如何建立新的 **Azure Data Studio 精靈延伸模組**。 延伸模組會在 Azure Data Studio 中提供和使用者互動的精靈。

在本文中，您將了解如何：
> [!div class="checklist"]
> - 安裝延伸模組產生器
> - 建立您的延伸模組
> - 將自訂精靈新增到延伸模組
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

## <a name="create-your-wizard-extension"></a>建立精靈延伸模組

### <a name="introduction-to-wizards"></a>精靈簡介

精靈是一種使用者介面類型，其可為使用者呈現逐步頁面，讓使用者按照順序填寫來完成工作。 常見的範例包括軟體安裝精靈和疑難排解精靈。 例如：

:::image type="content" source="media/wizard-extension/dacpac-wizard.gif" alt-text="Dacpac 精靈":::

由於在使用資料和延伸 Azure Data Studio 的功能時，精靈通常會很有幫助，因此 Azure Data Studio 提供 API 來建立您自己的自訂精靈。 我們將逐步解說如何產生精靈範本並加以修改，以建立您自己的自訂精靈。

### <a name="run-the-extension-generator"></a>執行延伸模組產生器

若要建立延伸模組：

1. 使用下列命令啟動延伸模組產生器：

   `yo azuredatastudio`

2. 從延伸模組類型清單選擇 [New Wizard or Dialog] \(新增精靈或對話方塊\)。 然後依序選取 [Wizard] \(精靈\)、[Getting Started Template] \(入門範本\)

3. 遵循步驟填入延伸模組名稱 (針對本教學課程，請使用 **My Test Extension**)，並新增描述。

    :::image type="content" source="media/wizard-extension/extension-generator.png" alt-text="延伸模組產生器":::

完成上述步驟會建立新的資料夾。 在 Visual Studio Code 中開啟資料夾，即可建立您自己的精靈延伸模組！

### <a name="run-the-extension"></a>執行延伸模組

讓我們執行延伸模組來查看精靈範本所提供的內容。 在執行前，請先確認已在 Visual Studio Code 中安裝 **Azure Data Studio 偵錯延伸模組**。

請在 VS Code 中選取 **F5** 來以偵錯模式啟動執行延伸模組的 Azure Data Studio。 然後，在 Azure Data Studio 中，在新的視窗中從命令選擇區 (Ctrl+Shift+P) 執行 [Launch Wizard] \(啟動精靈\)。 這會啟動此此延伸模組所提供的預設精靈：

:::image type="content" source="media/wizard-extension/wizard-template.gif" alt-text="精靈範本":::

接下來，我們將探討如何修改這個預設精靈。

### <a name="develop-the-wizard"></a>開發精靈

開始進行延伸模組開發的最重要檔案便是 `package.json`、`src/main.ts` 和 `vsc-extension-quickstart.md`：

- `package.json`:這是資訊清單檔案，其中註冊了 [啟動精靈] 命令。 這也是宣告 `main.ts` 為主要程式進入點的位置。
- `main.ts`:包含將 UI 元素新增至精靈的程式碼，例如頁面、文字和按鈕
- `vsc-extension-quickstart.md`:包含在開發時可能可作為實用參考的技術文件

讓我們對精靈進行變更：我們會新增第 4 個內容為空白的頁面。 按照以下方式修改 `src/main.ts`，在啟動精靈時便應該會看到顯示額外的頁面。

:::image type="content" source="media/wizard-extension/wizard-main.png" alt-text="精靈 main":::
當熟悉範本後，以下是可嘗試的其他概念：

- 將寬度為 300 的按鈕新增到新頁面
- 新增要放入按鈕的彈性元件
- 將動作新增到按鈕。 例如：當按一下按鈕時，啟動開啟檔案的對話方塊或開啟查詢編輯器。

## <a name="package-your-extension"></a>封裝您的延伸模組

若要分享給其他人，您必須將延伸模組封裝成單一檔案。 此檔案可發佈到 Azure Data Studio 延伸模組市集，或是在您的小組或社群分享。 若要執行這項操作，您必須從命令列安裝另一個 npm 套件：

```console
npm install -g vsce`
```

請依照需求編輯 `README.md`，然後巡覽至延伸模組的基礎目錄，並執行 `vsce package`。 您可選擇將存放庫與延伸模組連結，或在不連結的情況下繼續。 若要新增，請將類似的一行新增到 `package.json` 檔案。

```json
"repository": {
    "type": "git",
    "url": "https://github.com/anjalia/my-test-extension.git"
}
```

在新增這些行後，my-test-extension-0.0.1.vsix 便已建立，並已準備好在 Azure Data Studio 中安裝。

:::image type="content" source="media/wizard-extension/install-vsix.png" alt-text="安裝 VSIX":::

## <a name="publish-your-extension-to-the-marketplace"></a>將您的延伸模組發佈到市集

Azure Data Studio 延伸模組市集尚未完全實行，目前的程序是在其他地方 (例如 GitHub 版本頁面) 裝載延伸模組 VSIX，然後提交 PR 並將[此 JSON 檔案](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)更新為您的延伸模組資訊。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：
> [!div class="checklist"]
> - 安裝延伸模組產生器
> - 建立您的延伸模組
> - 將自訂精靈新增到延伸模組
> - 測試您的延伸模組
> - 封裝您的延伸模組
> - 將您的延伸模組發佈到市集

希望藉由閱讀本文，可激發您的靈感，建置自己的 Azure Data Studio 延伸模組。 我們支援儀表板深入解析 (針對 SQL Server 執行的精美圖表)、一些 SQL 特定的 API，以及從 Visual Studio Code 繼承的一組龐大現有擴充點。

如果您有些想法，但不確定如何著手，請提出問題或對 [azuredatastudio](https://twitter.com/azuredatastudio) 小組推文。

您可以隨時參考 [Visual Studio Code 延伸模組指南](https://code.visualstudio.com/docs/extensions/overview)，因為指南涵蓋了所有現有的 API 和模式。

若要了解如何在 Azure Data Studio 中使用 T-SQL，請完成 T-SQL 編輯器教學課程：

> [!div class="nextstepaction"]
> [使用 Transact-SQL 編輯器建立資料庫物件](../tutorial-sql-editor.md)
