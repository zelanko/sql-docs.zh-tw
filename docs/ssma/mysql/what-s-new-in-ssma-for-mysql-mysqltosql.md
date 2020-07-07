---
title: SSMA for MySQL 的新功能（MySQLToSql） |Microsoft Docs
description: 瞭解每個版本的 SQL Server 移轉小幫手（SSMA） for MySQL （MySQLToSQL）的變更。
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 7/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
ms.author: alexiva
ms.openlocfilehash: 1c0292d05624e2d3cb8640d719fc2c0e29474cb0
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000374"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>SSMA for MySQL 的新功能 (MySqlToSql)

本文列出每個版本中 MySQL 變更的 SQL Server 移轉小幫手（SSMA）。

## <a name="ssma-v811"></a>SSMA v 8.11

適用于 MySQL 的 SSMA 的 v 8.11 版本包含下列變更：

* 使用 MSAL.NET 程式庫進行互動式 Azure Active Directory 驗證

## <a name="ssma-v810"></a>SSMA v 8.10

適用于 MySQL 的 SSMA 的 v2.0 版本包含次要效能改進和 bug 修正。

## <a name="ssma-v89"></a>SSMA v 8。9

SSMA for MySQL 的8.9 版本包含下列變更：

* 空間類型資料移轉的修正
* 修正專案名稱中特殊字元的問題

## <a name="ssma-v88"></a>SSMA v 8。8

SSMA for MySQL 的 v3.0 版本包括：

* SQL Server 物件同步處理穩定性改善
* 在評定和轉換期間的 GUI 效能改進

## <a name="ssma-v87"></a>SSMA v 8。7

適用于 MySQL 的 SSMA 的8.7 版在圖形化使用者介面中有次要的修正和效能改進。

此外，SSMA for MySQL 現在會 `LIMIT` 在以 AZURE SQL 為目標時，提供子句的轉換。

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝此版本，您可以從[這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v86"></a>SSMA v 8。6

除了為了改善可用性和效能而設計的一組目標修正程式之外，新增可讓使用者在轉換後的程式碼中省略 SSMA 擴充屬性的設定，以增強 SSMA for MySQL 的 v 8.6 版本。

若要利用這項設定，請在 SSMA for MySQL 中流覽至 [**工具]**  >  [**專案設定**]  >  **[一般**  >  **轉換**]，然後在 [**其他**] 下將 [**省略擴充屬性**] 設定的值更新為 **[是]**。

![省略擴充屬性設定](../mysql/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝此版本，您可以從[這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v85"></a>SSMA v 8。5

SSMA for MySQL 的第8.5 版已增強，並支援 SQL server 中的 Azure Active Directory 驗證和 JSON 功能的基本支援，以及一組專為改善可用性和效能而設計的目標修正程式。

> [!IMPORTANT]
> 使用 SSMA v 8.5 時，.NET 4.7.2 是必要的安裝。 如果您需要安裝此版本，您可以從[這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v84"></a>SSMA v 8。4

SSMA for MySQL 的 v2.0 版本已透過專為處理協助工具問題而設計的目標修正來增強，並修正適用于 SQL Server 2016 和更新版本的最大索引資料行（允許32，而不是16）的相關錯誤。

> [!IMPORTANT]
> 透過8.4 的 SSMA 版本7.4，.NET 4.5.2 是必要的安裝。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for MySQL 的 v 8.3 版本已透過專為改善品質和轉換計量而設計的目標修正來增強。 此外，這一版的 SSMA for MySQL 提供了下列修正：

* 解決協助工具問題。
* `hierarchyid`在 SQL Server 中新增類型的基本支援。

## <a name="ssma-v82"></a>SSMA 8。2

SSMA for MySQL 的 v4.0 版本已透過一組目標修正來增強，其設計目的是要改善品質和轉換計量，以及的修正：

* 在資料移轉後停用非叢集索引的問題。
* 在無訊息安裝期間偵測 .NET Framework。
* 下載新版本時，會發生間歇性損毀。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA 8.1 到 v4.0 的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA 8。1

SSMA for MySQL 的8.1 版已透過專為改善品質和轉換計量而設計的目標修正來增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v4.0 到8.1 版的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA v 8。0

SSMA for MySQL 的8.0 版已透過專為改善品質和轉換計量而設計的目標修正來增強。 此版本也提供下列新功能：

* 支援做為目標**Azure SQL Database 受控執行個體**。 您現在可以建立以 Azure SQL Database 受控執行個體為目標的新專案：

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後的**修正建議程式**。 [在這裡](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)深入瞭解。

* 初步的資料庫/架構選擇。

  當連接到來源時，使用者現在可以選取想要的資料庫/架構。 只選取您打算遷移的架構，會在初始連接期間節省時間，並改善整體 SSMA 效能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

適用于 MySQL 的 SSMA 的：7.10 版本包含下列變更：

* 專為提供額外的安全性和隱私權保護而設計的目標修正，以符合全球需求的變更。
* 函數名稱和引數清單之間的空格轉換的修正。

## <a name="ssma-v79"></a>SSMA v 7。9

適用于 MySQL 的 SSMA 的 v 7.9 版本包含下列變更：

* 改善品質和轉換計量的目標修正程式。
* 將空間資料類型從 MySQL 遷移至 Azure SQL Database 的部分支援。
* 支援 SSMA 命令列來改變資料類型對應和專案喜好設定。
* 支援使用 SQL Server Integration Services （SSIS）來遷移資料。 轉換架構之後，您可以使用滑鼠右鍵內容功能表選項來建立 SSIS 封裝。
* SSMA 中的 [Azure SQL Database 連接] 對話方塊也已更改為指定完整的伺服器名稱。 在舊版的 SSMA 中，必須在專案設定中明確提及 Azure SQL Database 前置詞。

## <a name="ssma-v78"></a>SSMA 7.8 版

適用于 MySQL 的 SSMA 7.8 版包含下列變更：

* 變更 [專案設定] 中反白顯示的類型對應。
* 使用者停用遙測的能力。

## <a name="ssma-v77"></a>SSMA 7。7

SSMA for MySQL 的7.7 版包含下列變更：

* 適用于 MySQL 的 SSMA 已透過改善品質和轉換計量的目標修正來加強。
* 根據常用的需求，適用于 MySQL 的32位版本 SSMA 已恢復。 相較于先前的執行（在7.4 之前），有兩個安裝程式套件，但無法並存安裝。 因此，您必須根據您擁有的連線元件來選擇最適當的版本。 最好是盡可能使用64位版本。
* 適用于 MySQL 的 SSMA 現在具有 ODBC 連接字串連接模式，可讓您使用與 MySQL 相容的任何協力廠商 ODBC 驅動程式。

## <a name="ssma-v76"></a>SSMA v 7。6

SSMA for MySQL 的7.6 版已藉由改善品質和轉換計量，以及支援 SQL Server 2017 （公開預覽）的目標修正來增強。 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，不應用於生產環境遷移。

## <a name="ssma-v75"></a>SSMA v 7。5

SSMA for MySQL 的7.5 版已增強數項改良功能，以確保更方便殘障人士使用。

## <a name="ssma-v74"></a>SSMA 7。4

SSMA for MySQL 的7.4 版包含下列變更：

* 在來源和目標的架構物件探索期間，現在可以使用 [**查詢超時**] 選項。

    ![查詢超時選項](../media/query-timeout_red.png)
* 品質和轉換度量已根據客戶的意見反應，以目標修正進行改善。

> [!IMPORTANT]
> .NET 4.5.2 是安裝 SSMA 7.4 的必要條件。 此外，從7.4 開始，32位版本的 SSMA 即將中止。

## <a name="ssma-v73"></a>SSMA 7.3 版

SSMA for MySQL 的7.3 版包含下列變更：

* 改善品質和轉換計量，並根據客戶的意見反應進行目標修正。
* 透過下列專案公開的 SSMA 擴充性架構：
  * 將功能匯出至 SQL Server Data Tools （SSDT）專案。
    * 您現在可以將架構腳本從 SSMA 匯出至 SSDT 專案。 您可以使用架構腳本來進行其他架構變更，並部署您的資料庫。

      ![另存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  * 可供 SSMA 用來執行自訂轉換的程式庫。
    * 您現在可以建立可處理自訂語法轉換的程式碼，以及 SSMA 先前未處理的轉換。
      * 如需如何建立自訂轉換器的指示，請前往此 blog 文章，[延伸 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 下載範例專案，以便從這[篇 blog 文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)進行轉換。

## <a name="ssma-v72"></a>SSMA 7.2 版

適用于 MySQL 的 SSMA 7.2 版包含下列變更：

* 改善品質和轉換計量，並根據客戶的意見反應進行目標修正。
* 遙測增強功能，可提供更好的資料點來疑難排解客戶問題，並改善 SSMA 的轉換率。

## <a name="ssma-v71"></a>SSMA 7。1

適用于 MySQL 的 SSMA 7.1 版包含下列變更：

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援的目標平臺，可進行遷移。 這項功能在 technical preview 中，可讓您以 SQL server 為目標來進行架構和資料移動。
* SSMA 現在支援自動更新，以在最新版本的 SSMA 推出時立即下載。
* SSMA 可安裝的二進位檔現在會透過 Windows Installer 套件檔案（.msi）傳遞。

## <a name="may-2016"></a>2016 年 5 月

適用于 MySQL 的 SSMA 2016 年5月版本包含下列變更：

* 已新增 SQL Server 2016 的支援。
* 改良的剖析器和解析程式。
* 已移除 .NET 2.0 的安裝程式檢查。
* 已將延伸模組套件相依性從 .NET 3.5 更新為 .NET 4.0。
* 已修正 MySql 的預設 BigInt 類型對應。
* 已 `save-project` 修正 `open-project` SSMA 主控台的命令。
* 已修正 `securepassword` SSMA 主控台的命令。
* 已修正初始載入物件的計數。
* 已修正 MsSql 物件載入。
* 已修正全域設定中的 bug。

## <a name="march-2016"></a>2016 年 3 月

SSMA for MySQL 的2016年3月預覽版本新增了遷移至 SQL Server 2016 的支援。
  
## <a name="january-2016"></a>2016 年 1 月

適用于 MySQL 的 SSMA 2016 年1月維護版本包含下列變更：

* 已將 [查看記錄] 功能表項目新增至 SSMA （RFC 5706203）。
* 已新增遙測。
  
## <a name="july-2014"></a>2014 年 7 月

2014年7月版的 SSMA for MySQL 包含下列變更：
  
* 改良的 Azure SQL DB 程式碼轉換。
* 延伸模組套件功能已移至架構，以支援 Azure SQL DB。
* 已針對具有超過10k 物件的資料庫測試效能改進。
* 處理大量物件的 UI 改善。
* 反白顯示知名的 LOB 架構（因此可以在轉換時忽略）。
* 轉換速度改進。
* 在 UI 中顯示物件計數。
* 超過25% 的報表大小縮減。
* 已改善未分析之結構的錯誤訊息。
  
## <a name="april-2014"></a>2014 年 4 月

2014年4月版的 SSMA for MySQL 包含下列變更：
  
* 已新增 SQL Server 2014 的支援。
* 已修正關於轉換至 Azure 的 bug。
* 已修正 IE 10 中不可見報表頁面的相關 bug。
  
## <a name="july-2011"></a>2011 年 7 月

2011年7月版的 SSMA for MySQL 包含下列變更：
  
* 支援 `LIMIT` 將轉換成 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] `OFFSET` 。
* 改善資料移轉期間的錯誤報表。
  
## <a name="april-2011"></a>2011年4月

2011年4月版的 SSMA for MySQL 包含下列變更：
  
* 單一安裝「適用于 MySQL 的 SSMA」，其 [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] 支援 [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] 、 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 和 Azure SQL。
* 連接的能力 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 。
* 加強的用戶端資料移轉引擎，支援資料的平行遷移。
* 使用簡單和大量記錄復原模式來改善資料移轉效能。
* SSMA for MySQL 主控台版本支援回溯相容性。 您可以開啟先前版本所建立的專案，以 SSMA 5.0 版。
* SSMA for MySQL v 5.0 產品可以並存安裝（SxS）與舊版的 SSMA 產品。
  
## <a name="july-2010"></a>2010 年 7 月

2010年7月版的 SSMA for MySQL 包含下列功能：
  
**1. 使用者介面的增強功能：**

* MySQL 資料庫物件的 [SQL 模式] 索引標籤
* MySQL 資料庫物件的 [設定] 索引標籤
* MySQL 資料表的 [資料] 索引標籤
* 已更新轉換和遷移頁面中的專案設定
* 資料表層級的「資料移轉設定」
  
**2. 連接到 MySQL 和 SQL Server 的改良功能：**
  
* MySQL 中的 SSL 連線能力
* SQL Server 中的加密連接
  
**3. MySQL 的 [元資料庫] Explorer 的改良功能：**
  
* 載入所有 MySQL 資料庫物件及其各自的索引標籤。
  
**4. 物件轉換的改良功能：**
  
* MySQL 元資料庫物件的轉換-程式、函數、視圖、觸發程式和語句。
* 針對資料表中的空間資料類型提供有限的支援。
* 將 MySQL 函數轉換成 SQL Server 預存程式的選項
* 在物件轉換期間套用 SQL 模式和字元集對應的選項
  
**5. 資料移轉的改良功能：**  
  
* 支援使用伺服器端和用戶端資料移轉引擎來進行資料移轉
* 支援空間資料遷移
* 資料表的資料移轉自訂 SQL
  
**6. 適用于 MySQL 的 SSMA 主控台：**  
  
* 適用于 MySQL 的 SSMA 支援主控台功能  
* 腳本層級介面的支援  
  
## <a name="january-2010"></a>2010年1月

2010年1月版的 SSMA for MySQL 是最初發行版本。 其中包含下列功能：
  
* 已新增遷移至內部部署 SQL Server 和 Azure SQL 的支援。  
  
* **功能快照集：** MySQL 資料表/索引/條件約束的架構和資料移轉。
