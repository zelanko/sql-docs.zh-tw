---
title: SSMA for MySQL 的新功能 (MySQLToSql) |Microsoft Docs
description: 瞭解適用于 MySQL 的 SQL Server 移轉小幫手 (SSMA) 的變更 (每個版本的 MySQLToSQL) 。
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 9/28/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
ms.author: alexiva
ms.openlocfilehash: 75a82f8f87997dfa028a5e0b1ee7bae73c3913e6
ms.sourcegitcommit: b93beb4f03aee2c1971909cb1d15f79cd479a35c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/29/2020
ms.locfileid: "91497881"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>SSMA for MySQL 的新功能 (MySqlToSql)

本文列出在每個版本中，適用于 MySQL 變更的 SQL Server 移轉小幫手 (SSMA) 。

## <a name="ssma-v814"></a>SSMA v 8.14

除了許多改進以確保殘障人士能獲得更高的協助工具，8.14 版的 SSMA for MySQL 需要專案升級，因為它現在會在專案中繼資料中儲存完整的來源/目標伺服器版本。

## <a name="ssma-v813"></a>SSMA v 8.13

適用于 MySQL 的 SSMA v 8.13 版本包含下列變更：

* 轉換程式和函式呼叫時，請考慮隱含類型轉換
* 改善來源連接字串的記錄，以協助疑難排解連接問題

## <a name="ssma-v812"></a>SSMA v 8.12

適用于 MySQL 的 SSMA v 8.12 版本包含下列變更：

* 臨時表 DDL 的轉換

## <a name="ssma-v811"></a>SSMA v 8.11

適用于 MySQL 的 SSMA v 8.11 版本包含下列變更：

* 使用 MSAL.NET 程式庫進行互動式 Azure Active Directory 驗證

## <a name="ssma-v810"></a>SSMA v 8.10

SSMA for MySQL 的 v1.1 版本包含次要效能改進和 bug 修正。

## <a name="ssma-v89"></a>SSMA v 8。9

SSMA for MySQL 的8.9 版包含下列變更：

* 針對空間類型的資料移轉進行修正
* 修正專案名稱中特殊字元的問題

## <a name="ssma-v88"></a>SSMA v 8。8

適用于 MySQL 的 SSMA 8.8 版包含：

* SQL Server 物件同步處理穩定性改進
* 評估和轉換期間的 GUI 效能改進

## <a name="ssma-v87"></a>SSMA v 8。7

SSMA for MySQL 的 v 8.7 版本在圖形化使用者介面中有輕微的修正和效能改進。

此外，適用于 MySQL 的 SSMA 現在會 `LIMIT` 在以 AZURE SQL 為目標時，提供子句的轉換。

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v86"></a>SSMA v 8。6

除了針對改善可用性和效能而設計的一組目標修正之外，還新增了一個可讓使用者在轉換的程式碼中省略 SSMA 擴充屬性的設定，藉此增強 SSMA for MySQL 的 v 8.6 版本。

若要利用這項設定，請在 SSMA for MySQL 中流覽至 [**工具**  >  **專案設定**  >  **一般**  >  **轉換**]，然後在 [**其他**] 下，將 [**省略擴充屬性**] 設定的值更新為 **[是]**。

![省略擴充屬性設定](../mysql/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v85"></a>SSMA v 8。5

SSMA for MySQL 的8.5 版已增強，可支援 SQL server 中的 Azure Active Directory authentication 和 JSON 功能的基本支援，以及針對改善可用性和效能而設計的一組目標修正。

> [!IMPORTANT]
> 使用 SSMA v 8.5 時，.NET 4.7.2 是必要的安裝程式。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v84"></a>SSMA v 8。4

SSMA for MySQL 的8.4 版已利用專為解決協助工具問題而設計的目標修正程式，修正了與 max index columns 相關的錯誤， (為 SQL Server 2016 和更新版本提供32而非 16) 。

> [!IMPORTANT]
> 使用 SSMA 版本7.4 至8.4，.NET 4.5.2 是必要條件的安裝。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for MySQL 的 v 8.3 發行版本已透過專為改善品質和轉換度量而設計的目標修正來增強。 此外，此版本的 MySQL SSMA 提供下列修正：

* 解決協助工具問題。
* `hierarchyid`在 SQL Server 中加入類型的基本支援。

## <a name="ssma-v82"></a>SSMA v 8。2

SSMA for MySQL 的8.2 版已透過一組目標修正來增強，其設計目的是要改善品質和轉換度量，以及下列各項的修正：

* 資料移轉後停用非叢集索引的問題。
* 無訊息安裝期間的 .NET Framework 偵測。
* 下載新版本時所發生的間歇性損毀。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v4.0 至8.2 版的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA v 8。1

SSMA for MySQL 的8.1 版已透過專為改善品質和轉換度量而設計的目標修正來增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA 8.0 版更新為 v4.0 的失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA 8.0 版

適用于 MySQL 的 SSMA 8.0 版已利用專為改善品質和轉換度量而設計的目標修正來增強。 此版本也提供下列新功能：

* 支援以 **AZURE SQL 受控執行個體** 作為目標。 您現在可以建立以 Azure SQL 受控執行個體為目標的新專案：

  ![SQL MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後的 **修正程式**。 若要深入瞭解[，請參閱。](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 初步的資料庫/架構選取。

  連接到來源時，使用者現在可以選取想要的資料庫/架構。 只選取您打算遷移的架構，可在初始連接期間節省時間，並改善整體 SSMA 效能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

SSMA for MySQL 的 v 7.10 版本包含下列變更：

* 目標修正程式旨在提供額外的安全性和隱私權保護，以符合全球需求的變更。
* 在函數名稱和引數清單之間轉換空格的修正程式。

## <a name="ssma-v79"></a>SSMA v 7。9

SSMA for MySQL 的 v 7.9 版本包含下列變更：

* 改善品質和轉換度量的目標修正。
* 從 MySQL 將空間資料類型遷移至 Azure SQL Database 的部分支援。
* 支援 SSMA 命令列來改變資料類型對應和專案喜好設定。
* 支援使用 SQL Server Integration Services (SSIS) 來遷移資料。 轉換架構之後，您可以使用滑鼠右鍵內容功能表選項來建立 SSIS 封裝。
* SSMA 中的 [Azure SQL Database 連接] 對話方塊也已經改變，以指定完整的伺服器名稱。 在舊版 SSMA 中，必須在專案設定內明確提及 Azure SQL Database 前置詞。

## <a name="ssma-v78"></a>SSMA v 7。8

適用于 MySQL 的 SSMA 7.8 版包含下列變更：

* 在 [專案設定] 中反白顯示變更類型對應。
* 使用者停用遙測的能力。

## <a name="ssma-v77"></a>SSMA 7。7

SSMA for MySQL 的7.7 版包含下列變更：

* 適用于 MySQL 的 SSMA 已透過可改善品質和轉換度量的目標修正來增強。
* 根據熱門需求，適用于 MySQL 的32位版本 SSMA 已恢復。 相較于前一次的執行 (在 7.4) 之前，有兩個安裝程式套件，但無法並存安裝。 因此，您必須根據您擁有的連線元件，選擇最適當的版本。 如果可能的話，最好使用64位版本。
* SSMA for MySQL 現在具有 ODBC 連接字串連接模式，可讓您使用與 MySQL 相容的任何協力廠商 ODBC 驅動程式。

## <a name="ssma-v76"></a>SSMA v 7。6

SSMA for MySQL 的 v 7.6 版本已透過改善品質和轉換計量，並支援 SQL Server 2017 (公開預覽) 的目標修正來增強。 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，不應該用於生產環境的遷移。

## <a name="ssma-v75"></a>SSMA v 7。5

SSMA for MySQL 的7.5 版已增強許多改良功能，可確保更適合殘障人士使用的協助工具。

## <a name="ssma-v74"></a>SSMA 7。4

SSMA for MySQL 的7.4 版包含下列變更：

* **查詢超時**選項現在可在來源和目標的架構物件探索期間使用。

    ![query timeout 選項](../media/query-timeout_red.png)
* 根據客戶的意見反應，已改善目標修正的品質和轉換度量。

> [!IMPORTANT]
> .NET 4.5.2 是安裝 SSMA 7.4 的先決條件。 此外，從 v4.0 開始，32位版本的 SSMA 將會中止。

## <a name="ssma-v73"></a>SSMA v 7。3

SSMA for MySQL 的7.3 版包含下列變更：

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

SSMA for MySQL 的7.2 版包含下列變更：

* 根據客戶的意見反應，以目標修正改善品質和轉換度量。
* 遙測增強功能，可提供更好的資料點來對客戶問題進行疑難排解，並改善 SSMA 的轉換率。

## <a name="ssma-v71"></a>SSMA 7。1

SSMA for MySQL 的7.1 版包含下列變更：

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援遷移的目標平臺。 這項功能在 technical preview 中，可讓您以 SQL server 為目標來進行架構和資料移動。
* SSMA 現在支援自動更新，以在最新版本的 SSMA 可用時立即下載。
* SSMA 可安裝的二進位檔現在會透過 Windows Installer 套件檔案傳遞 ( .msi) 。

## <a name="may-2016"></a>2016 年 5 月

SSMA for MySQL 的2016版可能包含下列變更：

* 已新增 SQL Server 2016 的支援。
* 改良的剖析器和解析程式。
* 已移除 .NET 2.0 的安裝程式檢查。
* 已將延伸模組套件相依性從 .NET 3.5 更新為 .NET 4.0。
* 修正 MySql 的預設 BigInt 類型對應。
* Fixed `save-project` 和 `open-project` SSMA 主控台的命令。
* 已修正 `securepassword` SSMA 主控台的命令。
* 修正初始載入的物件計數。
* 已修正載入 MsSql 物件。
* 修正全域設定中的 bug。

## <a name="march-2016"></a>2016 年 3 月

SSMA for MySQL 的2016年3月預覽版本新增了遷移至 SQL Server 2016 的支援。
  
## <a name="january-2016"></a>2016 年 1 月

SSMA for MySQL 的2016年1月維護版本包含下列變更：

* 將 View Log 功能表項目新增至 SSMA (RFC 5706203) 。
* 已新增遙測。
  
## <a name="july-2014"></a>2014 年 7 月

SSMA for MySQL 的2014年7月版本包含下列變更：
  
* 改良的 Azure SQL Database 程式碼轉換。
* 擴充功能套件功能已移至架構，以支援 Azure SQL Database。
* 效能改進已針對具有超過10k 個物件的資料庫進行測試。
* 處理大量物件的 UI 改進。
* 醒目提示已知的 LOB 架構 (因此可以在轉換) 中忽略。
* 轉換速度改進。
* 在 UI 中顯示物件計數。
* 減少超過25% 的報表大小。
* 已改善未剖析之結構的錯誤訊息。
  
## <a name="april-2014"></a>2014 年 4 月

SSMA for MySQL 2014 年4月版本包含下列變更：
  
* 已新增 SQL Server 2014 的支援。
* 已修正有關轉換至 Azure 的 bug。
* 修正 IE 10 中有關不可見報表頁面的錯誤。
  
## <a name="july-2011"></a>2011 年 7 月

SSMA for MySQL 的2011年7月版本包含下列變更：
  
* 的轉換支援 `LIMIT` [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] `OFFSET` 。
* 改進資料移轉期間的錯誤報表。
  
## <a name="april-2011"></a>2011年4月

SSMA for MySQL 2011 年4月版本包含下列變更：
  
* 單一安裝「適用于 MySQL 的 SSMA」，可 [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] 支援 [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] 、 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 和 Azure SQL。
* 連接的能力 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 。
* 增強的用戶端資料移轉引擎，支援平行的資料移轉。
* 使用簡單和大量記錄復原模式來改善資料移轉效能。
* 適用于 MySQL 的 SSMA 主控台版本支援回溯相容性。 您可以開啟之前版本所建立的專案至 SSMA v 5.0。
* SSMA for MySQL 5.0 版產品可以與舊版 SSMA 產品並存安裝 (SxS) 。
  
## <a name="july-2010"></a>2010 年 7 月

SSMA for MySQL 的2010年7月版本包含下列功能：
  
**1. 消費者介面的改良功能：**

* MySQL 資料庫物件的 [SQL 模式] 索引標籤
* MySQL 資料庫物件的 [設定] 索引標籤
* MySQL 資料表的 [資料] 索引標籤
* 已更新轉換和遷移頁面中的專案設定
* 資料表層級的「資料移轉設定」
  
**2. 連接至 MySQL 和 SQL Server 的改良功能：**
  
* MySQL 中的 SSL 連線能力
* SQL Server 中的加密連接
  
**3. MySQL 元資料庫 Explorer 的改良功能：**
  
* 載入所有 MySQL 資料庫物件及其各自的索引標籤。
  
**4. 物件轉換的增強功能：**
  
* MySQL 元資料庫物件的轉換-程式、函數、視圖、觸發程式和語句。
* 對資料表中空間資料類型的有限支援。
* 將 MySQL 函數轉換成 SQL Server 預存程式的選項
* 在物件轉換期間套用 SQL 模式和字元集對應的選項
  
**5. 資料移轉的增強功能：**  
  
* 支援使用伺服器端和用戶端資料移轉引擎進行資料移轉
* 支援空間資料遷移
* 資料表的資料移轉自訂 SQL
  
**6. 適用于 MySQL 的 SSMA 主控台：**  
  
* 適用于 MySQL 的 SSMA 支援主控台功能  
* 支援腳本層級介面  
  
## <a name="january-2010"></a>2010年1月

SSMA for MySQL 的2010年1月版本是首次發行版本。 它包含下列功能：
  
* 已新增在內部部署 SQL Server 和 Azure SQL 中遷移的支援。  
  
* **功能快照：** MySQL 資料表/索引/條件約束的架構和資料移轉。
