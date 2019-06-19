---
title: 使用者和工作區設定
titleSuffix: Azure Data Studio
description: 如何自訂 Azure Data Studio 藉由修改使用者和工作區設定。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 883c0c98531311d77754fcbcdd86615283aecdc7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798066"
---
# <a name="modify-user-and-workspace-settings"></a>修改使用者和工作區設定

透過設定功能可以輕鬆配置 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 以滿足您的喜好。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 的編輯器、使用者介面和功能行為，幾乎都有可修改的選項。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供兩個不同範圍的設定：

* **使用者**這些設定會全域套用的任何執行個體[!INCLUDE[name-sos](../includes/name-sos-short.md)]您開啟。
* **工作區**工作區設定是設定特定至您的電腦上的資料夾及資料夾是在 「 總管 」 資訊看板中開啟時才可用。 在此範圍定義的設定會覆寫使用者範圍。

## <a name="creating-user-and-workspace-settings"></a>建立使用者和工作區設定

功能表命令**檔案** > **喜好設定** > **設定**(**程式碼** >  **偏好** > **設定**Mac 上) 提供使用者和工作區設定的進入點。 您會提供一份預設設定。 複製任何您想要將變更為適當的設定`settings.json`檔案。 在右邊的索引標籤可讓您快速切換使用者和工作區的設定檔。

您也可以開啟使用者和工作區設定**命令調色盤**(**Ctrl + Shift + P**) 與**喜好設定：開啟 使用者設定**和**喜好設定：開啟 設定 工作區**或使用鍵盤快速鍵 (**Ctrl +，** )。

下列範例會停用 在編輯器中的行號，並設定自動縮排的程式碼行。

![設定範例](media/settings/sample-settings.png)

藉由重新載入設定的變更[!INCLUDE[name-sos](../includes/name-sos-short.md)]之後已修改`settings.json`儲存檔案。

>**注意：** 工作區設定可用於整個小組共用專案特定設定。

## <a name="settings-file-locations"></a>設定檔案位置

根據您的平台的使用者設定檔位於此處：

* **Windows** `%APPDATA%\azuredatastudio\User\settings.json`
* **Mac** `$HOME/Library/Application Support/azuredatastudio/User/settings.json`
* **Linux** `$HOME/.config/azuredatastudio/User/settings.json`

工作區設定檔案位於您專案內`.[!INCLUDE[name-sos](../includes/name-sos-short.md)]`資料夾下。

## <a name="hot-exit"></a>最忙碌的結束

Azure Data Studio 會記住未儲存的變更至檔案，當您在預設情況下結束。 這是 Visual Studio Code 中的 [最忙碌的結束] 功能相同。

根據預設，熱結束已關閉。 藉由編輯啟用熱結束`files.hotExit`設定。 如需詳細資訊，請參閱 Visual Studio Code 文件中的[熱結束](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit)。


## <a name="tab-color"></a>索引標籤色彩

若要簡化用來識別您正在使用哪些連線，在編輯器中開啟的索引標籤可以有其設定為符合連線所屬的伺服器群組的色彩的色彩。 根據預設，索引標籤色彩預設為關閉的。 藉由編輯啟用索引標籤色彩`sql.tabColorMode`設定。

## <a name="additional-resources"></a>其他資源

因為 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 從 Visual Studio Code 繼承使用者和工作區設定功能，詳細的設定資訊可以參考[設定 Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings) 文章。
