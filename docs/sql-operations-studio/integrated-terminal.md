---
title: "SQL Operations Studio （預覽） 中的整合式終端機 |Microsoft 文件"
description: "深入了解 SQL Operations Studio （預覽） 中的整合式終端機。"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b55e86314dd075b61dac5751b29fc541fdf1e2c4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="integrated-terminal"></a>整合式終端機

在[!INCLUDE[name-sos](../includes/name-sos-short.md)]，您可以開啟整合式的終端機，一開始從工作區的根目錄開始。 這可以是很方便，因為您不需要切換視窗，或改變現有的終端機才能執行快速的命令列工作的狀態。

若要開啟 終端機：

* 使用**Ctrl +'**倒單引號字元的鍵盤快速鍵。
* 使用**檢視** | **整合的終端機**功能表命令。
* 從**命令選擇區**(**Ctrl + Shift + P**)，使用**切換檢視： 整合式終端機**命令。

![終端機](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> 您仍然可以使用 [總管] 中開啟外部的殼層**開啟命令提示字元中**命令 (**開啟 終端機**Mac 或 Linux) 如果您想要使用外部[!INCLUDE[name-sos](../includes/name-sos-short.md)]。

## <a name="managing-multiple-terminals"></a>管理多個終端機

您可以建立多個終端機開放給不同的位置，並輕鬆地巡覽其間。 您可以加入終端機的執行個體叫用的右上方的加號圖示**終端機** 面板，或藉由觸發**Ctrl + Shift +'**命令。 這會建立另一個項目可用於切換的下拉式清單。

![多個終端機](media/integrated-terminal/terminal-multiple-instances.png)

按鈕，可以藉由按下資源回收筒移除終端機的執行個體。

> [!TIP]
> 如果您廣泛地使用多個終端機，您可以加入的索引鍵繫結`focusNext`，`focusPrevious`和`kill`命令中所述[索引鍵繫結區段](#key-bindings)它們只利用鍵盤之間導覽。

## <a name="configuration"></a>組態

Shell 會使用預設值為`$SHELL`Linux 及 macOS，在 Windows 10 上的 PowerShell 和 cmd.exe 較早版本的 Windows 上。 這些可以手動設定的覆寫`terminal.integrated.shell.*`中[設定](settings.md)。 引數可以在 Linux 和 macOS 使用傳遞到終端機殼層`terminal.integrated.shellArgs.*`設定。

### <a name="windows"></a>Windows

正確設定在 Windows 上的 您的殼層會尋找正確的可執行檔，並更新設定。 以下是常見的 shell 可執行檔和它們的預設位置的清單：

```json
// 64-bit cmd if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\cmd.exe"
// 64-bit PowerShell if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\WindowsPowerShell\\v1.0\\powershell.exe"
// Git Bash
"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe"
// Bash on Ubuntu (on Windows)
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\bash.exe"
```

> [!NOTE]
> 若要做為整合式的終端機，shell 可執行檔必須是主控台應用程式，讓`stdin/stdout/stderr`可重新導向。

> [!TIP]
> 權限以執行整合式的終端機 shell [!INCLUDE[name-sos](../includes/name-sos-short.md)]。 如果您需要以提高權限 （系統管理員） 或不同的權限執行殼層命令，您可以使用平台的公用程式例如`runas.exe`終端機中。

### <a name="shell-arguments"></a>殼層引數

啟動時，可以將引數傳遞到殼層。

例如，若要啟用作為登入殼層執行 bash (執行`.bash_profile`)，傳入`-l`引數 （雙引號））：

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>終端機的顯示設定

您可以自訂的整合式終端機的字型和線條高度使用下列設定：

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>終端機的金鑰繫結

**檢視： 整合式切換終端機**命令繫結至**Ctrl +'**快速切換進入和離開檢視的整合式終端機的面板。

以下是快速瀏覽的整合式終端機中的鍵盤快速鍵：

索引鍵|命令
---|---
**Ctrl +'**|顯示整合的終端機
**Ctrl + Shift +'**|建立新的終端機
**Ctrl + 向上鍵**|向上捲動
**Ctrl + 向下鍵**|向下捲動
**Ctrl + PageUp**|向上捲動頁面
**Ctrl + PageDown**|向下捲動頁面
**Ctrl + Home**|捲動至上方
**Ctrl + End**|捲動到底部
**Ctrl + K**|清除 終端機

其他終端機的命令可提供，而且可以繫結至您的慣用的鍵盤快速鍵。

其中包括：

* `workbench.action.terminal.focus`： 專注終端機。 這是切換類似，但如果顯示著重而不是隱藏，終端機。
* `workbench.action.terminal.focusNext`： 著重下一個終端機的執行個體。
* `workbench.action.terminal.focusPrevious`： 著重前一個終端機的執行個體。
* `workbench.action.terminal.kill`： 移除目前的終端機執行個體。
* `workbench.action.terminal.runSelectedText`： 在終端機的執行個體中執行選取的文字。
* `workbench.action.terminal.runActiveFile`： 在終端機的執行個體中執行使用中的檔案。

### <a name="run-selected-text"></a>執行選取的文字

若要使用`runSelectedText`命令，在編輯器中選取文字，並執行命令**終端機： 執行選取的文字作用中終端機**透過**命令選擇區**(**Ctrl + Shift + P**). 終端機提示您執行選取的文字：

![執行選取的文字](media/integrated-terminal/terminal_run_selected.png)

如果沒有選取文字在使用中的編輯器中，游標所在的行是執行終端機。

### <a name="copy--paste"></a>複製和貼上

複製和貼上的按鍵組合，請依照下列平台標準：

* Linux: **Ctrl + Shift + C**和**Ctrl + Shift + V**
* Mac: **Cmd + C**和**Cmd + V**
* Windows: **Ctrl + C**和**Ctrl + V**

### <a name="find"></a>尋找

整合式終端機有基本的尋找功能，可與觸發**Ctrl + F**。

如果您想**Ctrl + F**移至殼層，而不是啟動 Linux 及 Windows 上的 [尋找] widget，您需要移除按鍵就像這樣：

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>重新命名終端機工作階段

整合式終端機工作階段可以立即重新命名使用**終端機： 重新命名**(`workbench.action.terminal.rename`) 命令。 終端機的選取範圍下拉式清單中，會顯示新的名稱。

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>強制將透過終端機的金鑰繫結

而焦點是在整合式終端機中，許多索引鍵繫結將無法運作，因為按鍵動作會傳遞至，且由本身的終端機。 `terminal.integrated.commandsToSkipShell`設定可以用來取得解決這個問題。 它包含的命令名稱，其按鍵繫結的殼層略過處理，並改為處理的陣列[!INCLUDE[name-sos](../includes/name-sos-short.md)]索引鍵繫結系統。 根據預設，這會包括所有終端機按鍵繫結除了選取幾個常用按鍵繫結。

