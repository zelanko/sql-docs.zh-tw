---
title: 整合式終端機
titleSuffix: Azure Data Studio
description: 深入了解在 Azure Data Studio 整合式終端機。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 13a0e3c17f45e0ba136d83f832d3531bc8059884
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959531"
---
# <a name="integrated-terminal"></a>整合式終端機

在  [!INCLUDE[name-sos](../includes/name-sos-short.md)]，您可以開啟整合式終端機中，一開始啟動您的工作區的根目錄。 這可能會很方便，因為您不需要切換視窗，或改變現有的終端機執行快速的命令列工作的狀態。

若要開啟 終端機：

* 使用**Ctrl +'** 使用倒單引號字元的鍵盤快速鍵。
* 使用**檢視** | **整合式終端機**功能表命令。
* 從**命令調色盤**(**Ctrl + Shift + P**)，使用**切換檢視： 整合式終端機**命令。

![終端機](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> 您仍然可以使用 [總管] 中開啟外部殼層**在命令提示字元中開啟**命令 (**在終端機中開啟**Mac 或 Linux 上) 如果您想要工作外[!INCLUDE[name-sos](../includes/name-sos-short.md)]。

## <a name="managing-multiple-terminals"></a>管理多個終端機

您可以建立多個終端機開放給不同的位置，並輕鬆地巡覽至它們。 您可以加入終端機的執行個體叫用的右上方的加號圖示**終端機** 面板，或藉由觸發**Ctrl + Shift +'** 命令。 這可用來切換這些下拉式清單中建立另一個項目。

![多個終端機](media/integrated-terminal/terminal-multiple-instances.png)

移除資源回收筒可以按鈕的按下終端機執行個體。

> [!TIP]
> 如果您廣泛地使用多個終端機，您可以加入索引鍵繫結`focusNext`，`focusPrevious`並`kill`命令中所述[按鍵繫結區段](#key-bindings)允許它們只使用鍵盤之間巡覽。

## <a name="configuration"></a>組態

使用預設的殼層`$SHELL`Linux 和 macOS、 Windows 10 上的 PowerShell 和 cmd.exe 在舊版 Windows 上。 這些可以覆寫手動設定`terminal.integrated.shell.*`中[設定](settings.md)。 引數可以傳遞至終端機的殼層上 Linux 和 macOS 使用`terminal.integrated.shellArgs.*`設定。

### <a name="windows"></a>Windows

正確設定在 Windows 上的 您的殼層是找出正確的可執行檔，並更新設定。 以下是常見的殼層可執行檔和它們的預設位置的清單：

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
> 若要做為整合式終端機，shell 可執行檔必須是主控台應用程式，讓`stdin/stdout/stderr`可以被重新導向。

> [!TIP]
> 整合式終端機的殼層執行的權限[!INCLUDE[name-sos](../includes/name-sos-short.md)]。 如果您需要以提高權限 （系統管理員） 或不同的權限執行 shell 命令，您可以使用平台公用程式例如`runas.exe`終端機中。

### <a name="shell-arguments"></a>殼層的引數

啟動時，可以將引數傳遞到殼層。

例如，若要啟用作為登入 shell 執行 bash (哪些回合`.bash_profile`)，傳入`-l`（含雙引號） 的引數：

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>終端機的顯示設定

您可以自訂的整合式終端機的字型和行高以下列設定：

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>終端機的按鍵繫結

**檢視：切換 [整合式終端機**命令已繫結至**Ctrl +'** 快速切換流入和流出檢視整合式終端機] 面板。

以下是快速瀏覽整合式終端機中的鍵盤快速鍵：

|索引鍵|命令|  
|---|---|  
|**Ctrl+\`**|顯示整合式終端機|  
|**Ctrl+Shift+\`**|建立新的終端機|  
|**Ctrl+Up**|向上捲動|  
|**Ctrl+Down**|向下捲動|  
|**Ctrl+PageUp**|向上捲動一頁|  
|**Ctrl+PageDown**|向下捲動一頁|  
|**Ctrl+Home**|捲動至上方|  
|**Ctrl+End**|捲動至底端|  
|**Ctrl+K**|清除 終端機|  

其他終端機命令可用，並可以繫結至您慣用的鍵盤快速鍵。

其中包括：

* `workbench.action.terminal.focus`:焦點終端機。 這就像是切換，但著重的終端機，而非隱藏它，它是否可見。
* `workbench.action.terminal.focusNext`:著重的下一步 的終端機執行個體。
* `workbench.action.terminal.focusPrevious`:將重點放上一個終端機執行個體。
* `workbench.action.terminal.kill`:移除目前的終端機執行個體。
* `workbench.action.terminal.runSelectedText`:在終端機執行個體中執行選取的文字。
* `workbench.action.terminal.runActiveFile`:在終端機執行個體中執行作用中的檔案。

### <a name="run-selected-text"></a>執行選取的文字

若要使用`runSelectedText`命令，在編輯器中選取文字，並執行命令**終端機：在使用中的終端機中執行已選取的文字**經由**命令選擇區**(**Ctrl + Shift + P**)。 終端機中嘗試執行選取的文字：

![執行選取的文字](media/integrated-terminal/terminal_run_selected.png)

如果在使用中的編輯器中不選取任何文字，則在終端機中執行游標所在列。

### <a name="copy--paste"></a>複製和貼上

複製並貼上的按鍵繫結關係，請依照下列平台標準：

* Linux：**Ctrl + Shift + C**和**Ctrl + Shift + V**
* Mac:**Cmd + C**和**Cmd + V**
* Windows:**Ctrl + C**和**Ctrl + V**

### <a name="find"></a>尋找

整合式終端機有基本的尋找功能，即可觸發**Ctrl + F**。

如果您想**Ctrl + F**若要前往的殼層，而不是啟動 Linux 和 Windows 上的尋找小工具，您需要移除按鍵繫結關係如下：

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>重新命名終端機工作階段

整合式終端機工作階段可以立即重新命名使用**終端機：重新命名**(`workbench.action.terminal.rename`) 命令。 新的名稱會顯示終端機的選取範圍下拉式清單中。

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>強制將透過終端機中的索引鍵繫結

當焦點在整合式終端機中時，許多的按鍵繫結將無法運作，因為按鍵輸入會傳遞至，並由本身的終端機。 `terminal.integrated.commandsToSkipShell`設定可用來解決這個問題。 它包含的命令名稱，其索引鍵繫結殼層來略過處理，並改為處理的陣列[!INCLUDE[name-sos](../includes/name-sos-short.md)]金鑰繫結系統。 根據預設，這會包括所有終端機的按鍵繫結除了選取幾個常用的按鍵繫結。

