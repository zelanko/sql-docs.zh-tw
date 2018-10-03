---
title: 建立 Azure Data Studio 擴充功能 |Microsoft Docs
description: 將擴充功能新增至 Azure Data Studio
ms.custom: tools|sos
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.prod_service: sql-tools
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8935d641c8c3fa6da58b5f7c2d8b5560664a6486
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "48038055"
---
# <a name="extend-the-functionality-of-includename-sosincludesname-sos-shortmd"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)]的擴充模組

[!INCLUDE[name-sos](../includes/name-sos-short.md)]提供了一種對基本的 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 安裝更多功能的簡單方法。

延伸模組會提供 Azure Data Studio 小組 (Microsoft)，以及第 3 個合作對象社群 （您 ！）。


## <a name="author-an-extension"></a>撰寫擴充功能

如果您想要擴充 Azure Data Studio，您可以建立您自己的延伸模組，並將它發行到 「 擴充程式庫。

**撰寫延伸模組**

***必要條件***

若要開發延伸模組中，您在已安裝，而且可在您 $PATH 需要 Node.js 它。 Node.js 包含 npm，Node.js 套件管理員，將用於安裝延伸模組產生器。

若要開始新的副檔名，您可以使用 Azure 資料 Studio 延伸模組產生器。 Yeoman[延伸模組產生器](https://www.npmjs.com/package/generator-sqlops)可以很容易就能建立簡單的延伸模組專案。 若要啟動產生器，在命令提示字元中輸入下列命令：

`npm install -g yo generator-sqlops`

`yo sqlops`


**擴充性參考**

若要深入了解 Azure 資料 Studio 擴充性，請參閱[擴充性概觀](extensibility.md)。 您也可以查看如何使用現有 API 的範例[範例](https://github.com/Microsoft/azuredatastudio/tree/master/samples)。


## <a name="debug-an-extension"></a>偵錯擴充功能

您可以偵錯您使用 Visual Studio Code 擴充功能的新延伸模組[Azure 資料 Studio 偵錯](https://github.com/kevcunnane/sqlops-debug)。

步驟
- 開啟您的延伸模組與[Visual Studio Code](https://code.visualstudio.com/)
- 安裝 Azure 資料 Studio 偵錯擴充功能
- 按下**F5**或按一下 [偵錯] 圖示，然後按一下**開始**。
- Azure Data Studio 的新執行個體啟動特殊模式 （延伸模組開發主應用程式），這個新執行個體現在是知道您的延伸模組。


## <a name="create-an-extension-package"></a>建立延伸模組套件

撰寫您的延伸模組之後，您需要建立 VSIX 封裝，可以將它安裝在 Azure Data Studio。 您可以使用[vsce](https://github.com/Microsoft/vscode-vsce)建立 VSIX 封裝。

`npm install -g vsce`

`vsce package`


## <a name="publish-an-extension"></a>發行擴充功能

若要將您新的延伸模組發佈至 Azure Data Studio 中：

1. 您將延伸加入至 https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. 我們目前沒有任何支援主機協力廠商延伸模組，因此而不是下載擴充功能，Azure Data Studio 具有瀏覽至下載頁面的選項。 若要設定您的延伸模組的下載頁面，設定資產 」 Microsoft.AzureDataStudio.DownloadPage"的值。
3. 建立針對延伸模組版本/分支的提取要求。
4. 傳送給小組的檢閱要求。

將檢閱您的延伸模組，並將它新增至延伸模組資源庫中。

**發行延伸模組更新**發行更新的程序是類似於發佈的延伸模組。 請確定在 package.json 中更新的版本
