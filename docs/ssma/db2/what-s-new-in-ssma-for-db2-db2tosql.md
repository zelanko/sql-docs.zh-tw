---
title: SSMA for DB2 (DB2ToSQL) 的新功能 |Microsoft Docs
description: 瞭解每個版本的 SQL Server 移轉小幫手 (SSMA) for DB2 (DB2ToSQL) 的變更。
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 12/17/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
ms.author: alexiva
ms.openlocfilehash: 37d0898d242073c9bc842d0d3cca645acc02a851
ms.sourcegitcommit: a16b98d3bf3eeb58f5d2aeece2464f8a96e2b4a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2020
ms.locfileid: "97665819"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>SSMA for DB2 的新功能 (DB2ToSQL) 

本文列出每個版本中 SQL Server 移轉小幫手 DB2 變更的 (SSMA) 。

## <a name="ssma-v816"></a>SSMA v 8.16

SSMA for DB2 的 v 8.16 版本包含下列變更：

* 修正具有特殊字元的資料行別名轉換
* 修正子句的轉換 `SELECTIVITY`
* 改進子句的轉換 `WITH ROW MOVEMENT`
* 移除舊版剖析器的支援
* 修正無法從資料庫重新整理之物件的問題

## <a name="ssma-v815"></a>SSMA v 8.15

除了許多協助工具改進之外，SSMA for DB2 的8.15 版本也包含下列變更：

* `MIN` / `MAX` 使用日期/時間引數修正彙總函式的轉換
* 修正 `VARCHAR_FORMAT` 使用預留位置時模擬函式中的 bug `DD`
* 改善資料類型的類型對應 `TIME`
* `ROUND` `TRUNC` 使用數值引數改善和函式的轉換
* 改造評量報告以在新式瀏覽器中工作
* 使用資料庫提供的授權單位進行 Azure AD authentication
* 改善從檔案載入之語句的命名

## <a name="ssma-v814"></a>SSMA v 8.14

除了許多改進以確保殘障人士能獲得更高的協助工具，8.14 版的 SSMA for DB2 需要專案升級，因為它現在會在專案中繼資料中儲存完整的來源/目標伺服器版本。

## <a name="ssma-v813"></a>SSMA v 8.13

SSMA for DB2 的 v 8.13 版本包含下列變更：

* 支援篩選的唯一索引
* 轉換程式和函式呼叫時，請考慮隱含類型轉換
* 改善來源連接字串的記錄，以協助疑難排解連接問題

## <a name="ssma-v812"></a>SSMA v 8.12

SSMA for DB2 的 v 8.12 版本包含下列變更：

* 函數的轉換 `STRIP`
* 改進程式選項剖析

## <a name="ssma-v811"></a>SSMA v 8.11

SSMA for DB2 的 v 8.11 版本包含下列變更：

*  (7.1 和更新版本的 DB2 支援) 
* 和的翻譯 `SQLSTATE``SQLCODE`
* 函式內副作用運算子的轉換錯誤訊息
* 使用 MSAL.NET 程式庫進行互動式 Azure Active Directory 驗證

## <a name="ssma-v810"></a>SSMA v 8.10

SSMA for DB2 的 v1.1 版本可解決外鍵探索中的回歸，並包含次要效能改進。

## <a name="ssma-v89"></a>SSMA v 8。9

SSMA for DB2 的 v 8.9 版本包含下列變更：

* 函數轉換的修正 `TIMESTAMPDIFF`
* 分割索引存在時的索引探索修正
* 修正在其他架構中定義主要索引時的外鍵探索
* 改進符合內建函數名稱的資料行轉換
* 修正專案名稱中特殊字元的問題

## <a name="ssma-v88"></a>SSMA v 8。8

SSMA for DB2 的8.8 版包含：

* SQL Server 物件同步處理穩定性改進
* 評估和轉換期間的 GUI 效能改進
* 從更新到的對應 `ROWID` `varbinary(40)` ，以加速資料移轉
* 改進的 `SELECT ... FROM NEW/OLD TABLE` 語句轉換
* 程式和函式之語句的新轉換 `ALTER`
* 解構指派的新轉換

## <a name="ssma-v87"></a>SSMA v 8。7

SSMA for DB2 的8.7 版包含全新的 DB2 語法剖析器，以及圖形化使用者介面中的次要修正和效能改進。

此外，SSMA for DB2 現在提供：

* 從 LUW 上的 DB2 進行遷移時，用於探索外鍵的修正。
* 改進的 `SELECT ... FOR UPDATE` 語句轉換。
* 改進 `COUNT` MQ 資料表中函數的轉換。
* 語句的轉換 `SAVEPOINT` 。
* 轉換以模擬 `NULL` values in 子句中的 DB2's 行為 `ORDER BY` 。
* 剖析語句的支援 `ASSOCIATE RESULT SET` 。

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v86"></a>SSMA v 8。6

除了針對改善可用性和效能而設計的一組目標修正之外，還新增了一個可讓使用者在轉換後的程式碼中省略 SSMA 擴充屬性的設定，藉此增強 SSMA for DB2 的 v 8.6 版本。

若要利用這項設定，請在 SSMA for DB2 中，流覽至 [**工具**  >  **專案設定**  >  **一般**  >  **轉換**]，然後在 [**其他**] 下，將 [**省略擴充屬性**] 設定的值更新為 **[是]**。

![省略擴充屬性設定](../db2/media/ssma-omit-extended-properties.png)

此外，SSMA for DB2 現在提供：

* 使用預設引數值之函式的轉換修正。
* 已改善函式的 `PARAMETER` 子句剖析。
* 轉換語句的能力 `LEAVE` 。

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v85"></a>SSMA v 8。5

SSMA for DB2 的8.5 版已透過支援 SQL server 中的 Azure Active Directory authentication 和 JSON 功能的基本支援來增強，並提供一組針對改善可用性和效能而設計的目標修正。

此外，SSMA for DB2 的增強功能如下：

* 支援使用加入語句的轉換 `GET DIAGNOSTICS` `ROW_NUMBER` 。
* 修正未遵守物件名稱開頭之空格的相關 bug。

> [!IMPORTANT]
> 使用 SSMA v 8.5 時，.NET 4.7.2 是必要的安裝程式。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v84"></a>SSMA v 8。4

SSMA for DB2 的8.4 版已利用專為解決協助工具問題而設計的目標修正程式來增強，並修正與 max index columns 相關的錯誤 (，以允許 SQL Server 2016 和更新版本的32而非 16) 。

> [!IMPORTANT]
> 使用 SSMA 版本7.4 至8.4，.NET 4.5.2 是必要條件的安裝。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for DB2 的 v 8.3 發行版本已利用專為改善品質和轉換度量而設計的目標修正來增強。 此外，此版本的 SSMA for DB2 提供下列修正：

* 解決協助工具問題。
* `hierarchyid`在 SQL Server 中加入類型的基本支援。
* 使用將 z/OS 探索查詢中的修剪函數使用方式取代為 `RTRIM` / `LTRIM` 。
* 當以「標準模式」連接時，允許使用者指定套件集合 (預設為 `NULLID`) 。
* 加入的轉換 `CREATE TABLE AS SELECT` 。
* 改善全域臨時表的轉換。
* 解決物件唯一性檢查順序的問題，以設定資料表在條件約束上的優先順序（如果名稱衝突）。
* 解決針對 `DATE` z/OS 載入和的預設資料行值時所發生的問題 `TIMESTAMP` 。
* 支援 Unicode 換行字元 (也稱為 `NEL`) 。
* 解決具有遺失子句的資料指標轉換問題 `RETURN TO` 。
* 新增標籤和的支援 `GOTO` 。

## <a name="ssma-v82"></a>SSMA v 8。2

SSMA for DB2 的8.2 版已增強，可解決從 SSMA 主控台工具連接到 Azure SQL Database 的問題，以及在轉換期間遺漏 view 宣告中的 COUNT_BIG 資料行。 此外，此版本還包含一組目標修正程式，其設計目的是要改善品質和轉換度量，以及下列各項的修正：

* 資料移轉後停用非叢集索引的問題。
* 無訊息安裝期間的 .NET Framework 偵測。
* 下載新版本時所發生的間歇性損毀。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v4.0 至8.2 版的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA v 8。1

SSMA for DB2 的8.1 版已增強，可提供專為改善品質和轉換度量而設計的目標修正。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA 8.0 版更新為 v4.0 的失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA 8.0 版

SSMA for DB2 8.0 版的增強功能，可提供旨在改善品質和轉換度量的目標修正。 此版本也提供下列新功能：

* 支援以 **AZURE SQL 受控執行個體** 作為目標。 您現在可以建立以 Azure SQL 受控執行個體為目標的新專案：

  ![SQL MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後的 **修正程式**。 若要深入瞭解[，請參閱。](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 初步的資料庫/架構選取。

  連接到來源時，使用者現在可以選取想要的資料庫/架構。 只選取您打算遷移的架構，可在初始連接期間節省時間，並改善整體 SSMA 效能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

SSMA for DB2 的 v 7.10 版本包含下列變更：

* 目標修正程式旨在提供額外的安全性和隱私權保護，以符合全球需求的變更。
* 區塊轉換的修正程式 `BEGIN-END` 。

## <a name="ssma-v79"></a>SSMA v 7。9

SSMA for DB2 的 v 7.9 版本包含下列變更：

* 改善品質和轉換度量的目標修正。
* 支援 SSMA 命令列來改變資料類型對應和專案喜好設定。
* 支援使用 SQL Server Integration Services (SSIS) 來遷移資料。 轉換架構之後，您可以使用滑鼠右鍵內容功能表選項來建立 SSIS 封裝。
* SSMA 中的 [Azure SQL Database 連接] 對話方塊也已經改變，以指定完整的伺服器名稱。 在舊版 SSMA 中，必須在專案設定內明確提及 Azure SQL Database 前置詞。

## <a name="ssma-v78"></a>SSMA v 7。8

SSMA for DB2 的7.8 版包含下列變更：

* 在 [ *專案設定*] 中反白顯示變更類型對應。
* 使用者停用遙測的能力。

## <a name="ssma-v77"></a>SSMA 7。7

SSMA for DB2 的7.7 版包含下列變更：

* 改善品質和轉換度量的目標修正。
* 根據熱門需求，32位版本的 SSMA for DB2 已恢復。 相較于先前的執行 (在7.4 版之前) ，有兩個安裝程式套件，但無法並存安裝。 因此，您必須根據您擁有的連線元件，選擇最適當的版本。 如果可能的話，最好使用64位版本。

## <a name="ssma-v76"></a>SSMA v 7。6

SSMA for DB2 的 v 7.6 版本已透過改善品質和轉換度量的目標修正來增強，並支援 SQL Server 2017 (公開預覽) 。 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，不應該用於生產環境的遷移。

## <a name="ssma-v75"></a>SSMA v 7。5

SSMA for DB2 的7.5 版已增強許多改良功能，可確保行動不便人士能獲得更高的協助工具。

## <a name="ssma-v74"></a>SSMA 7。4

SSMA for DB2 的7.4 版包含下列變更：

* **查詢超時** 選項現在可在來源和目標的架構物件探索期間使用。

  ![query timeout 選項](../media/query-timeout_red.png)

* 根據客戶的意見反應，已改善目標修正的品質和轉換度量。

  > [!IMPORTANT]
  > .NET 4.5.2 是安裝 SSMA 7.4 的先決條件。 此外，從7.4 版開始，32位版本的 SSMA 已中止。

## <a name="ssma-v73"></a>SSMA v 7。3

SSMA for DB2 的7.3 版包含下列變更：

* 根據客戶的意見反應，以目標修正改善品質和轉換度量。
* 透過下列專案公開的延伸架構 SSMA：
  * 將功能匯出至 SQL Server Data Tools (SSDT) 專案。
    * 您現在可以將架構腳本從 SSMA 匯出至 SSDT 專案。 您可以使用架構腳本進行額外的架構變更，並部署您的資料庫。

      ![另存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  * SSMA 可使用的程式庫，以執行自訂轉換。
    * 您現在可以建立程式碼，該程式碼可以處理 SSMA 先前未處理的自訂語法轉換和轉換。
      * 您可以在這篇 blog 文章中找到如何建立自訂轉換器的指示， [擴充 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 從這 [篇 blog 文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)下載範例專案以進行轉換。

## <a name="ssma-v72"></a>SSMA 7.2 版

SSMA for DB2 的7.2 版包含下列變更：

* 根據客戶的意見反應，以目標修正改善品質和轉換度量。
* 遙測增強功能，可提供更好的資料點來對客戶問題進行疑難排解，並改善 SSMA 的轉換率。

## <a name="ssma-v71"></a>SSMA 7。1

SSMA for DB2 的7.1 版包含下列變更：

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援遷移的目標平臺。 這項功能在 technical preview 中，可讓您以 SQL server 為目標來進行架構和資料移動。
* 支援自動更新，以便在最新版的 SSMA 可供使用時立即下載。
* SSMA 可安裝的二進位檔現在會透過 Windows Installer 套件檔案傳遞 ( .msi) 。

## <a name="may-2016"></a>2016 年 5 月

SSMA for DB2 2016 版的版包含下列變更：

* 已新增 SQL Server 2016 的支援。
* 新增 DB2 記憶體中和一般資料表的轉換，以 SQL Server 記憶體內部和 hekaton 功能。
* 已將 DB2 存取控制的轉換新增至 SQL Server 的原則物件 (資料列層級安全性 for DB2) 。
* 已將 DB2 系統版本設定資料表的轉換新增至 SQL Server 時態表。
* 改進 DB2 剖析器和解析程式。
* 已移除 .NET 2.0 的安裝程式檢查。
* 已 \* 從 Db2 安裝程式移除不必要的 .dll。
* Fixed `save-project` 和 `open-project` SSMA 主控台的命令。
* 已修正 `securepassword` SSMA 主控台的命令。
* 修正初始載入的物件計數。
* 修正全域設定中的 bug。
  
## <a name="march-2016"></a>2016 年 3 月

SSMA for DB2 的2016年3月預覽版本新增了遷移至 SQL Server 2016 的支援。

## <a name="january-2016"></a>2016 年 1 月

SSMA for DB2 的2016年1月維護版本包含下列變更：
  
* 已新增一些標準函式的支援。
* 已修正 DB2 剖析器錯誤。
* 已修正 (RFC 5690920) 的 DB2 v9 zOS 支援。
* 修正轉換期間的 DB2 未解析識別碼錯誤。
* 將 View Log 功能表項目新增至 SSMA (RFC 5706203) 。
* 已新增遙測。
  
## <a name="november-2014"></a>November 2014

SSMA for DB2 的2014年11月版本是初始發行版本。
