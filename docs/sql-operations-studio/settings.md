---
title: SQL Operations Studio （預覽） 使用者和工作區設定 |Microsoft 文件
description: 如何修改 SQL Operations Studio （預覽） 使用者和工作區設定。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 67f60d30693eeb60030f3a977ec1bcf5a1f98be1
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2018
ms.locfileid: "34235135"
---
# <a name="user-and-workspace-settings"></a>使用者和工作區設定

透過設定功能可以輕鬆配置 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 以滿足您的喜好。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 的編輯器、使用者介面和功能行為，幾乎都有可修改的選項。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供兩個不同範圍的設定：

* **使用者**這些設定會全域套用至任何執行個體[!INCLUDE[name-sos](../includes/name-sos-short.md)]開啟。
* **工作區**工作地區設定是您的電腦上的資料夾特有的設定，只能用於在檔案總管 [資訊看板] 中開啟資料夾時。 定義領域上設定覆寫使用者領域。

## <a name="creating-user-and-workspace-settings"></a>建立使用者和工作區設定

功能表命令**檔案** > **喜好設定** > **設定**(**程式碼** >  **喜好設定** > **設定**Mac 上) 提供使用者和工作區設定的進入點。 為您提供的預設設定清單。 複製任何您想要變更為適當的設定`settings.json`檔案。 在右邊的索引標籤可讓您快速切換使用者和工作區的設定檔。

您也可以開啟中的使用者和工作區設定**命令選擇區**(**Ctrl + Shift + P**) 與**喜好設定： 開啟 使用者設定**和**開啟工作區設定喜好設定：** 或使用鍵盤快速鍵 (**Ctrl +**)。

下列範例會停用編輯器中的行號，並設定自動縮排程式碼行。

![設定範例](media/settings/sample-settings.png)

設定的變更會重新載入由[!INCLUDE[name-sos](../includes/name-sos-short.md)]之後修改`settings.json`儲存檔案。

>**注意：** 工作區設定可用於整個小組共用專案專屬的設定。

## <a name="settings-file-locations"></a>設定檔案位置

根據您的平台的使用者設定檔的位置為：

* **Windows** `%APPDATA%\sqlops\User\settings.json`
* **Mac** `$HOME/Library/Application Support/sqlops/User/settings.json`
* **Linux** `$HOME/.config/sqlops/User/settings.json`

工作區設定檔案位於您專案內`.[!INCLUDE[name-sos](../includes/name-sos-short.md)]`資料夾下。

## <a name="hot-exit"></a>熱結束

當您離開時，SQL Operations Studio 預設記住未儲存檔案的變更。 這與 Visual Studio Code 熱結束功能相同。

根據預設，熱結束為關閉。 您可以藉由編輯 `files.hotExit` 設定以啟用熱結束。 如需詳細資訊，請參閱 Visual Studio Code 文件中的[熱結束](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit)。 


## <a name="tab-color"></a>索引標籤色彩

若要簡化用來識別您正在使用哪些連線，在編輯器中開啟的索引標籤可以有其設定以符合連接所屬的伺服器群組的色彩的色彩。 根據預設，索引標籤色彩預設為關閉的。 藉由編輯啟用索引標籤色彩`sql.tabColorMode`設定。

## <a name="additional-resources"></a>其他資源

因為 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 從 Visual Studio Code 繼承使用者和工作區設定功能，詳細的設定資訊可以參考[設定 Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings) 文章。
