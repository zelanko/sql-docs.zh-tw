---
title: SSMA 中 MySQL (MySQLSql) 的新增功能 |微軟文件
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
ms.author: jtoland;alexiva
ms.openlocfilehash: 9d5c33bbb9e09a5a833c928547a5ec659fe43c96
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625554"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>SSMA for MySQL 的新功能 (MySqlToSql)

本文列出了每個版本中 MySQL 更改的 SQL 伺服器遷移助手 (SSMA)。

## <a name="ssma-v88"></a>SSMA v8.8

適用於 MySQL 的 SSMA 的 v8.8 版本包括:

* SQL Server 物件同步穩定性改進
* 評估並轉換期間的 GUI 效能改進

## <a name="ssma-v87"></a>SSMA v8.7

MySQL 的 SSMA v8.7 版本在圖形用戶介面中具有輕微的修復和性能改進。

此外,MySQL 的 SSMA`LIMIT`現在為 面向 Azure SQL 時提供子句的轉換。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v86"></a>SSMA v8.6

除了一組旨在提高可用性和性能的有針對性的修補程式外,MySQL 的 V8.6 版本還通過添加允許使用者在轉換後的代碼中省略 SSMA 擴展屬性的設置進行了增強。

要利用此設定,在 MySQL 的 SSMA 中,導航到**工具** > **專案設置** > **常規** > **轉換**,然後在**Misc**下,將 **「省略擴展屬性**」設置的值更新為 **"是**"。

![省略延伸屬性設定](../mysql/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v85"></a>SSMA v8.5

支援 Azure Active Directory 身份驗證和對 SQL 伺服器中的 JSON 功能的基本支援,以及一組旨在提高可用性和性能的有針對性的修補程式,增強了 MySQL 的 SSMA v8.5 版本。

> [!IMPORTANT]
> 使用 SSMA v8.5 時,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v84"></a>SSMA v8.4

MySQL 的 SSMA v8.4 版本通過有針對性的修補程式進行增強,這些修補程式旨在解決輔助功能問題並修復 SQL Server 2016 和更高版本的最大索引列(允許 32 而不是 16)相關的 Bug。

> [!IMPORTANT]
> 對於 SSMA 版本 7.4 但 8.4,.NET 4.5.2 是安裝的先決條件。

## <a name="ssma-v83"></a>SSMA v8.3

MySQL 的 SSMA v8.3 版本通過旨在提高品質和轉換指標的有針對性的修補程式進行增強。 此外,此版本的 MySQL 的 SSMA 提供了以下修補程式:

* 解決輔助功能問題。
* 添加對`hierarchyid`SQL Server 類型的基本支援。

## <a name="ssma-v82"></a>SSMA v8.2

MySQL 的 SSMA v8.2 版本透過一組旨在提高品質和轉換指標的有針對性的修補程式以及用於以下的修補程式進行增強:

* 數據遷移后禁用的非群集索引的問題。
* 在靜默安裝期間檢測 .NET 框架。
* 下載新版本時發生的間歇性崩潰。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v8.1 到 v8.2 的更新失敗。 如果您遇到此錯誤,請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA v8.1

MySQL 的 SSMA v8.1 版本通過旨在提高品質和轉換指標的有針對性的修補程式進行增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v8.0 到 v8.1 的更新失敗。 如果您遇到此錯誤,請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA v8.0

MySQL 的 SSMA v8.0 版本透過旨在提高品質和轉換指標的有針對性的修補程式進行增強。 此版本還提供以下新功能:

* 支援**Azure SQL 資料庫託管實例**作為目標。 現在,您可以建立針對 Azure SQL 資料庫託管實例的新專案:

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後**修復顧問**。 此處瞭解有關它的更多[。](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 初步資料庫/架構選擇。

  連接到源時,用戶現在可以選擇感興趣的資料庫/架構。 僅選擇計畫遷移的架構將節省時間連接期間的時間,並提高 SSMA 的整體性能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

MySQL 的 SSMA v7.10 版本包含以下變更:

* 旨在提供額外安全和隱私保護以滿足全球需求變化的有針對性的修補程式。
* 函數名稱和參數清單之間空間轉換的修復程式。

## <a name="ssma-v79"></a>SSMA v7.9

MySQL 的 SSMA v7.9 版本包含以下變更:

* 提高品質和轉化指標的針對性修復。
* 部分支援將空間資料類型從 MySQL 遷移到 Azure SQL 資料庫。
* 支援 SSMA 命令列以更改資料類型映射和專案首選項。
* 支援使用 SQL 伺服器整合服務 (SSIS) 遷移資料。 轉換架構後,可以使用右鍵單擊上下文菜單選項創建 SSIS 包。
* SSMA 中的 Azure SQL 資料庫連接對話方塊也已更改,以指定完全限定的伺服器名稱。 在 SSMA 的早期版本中,必須在專案設置中顯式提及 Azure SQL 資料庫前綴。

## <a name="ssma-v78"></a>SSMA v7.8

MySQL 的 SSMA v7.8 版本包含以下變更:

* 更改類型對應在項目設定中突出顯示。
* 使用者禁用遙測功能。

## <a name="ssma-v77"></a>SSMA v7.7

MySQL 的 SSMA v7.7 版本包含以下變更:

* MySQL 的 SSMA 已通過提高品質和轉換指標的針對性修補程序進行了增強。
* 根據大眾需求,MySQL 的 32 位版本的 SSMA 又回來了。 與以前的實現(在 v7.4 之前)相比,有兩個安裝程式包,但不能並排安裝。 因此,您必須根據擁有的連接元件選擇最合適的版本。 如果可能,最好使用 64 位元版本。
* MySQL 的 SSMA 現在具有 ODBC 連接字串連接模式,允許您使用與 MySQL 相容的任何第三方 ODBC 驅動程式。

## <a name="ssma-v76"></a>SSMA v7.6

MySQL 的 SSMA v7.6 版本已通過提高品質和轉換指標的針對性修補程式以及支援 SQL Server 2017(公共預覽)進行了增強。 Windows 和 Linux 上對 SQL Server 2017 的支援處於公共預覽版,不應用於生產遷移。

## <a name="ssma-v75"></a>SSMA v7.5

MySQL SSMA 的 v7.5 版本經過多次改進得到了增強,以確保殘障人士獲得更大的可訪問性。

## <a name="ssma-v74"></a>SSMA v7.4

MySQL 的 SSMA v7.4 版本包含以下變更:

* **查詢超時**選項現在在源和目標架構對象發現期間可用。

    ![查詢逾時選項](../media/query-timeout_red.png)
* 品質和轉化指標已根據客戶反饋通過有針對性的修復得到了改進。

> [!IMPORTANT]
> .NET 4.5.2 是安裝 SSMA v7.4 的先決條件。 此外,從 v7.4 開始,SSMA 的 32 位元版本正在停產。

## <a name="ssma-v73"></a>SSMA v7.3

MySQL 的 SSMA v7.3 版本包含以下變更:

* 根據客戶反饋有針對性地修復,提高品質和轉化指標。
* 透過以下項目公開的 SSMA 可擴充性框架:
  * 將功能匯出到 SQL 伺服器資料工具 (SSDT) 專案。
    * 現在,您可以將架構腳本從 SSMA 匯出到 SSDT 專案。 您可以使用架構腳本進行其他架構更改並部署資料庫。

      ![另存為 SSDT 專案指令](../media/export-schema-scripts_red.png)
  * SSMA 可使用用於執行自定義轉換的庫。
    * 現在,您可以建構可以處理 SSMA 以前未處理的自訂語法轉換和轉換的代碼。
      * 有關如何建構自訂轉換器的說明,可在此部落格文章,[擴充 SQL 伺服器移轉助手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 從這個[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)下載一個轉換的範例專案。

## <a name="ssma-v72"></a>SSMA v7.2

MySQL 的 SSMA v7.2 版本包含以下變更:

* 根據客戶反饋有針對性地修復,提高品質和轉化指標。
* 遙測增強功能,以提供更好的數據點,以解決客戶問題並提高 SSMA 的轉化率。

## <a name="ssma-v71"></a>SSMA v7.1

MySQL 的 SSMA v7.1 版本包含以下變更:

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援遷移的目標平臺。 此功能處於技術預覽中,允許架構和數據移動以目標 SQL 伺服器為目標。
* SSMA 現在支援自動更新,以便一旦 SSMA 可用,立即下載。
* SSMA 可安裝二進位檔案現在透過 Windows 安裝套件檔 (.msi) 傳遞。

## <a name="may-2016"></a>2016 年 5 月

2016 年 5 月版本的 MySQL 的 SSMA 包含以下變更:

* 添加了對 SQL Server 2016 的支援。
* 改進的解析器和解析器。
* 已刪除的安裝程式檢查 .NET 2.0。
* 將擴展包依賴項從 .NET 3.5 更新為 .NET 4.0。
* 修復了 MySql 的預設 BigInt 類型映射。
* SSMA 主控台`save-project`的`open-project`固定和命令。
* SSMA 主控台`securepassword`的固定 命令。
* 修復了初始載入的物件計數。
* 修復了MsSql物件載入。
* 修復了全域設置中的 Bug。

## <a name="march-2016"></a>2016 年 3 月

MySQL 的 SSMA 預覽版 2016 年 3 月增加了對遷移到 SQL Server 2016 的支援。
  
## <a name="january-2016"></a>2016 年 1 月

MySQL 的 SSMA 2016 年 1 月維護版本包含以下變更:

* 將檢視日誌功能表項添加到 SSMA (RFC 5706203)。
* 添加了遙測。
  
## <a name="july-2014"></a>2014 年 7 月

2014 年 7 月版本的 MySQL 的 SSMA 包含以下變更:
  
* 改進了 Azure SQL DB 代碼轉換。
* 擴展包功能移動到架構以支援 Azure SQL DB。
* 對具有 10k 個以上對象的資料庫測試了性能改進。
* 用於處理大量物件的 UI 改進。
* 突出顯示眾所周知的 LOB 架構(以便在轉換中忽略它們)。
* 轉換速度改進。
* 在 UI 中顯示物件計數。
* 報表大小縮減超過 25%。
* 改進了未解析構造的錯誤消息。
  
## <a name="april-2014"></a>2014 年 4 月

2014 年 4 月版本的 MySQL 的 SSMA 包含以下變更:
  
* 添加了對 SQL Server 2014 的支援。
* 修復了有關轉換為 Azure 的錯誤。
* 修復了 IE 10 中不可見報表頁的 Bug。
  
## <a name="july-2011"></a>2011 年 7 月

2011 年 7 月版本的 MySQL 的 SSMA 包含以下變更:
  
* 支援轉換為`LIMIT`[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]`OFFSET`。
* 改進了數據遷移期間的錯誤報告。
  
## <a name="april-2011"></a>2011年4月

2011 年 4 月版本的 MySQL 的 SSMA 包含以下變更:
  
* 支援的"SSMA 表示MySQL"的單[!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)]一[!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]可[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]安裝 ,支援和Azure SQL。
* 連接[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]的能力。
* 增強的用戶端數據遷移引擎,支援數據的並行遷移。
* 使用簡單和批量記錄恢復模型提高了數據遷移性能。
* 適用於 MySQL 主控台版本的 SSMA 支援向後相容性。 您可以打開早期版本創建的專案 SSMA v5.0。
* MySQL v5.0 產品的 SSMA 可以與舊版本的 SSMA 產品並排安裝 (SxS)。
  
## <a name="july-2010"></a>2010 年 7 月

2010 年 7 月版本的 MySQL 的 SSMA 包含以下功能:
  
**1. 使用者介面的改進:**

* MySQL 資料庫物件的「SQL 模式」選項卡
* MySQL 資料庫物件的「設定」選項卡
* MySQL 表的「資料」選項卡
* 轉換並移至移動頁中更新的項目設定
* 表級別的"數據遷移設置"
  
**2. 連線到 MySQL 與 SQL 伺服器的改進:**
  
* MySQL 的 SSL 連線
* SQL 伺服器中的加密連線
  
**3. MySQL 函式庫資源管理員的改進:**
  
* 載入所有 MySQL 資料庫物件及其各自的選項卡。
  
**4. 物件轉換的改進:**
  
* MySQL 物件轉換 - 過程、函數、檢視、觸發器和語句。
* 對錶中空間數據類型的支援有限。
* 將 MySQL 函數轉換為 SQL 伺服器儲存過程的選項
* 在物件轉換期間套用 SQL 模式與字元集對應的選項
  
**5. 資料移轉的改進:**  
  
* 使用伺服器端及客戶端資料移動引擎支援資料移轉
* 支援空間資料移轉
* 為表資料移至自訂 SQL
  
**6. MySQL 主控台的 SSMA:**  
  
* 支援適用於 MySQL 的 SSMA 的主控台功能  
* 支援文稿介面  
  
## <a name="january-2010"></a>2010年1月

2010 年 1 月版本的 MySQL SSMA 是初始版本。 它包含以下功能:
  
* 添加了對本地 SQL 伺服器和 Azure SQL 遷移的支援。  
  
* **功能快照:** MySQL 表/索引/約束的架構和數據遷移。
