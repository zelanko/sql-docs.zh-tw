---
title: 總覽
titleSuffix: Azure Data Studio
description: Azure Data Studio 是免費、 輕量級工具，來管理 SQL Server、 Azure SQL Database 和 Azure SQL 資料倉儲在 Windows、 macOS 和 Linux 上執行。
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: overview
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7369893be3cd42dab0e0c0cd870a52c639083b5
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161605"
---
# <a name="what-is-azure-data-studio"></a>什麼是 Azure Data Studio？

Azure Data Studio 是跨平台資料庫工具，供資料專業人員使用 Microsoft 家族的內部部署和雲端資料平台，在 Windows、 MacOS 和 Linux 上的。

先前的預覽名稱 SQL Operations Studio 發行，Azure Data Studio 提供 Intellisense、 程式碼片段、 原始檔控制整合和整合式終端機使用現代的編輯器體驗。 它在設計時將資料庫平台使用者納入考量，內建查詢結果集合圖表功能和可自訂自的儀表板。

**[下載並安裝 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)**


## <a name="sql-code-editor-with-intellisense"></a>具有 IntelliSense 的 SQL 程式碼編輯器

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 提供現代、 以鍵盤為主的 SQL 程式碼撰寫體驗，可讓您日常的工作更容易利用內建功能，例如多個索引標籤式視窗、 豐富的 SQL 編輯器、 IntelliSense、 關鍵字完成、 程式碼片段、 程式碼巡覽、 和原始檔控制整合 (Git)。 執行隨 SQL 查詢、 檢視以及將結果儲存為文字、 JSON 或 Excel。 編輯資料、 組織您最愛的資料庫的連接，並瀏覽熟悉的物件瀏覽體驗中的資料庫物件。 若要了解如何使用 SQL 編輯器，請參閱[使用 SQL 編輯器來建立資料庫物件](tutorial-sql-editor.md)。

## <a name="smart-sql-code-snippets"></a>智慧型 SQL 程式碼片段

SQL 程式碼片段會產生適當的 SQL 語法來建立資料庫、 資料表、 檢視、 預存程序、 使用者、 登入、 角色等等，並更新現有的資料庫物件。 使用智慧程式碼片段快速建立資料庫副本以進行開發或測試，並生成和執行 CREATE 和 INSERT 指令。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 也提供功能來建立自訂的 SQL 程式碼片段。 若要進一步了解，請參閱[建立和使用程式碼片段](code-snippets.md)。


## <a name="customizable-server-and-database-dashboards"></a>可自訂的伺服器和資料庫儀表板

建立豐富可自訂的儀表板來監視，並快速移難排解在您的資料庫中的效能瓶頸。 若要深入了解 insight widget 和資料庫 （和伺服器）的儀表板，請參閱[透過 insight widget 管理伺服器和資料庫](insight-widgets.md)。

## <a name="connection-management-server-groups"></a>連接管理（伺服器群組）

伺服器群組提供一種方式組織的伺服器和您使用的資料庫的連接資訊。 如需詳細資訊，請參閱 <<c0> [ 伺服器群組](server-groups.md)。

## <a name="integrated-terminal"></a>整合式終端機

在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 使用者介面的整合式終端機視窗中，使用您喜歡的命令列工具 (例如：Bash, PowerShell, sqlcmd, bcp和 ssh)。 若要深入了解整合式終端機，請參閱[整合式終端機](integrated-terminal.md)。

## <a name="extensibility-and-extension-authoring"></a>擴充性和擴充功能撰寫

增強[!INCLUDE[name-sos](../includes/name-sos-short.md)]擴充功能的基底的安裝體驗。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 資料管理活動，以及支援擴充功能撰寫提供擴充點。

若要了解中的擴充性[!INCLUDE[name-sos](../includes/name-sos-short.md)]，請參閱 <<c2> [ 擴充性](extensibility.md)。
若要深入了解撰寫延伸模組，請參閱[延伸模組製作](extension-authoring.md)。

## <a name="feature-comparison-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 的功能比較

**使用 Azure Data Studio，如果您：**
- 要在 macOS 或 Linux 上執行
- 連線到 SQL Server 2019 巨量資料叢集
- 大部分的時間編輯或執行查詢
- 必須要能夠快速圖表，並以視覺化方式檢視結果集
- 可以執行大部分的系統管理工作，透過使用 sqlcmd 或 Powershell 整合式終端機
- 精靈的使用體驗的最少需要
- 不需要進行深入的系統管理的設定

**使用 SQL Server Management Studio，如果您：**
- 資料庫管理工作的支出最多的時間
- 進行深度管理組態
- 進行安全性管理，包括使用者管理、 弱點評量和組態的安全性功能
- 使用於報告的 SQL Server 查詢存放區
- 需要進行效能微調建議程式和儀表板的使用
- 正在匯入/匯出的 Dacpac
- 需要存取已註冊的伺服器和想要控制 SQL Server 在 Windows 上的服務

### <a name="shell"></a>Shell

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Azure 登入|是|是|
|儀表板|是||
|延伸模組|是||
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
|產生指令碼精靈||是|
|Import\Export DACPAC||是|
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

### <a name="operating-system-support"></a>作業系統支援

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|Linux|是||
|macOS|是||
|視窗|是|是|

### <a name="data-engineering"></a>資料工程

|功能|Azure Data Studio|SSMS|
|:---|:---|:---|
|建立外部資料表精靈|預覽||
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



## <a name="next-steps"></a>後續步驟
- [下載並安裝 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [連線及查詢 SQL Server](quickstart-sql-server.md)
- [連線及查詢 Azure SQL Database](quickstart-sql-database.md)
