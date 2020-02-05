---
title: PowerShell 延伸模組
titleSuffix: Azure Data Studio
description: 安裝和使用適用於 Azure Data Studio 的 PowerShell
ms.custom: seodec18
ms.date: 04/19/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
manager: matthend
ms.openlocfilehash: 72c4d64cc93ab564b9b8b04a838f8226982890f0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75257583"
---
# <a name="powershell-editor-support-for-azure-data-studio"></a>Azure Data Studio 的 PowerShell 編輯器支援

此延伸模組讓 [Azure Data Studio](https://github.com/Microsoft/azuredatastudio) 得以提供豐富的 PowerShell 編輯器支援。
現在，您可以使用 Azure Data Studio 所提供近似於 IDE 的絕佳介面，撰寫和偵錯 PowerShell 指令碼。

![PowerShell 延伸模組](media/powershell-extension/powershell-extension.png)


## <a name="features"></a>特性

- 語法醒目提示
- 程式碼片段
- Cmdlet 等的 IntelliSense
- 由 [PowerShell 指令碼分析器](http://github.com/PowerShell/PSScriptAnalyzer)提供的規則式分析
- 移至 Cmdlet 和變數的定義
- 尋找 Cmdlet 和變數的參考
- 文件和工作區符號探索
- 使用 <kbd>F8</kbd> 執行選取的 PowerShell 程式碼選取範圍
- 使用 <kbd>Ctrl</kbd>+<kbd>F1</kbd> 為游標下的符號啟動線上說明
- 基本互動式主控台支援！


## <a name="installing-the-extension"></a>安裝延伸模組

您可以遵循 [Azure Data Studio 文件](https://docs.microsoft.com/sql/azure-data-studio/extensions)中的步驟，安裝 PowerShell 延伸模組的正式版本。
在 [延伸模組] 窗格中搜尋 "PowerShell" 延伸模組，然後在此進行安裝。  您會自動收到任何延伸模組未來更新的相關通知！

您也可以從我們的[版本頁面](https://github.com/PowerShell/vscode-powershell/releases)安裝 VSIX 套件，然後透過命令列進行安裝：

```powershell
azuredatastudio --install-extension PowerShell-<version>.vsix
```

## <a name="platform-support"></a>平台支援

- **Windows 7 到 10** 搭配 Windows PowerShell v3 和更新版本，以及 PowerShell Core
- **Linux** 搭配 PowerShell Core (所有 PowerShell 支援的發行版本)
- **macOS** 搭配 PowerShell Core

請參閱[常見問題集](https://github.com/PowerShell/vscode-powershell/wiki/FAQ)，取得常見問題的解答。

## <a name="installing-powershell-core"></a>安裝 PowerShell Core

如果您在 MacOS 或 Linux 上執行 Azure Data Studio，您可能也需要安裝 PowerShell Core。

PowerShell Core 是 [GitHub](https://github.com/powershell/powershell) 上的開放原始碼專案。
如需在 MacOS 或 Linux 平台上安裝 PowerShell Core 的詳細資訊，請參閱下列文章：

- [在 Linux 上安裝 PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [在 macOS 上安裝 PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)

## <a name="example-scripts"></a>範例指令碼

延伸模組的 `examples` 資料夾中有一些範例指令碼，可用於探索 PowerShell 編輯和偵錯功能。  請查看內含的 [README.md](https://github.com/PowerShell/vscode-powershell/blob/master/examples/README.md) 檔案，深入了解使用方式。

您可以在以下路徑找到此資料夾：

```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.PowerShell-<version>/examples
```

或者，如果您使用的是延伸模組的預覽版本

 ```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.powershell-preview-<version>/examples
```

若要在 Azure Data Studio 中開啟/查看延伸模組的範例，請從您的 PowerShell 命令提示字元執行下列程式碼：

```powershell
azuredatastudio (Get-ChildItem $Home\.azuredatastudio\extensions\ms-vscode.PowerShell-*\examples)[-1]
```

### <a name="creating-and-opening-files"></a>建立和開啟檔案

若要在編輯器內建立和開啟新的檔案，請從 PowerShell 整合式終端使用 New-EditorFile。

```powershell
PS C:\temp> New-EditorFile ExportData.ps1
```

此命令適用於所有檔案類型，而不只是 PowerShell 檔案。

```powershell
PS C:\temp> New-EditorFile ImportData.py
```

若要在 Azure Data Studio 中開啟一或多個檔案，請使用 `Open-EditorFile` 命令。

```powershell
Open-EditorFile ExportData.ps1, ImportData.py
```

### <a name="no-focus-on-console-when-executing"></a>執行時的焦點不在主控台

對於習慣使用 SSMS 的使用者而言，已經習慣能夠執行查詢，之後不需要切換回查詢窗格，即能再次重新執行。  在此情況下，可能會覺得程式碼編輯器的預設行為很奇怪。  若要在使用 <kbd>F8</kbd> 執行時將焦點維持在編輯器中，請變更下列設定：

```json
"powershell.integratedConsole.focusConsoleOnExecute": false
```

為了達到協助目的，預設值為 `true`。

請注意，即使您使用明確呼叫輸入的命令 (例如 `Get-Credential`)，此設定也會防止焦點變更為主控台。

## <a name="sql-powershell-examples"></a>SQL PowerShell 範例
若要使用這些範例 (如下所示)，您必須從 [PowerShell 資源庫](https://www.powershellgallery.com/packages/SqlServer)安裝 SqlServer 模組。

```powershell
Install-Module -Name SqlServer
```

> [!NOTE]
> 在 `21.1.18102` 版和更新版本中，除了 Windows PowerShell 以外，`SqlServer` 模組也支援 [PowerShell Core](https://github.com/PowerShell/PowerShell) 6.2 和更新版本。

在此範例中，我們使用 `Get-SqlInstance` Cmdlet 取得 ServerA 與 ServerB 的 Server SMO 物件。  此命令的預設輸出會包含執行個體名稱、版本、Service Pack 與執行個體的 CU 更新層級。

```powershell
Get-SqlInstance -ServerInstance ServerA, ServerB
```

該輸出看起來如下列範例所示：

```
Instance Name             Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------             -------    ------------ -----------  ------------ ----------------
ServerA                   13.0.5233  SP2          CU4          Windows      Windows Server 2016 Datacenter
ServerB                   14.0.3045  RTM          CU12         Linux        Ubuntu
```
`SqlServer` 模組包含名為 `SQLRegistration` 的提供者，可讓您以程式設計方式存取下列儲存的 SQL Server 連接類型：

+ 資料庫引擎伺服器 (已註冊的伺服器)
+ 中央管理伺服器 (CMS)
+ Analysis Services
+ Integration Services
+ Reporting Services

 在下列範例中，我們將執行 `dir` (`Get-ChildItem` 的別名)，取得已註冊伺服器檔案中列出的所有 SQL Server 執行個體清單。

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse 
```

該輸出看起來可能如下列範例所示：

```powershell
Mode Name
---- ----
-    ServerA
-    ServerB
-    localhost\SQL2017
-    localhost\SQL2016Happy
-    localhost\SQL2017
```

對於涉及某個資料庫的許多作業，或某個資料庫內的許多物件，可以使用 `Get-SqlDatabase` Cmdlet。  如果您同時提供 `-ServerInstance` 和 `-Database` 參數的值，只會擷取一個資料庫物件。  不過，如果您只指定 `-ServerInstance` 參數，就會傳回該執行個體上所有資料庫的完整清單。

該輸出看起來如下列範例所示：

```
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2017   Normal      336.00 MB   57.01 MB Simple       140 sa
master               Normal        6.00 MB  368.00 KB Simple       140 sa
model                Normal       16.00 MB    5.53 MB Full         140 sa
msdb                 Normal       48.44 MB    1.70 MB Simple       140 sa
PBIRS                Normal      144.00 MB   55.95 MB Full         140 sa
PBIRSTempDB          Normal       16.00 MB    4.20 MB Simple       140 sa
SSISDB               Normal      325.06 MB   26.21 MB Full         140 sa
tempdb               Normal       72.00 MB   61.25 MB Simple       140 sa
WideWorldImporters   Normal         3.2 GB     2.6 GB Simple       130 sa
```

下一個範例使用 `Get-SqlDatabase` Cmdlet 擷取 ServerB 執行個體上的所有資料庫清單，然後顯示方格/資料表 (使用 `Out-GridView` Cmdlet) 以選取應備份的資料庫。  使用者按一下 [確定] 按鈕之後，只會備份醒目提示的資料庫。

```powershell
Get-SqlDatabase -ServerInstance ServerB |
Out-GridView -PassThru |
Backup-SqlDatabase -CompressionOption On
```

此範例同樣會取得已註冊伺服器檔案中列出的所有 SQL Server 執行個體清單，然後針對每個列出的 SQL Server 執行個體呼叫 `Get-SqlAgentJobHistory`，回報從午夜起每個失敗的 SQL Agent 作業。

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE {$_.Mode -ne 'd' } |
FOREACH {
    Get-SqlAgentJobHistory -ServerInstance  $_.Name -Since Midnight -OutcomesType Failed
}
```

在此範例中，我們將執行 `dir` (`Get-ChildItem` 的別名)，取得已註冊伺服器檔案中列出的所有 SQL Server 執行個體清單，然後使用 `Get-SqlDatabase` Cmdlet 取得每個執行個體的資料庫清單。

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE { $_.Mode -ne 'd' } |
FOREACH {
    Get-SqlDatabase -ServerInstance $_.Name
}
```

該輸出看起來如下列範例所示：

```
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level      
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2017   Normal      336.00 MB   57.01 MB Simple       140 sa   
master               Normal        6.00 MB  368.00 KB Simple       140 sa   
model                Normal       16.00 MB    5.53 MB Full         140 sa   
msdb                 Normal       48.44 MB    1.70 MB Simple       140 sa   
PBIRS                Normal      144.00 MB   55.95 MB Full         140 sa   
PBIRSTempDB          Normal       16.00 MB    4.20 MB Simple       140 sa   
SSISDB               Normal      325.06 MB   26.21 MB Full         140 sa   
tempdb               Normal       72.00 MB   61.25 MB Simple       140 sa   
WideWorldImporters   Normal         3.2 GB     2.6 GB Simple       130 sa   
```

## <a name="reporting-problems"></a>回報問題

如果您遇到任何 PowerShell 延伸模組的問題，請參閱[疑難排解文件](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md)，取得診斷和回報問題的相關資訊。

#### <a name="security-note"></a>安全性注意事項

如有任何安全性問題，請參閱[這裡](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md#note-on-security)。

## <a name="contributing-to-the-code"></a>參與程式碼

如需如何參與此延伸模組的詳細資訊，請參閱[開發文件](https://github.com/PowerShell/vscode-powershell/blob/master/docs/development.md)！

## <a name="maintainers"></a>維護人員

- [Keith Hill](https://github.com/rkeithhill) - [@r_keith_hill](http://twitter.com/r_keith_hill)
- [Tyler Leonhardt](https://github.com/tylerl0706) - [@TylerLeonhardt](http://twitter.com/tylerleonhardt)
- [Rob Holt](https://github.com/rjmholt)

## <a name="license"></a>授權

此延伸模組是[依據 MIT 授權條款授權](https://github.com/PowerShell/vscode-powershell/blob/master/LICENSE.txt)。 如需此專案版本隨附協力廠商二進位檔的詳細資訊，請參閱[協力廠商通知](https://github.com/PowerShell/vscode-powershell/blob/master/Third%20Party%20Notices.txt)檔案。

## <a name="code-of-conductconduct-md"></a>[管理辦法][conduct-md]

此專案採用了 [Microsoft 開放原始碼管理辦法][conduct-code]。
如需詳細資訊，請參閱[管理辦法常見問題集][conduct-FAQ]，如有其他問題或意見，請連絡 [opencode@microsoft.com][conduct-email]。

[conduct-code]: https://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: https://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
