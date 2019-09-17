---
title: SSMA for DB2 的新功能（DB2ToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/06/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 118cb0430a7db1afc2a7537fb19c24b22dc6dd1f
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2019
ms.locfileid: "70745373"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>SSMA for DB2 的新功能（DB2ToSQL）

本文列出每個版本中 DB2 變更的 SQL Server 移轉小幫手（SSMA）。

## <a name="ssma-v84"></a>SSMA v 8。4

SSMA for DB2 的 v2.0 版本已使用目標修正來增強，其設計目的是為了解決協助工具問題，並修正與最大索引資料行（允許32，而不是16）有關 SQL Server 2016 和更新版本的錯誤。

> [!IMPORTANT]
> 在 SSMA 7.4 和更新版本中，.Net 4.5.2 是必要的安裝。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for DB2 的 v 8.3 版本已透過專為改善品質和轉換計量而設計的目標修正來增強。 此外，這一版的 SSMA for DB2 提供了下列修正：

* 解決協助工具問題
* 在 SQL Server 中新增 ' hierarchyid ' 類型的基本支援
* 以 RTRIM/LTRIM 取代 z/OS 探索查詢中的 TRIM 函數使用方式
* 允許使用者在以「標準模式」（預設為 NullID）連接時指定封裝集合
* 將 CREATE TABLE 的轉換新增為 SELECT
* 改善全域臨時表的轉換
* 解決物件唯一性檢查順序的問題，以根據條件約束來設定資料表的優先順序（如果名稱衝突）
* 解決針對 z/OS 的日期和時間戳記載入預設資料行值的問題
* 支援 Unicode 換行字元（也稱為 NEL）
* 解決具有遺漏 RETURN TO 子句的資料指標轉換問題
* 新增標籤和 GOTO 的支援

## <a name="ssma-v82"></a>SSMA v8.2

SSMA for DB2 的8.2 版已增強，可解決從 SSMA 主控台工具 Azure SQL Database 連線的問題，並在轉換期間遺漏 views 宣告中的 COUNT_BIG 資料行。 此外，此版本還包含一組目標的修正程式，其設計目的是要改善品質和轉換計量，以及的修正：

* 資料移轉後停用非叢集索引的問題。
* 在無訊息安裝期間偵測 .NET Framework。
* 下載新版本時，會發生間歇性損毀。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA 8.1 到 v4.0 的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA v8.1

SSMA for DB2 的8.1 版已增強，可提供專為改善品質和轉換計量而設計的目標修正程式。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v4.0 到8.1 版的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA v8.0

SSMA for DB2 的8.0 版已增強，可提供設計來改善品質和轉換計量的目標修正程式。 此版本也提供下列新功能：

* 支援做為目標**Azure SQL Database 受控執行個體**。 您現在可以建立以 Azure SQL Database 受控執行個體為目標的新專案：

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後的**修正建議程式**。 [在這裡](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)深入瞭解。

* 初步的資料庫/架構選擇。

  當連接到來源時，使用者現在可以選取想要的資料庫/架構。 只選取您打算遷移的架構，會在初始連接期間節省時間，並改善整體 SSMA 效能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

SSMA for DB2 的 v 7.10 版本包含下列變更：

* 專為提供額外的安全性和隱私權保護而設計的目標修正，以符合全球需求的變更。
* 開始-結束區塊轉換的修正。

## <a name="ssma-v79"></a>SSMA v7.9

SSMA for DB2 的 v 7.9 版本包含下列變更：

* 改善品質和轉換計量的目標修正程式。
* 支援 SSMA 命令列來改變資料類型對應和專案喜好設定。
* 支援使用 SQL Server Integration Services （SSIS）來遷移資料。 轉換架構之後，您可以使用滑鼠右鍵內容功能表選項來建立 SSIS 封裝。
* SSMA 中的 [Azure SQL Database 連接] 對話方塊也已更改為指定完整的伺服器名稱。 在舊版的 SSMA 中，必須在專案設定中明確提及 Azure SQL Database 前置詞。

## <a name="ssma-v78"></a>SSMA v7.8

SSMA for DB2 的7.8 版本包含下列變更：

* 變更 [專案設定] 中反白顯示的類型對應。
* 使用者停用遙測的能力。

## <a name="ssma-v77"></a>SSMA v7.7

SSMA for DB2 的7.7 版包含下列變更：

* 改善品質和轉換計量的目標修正程式。
* 根據受歡迎的需求，32位版本的 SSMA for DB2 已恢復。 相較于先前的執行（在 v4.0 之前），有兩個安裝程式套件，但無法並存安裝。 因此，您必須根據您擁有的連線元件來選擇最適當的版本。 最好是盡可能使用64位版本。

## <a name="ssma-v76"></a>SSMA v7.6

SSMA for DB2 的7.6 版已藉由改善品質和轉換計量，以及支援 SQL Server 2017 （公開預覽）的目標修正來增強。 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，不應用於生產環境遷移。

## <a name="ssma-v75"></a>SSMA v7.5

SSMA for DB2 的7.5 版已增強了數項改良功能，可確保殘障人士更能使用。

## <a name="ssma-v74"></a>SSMA v7.4

SSMA for DB2 的7.4 版包含下列變更：

* 在來源和目標的架構物件探索期間，現在可以使用 [**查詢超時**] 選項。

  ![查詢超時選項](../media/query-timeout_red.png)

* 品質和轉換度量已根據客戶的意見反應，以目標修正進行改善。

  > [!IMPORTANT]
  > .Net 4.5.2 是安裝 SSMA 7.4 的必要條件。 此外，從7.4 版開始，已停止32位版本的 SSMA。

## <a name="ssma-v73"></a>SSMA v7.3

SSMA for DB2 的7.3 版包含下列變更：

* 改善品質和轉換計量，並根據客戶的意見反應進行目標修正。
* 透過下列專案公開的 SSMA 擴充性架構：
  * 將功能匯出至 SQL Server Data Tools （SSDT）專案。
    * 您現在可以將架構腳本從 SSMA 匯出至 SSDT 專案。 您可以使用架構腳本來進行其他架構變更，並部署您的資料庫。

      ![另存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  * 可供 SSMA 用來執行自訂轉換的程式庫。
    * 您現在可以建立可處理自訂語法轉換的程式碼，以及 SSMA 先前未處理的轉換。
      * 如需如何建立自訂轉換器的指示，請前往此 blog 文章，[延伸 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 下載範例專案，以便從這[篇 blog 文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)進行轉換。

## <a name="ssma-v72"></a>SSMA v7.2

SSMA for DB2 的7.2 版包含下列變更：

* 改善品質和轉換計量，並根據客戶的意見反應進行目標修正。
* 遙測增強功能，可提供更好的資料點來疑難排解客戶問題，並改善 SSMA 的轉換率。

## <a name="ssma-v71"></a>SSMA v7.1

SSMA for DB2 的7.1 版包含下列變更：

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援的目標平臺，可進行遷移。 這項功能在 technical preview 中，可讓您以 SQL server 為目標來進行架構和資料移動。
* 支援自動更新，以在最新版本的 SSMA 可用時立即下載。
* SSMA 可安裝的二進位檔現在會透過 Windows installer 封裝檔案（.msi）傳遞。

## <a name="may-2016"></a>5月2016

SSMA for DB2 的2016年5月版本包含下列變更：  

* 已新增 SQL Server 2016 的支援。
* 新增 DB2 記憶體內部和一般資料表的轉換，以 SQL Server 記憶體內部和 hekaton 功能。
* 已將 DB2 存取控制的轉換新增至 SQL Server 原則物件（適用于 DB2 的資料列層級安全性）。
* 已將 DB2 系統設定版本的資料表轉換成 SQL Server 時態表。
* 改良的 DB2 剖析器和解析程式。
* 已移除 .Net 2.0 的安裝程式檢查。
* 已從 Db2 安裝程式移除不必要的 * .dll。
* 已修正 SSMA 主控台的 [儲存專案] 和 [開啟專案] 命令。
* 已修正 SSMA 主控台的 "securepassword" 命令。
* 已修正初始載入物件的計數。
* 已修正全域設定中的 bug。
  
## <a name="march-2016"></a>2016年3月

SSMA for DB2 的2016年3月預覽版本將支援遷移至 SQL Server 2016。

## <a name="january-2016"></a>2016年1月

SSMA for DB2 的2016年1月維護版本包含下列變更：  
  
* 已新增許多標準函式的支援。  
* 已修正 DB2 剖析器錯誤。  
* 已修正 DB2 v9 zOS 支援（RFC 5690920）。  
* 已修正在轉換期間無法解析的 DB2 未解決識別碼錯誤。  
* 已將 [查看記錄] 功能表項目新增至 SSMA （RFC 5706203）。  
* 已新增遙測。
  
## <a name="november-2014"></a>2014年11月

2014年11月版本的 SSMA for DB2 是初始版本。
