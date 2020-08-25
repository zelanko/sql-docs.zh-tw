---
title: 使用者與工作區設定
description: 了解如何使用設定來自訂 Azure Data Studio 的編輯器、使用者介面，以及功能行為，以符合您的喜好設定。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.reviewer: alayu, maghan, sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 2196bd9c4445f700fd1a697db3edcb5879b1f44b
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2020
ms.locfileid: "88746158"
---
# <a name="modify-user-and-workspace-settings"></a>修改使用者與工作區設定

您可依照自己的偏好來透過設定以輕鬆地設定 Azure Data Studio。 幾乎每個 Azure Data Studio 的編輯器、使用者介面與功能行為各部分都有可修改選項。

Azure Data Studio 提供兩種不同的設定範圍：

* **使用者**：這些設定會全域套用至開啟的所有 Azure Data Studio 執行個體。
* **工作區**：工作區設定是您電腦上資料夾特定的設定，只有在 [Explorer] 提要欄位中開啟資料夾時才可使用。 在此範圍中定義的設定會覆寫使用者範圍。

## <a name="creating-user-and-workspace-settings"></a>建立使用者與工作區設定

功能表命令 [檔案] > [喜好設定] > [設定] (在 Mac 上為 [程式碼] > [喜好設定] > [設定])，提供可設定使用者與工作區設定的進入點。 系統會提供您一份 [預設設定] 清單。 將您任何要變更的設定複製到適當的 `settings.json` 檔案。 右側的索引標籤可讓您在使用者與工作區設定檔案之間快速切換。

您也可以從**命令選擇區** (**Ctrl+Shift+P**) 使用 [喜好設定:開啟使用者設定] 和 [喜好設定:開啟工作區設定]，或使用鍵盤快速鍵 (**Ctrl+,** )，開啟使用者與工作區設定。

下列範例會停用編輯器中的行號，並將程式碼行設定為自動縮排。

![範例設定](media/settings/sample-settings.png)

儲存修改的 `settings.json` 檔案之後， Azure Data Studio 會重新載入變更的設定。

> [!NOTE] 
> 工作區設定對於跨小組共用專案特定的設定很有用。

## <a name="settings-file-locations"></a>設定檔案位置

根據您的平台，使用者設定檔案的位置如下：

* **Windows** `%APPDATA%\azuredatastudio\User\settings.json`
* **Mac** `$HOME/Library/Application Support/azuredatastudio/User/settings.json`
* **Linux** `$HOME/.config/azuredatastudio/User/settings.json`

工作區設定檔案位於您專案的 `.Azure Data Studio` 資料夾底下。

## <a name="hot-exit"></a>Hot Exit

根據預設，當您結束時，Azure Data Studio 會記住未儲存的檔案變更。 這與 Visual Studio Code 中的 Hot Exit 功能相同。

Hot Exit 預設為關閉。 您可以編輯 `files.hotExit` 設定，啟用 Hot Exit。 如需詳細資訊，請參閱 [Hot Exit (Visual Studio Code 文件中)](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit)。


## <a name="tab-color"></a>索引標籤色彩

為了更容易識別您所使用的連線，在編輯器中開啟索引標籤時，可將色彩設定為符合連線所屬伺服器群組的色彩。 索引標籤色彩預設為關閉。 您可以編輯 `sql.tabColorMode` 設定，啟用索引標籤色彩。

## <a name="additional-resources"></a>其他資源

因為 Azure Data Studio 會從 Visual Studio Code 繼承其使用者與工作區設定功能，所以如需設定的詳細資訊，請參閱 [Visual Studio Code 的設定](https://code.visualstudio.com/docs/getstarted/settings)一文。
