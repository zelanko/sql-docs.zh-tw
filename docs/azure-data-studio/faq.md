---
title: 常見問題集
titleSuffix: Azure Data Studio
description: 關於 Azure Data Studio 的常見問題集 (FAQ)。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 1916a10a468fdc44c021e410eb1521cb7c219d58
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959541"
---
# <a name="includeazure-data-studioincludesname-sosmd-faq"></a>[!INCLUDE[Azure Data Studio](../includes/name-sos.md)] 常見問題集

## <a name="what-is-azure-data-studio"></a>什麼是 Azure Data Studio？

Azure Data Studio 是新的開放原始碼、跨平台的桌面環境，適用於在 Windows、MacOS 和 Linux 上使用內部部署和雲端資料平台的 Azure 資料系列的資料專業人員。 Azure Data Studio 過去是以 SQL Operations Studio 的預覽名稱發行，它可提供新式編輯器體驗，其中包含快速的 IntelliSense、程式碼片段、原始檔控制整合及整合式終端。 它在工程設計時考慮到資料平台使用者，並內建了查詢結果集的圖表和可自訂的儀表板。

研究顯示使用者在查詢編輯時所花費的時間量，比 SQL Server Management Studio 的任何其他工作更多。 基於這個理由，Azure Data Studio 的設計極端著重於最常使用的功能，並提供額外的體驗作為產品的選擇性延伸模組。 這可讓每個使用者將其環境自訂為最常使用的工作流程。


## <a name="how-much-does-azure-data-studio-cost"></a>Azure Data Studio 的成本是多少？

Azure Data Studio 可供私人或商業用途免費使用。

## <a name="who-should-use-azure-data-studio"></a>誰應該使用 Azure Data Studio

任何人都可以使用 Azure Data Studio。 不過，它是設計來簡化資料庫開發人員、資料庫管理員、系統管理員和獨立軟體廠商所執行的工作。

## <a name="what-can-i-do-with-azure-data-studio"></a>我能用 Azure Data Studio 來做什麼？

Azure Data Studio 建置於 Visual Studio Code 之上，並在與 SQL Server、Azure SQL Database、Azure SQL DW 搭配使用時，提供輕量、以鍵盤為主的新式程式碼工作流程體驗。 Azure Data Studio 利用多個索引標籤視窗、豐富的 SQL 編輯器、IntelliSense、關鍵字完成、程式碼片段與程式碼導覽和原始檔控制整合 (Git 和 TFS) 等內建功能，使您每日仰賴的核心體驗變得輕鬆簡單。 您可以在熟悉的物件瀏覽體驗中執行隨選查詢、檢視結果並將其儲存為文字、JSON 或 Excel、編輯資料、組織及管理您慣用的資料庫連線，以及瀏覽資料庫物件。

在 Azure Data Studio 使用者介面的整合式終端機視窗中，使用您慣用的命令列工具 (例如 Bash、PowerShell、sqlcmd、bcp、psql 和 ssh)。 針對您的資料庫物件輕鬆產生並執行 CREATE 和 INSERT 指令碼，以建立資料庫複本供開發或測試之用。 利用智慧型程式碼片段和豐富的圖形化體驗，以建立新的資料庫和資料庫物件 (例如資料表、檢視、預存程式、使用者、登入、角色等)，或更新現有的資料庫物件，可提高您的生產力。 使用可自訂的豐富儀表板來監視內部部署、Azure 或任何雲端中的資料庫效能瓶頸，並針對這些瓶頸進行快速疑難排解。

Azure Data Studio 提供一致的資料庫備份與還原體驗。 透過 SQL Server Always-On 可用性群組的計劃支援，您可以針對關鍵任務 SQL Server 資料庫輕鬆地設定、監視 AG 及對其進行疑難排解，並在嚴重損壞期間快速容錯移轉至次要資料庫。 Azure Data Studio 的設計，是為了讓您在所選擇作業系統上的選擇資料庫 DevOps 生命週期中更具生產力。 如此一來，您隨時都能進行掌控，而且可以降低風險、更快地解決問題，並持續提供超出客戶期望的價值。

## <a name="is-azure-data-studio-open-source"></a>Azure Data Studio 是開放原始碼嗎？

您可以在 GitHub 上取得 Azure Data Studio 及其資料提供者的原始程式碼。 前端 Azure Data Studio (以 Visual Studio Code 為基礎) 的原始程式碼可在原始程式碼的使用者授權合約下取得，該合約提供修改和使用軟體的權限，但不能在雲端服務中進行重新散發或裝載。 資料提供者的原始程式碼可在 MIT 授權下取得，網址為：[https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice)。

## <a name="do-we-plan-to-open-source-ssms"></a>我們計劃開放原始碼 SSMS 嗎？

資料分割 不過，下一代多 OS CLI 與 GUI 工具是開放原始碼。 例如，VS Code 的 mssql 延伸模組、mssql-scripter 和 msql-CLI 都是 GitHub 上的開放原始碼。 您可以在 GitHub 上取得 Azure Data Studio 的原始程式碼。  

## <a name="now-that-there-is-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>現在有了 Azure Data Studio，Microsoft 打算淘汰 SSMS 和 SSDT 嗎？ 

資料分割 除了新一代的多 OS 和多 DB CLI 與 GUI 工具以外，還會繼續進行對旗艦版 Windows 工具 (SSMS、SSDT、PowerShell) 的投資。 其目標是要讓客戶選擇使用為其案例選擇的平台上所需的工具。 Azure Data Studio 更密切著重在查詢編輯和資料開發方面的體驗，而研究顯示為 SQL Server Management Studio 中依程度列出的最常使用功能。 其他高價值的系統管理功能 (例如備份、還原、代理程式作業管理和伺服器分析) 也可提供作為 Azure Data Studio 中的延伸模組。 Azure Data Studio 也是跨平台產品，可讓使用者能夠在他們選擇的平台上工作。 不過，SQL Server Management Studio 仍然提供最廣泛的系統管理功能，而且仍然是平台管理工作的旗艦工具。 

## <a name="when-should-i-use-azure-data-studio-vs-sql-server-management-studio"></a>何時應該使用 Azure Data Studio 與 SQL Server Management Studio？

 在下列情況下使用 Azure Data Studio：

- 將大部分的時間花在編輯或執行查詢。
- 需要能夠快速繪製和視覺化結果集。
- 可以使用 sqlcmd 或 Powershell 透過整合式終端機來執行大部分的系統管理工作。
- 對精靈體驗的需求最少。
- 不需要執行深層管理或平台相關設定。
- 需要在 macOS 或 Linux 上執行。

 在下列情況下使用 SQL Server Management Studio：

- 將大部分的時間花在資料庫管理工作。
- 正在執行複雜的系統管理或平台設定。
- 正在執行安全性管理，包括使用者管理、漏洞評量，以及安全性功能的設定。
- 需要使用效能微調建議程式和儀表板。
- 使用資料庫圖表和資料表設計工具。
- 正在執行 DACPAC 的匯入/匯出。
- 需要存取已註冊的伺服器。
- 利用 sqlcmd 模式、即時查詢統計資料或用戶端統計資料。

## <a name="feature-comparison"></a>功能比較

### <a name="shell-features"></a>Shell 功能

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Azure 登入|是|是|
|儀表板|是| |
|延伸模組|是| |
|整合式終端|是||
|物件總管|是|是|
|物件指令碼|是|是|
|專案系統|是||
|從資料表選取|是|是|
|原始程式碼控制|是||
|工作窗格|是||
|佈景主題|是||
|深色模式|是||
|Azure 資源總管|預覽||
|產生指令碼精靈||是
|滙入\匯出 DACPAC||是|
|物件屬性||是|
|資料表設計工具||是|

### <a name="query-editor"></a>查詢編輯器

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|圖表檢視器|是||
|將結果匯出至 CSV、JSON、XLSX|是||
|IntelliSense|是|是|
|程式碼片段|是|是|
|顯示計畫|預覽|是|
|用戶端統計資料||是|
|即時查詢統計資料||是|
|查詢選項||是|
|將結果存檔||是|
|以文字顯示結果||是|
|空間檢視器||是|
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
|HDFS 整合|預覽||
|筆記型電腦|預覽||

### <a name="database-administration"></a>資料庫管理

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|備份 / 還原|是|是|
|一般檔案匯入|預覽|是|
|SQL 代理程式|預覽|是|
|SQL Profiler|預覽|是|
|Always On||是|
|永遠加密||是|
|複製資料精靈||是|
|資料調整建立程式||是|
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


## <a name="azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>Azure Data Studio 缺少 SSMS/SSDT 中的功能。 您會新增該功能嗎？

這取決於案例與客戶/商務需求。 若要協助排定優先順序，請在 [GitHub](https://github.com/microsoft/azuredatastudio/issues) 上提出建議。

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>我了解 Azure Data Studio 和 VS Code 的 mssql 延伸模組是由幕後使用 SMO API 的新工具服務提供技術支援。 SMO 是否可以在 Linux 和 macOS 上使用？

SMO API 還無法在 Linux 或 macOS 上以消費方式使用。 我們已將 Azure Data Studio 所需且計劃在藍圖期間進行擴充的 SMO API 子集移植到 .NET Core。 SQL 工具服務位於 GitHub 上：[https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice)。

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>您是否計劃將 DACFx API 和/或 sqlpackage.exe 和/或 SSDT 移植到 Linux 和 macOS？

其已納入長期藍圖。 若要協助排定優先順序，請在 [GitHub](https://github.com/microsoft/azuredatastudio/issues) 上提出建議。

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>SQL PowerShell Cmdlet 是否可以在 Linux 和 macOS 上使用？

SQL PowerShell 目前可以在 PowerShell 資源庫上取得，而您可以在 Windows 上使用它來與任何地方執行的 SQL Server 搭配執行，包括 Linux 上的 SQL。 在 Linux 和 macOS 上提供 SQL PowerShell Cmdlet 的需求已納入藍圖中。 若要協助排定優先順序，請在 [GitHub](https://github.com/microsoft/azuredatastudio/issues) 上提出建議。

## <a name="who-usually-uses-azure-data-studio"></a>誰通常會使用 Azure Data Studio？

開發人員和 DBA 通常是 Azure Data Studio 的使用者。

## <a name="does-azure-data-studio-integrate-with-azure-sql-data-warehouse"></a>Azure Data Studio 是否與 Azure SQL 資料倉儲整合？

是的。 Azure SQL 資料倉儲的 Azure Data Studio 支援目前處於預覽階段，可與 Azure SQL Database 受控執行個體和 SQL Server 2019 巨量資料搭配使用。

## <a name="why-is-azure-data-studio-important-for-the-new-version-of-sql-server"></a>為什麼 Azure Data Studio 對 SQL Server 的新版本來說很重要？

隨著 SQL Server 將其功能延伸到巨量資料空間，它需要新的工具來支援這些使用案例。 基於這個理由，Azure Data Studio 今日推出支援 SQL Server 巨量資料的新預覽體驗，包括 SQL Server 工具組中的首次筆記本體驗，以及可從遠端 SQL Server 和 Oracle 執行個體輕鬆且快速地存取資料的新 [建立外部資料表] 精靈。
