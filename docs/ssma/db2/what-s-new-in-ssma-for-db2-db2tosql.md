---
title: DB2 (DB2ToSQL) SSMA 中的新增功能 |微軟文件
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
ms.author: jtoland;alexiva
ms.openlocfilehash: 53a159627750a5ec66b5aa0b3fd6510c647e26a5
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625518"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>DB2 (DB2ToSQL) SSMA 中的新增功能

本文列出了每個版本中 DB2 更改的 SQL 伺服器遷移助手 (SSMA)。

## <a name="ssma-v88"></a>SSMA v8.8

DB2 的 SSMA v8.8 版本包括:

* SQL Server 物件同步穩定性改進
* 評估並轉換期間的 GUI 效能改進
* 更新映射,`ROWID``varbinary(40)`以方便資料移轉
* 改進敘述轉換`SELECT ... FROM NEW/OLD TABLE`
* 程式和職能`ALTER`報表的新轉換
* 解構配置的新轉換

## <a name="ssma-v87"></a>SSMA v8.7

DB2 的 SSMA v8.7 版本包括全新的 DB2 語法解析器,以及圖形使用者介面中的次要修復和性能改進。

此外,DB2 的 SSMA 現在提供:

* 在 LUW 上從 DB2 遷移時發現外鍵的修復程式。
* 改進了語句`SELECT ... FOR UPDATE`的轉換。
* 改進了`COUNT`MQ 表中函數的轉換。
* 語句的`SAVEPOINT`轉換。
* 轉換以類比 DB2`NULL`對`ORDER BY`子句中 的值的行為。
* 分析對關聯結果設置語句的支援。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v86"></a>SSMA v8.6

除了一組旨在提高可用性和性能的有針對性的修補程式外,DB2 的 V8.6 版本透過添加允許使用者在轉換後的代碼中省略 SSMA 擴充屬性的設置進行了增強。

要利用此設定,在 DB2 的 SSMA 中,導航到 **「工具** > **專案設定** > **常規** > **轉換**」,然後在**Misc**下,將 **「省略擴展屬性**」設置的值更新為 **"是**"。

![省略延伸屬性設定](../db2/media/ssma-omit-extended-properties.png)

此外,DB2 的 SSMA 現在提供:

* 用於轉換使用預設參數值的函數的修復程式。
* 改進了函數子`PARAMETER`句的解析。
* 轉換`LEAVE`語句的能力。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v85"></a>SSMA v8.5

支援 Azure Active Directory 身份驗證和對 SQL 伺服器中的 JSON 功能的基本支援,以及一組旨在提高可用性和性能的有針對性的修補程式,增強了 DB2 的 SSMA v8.5 版本。

此外,DB2 的 SSMA 還通過:

* 支援將轉換添加到`GET DIAGNOSTICS`語句。 `ROW_NUMBER`
* 與物件名稱開頭未受尊重的空間相關的 Bug 的修復。

> [!IMPORTANT]
> 使用 SSMA v8.5 時,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v84"></a>SSMA v8.4

DB2 的 SSMA v8.4 版本通過有針對性的修補程式進行增強,這些修補程式旨在解決輔助功能問題並修復 SQL Server 2016 和更高版本的最大索引列(允許 32 而不是 16)相關的 Bug。

> [!IMPORTANT]
> 對於 SSMA 版本 7.4 但 8.4,.NET 4.5.2 是安裝的先決條件。

## <a name="ssma-v83"></a>SSMA v8.3

DB2 的 SSMA v8.3 版本透過旨在提高品質和轉換指標的有針對性的修補程式進行增強。 此外,此版本的 DB2 的 SSMA 提供了以下修補程式:

* 解決輔助功能問題。
* 添加對`hierarchyid`SQL Server 類型的基本支援。
* 將 z/OS 查詢中的`RTRIM`/`LTRIM`TRIM 函數用法取代為 。
* 允許使用者在"標準模式"連接時指定包集合(預設為`NULLID`)。
* 新增轉換`CREATE TABLE AS SELECT`。
* 改進全域臨時表的轉換。
* 解決物件唯一性檢查順序的問題,以便在名稱衝突時將表優先於約束的優先順序。
* 解決為 z/OS`DATE`載`TIMESTAMP`入 預設 列值的問題。
* 支援 Unicode 行饋送字`NEL`元( 也稱為 )。
* 解決缺少`RETURN TO`子句的游標轉換問題。
* 添加對標籤和`GOTO`的支援。

## <a name="ssma-v82"></a>SSMA v8.2

DB2 的 SSMA v8.2 版本得到了增強,用於解決從 SSMA 控制台工具連接到 Azure SQL 資料庫的問題,並在轉換期間在視圖聲明中缺少COUNT_BIG列。 此外,此版本還包括一組旨在提高品質和轉化指標的有針對性的修補程式,以及用於以下的修補程式:

* 數據遷移后禁用的非群集索引的問題。
* 在靜默安裝期間檢測 .NET 框架。
* 下載新版本時發生的間歇性崩潰。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v8.1 到 v8.2 的更新失敗。 如果您遇到此錯誤,請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA v8.1

DB2 的 SSMA v8.1 版本得到增強,可提供旨在提高品質和轉換指標的有針對性的修補程式。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v8.0 到 v8.1 的更新失敗。 如果您遇到此錯誤,請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA v8.0

DB2 的 SSMA v8.0 版本得到了增強,可提供旨在提高品質和轉換指標的有針對性的修補程式。 此版本還提供以下新功能:

* 支援**Azure SQL 資料庫託管實例**作為目標。 現在,您可以建立針對 Azure SQL 資料庫託管實例的新專案:

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後**修復顧問**。 此處瞭解有關它的更多[。](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 初步資料庫/架構選擇。

  連接到源時,用戶現在可以選擇感興趣的資料庫/架構。 僅選擇計畫遷移的架構將節省時間連接期間的時間,並提高 SSMA 的整體性能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

DB2 的 SSMA v7.10 版本包含以下變更:

* 旨在提供額外安全和隱私保護以滿足全球需求變化的有針對性的修補程式。
* 用於轉換塊的`BEGIN-END`修復程式。

## <a name="ssma-v79"></a>SSMA v7.9

DB2 的 SSMA v7.9 版本包含以下變更:

* 提高品質和轉化指標的針對性修復。
* 支援 SSMA 命令列以更改資料類型映射和專案首選項。
* 支援使用 SQL 伺服器整合服務 (SSIS) 遷移資料。 轉換架構後,可以使用右鍵單擊上下文菜單選項創建 SSIS 包。
* SSMA 中的 Azure SQL 資料庫連接對話方塊也已更改,以指定完全限定的伺服器名稱。 在 SSMA 的早期版本中,必須在專案設置中顯式提及 Azure SQL 資料庫前綴。

## <a name="ssma-v78"></a>SSMA v7.8

DB2 的 SSMA v7.8 版本包含以下變更:

* 更改類型對應在*項目設定*中突出顯示。
* 使用者禁用遙測功能。

## <a name="ssma-v77"></a>SSMA v7.7

DB2 的 SSMA v7.7 版本包含以下變更:

* 提高品質和轉化指標的針對性修復。
* 根據大眾需求,DB2 的 32 位版本的 SSMA 又回來了。 與以前的實現(在 v7.4 之前)相比,有兩個安裝程式包,但不能並排安裝。 因此,您必須根據擁有的連接元件選擇最合適的版本。 如果可能,最好使用 64 位元版本。

## <a name="ssma-v76"></a>SSMA v7.6

DB2 的 SSMA v7.6 版本透過提高品質和轉換指標的針對性修補程式以及支援 SQL Server 2017(公共預覽)來增強。 Windows 和 Linux 上對 SQL Server 2017 的支援處於公共預覽版,不應用於生產遷移。

## <a name="ssma-v75"></a>SSMA v7.5

DB2 的 SSMA v7.5 版本通過多項改進進行了增強,以確保殘障人士獲得更大的可訪問性。

## <a name="ssma-v74"></a>SSMA v7.4

DB2 的 SSMA v7.4 版本包含以下變更:

* **查詢超時**選項現在在源和目標架構對象發現期間可用。

  ![查詢逾時選項](../media/query-timeout_red.png)

* 品質和轉化指標已根據客戶反饋通過有針對性的修復得到了改進。

  > [!IMPORTANT]
  > .NET 4.5.2 是安裝 SSMA v7.4 的先決條件。 此外,從 v7.4 開始,SSMA 的 32 位版本已停產。

## <a name="ssma-v73"></a>SSMA v7.3

DB2 的 SSMA v7.3 版本包含以下變更:

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

DB2 的 SSMA v7.2 版本包含以下變更:

* 根據客戶反饋有針對性地修復,提高品質和轉化指標。
* 遙測增強功能,以提供更好的數據點,以解決客戶問題並提高 SSMA 的轉化率。

## <a name="ssma-v71"></a>SSMA v7.1

DB2 的 SSMA v7.1 版本包含以下變更:

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援遷移的目標平臺。 此功能處於技術預覽中,允許架構和數據移動以目標 SQL 伺服器為目標。
* 支援自動更新,以便一旦 SSMA 可用,立即下載。
* SSMA 可安裝二進位檔案現在透過 Windows 安裝套件檔 (.msi) 傳遞。

## <a name="may-2016"></a>2016 年 5 月

2016 年 5 月版本的 DB2 的 SSMA 包含以下變更:

* 添加了對 SQL Server 2016 的支援。
* 將 DB2 記憶體中表和常規表轉換為 SQL Server 記憶體中和 hekaton 功能。
* 將 DB2 存取控制項轉換為 SQL Server 策略物件(DB2 的行級安全性)。
* 將 DB2 系統版本化表轉換為 SQL Server 臨時性表。
* 改進了 DB2 解析器和解析器。
* 已刪除的安裝程式檢查 .NET 2.0。
* 從\*Db2 安裝程式中移除了不必要的 .dll。
* SSMA 主控台`save-project`的`open-project`固定和命令。
* SSMA 主控台`securepassword`的固定 命令。
* 修復了初始載入的物件計數。
* 修復了全域設置中的 Bug。
  
## <a name="march-2016"></a>2016 年 3 月

DB2 的 SSMA 預覽版 2016 年 3 月增加了對遷移到 SQL Server 2016 的支援。

## <a name="january-2016"></a>2016 年 1 月

DB2 的 SSMA 2016 年 1 月維護版本包含以下變更:
  
* 增加了對許多標準功能的支援。
* 修復了 DB2 分析器錯誤。
* 固定 DB2 v9 zOS 支援 (RFC 5690920)。
* 修復了轉換過程中未解決的 DB2 標識符錯誤。
* 將檢視日誌功能表項添加到 SSMA (RFC 5706203)。
* 添加了遙測。
  
## <a name="november-2014"></a>November 2014

2014 年 11 月版本的 DB2 的 SSMA 是初始版本。
