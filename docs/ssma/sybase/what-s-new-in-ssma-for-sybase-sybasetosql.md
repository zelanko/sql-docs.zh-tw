---
title: SAP ASE SSMA 的新增功能 (SybaseToSQL) |微軟文件
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
ms.author: jtoland;alexiva
ms.openlocfilehash: 7f23c7e1c676b4ade42b43cf963e0fa6956f93c6
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625590"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>SAP ASE SSMA 中的新增功能(SybaseToSQL)

本文列出了每個版本中 SAP ASE(以前 SSMA 表示 Sybase)更改的 SQL 伺服器遷移助理 (SSMA)。

## <a name="ssma-v88"></a>SSMA v8.8

適用於 SAP ASE 的 SSMA v8.8 版本包括:

* SQL Server 物件同步穩定性改進
* 評估並轉換期間的 GUI 效能改進
* 修復了物件 SQL 定義缺少字元的問題

## <a name="ssma-v87"></a>SSMA v8.7

用於 SAP ASE 的 SSMA v8.7 版本在圖形用戶介面中具有輕微的修復和性能改進。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v86"></a>SSMA v8.6

除了一組旨在提高可用性和性能的有針對性的修補程式外,SAP ASE 的 SSMA v8.6 版本透過添加允許使用者在轉換後的代碼中省略 SSMA 擴展屬性的設置進行了增強。

要利用此設定,在 SAP ASE 的 SSMA 中,導航到**工具** > **專案設置** > **常規** > **轉換**,然後在**Misc**下,將 **「省略擴展屬性**」設置的值更新為 **"是**"。

![省略延伸屬性設定](../sybase/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v85"></a>SSMA v8.5

支援 Azure Active Directory 身份驗證和 SQL 伺服器中對 JSON 功能的基本支援,以及一組旨在提高可用性和性能的有針對性的修補程式,增強了用於 SAP ASE 的 SSMA 的 v8.5 版本。

此外,SAP ASE 的 SSMA 現在允許您隱藏系統表和檢視(將其排除在轉換之外)。

> [!IMPORTANT]
> 使用 SSMA v8.5 時,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v84"></a>SSMA v8.4

針對 SAP ASE 的 SSMA v8.4 版本通過有針對性的修補程式進行增強,這些修補程式旨在解決輔助功能問題並修復 SQL Server 2016 和更高版本的最大索引列(允許 32 而不是 16)相關的 Bug。

> [!IMPORTANT]
> 對於 SSMA 版本 7.4 到 8.4,.NET 4.5.2 是安裝的先決條件。

## <a name="ssma-v83"></a>SSMA v8.3

面向 SAP ASE 的 SSMA v8.3 版本透過旨在提高品質和轉換指標的有針對性的修補程式進行增強。 此外,此版本的 SAP ASE SSMA 提供了以下修補程式:

* 解決輔助功能問題
* 新增對`hierarchyid`SQL Server 類型的基本支援

## <a name="ssma-v82"></a>SSMA v8.2

用於 SAP ASE 的 SSMA v8.2 版本透過一組旨在提高品質和轉換指標的有針對性的修補程式以及用於以下的修補程式進行增強:

* 數據遷移后禁用的非群集索引的問題。
* 在靜默安裝期間檢測 .NET 框架。
* 下載新版本時發生的間歇性崩潰。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v8.1 到 v8.2 的更新失敗。 如果您遇到此錯誤,請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA v8.1

面向 SAP ASE 的 SSMA v8.1 版本透過旨在提高品質和轉換指標的有針對性的修補程式進行增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v8.0 到 v8.1 的更新失敗。 如果您遇到此錯誤,請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA v8.0

針對 SAP ASE 的 SSMA v8.0 版本透過旨在提高品質和轉換指標的有針對性的修補程式進行增強。 此外,此版本還提供以下新功能:

* 支援**Azure SQL 資料庫託管實例**作為目標。 現在,您可以建立針對 Azure SQL 資料庫託管實例的新專案:

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後**修復顧問**。 此處瞭解有關它的更多[。](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 初步資料庫/架構選擇。

  連接到源時,用戶現在可以選擇感興趣的資料庫/架構。 僅選擇計畫遷移的架構將節省時間連接期間的時間,並提高 SSMA 的整體性能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

針對 SAP ASE 的 SSMA v7.10 版本透過針對性的修補程式進行了增強,旨在提供額外的安全和隱私保護,以滿足全球需求的變化。

## <a name="ssma-v79"></a>SSMA v7.9

用於 SAP ASE 的 SSMA v7.9 版本包含以下變更:

* 提高品質和轉化指標的針對性修復。
* 支援 SSMA 命令列以更改資料類型映射和專案首選項。
* 支援使用 SQL 伺服器整合服務 (SSIS) 遷移資料。 轉換架構後,可以使用右鍵單擊上下文菜單選項創建 SSIS 包。
* SSMA 中的 Azure SQL 資料庫連接對話方塊也已更改,以指定完全限定的伺服器名稱。 在 SSMA 的早期版本中,必須在專案設置中顯式提及 Azure SQL 資料庫前綴。

## <a name="ssma-v78"></a>SSMA v7.8

用於 SAP ASE 的 SSMA v7.8 版本包含以下變更:

* 更改類型對應在**項目設定**中突出顯示。
* 使用者禁用遙測功能。

## <a name="ssma-v77"></a>SSMA v7.7

用於 SAP ASE 的 SSMA v7.7 版本包含以下變更:

* SAP ASE 的 SSMA 已通過提高品質和轉化指標的有針對性的修補程式進行了增強。
* 根據大眾需求,SAP ASE 的 32 位版本的 SSMA 又回來了。 與以前的實現(在 v7.4 之前)相比,有兩個安裝程式包,但不能並排安裝。 因此,您必須根據擁有的連接元件選擇最合適的版本。 如果可能,最好使用 64 位元版本。

## <a name="ssma-v76"></a>SSMA v7.6

用於 SAP ASE 的 SSMA v7.6 版本包含以下變更:

* 提高品質和轉換指標並支援 SQL Server 2017(公共預覽)的針對性修補程式。 Windows 和 Linux 上對 SQL Server 2017 的支援處於公共預覽版,不應用於生產遷移。
* 支援轉換 Sybase 函數。

## <a name="ssma-v75"></a>SSMA v7.5

用於 SAP ASE 的 SSMA v7.5 版本(以前適用於 Sybase 的 SSMA)包含以下變更:

* 若干改進,以確保殘疾人更容易獲得無障礙環境。
* 支援`CREATE OR REPLACE`語法。

## <a name="ssma-v74"></a>SSMA v7.4

Sybase 的 SSMA v7.4 版本包含以下變更:

* **查詢超時**選項現在在源和目標架構對象發現期間可用。

  ![查詢逾時選項](../media/query-timeout_red.png)
* 品質和轉化指標已根據客戶反饋通過有針對性的修復得到了改進。

  > [!IMPORTANT]
  > .NET 4.5.2 是安裝 SSMA v7.4 的先決條件。 此外,從 v7.4 開始,SSMA 的 32 位元版本正在停產。

## <a name="ssma-v73"></a>SSMA v7.3

Sybase 的 SSMA v7.3 版本包含以下變更:

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

Sybase 的 SSMA v7.2 版本包含以下變更:

* 根據客戶反饋有針對性地修復,提高品質和轉化指標。
* 遙測增強功能,以提供更好的數據點,以解決客戶問題並提高 SSMA 的轉化率。

## <a name="ssma-v71"></a>SSMA v7.1

Sybase 的 SSMA v7.1 版本包含以下變更:

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援遷移的目標平臺。 此功能處於技術預覽中,支援針對 SQL 伺服器的架構和數據移動。
* 支援自動更新,以便一旦 SSMA 可用,立即下載。
* SSMA 可安裝二進位檔案現在透過 Windows 安裝套件檔 (.msi) 傳遞。

## <a name="may-2016"></a>2016 年 5 月

2016 年 5 月版本的 SSMA 適用於 Sybase 包含以下變更:

* 添加了對 SQL Server 2016 的支援。
* 已刪除的安裝程式檢查 .NET 2.0。
* 將擴展包依賴項從 .NET 3.5 更新為 .NET 4.0。
* SSMA 主控台`save-project`的`open-project`固定和命令。
* SSMA 主控台`securepassword`的固定 命令。
* 修復了初始載入的物件計數。
* 修復了全域設置中的 Bug。

## <a name="march-2016"></a>2016 年 3 月

Sybase 的 SSMA 預覽版 2016 年 3 月增加了對遷移到 SQL Server 2016 的支援。

## <a name="january-2016"></a>2016 年 1 月

Sybase 的 SSMA 2016 年 1 月維護版本包含以下變更:

* 將檢視日誌功能表項添加到 SSMA (RFC 5706203)。
* 添加了遙測。

## <a name="july-2014"></a>2014 年 7 月

2014 年 7 月版本的 SSMA 適用於 Sybase 包含以下變更:

* 改進了 Azure SQL DB 代碼轉換。
* 將擴展包功能移動到架構以支援 Azure SQL DB。
* 為具有 10k 個以上對象的資料庫測試的性能改進。
* 添加了用於處理大量物件的UI改進。
* 添加了突出顯示已知 LOB 架構(以便在轉換中忽略它們)的能力。
* 添加了轉換速度改進。
* 添加了在 UI 中顯示物件計數的能力。
* 報表大小減少 25% 以上。
* 改進了未解析構造的錯誤消息。

## <a name="april-2014"></a>2014 年 4 月

2014 年 4 月版本的 SSMA 適用於 Sybase 包含以下變更:

* 添加了對 MS SQL Server 2014 的支援。
* 修復了有關轉換為 Azure 的錯誤。
* 修復了 IE 10 中不可見報表頁的 Bug。

## <a name="january-2012"></a>2012 年 1 月

Sybase 的 SSMA 2012 年 1 月版本包含以下變更:

* 添加了對回滾觸發器轉換的支援。
* 提供了用於轉換`@@ROWCOUNT`和`@@ERROR`在同`SET`一語句中的修復程式。

## <a name="july-2011"></a>2011 年 7 月

2011 年 7 月版 SSMA 用於 Sybase 提供了資料遷移期間改進的錯誤報告。

## <a name="april-2011"></a>2011年4月

2011 年 4 月版本的 SSMA 適用於 Sybase 包含以下變更:

* 整合的「SSMA 用於 Sybase」[!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]產品[!INCLUDE [ssSQL11](../../includes/ssSQL11-md.md)][!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)], 支援和 Azure SQL。
* 添加了對連接和遷移到[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]的支援。
* 添加了一個新功能,用於將 Sybase 資料庫轉換為 Azure SQL。
* 增強的用戶端數據遷移引擎,支援數據的並行遷移。
* 使用簡單和批量記錄恢復模型提高了數據遷移性能。
* 添加了將區分大小寫 Sybase 資料庫正確轉換為區分大小寫的 SQL Server 的功能。
* 對 Sybase ASE 非 ANSI 聯接文句轉換為 SQL Server ANSI 聯接文句的附加支援已擴展到 DELETE 和更新語句。
* 提供其他連線選項,用於使用 Sybase ASE ODBC 提供者和 Sybase ASE ADO.NET 提供者連接到 Sybase ASE 伺服器。
* 刪除了對稱為`SysDB`的單獨資料庫的依賴項,該資料庫包含 Sybase 模擬函數(作為擴展包的一部分安裝)。
* 添加了在群集上安裝[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]Sybase 擴展包 SSMA 的能力。
* 添加了早期版本的 SSMA(v4.0 和 v4.2)創建的專案的向後相容性。
* 添加了使用舊版本的 SSMA(v4.0 和 v4.2)並行安裝 Sybase v5.0 產品的 SSMA 功能。

## <a name="july-2010"></a>2010 年 7 月

Sybase 的 SSMA 2010 年 7 月版本新增:

* 支援遷移到 SQL Server 2008 R2。
* 用於命令列執行的新 SSMA 主控台應用程式。
* 使用伺服器端和客戶端數據遷移引擎支援數據遷移。
* 在資料遷移中支援"自定義 SELECT"語句。
* 支援從 Sybase ASE 15.0.3 和 15.5 遷移。

## <a name="june-2008"></a>2008 年 6 月

Sybase 的 SSMA 2008 年 6 月版本包含以下變更:

* 添加了 SSMA 測試程式,自動測試資料庫物件轉換和 SSMA 進行的資料移轉。 完成所有 SSMA 遷移步驟後,使用 SSMA 測試程序驗證轉換的物件是否以相同的方式工作,以及所有數據是否正確傳輸。
* 添加了 SQL 前轉換。 用戶現在可以為要在轉換中使用的每個源過程指定臨時表(和其他物件)聲明。
* 在物件轉換方面增加了改進:
  * 加入已修訂的轉化。
  * 聚合和非聚合,沒有/按子句分組。
  * 具有`IDENTITY`語句的`SELECT INTO`函數。
  * 僅數據鎖定的群集約束和索引。
  * 由創建`SELECT INTO`的暫時表。
  * 臨時表的約束/索引。
  * 支援[!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]新的約會時間類型。
  * Sybase 15.0 連接和數據類型支援。

## <a name="may-2007"></a>2007 年 5 月

2007 年 5 月 SSMA 版本的 Sybase 補充說:

* 保存專案時更快地載入資料庫內容的能力。
* 支援 SQL Server 格式化的 SQL 模式下使用者輸入的註釋。
* 物件轉換的改進。

## <a name="november-2006"></a>2006年11月

Sybase 的 SSMA 2006 年 11 月版本包含以下變更:

* 新增新的全域設定:
  * 您可以選擇在編輯器視窗中顯示行號。
  * 您可以將 SSMA 設定為提示替換重複的物件,或者始終或從不在架構轉換期間替換重複的物件。
* 新增一個新的轉換選項,允許您設定 SSMA 處理以下情況的方式:
  * 包含`CAST`二`CONVERT`進位字串的或語句。
  * 檢查相等表達式中的空值。
  * 代理表。
  * 使用者訊息錯誤編號`RAISERROR`。
  * `UPDATE`包含未解析識別碼的語句。
* 添加了一個新的遷移選項,用於指定 SSMA 如何[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]處理超出 日期範圍的日期。
* 在**SQL**選項卡上添加了格式化的**SQL**設置,該設置為代碼設定格式以提高可讀性。
* 錯誤修復,包括:
  * SSMA 現在`LOCK TABLE <table> IN { SHARED | EXCLUSIVE } MODE`透過表表上的`TABLOCK``SELECT`後續`TABLOCKX`查詢 添加 或提示來轉換語句。
  * 現在,當字元表達式中使用二進位類型時,將添加必要的強制轉換。
  * 記憶體和性能改進。

## <a name="july-2006"></a>2006年7月

2006 年 7 月版的 SSMA for Sybase 是最早的版本。

## <a name="see-also"></a>另請參閱

[開始使用 SSMA 進行 Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
