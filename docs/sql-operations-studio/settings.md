---
title: "SQL 作業 Studio （預覽） 使用者和工作區設定 |Microsoft 文件"
description: "如何修改 SQL 作業 Studio （預覽） 使用者和工作區設定。"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6e87461fb2973bec630ed21975a80cdbc17cd1cd
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="user-and-workspace-settings"></a>使用者和工作區設定

所以可以輕鬆地設定[!INCLUDE[name-sos](../includes/name-sos-short.md)]透過設定您自己的需要。 幾乎所有屬於[!INCLUDE[name-sos](../includes/name-sos-short.md)]的編輯器、 使用者介面和功能的行為有選項可修改。

[!INCLUDE[name-sos](../includes/name-sos-short.md)]提供兩個不同的範圍的設定：

* **使用者**這些設定會全域套用至任何執行個體[!INCLUDE[name-sos](../includes/name-sos-short.md)]開啟。
* **工作區**工作地區設定是您的電腦上的資料夾特有的設定，只能用於在檔案總管 [資訊看板] 中開啟資料夾時。 定義領域上設定覆寫使用者領域。

## <a name="creating-user-and-workspace-settings"></a>建立使用者和工作區設定

功能表命令**檔案** > **喜好設定** > **設定**(**程式碼** >  **喜好設定** > **設定**Mac 上) 提供使用者和工作區設定的進入點。 為您提供的預設設定清單。 複製任何您想要變更為適當的設定`settings.json`檔案。 在右邊的索引標籤可讓您快速切換使用者和工作區的設定檔。

您也可以開啟中的使用者和工作區設定**命令選擇區**(**Ctrl + Shift + P**) 與**喜好設定： 開啟 使用者設定**和**開啟工作區設定喜好設定：**或使用鍵盤快速鍵 (**Ctrl +**)。

下列範例會停用編輯器中的行號，並設定文字換行自動根據編輯器的大小。

![設定範例](media/settings/sample-settings.png)

設定的變更會重新載入由[!INCLUDE[name-sos](../includes/name-sos-short.md)]之後修改`settings.json`儲存檔案。

>**注意：**工作區設定可用於整個小組共用專案專屬的設定。

## <a name="settings-file-locations"></a>設定檔案位置

根據您的平台的使用者設定檔的位置為：

* **Windows** `%APPDATA%\sqlops\User\settings.json`
* **Mac** `$HOME/Library/Application Support/sqlops/User/settings.json`
* **Linux** `$HOME/.config/sqlops/User/settings.json`

工作區設定檔案位於`.[!INCLUDE[name-sos](../includes/name-sos-short.md)]`專案資料夾中的。

## <a name="hot-exit"></a>熱結束

SQL 作業 Studio 將檔案記住未儲存的變更，當您結束預設。 這是在 Visual Studio 程式碼中的熱結束功能相同。

根據預設，熱結束已關閉。 啟用作用結束藉由編輯`files.hotExit`設定。 如需詳細資訊，請參閱[（在 Visual Studio 程式碼文件中） 的熱結束](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit)。


## <a name="tab-color"></a>索引標籤色彩

若要簡化用來識別您正在使用哪些連線，在編輯器中開啟的索引標籤可以有其設定以符合連接所屬的伺服器群組的色彩的色彩。 根據預設，索引標籤色彩預設為關閉的。 藉由編輯啟用索引標籤色彩`sql.tabColorMode`設定。

## <a name="additional-resources"></a>其他資源

因為[!INCLUDE[name-sos](../includes/name-sos-short.md)]繼承功能，從 Visual Studio 程式碼，設定的詳細資訊是在使用者和工作區設定[設定 Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings)發行項。
