---
title: 整合式終端
description: 了解如何開啟整合到 Azure Data Studio 的終端。 整合式終端可能會比個別的終端更方便。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: azure-data-studio
ms.technology: ''
ms.reviewer: alayu, maghan, sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 127ea216dccab32a17199b2b5b9e0f3f8d577c24
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411084"
---
# <a name="integrated-terminal"></a>整合式終端

在 Azure Data Studio 中，您可以開啟整合式終端，最初先從工作區的根目錄開始。 這可能很方便，因為您不必切換視窗或改變現有終端的狀態，即可執行快速命令列工作。

若要開啟終端：

* 使用 **Ctrl+`** 鍵盤快速鍵 (搭配反引號字元)。
* 使用 [檢視] | [整合式終端] 功能表命令。
* 從**命令選擇區** (**Ctrl+Shift+P**)，使用 [View:Toggle Integrated Terminal] \(檢視: 切換整合式終端\) 命令。

![終端](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> 如果您偏好在 Azure Data Studio 外部工作，您仍然可以使用 Explorer 的 [在命令提示字元中開啟] 命令 (在 Mac 或 Linux 上為 [在終端機中開啟])，開啟外部殼層。

## <a name="managing-multiple-terminals"></a>管理多個終端

您可以建立多個在不同位置開啟的終端，並輕鬆地在其間巡覽。 藉由叫用 [終端] 面板右上方的加號圖示或觸發 **Ctrl+Shift+`** 命令，即可新增終端執行個體。 這會在下拉式清單中建立另一個可用於在其間切換的項目。

![多個終端](media/integrated-terminal/terminal-multiple-instances.png)

按 [垃圾桶] 按鈕即可移除終端執行個體。

> [!TIP]
> 如果您大規模地使用多個終端，您可以如[按鍵繫結關係](#key-bindings)一節中所述，新增 `focusNext`、`focusPrevious` 和 `kill` 命令的按鍵繫結關係，允許只使用鍵盤在其間巡覽。

## <a name="configuration"></a>組態

此殼層預設會使用 `$SHELL` (Linux 和 macOS)、PowerShell (Windows 10) 和 cmd.exe (舊版 Windows)。 您可以藉由在[設定](settings.md)中設定 `terminal.integrated.shell.*`，手動覆寫這些值。 您可以使用 `terminal.integrated.shellArgs.*` 設定，將引數傳遞至 Linux 和 macOS 上的終端殼層。

### <a name="windows"></a>Windows

在 Windows 上正確設定您的殼層，對於尋找正確的可執行檔並更新設定至關重要。 以下是常見的殼層可執行檔及其預設位置清單：

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
> 若要作為整合式終端使用，殼層可執行檔必須是主控台應用程式，才能重新導向 `stdin/stdout/stderr`。

> [!TIP]
> 整合式終端殼層會以 Azure Data Studio 的權限執行。 如果您需要以較高 (系統管理員) 或不同的權限執行殼層命令，您可以在終端內使用平台公用程式 (例如 `runas.exe`)。

### <a name="shell-arguments"></a>殼層引數

您可以在殼層啟動時，將引數傳遞過去。

例如，若要以登入殼層的方式執行 Bash (這會執行 `.bash_profile`)，請傳入 `-l` 引數 (以雙引號括住)：

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>終端顯示設定

您可以使用下列設定，自訂整合式終端字型和行高：

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a name="terminal-key-bindings"></a><a id="key-bindings"></a>終端按鍵繫結關係

[View: Toggle Integrated Terminal] \(檢視: 切換整合式終端\) 命令會繫結至 **Ctrl+`** ，快速在檢視中開啟和關閉整合式終端面板。

以下是可在整合式終端內快速巡覽的鍵盤快速鍵：

|Key|Command|  
|---|---|  
|**Ctrl+\`**|顯示整合式終端|  
|**Ctrl+Shift+\`**|建立新的終端|  
|**Ctrl+向上鍵**|向上捲動|  
|**Ctrl+向下鍵**|向下捲動|  
|**Ctrl+PageUp**|向上捲動頁面|  
|**Ctrl+PageDown**|向下捲動頁面|  
|**Ctrl+Home**|捲動至頂端|  
|**Ctrl+End**|捲動至底端|  
|**Ctrl+K**|清除終端|  

還有其他終端命令可供使用，並可繫結至您慣用的鍵盤快速鍵。

其中包括：

* `workbench.action.terminal.focus`:將焦點放在終端。 這就像是切換，但如果終端可見，則會聚焦於終端，而不是加以隱藏。
* `workbench.action.terminal.focusNext`:將焦點放在下一個終端執行個體。
* `workbench.action.terminal.focusPrevious`:將焦點放在上一個終端執行個體。
* `workbench.action.terminal.kill`:移除目前的終端執行個體。
* `workbench.action.terminal.runSelectedText`:在終端執行個體中執行選取的文字。
* `workbench.action.terminal.runActiveFile`:在終端執行個體中執行使用中的檔案。

### <a name="run-selected-text"></a>執行選取的文字

若要使用 `runSelectedText` 命令，請在編輯器中選取文字，然後執行 [終端:在使用中的終端執行選取的文字] (透過**命令選擇區** (**Ctrl+Shift+P**))。 終端會嘗試執行選取的文字：

![執行選取的文字](media/integrated-terminal/terminal_run_selected.png)

如果在使用中的編輯器沒有選取任何文字，則會在終端執行游標所在的行。

### <a name="copy--paste"></a>複製並貼上

複製並貼上的按鍵繫結關係遵循下列平台標準：

* Linux：**Ctrl+Shift+C** 和 **Ctrl+Shift+V**
* Mac：**Cmd+C** 和 **Cmd+V**
* Windows：**Ctrl+C** 和 **Ctrl+V**

### <a name="find"></a>Find

整合式終端具有基本的尋找功能，可透過 **Ctrl+F** 加以觸發。

在 Linux 和 Windows 上，如果您想要以 **Ctrl+F** 移至殼層而不是啟動 [尋找] 小工具，您必須移除按鍵繫結關係，如下所示：

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>重新命名終端工作階段

現在可以使用[終端:重新命名] (`workbench.action.terminal.rename`) 命令，重新命名整合式終端工作階段。 新的名稱會顯示在終端選取下拉式清單中。

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>強制按鍵繫結關係通過終端

雖然焦點是在整合式終端，但許多按鍵繫結關係會因為按鍵輸入傳遞至終端本身並由其取用而無法運作。 `terminal.integrated.commandsToSkipShell` 設定可用來解決此問題。 此設定包含命令名稱的陣列，其按鍵繫結關係會略過殼層處理，而改由 Azure Data Studio 按鍵繫結關係系統處理。 根據預設，這包括所有的終端按鍵繫結關係，以及幾個選取的常用按鍵繫結關係。

