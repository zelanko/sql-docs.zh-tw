---
title: 常見問題集
titleSuffix: Azure Data Studio
description: 有關 Azure Data Studio 常見問題 (faq)。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 129e7de66e896e1f452c5d68fc4891d9cc5eafa3
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030328"
---
# <a name="includeazure-data-studioincludesname-sosmd-faq"></a>[!INCLUDE[Azure Data Studio](../includes/name-sos.md)] 常見問題集

## <a name="what-is-azure-data-studio"></a>什麼是 Azure Data Studio？

Azure Data Studio 是一個新的開放原始碼的跨平台桌面環境，可讓資料專業人員在 Windows、MacOS 與 Linux 上使用內部與雲端資料平台的 Azure 資料系列服務。 先前以預覽名稱 SQL Operations Studio 發行，Azure Data Studio 提供現代化編輯器體驗，具有閃電般快速的 IntelliSense、程式碼片段、原始檔控制整合和整合式終端機。 它在設計時將資料庫平台使用者納入考量，內建查詢結果集合圖表功能和可自訂自的儀表板。

研究顯示，在使用 SQL Server Management Studio 時與任何其他工作相比，使用者花費更多時間在查詢編輯上。 基於這個理由，Azure Data Studio 深度專注在使用頻率最高的功能，並以可選用擴充套件加入產品以提供額外體驗。 這允許每個使用者根據他們最常使用的工作流程來自訂其環境。


## <a name="how-much-does-azure-data-studio-cost"></a>Azure Data Studio 費用是多少？

Azure Data Studio 提供私人或商業用途免費使用。

## <a name="who-should-use-azure-data-studio"></a>誰應該使用 Azure Data Studio

任何人都可以使用 Azure Data Studio。 不過，它可簡化資料庫開發人員、 資料庫管理員、 系統管理員及獨立軟體廠商所執行的工作。

## <a name="what-can-i-do-with-azure-data-studio"></a>我可以使用 Azure Data Studio 來做什麼？

Azure Data Studio 以 Visual Studio Code 建置，並提供輕量型、 鍵盤焦點的現代程式碼工作流程體驗，當使用 SQL Server，Azure SQL Database、 Azure SQL DW。 Azure Data Studio 可讓您依賴每一天，簡單又容易使用內建的功能，例如多索引標籤式視窗、 豐富的 SQL 編輯器、 IntelliSense、 關鍵字完成、 程式碼片段和程式碼瀏覽和原始檔控制整合 (Git 核心經驗和 TFS）。 您可以執行隨選查詢，檢視 & 將結果儲存為文字、 JSON 或 Excel、 編輯資料、 組織和管理您最愛的資料庫的連線，並瀏覽中熟悉的物件瀏覽經驗的資料庫物件。

使用您最愛的命令列工具 (例如 Bash、 PowerShell、 sqlcmd、 bcp、 psql，和 ssh) 在整合式終端機視窗中，直接在 Azure Data Studio 使用者介面中。 輕鬆產生並執行建立與您的資料庫物件，以建立您用於開發或測試用途的資料庫副本的 INSERT 指令碼。 提升產能，智慧型程式碼片段和豐富的圖形化體驗，建立新的資料庫和資料庫物件 （例如資料表、 檢視、 預存程序、 使用者、 登入、 角色等） 或更新現有的資料庫物件。 使用豐富可自訂儀表板來監視，並快速移難排解效能瓶頸在資料庫內部，而在 Azure 或任何雲端。

Azure Data Studio 提供一致的體驗，來備份和還原您的資料庫。 SQL Server Always-On 可用性群組的計劃支援，您可以輕鬆地設定、 監視和疑難排解的任務關鍵性的 SQL Server 資料庫和快速容錯移轉至次要資料庫的 Ag，在發生災害時。 Azure Data Studio 旨在讓您選擇在您選擇的作業系統上的資料庫 DevOps 生命週期中更具生產力。 如此一來，您永遠在控制項中，而且您可以降低風險、 解決問題的速度，並持續不斷地交付超出客戶預期的值。

## <a name="is-azure-data-studio-open-source"></a>是 Azure Data Studio 開放原始碼嗎？

Azure Data Studio 和其資料提供者的原始程式碼可在 GitHub 上。 前端的 Azure Data Studio （此作業取決於 Visual Studio Code） 的原始程式碼位在原始程式碼提供修改及使用軟體，但是不能將其重新散發，或裝載在雲端服務中的權限的使用者授權合約。 資料提供者的原始程式碼可在 MIT license [ https://github.com/Microsoft/sqltoolsservice ](https://github.com/Microsoft/sqltoolsservice)。

## <a name="do-we-plan-to-open-source-ssms"></a>我們計劃開放原始碼 SSMS？

資料分割 不過下, 一代的多重作業系統 CLI 和 GUI 工具是開放原始碼。 比方說，VS Code、 mssql-scripter 和 msql CLI mssql 擴充功能是在 GitHub 上的所有開放原始碼。 使用 GitHub 上適用於 Azure 資料 Studio 原始程式碼。  

## <a name="now-that-there-is-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>現在已有 Azure Data Studio，沒有 Microsoft 計劃取代 SSMS 和 SSDT 嗎？ 

資料分割 除了下一代的多重作業系統或多個 DB CLI 和 GUI 工具，將會繼續投資旗艦級 Windows 工具 （SSMS、 SSDT、 PowerShell）。 目標是要提供客戶選擇自己選擇的平台上使用他們想要的工具，其案例。 Azure Data Studio 更緊密地致力於查詢編輯經驗，而且資料開發的研究顯示 SQL Server Management Studio 中的最常用的功能依重要性排序。 為 Azure Data Studio 中的延伸模組還有其他高價值系統管理功能，例如備份、 還原、 代理程式作業管理，和伺服器程式碼剖析。 Azure 資料 Studio 也是跨平台，可讓使用者在其選擇的平台上運作。 不過，SQL Server Management Studio 仍然提供最大範圍的系統管理功能，而且仍然平台管理工作的旗艦版工具。 

## <a name="when-should-i-use-azure-data-studio-vs-sql-server-management-studio"></a>當我應該使用 Azure Data Studio 與 SQL Server Management Studio 嗎？

*使用 Azure Data Studio，如果您：*

- 花費大部分的時間編輯或執行查詢。
- 需要快速圖表，並以視覺化方式檢視結果集的功能。
- 可以執行大部分的系統管理工作，透過使用 sqlcmd 或 Powershell 整合式終端機。
- 有精靈 」 的使用體驗的最小需求。
- 不需要執行系統管理的深層 」 或 「 平台相關的設定。
- 要在 macOS 或 Linux 上執行。

*使用 SQL Server Management Studio，如果您：*

- 資料庫管理工作的支出最多的時間。
- 執行複雜的系統管理或平台設定。
- 正在做的安全性管理，包括使用者管理、 弱點評量以及組態的安全性功能。
- 需要進行效能微調建議程式和儀表板的使用。
- 使用資料庫圖表及資料表設計工具。
- 正在匯入/匯出的 Dacpac。
- 需要存取已註冊的伺服器。
- 請使用 sqlcmd 模式，即時查詢統計資料或用戶端統計資料。

## <a name="feature-comparison"></a>功能比較

### <a name="shell-features"></a>殼層功能

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Azure 登入|是|是|
|儀表板|是| |
|延伸模組|是| |
|整合式終端機|是||
|物件總管|是|是|
|物件指令碼|是|是|
|專案系統|是||
|從資料表選取|是|是|
|原始程式碼控制|是||
|工作窗格|是||
|佈景主題|是||
|深色的模式|是||
|Azure 資源總管|預覽||
|產生指令碼精靈||是
|DACPAC 匯入/匯出||是|
|物件屬性||是|
|資料表設計工具||是|

### <a name="query-editor"></a>查詢編輯器

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|圖表檢視器|是||
|將結果匯出至 CSV、 JSON、 XLSX|是||
|IntelliSense|是|是|
|程式碼片段|是|是|
|顯示計畫|預覽|是|
|用戶端統計資料||是|
|即時查詢統計資料||是|
|查詢選項||是|
|將結果存檔||是|
|以文字顯示結果||是|
|空間的檢視器||是|
|SQLCMD||是|
|T-SQL 偵錯工具||是|

### <a name="operating-system-support"></a>作業系統支援

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Windows|是|是|
|macOS|是||
|Linux|是||

### <a name="data-engineering"></a>資料工程

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|外部資料精靈|預覽||
|HDFS 的整合|預覽||
|筆記型電腦|預覽||

### <a name="database-administration"></a>資料庫管理

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|備份/還原|是|是|
|一般檔案匯入|預覽|是|
|SQL 代理程式|預覽|是|
|SQL Profiler|預覽|是|
|Always On||是|
|永遠加密||是|
|複製資料精靈||是|
|Tuning Advisor 的資料||是|
|資料庫圖表||是|
|錯誤記錄檔檢視器||是|
|維護計畫||是|
|多伺服器查詢||是|
|原則式管理||是|
|PolyBase||是|
|查詢存放區||是|
|已註冊的伺服器||是|
|複寫||是|
|安全性管理||是|
|Service Broker||是|
|SQL Mail||是|
|範本總管||是|
|弱點評量||是|
|XEvent 管理||是|


## <a name="azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>Azure Data Studio 遺漏 SSMS/SSDT 中的功能。 您會將它加入嗎？

這取決於案例和客戶/商務需求。 為了協助排列優先順序，在上提出建議[GitHub](https://github.com/microsoft/azuredatastudio/issues)。

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>我了解 Azure Data Studio 和適用於 VS Code 的 mssql 擴充功能，由實際上會使用 SMO Api 的新工具服務。 SMO 是適用於 Linux 和 macOS 的？

SMO Api 目前不提供 Linux 或 macOS 上可取用的方式。 我們將移植到.NET Core，我們所需的 Azure Data Studio，而且我們打算展開計劃的一部分的 SMO Api 的子集。 在 GitHub 上的 SQL 工具服務是： [ https://github.com/Microsoft/sqltoolsservice ](https://github.com/Microsoft/sqltoolsservice)。

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>您是否計劃的 DACFx Api 及/或 sqlpackage.exe 和/或 SSDT 至 Linux 和 macOS 的連接埠？

它是在較長期的規劃。 為了協助排列優先順序，在上提出建議[GitHub](https://github.com/microsoft/azuredatastudio/issues)。

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>SQL PowerShell cmdlet 都可在 Linux 和 macOS 上使用？

SQL PowerShell 現在已發佈至 PowerShell 資源庫，並使用在 Windows 上使用 SQL Server 執行任意位置，包括在 Linux 上的 SQL。 提供 SQL PowerShell cmdlet，在 Linux 及 macOS 上的，已在藍圖。 為了協助排列優先順序，在上提出建議[GitHub](https://github.com/microsoft/azuredatastudio/issues)。

## <a name="who-usually-uses-azure-data-studio"></a>通常，誰會使用 Azure Data Studio？

開發人員和 Dba 通常是 Azure Data Studio 的使用者。

## <a name="does-azure-data-studio-integrate-with-azure-sql-data-warehouse"></a>Azure Data Studio 不會使用 Azure SQL 資料倉儲整合？

是的。 Azure SQL 資料倉儲的 azure Data Studio 支援目前為預覽狀態，以及 Azure SQL Database 受控執行個體，與 SQL Server 2019 巨量資料。

## <a name="why-is-azure-data-studio-important-for-the-new-version-of-sql-server"></a>為何重要的新版本的 SQL Server 的 Azure Data Studio？

由於 SQL Server 擴充其功能的巨量資料空間，因此它需要新的工具，來支援這些使用案例。 基於這個理由，Azure Data Studio 會立即傳送新的預覽體驗，支援的 SQL Server 巨量資料，包括第一個以往在 SQL Server 工具組和新的 Create External Table 精靈，可存取的資料，從遠端 SQL 的 notebook 體驗Server 和 Oracle 執行個體輕鬆且快速。
