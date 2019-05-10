---
title: PowerShell 延伸模組
titleSuffix: Azure Data Studio
description: 安裝和使用 PowerShell for Azure Data Studio
ms.custom: seodec18
ms.date: 04/19/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
manager: matthend
ms.openlocfilehash: c7a2dbdccf92a52d5733a04915acc3f76dc3f033
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105952"
---
# <a name="powershell-editor-support-for-azure-data-studio"></a>Azure Data Studio 的 PowerShell 編輯器支援

此擴充功能提供豐富的 PowerShell 編輯器支援，在[Azure Data Studio](https://github.com/Microsoft/azuredatastudio)。
現在您可以撰寫和偵錯 PowerShell 指令碼使用 Azure Data Studio 提供的絕佳類似 IDE 的介面。

![PowerShell 延伸模組](media/powershell-extension/powershell-extension.png)


## <a name="features"></a>功能

- 語法醒目提示
- 程式碼片段
- 適用於 cmdlet 和更多功能的 IntelliSense
- 所提供的規則為基礎分析[PowerShell 指令碼分析器](http://github.com/PowerShell/PSScriptAnalyzer)
- 移至定義 cmdlet 和變數
- 尋找 cmdlet 和變數的參考
- 文件和工作區的符號探索
- 執行選取的 PowerShell 程式碼中使用的選取範圍<kbd>F8</kbd>
- 啟動下資料指標使用的符號的線上說明<kbd>Ctrl</kbd>+<kbd>F1</kbd>
- 基本的互動式主控台支援 ！


## <a name="installing-the-extension"></a>安裝延伸模組

您可以依照下列中的步驟來安裝官方發行的 PowerShell 延伸模組[Azure Data Studio 文件](https://docs.microsoft.com/sql/azure-data-studio/extensions)。
在 [擴充功能] 窗格中，搜尋"PowerShell"延伸模組並安裝。  您會收到自動任何未來的擴充功能更新 ！

您也可以安裝 VSIX 套件從我們[版本頁面](https://github.com/PowerShell/vscode-powershell/releases)並透過命令列安裝：

```powershell
azuredatastudio --install-extension PowerShell-<version>.vsix
```

## <a name="platform-support"></a>平台支援

- **Windows 7 到 10**包含 Windows PowerShell v3 和更新版本，和 PowerShell Core
- **Linux** ，但 PowerShell Core （所有 PowerShell 支援的散發套件）
- **macOS** ，但 PowerShell Core

讀取[常見問題集](https://github.com/PowerShell/vscode-powershell/wiki/FAQ)常見問題的解答。

## <a name="installing-powershell-core"></a>安裝 PowerShell Core

如果您在 MacOS 或 Linux 上執行 Azure Data Studio，您可能也需要安裝 PowerShell Core。

PowerShell Core 是開放原始碼專案上[GitHub](https://github.com/powershell/powershell)。
如需有關如何在 MacOS 或 Linux 平台上安裝 PowerShell Core 的詳細資訊，請參閱下列文章：

- [在 Linux 上安裝 PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [在 macOS 上安裝 PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)

## <a name="example-scripts"></a>範例指令碼

中的擴充功能有一些範例指令碼`examples`資料夾可供您探索 PowerShell 編輯和偵錯功能。  查看包含[README.md](https://github.com/PowerShell/vscode-powershell/blob/master/examples/README.md)檔案，以深入了解如何使用它們。

此資料夾可以位於下列路徑：

```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.PowerShell-<version>/examples
```

如果您使用擴充功能的預覽版本

 ```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.powershell-preview-<version>/examples
```

開啟/擴充功能的範例中檢視 Azure Data Studio，請從 PowerShell 命令提示字元執行下列程式碼：

```powershell
azuredatastudio (Get-ChildItem $Home\.azuredatastudio\extensions\ms-vscode.PowerShell-*\examples)[-1]
```

### <a name="creating-and-opening-files"></a>建立和開啟檔案

若要建立並開啟新的檔案在編輯器內，使用 新增-EditorFile 從 PowerShell 整合式終端機中。

```powershell
PS C:\temp> New-EditorFile ExportData.ps1
```

此命令適用於任何檔案類型，而不只是 PowerShell 檔案。

```powershell
PS C:\temp> New-EditorFile ImportData.py
```

若要在 Azure 資料 Studio 中開啟一個或多個檔案，請使用`Open-EditorFile`命令。

```powershell
Open-EditorFile ExportData.ps1, ImportData.py
```

### <a name="no-focus-on-console-when-executing"></a>在主控台中執行時沒有焦點

這些是用來使用 SSMS 所使用的使用者，你很習慣能夠執行查詢，以及能夠重新而不需要切換回 [查詢] 窗格中再次執行。  在此情況下，程式碼編輯器的預設行為可能會覺得奇怪，給您。  若要將焦點保持在編輯器中，當您執行與<kbd>F8</kbd>變更下列設定：

```json
"powershell.integratedConsole.focusConsoleOnExecute": false
```

預設值是`true`協助工具。

請注意這項設定會防止焦點變更至主控台，即使您使用的命令，明確呼叫的輸入，例如`Get-Credential`。

## <a name="sql-powershell-examples"></a>SQL PowerShell 範例
若要使用這些範例中 （如下所示），您需要安裝 SqlServer 模組，從[PowerShell 資源庫](https://www.powershellgallery.com/packages/SqlServer)。

```powershell
Install-Module -Name SqlServer
```

> [!NOTE]
> 與版本`21.1.18102`版，與`SqlServer`模組支援[PowerShell Core](https://github.com/PowerShell/PowerShell) 6.2 與更高層級，除了 Windows PowerShell 之外。

在此範例中，我們會使用`Get-SqlInstance`cmdlet 來取得 ServerA 與 ServerB Server SMO 物件。  預設輸出，此命令會包含執行個體的名稱，如版本、 Service Pack & CU 執行個體的更新層級。

```powershell
Get-SqlInstance -ServerInstance ServerA, ServerB
```

以下是範例，這方面的輸出看起來像：

```
Instance Name             Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------             -------    ------------ -----------  ------------ ----------------
ServerA                   13.0.5233  SP2          CU4          Windows      Windows Server 2016 Datacenter
ServerB                   14.0.3045  RTM          CU12         Linux        Ubuntu
```
`SqlServer`模組包含名為提供者`SQLRegistration`可讓您以程式設計方式存取儲存的 SQL Server 連線的下列類型：

+ 資料庫引擎伺服器 （已註冊的伺服器）
+ 中央管理伺服器 (CMS)
+ Analysis Services
+ Integration Services
+ Reporting Services

 在下列範例中，我們將進行`dir`(別名，以供`Get-ChildItem`) 以取得所有已註冊的伺服器檔案中所列的 SQL Server 執行個體的清單。

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse 
```

以下是範例，這方面的輸出如下所示：

```powershell
Mode Name
---- ----
-    ServerA
-    ServerB
-    localhost\SQL2017
-    localhost\SQL2016Happy
-    localhost\SQL2017
```

牽涉到資料庫或資料庫內物件的許多作業`Get-SqlDatabase`指令程式可用。  如果您同時提供值`-ServerInstance`和`-Database`會擷取參數，只有一個資料庫物件。  不過，如果您只有指定`-ServerInstance`參數，將會傳回該執行個體上的所有資料庫的完整清單。

以下是範例，這方面的輸出看起來像：

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

下一個範例會使用`Get-SqlDatabase`cmdlet 來擷取一份所有 ServerB 執行個體的資料庫，然後呈現方格/資料表 (使用`Out-GridView`cmdlet) 來選取應該備份的資料庫。  一旦使用者按一下 [確定] 按鈕，將會反白顯示的資料庫備份。

```powershell
Get-SqlDatabase -ServerInstance ServerB |
Out-GridView -PassThru |
Backup-SqlDatabase -CompressionOption On
```

此範例中，同樣地，取得清單中的所有已註冊的伺服器檔案中所列的 SQL Server 執行個體接著會呼叫`Get-SqlAgentJobHistory`午夜，每個 SQL Server 執行個體所列報告每個失敗的 SQL Agent 作業。

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE {$_.Mode -ne 'd' } |
FOREACH {
    Get-SqlAgentJobHistory -ServerInstance  $_.Name -Since Midnight -OutcomesType Failed
}
```

在此範例中，我們將進行`dir`(別名，以供`Get-ChildItem`) 來取得所有已註冊的伺服器檔案中所列的 SQL Server 執行個體的清單，然後使用`Get-SqlDatabase`cmdlet 來取得每個這些執行個體的資料庫清單。

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE { $_.Mode -ne 'd' } |
FOREACH {
    Get-SqlDatabase -ServerInstance $_.Name
}
```

以下是範例，這方面的輸出看起來像：

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

## <a name="reporting-problems"></a>報告問題

如果您遇到任何 PowerShell 延伸模組的問題，請參閱[疑難排解文件](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md)如需診斷和報告問題。

#### <a name="security-note"></a>安全性注意事項

如需任何安全性問題，請參閱[此處](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md#note-on-security)。

## <a name="contributing-to-the-code"></a>提供給程式碼

請參閱[開發文件](https://github.com/PowerShell/vscode-powershell/blob/master/docs/development.md)如需詳細資訊如何參與編輯此延伸模組 ！

## <a name="maintainers"></a>其困難之處

- [Keith Hill](https://github.com/rkeithhill) - [@r_keith_hill](http://twitter.com/r_keith_hill)
- [Tyler Leonhardt](https://github.com/tylerl0706) - [@TylerLeonhardt](http://twitter.com/tylerleonhardt)
- [Rob Holt](https://github.com/rjmholt)

## <a name="license"></a>使用權

此延伸模組[MIT 授權](https://github.com/PowerShell/vscode-powershell/blob/master/LICENSE.txt)。 如需我們加入與此專案的版本的協力廠商二進位檔的詳細資訊，請參閱[協力廠商通知](https://github.com/PowerShell/vscode-powershell/blob/master/Third%20Party%20Notices.txt)檔案。

## <a name="code-of-conductconduct-md"></a>[程式碼管理辦法][conduct-md]

此專案已採用[Microsoft 開放來源的管理辦法][conduct-code]。
如需詳細資訊，請參閱 <<c0> [ 程式碼的管理辦法常見問題集][ conduct-FAQ] ，或連絡[ opencode@microsoft.com ] [ conduct-email]有任何其他問題或意見。

[conduct-code]: http://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: http://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[conduct-md]: https://github.com/PowerShell/vscode-powershell/blob/master/CODE_OF_CONDUCT.md
