---
title: 建立延伸模組
description: 您可以使用延伸模組將功能新增到 Azure Data Studio。 了解如何建立延伸模組，以及如何將延伸模組發佈到延伸模組資源庫。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: bd2a20857c8f16ea2b2d71ebfcb620bcea3f0190
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778417"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>藉由建立 Azure Data Studio 延伸模組來擴充功能

Azure Data Studio 中的延伸模組提供一種簡單方式，其可將更多功能新增至基底 Azure Data Studio 安裝。

延伸模組是由 Azure Data Studio 小組 (Microsoft) 及協力廠商社群 (您！) 提供。


## <a name="author-an-extension"></a>撰寫延伸模組

如果您有興趣擴充 Azure Data Studio，您可以建立自己的延伸模組，並將其發佈至延伸模組資源庫。

**撰寫延伸模組**

***先決條件***

若要開發延伸模組，則需要安裝 [Node.js](https://nodejs.org/)，並使其可在 `$PATH` 中使用。 Node.js 包含 npm，也就是 Node.js 套件管理員，可用來安裝延伸模組產生器。

若要建立新的延伸模組，則可使用 Azure Data Studio 延伸模組產生器。 Yeoman [延伸模組產生器](https://www.npmjs.com/package/generator-azuredatastudio)對於延伸模組專案而言是一個很好的起點。 若要啟動產生器，請在命令提示字元中鍵入下列命令：

```
npm install -g yo generator-azuredatastudio # Install the generator
yo azuredatastudio
```

如需如何開始使用延伸模組範本的詳細指引，請參閱[建立延伸模組](./tutorial-create-extension.md?view=sql-server-ver15)，並遵循指示建立按鍵對應延伸模組。

**擴充性參考**

若要了解 Azure Data Studio 擴充性，請參閱[擴充性概觀](extensibility.md)。 您也可以在現有[範例](https://github.com/Microsoft/azuredatastudio/tree/main/samples)中查看如何使用 API 的範例。


## <a name="debug-an-extension"></a>對延伸模組進行偵錯

您可以使用 Visual Studio Code 延伸模組 [Azure Data Studio Debug](https://github.com/kevcunnane/sqlops-debug)，對新的延伸模組進行偵錯。

步驟
1. 使用 [Visual Studio Code](https://code.visualstudio.com/) 開啟延伸模組。
1. 安裝 Azure Data Studio 偵錯延伸模組。
1. 按 **F5** 或按一下偵錯圖示，然後按一下 [啟動]。
1. Azure Data Studio 的新執行個體會以特殊模式 (延伸模組開發主機) 啟動，且這個新執行個體現可識別您的延伸模組。


## <a name="create-an-extension-package"></a>建立延伸模組套件

撰寫延伸模組之後，您必須建立 VSIX 套件，才能將其安裝至 Azure Data Studio。 您可使用 [vsce](https://github.com/Microsoft/vscode-vsce) (Visual Studio Code 延伸模組) 來建立 VSIX 套件。 

```
npm install -g vsce
cd myExtensionName
vsce package
# The myExtensionName.vsix file has now been generated
```

透過 VSIX 套件，您可共用 `.vsix` 檔案，並從 [命令選擇區] 使用 [延伸模組：從 VSIX 檔案進行安裝] 命令，將延伸模組安裝至 Azure Data Studio，即可在本機和私人位置共用延伸模組。


## <a name="publish-an-extension"></a>發佈延伸模組

若要將您的新延伸模組發佈至 Azure Data Studio：

1. 將延伸模組新增至 https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. 我們目前不支援裝載協力廠商的延伸模組，因此 Azure Data Studio 會讓您選擇瀏覽至下載頁面，而不是下載延伸模組。 若要設定延伸模組的下載頁面，請設定 "Microsoft.AzureDataStudio.DownloadPage" 資產值。
3. 依據版本/延伸模組分支建立 PR。
4. 將檢閱要求傳送給小組。

我們會檢閱您的延伸模組，並新增至延伸模組資源庫。

**發佈延伸模組更新**

發佈更新與發佈延伸模組的程序類似。 請確定已更新 package.json 中的版本。