---
title: SSMA 中用於造訪的新增功能 (訪問到SQL) |微軟文件
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
ms.author: jtoland;alexiva
ms.openlocfilehash: 2fd3da31e6a635a65f3d2a2f75320dd0586159d9
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625576"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>SSMA 中用於存取的新增功能(存取SQL)

本文列出了 SQL Server 遷移助手 (SSMA) 用於每個版本中的訪問更改。

## <a name="ssma-v88"></a>SSMA v8.8

用於存取的 SSMA 的 v8.8 版本包括:

* SQL Server 物件同步穩定性改進
* 評估並轉換期間的 GUI 效能改進
* 全新存取語法解析器,進一步提高轉換性能

## <a name="ssma-v87"></a>SSMA v8.7

SSMA 的 v8.7 版本改進`IIF`了查詢中 功能的轉換,以及圖形使用者介面中的一些小修復和性能改進。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v86"></a>SSMA v8.6

除了一組旨在提高可用性和性能的有針對性的修補程式外,通過添加允許使用者在轉換後的代碼中省略 SSMA 擴展屬性的設置,還增強了 SSMA 訪問版本的 v8.6 版本。

要利用此設定,在 SSMA 中訪問,導航到 **「工具** > **專案設定** > **」,** > **然後**在**Misc**下,將 **「Omit 擴展屬性**」設置的值更新為 **"是**"。

![省略延伸屬性設定](../access/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v85"></a>SSMA v8.5

通過支援 Azure Active Directory 身份驗證和 SQL 伺服器中對 JSON 功能的基本支援,以及旨在提高可用性和性能的一組有針對性的修補程式,SSMA 的 v8.5 版本得到了增強。

此外,SSMA 訪問現在支援轉換多個標準函數`ISNULL`( 等`IIF`)。

> [!IMPORTANT]
> 使用 SSMA v8.5 時,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v84"></a>SSMA v8.4

SSMA 的 v8.4 版本通過有針對性的修補程式進行增強,這些修補程式旨在解決輔助功能問題並修復 SQL Server 2016 和更高版本的最大索引列(允許 32 而不是 16)相關的 Bug。

> [!IMPORTANT]
> 對於 SSMA 版本 7.4 但 8.4,.NET 4.5.2 是安裝的先決條件。

## <a name="ssma-v83"></a>SSMA v8.3

SSMA 的 v8.3 版本透過旨在提高品質和轉換指標的有針對性的修補程序進行增強。 此外,此版本的 SSMA 用於存取提供以下修補程式:

* 解決輔助功能問題。
* 添加對`hierarchyid`SQL Server 類型的基本支援。

## <a name="ssma-v82"></a>SSMA v8.2

SSMA 的 v8.2 版本透過旨在提高品質和轉換指標的有針對性的修補程序進行增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v8.1 到 v8.2 的更新失敗。 如果您遇到此錯誤,請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA v8.1

SSMA 的 v8.1 版本透過旨在提高品質和轉換指標的有針對性的修補程序進行增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v8.0 到 v8.1 的更新失敗。 如果您遇到此錯誤,請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA v8.0

SSMA 面向訪問的 v8.0 版本通過旨在提高品質和轉換指標的有針對性的修補程式進行增強。 此版本還提供以下新功能:

* 支援**Azure SQL 資料庫託管實例**作為目標。 現在,您可以建立針對 Azure SQL 資料庫託管實例的新專案:

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後**修復顧問**。 此處瞭解有關它的更多[。](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Accelerate-your-Oracle-migrations-with-new-machine-learning/ba-p/368733)

* 初步資料庫/架構選擇。

    連接到源時,用戶現在可以選擇感興趣的資料庫/架構。 僅選擇計畫遷移的架構將節省時間連接期間的時間,並提高 SSMA 的整體性能。

   ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

SSMA 的 v7.10 版本通過有針對性的修補程式進行了增強,旨在提供額外的安全和隱私保護,以滿足全球需求的變化。

## <a name="ssma-v79"></a>SSMA v7.9

SSMA 的 v7.9 版本包含以下變更:

* 提高品質和轉化指標的針對性修復。
* 支援 SSMA 命令列以更改資料類型映射和專案首選項。
* SSMA 中的 Azure SQL 資料庫連接對話方塊也已更改,以指定完全限定的伺服器名稱。 在 SSMA 的早期版本中,必須在專案設置中顯式提及 Azure SQL 資料庫前綴。

## <a name="ssma-v78"></a>SSMA v7.8

SSMA 的 v7.8 版本包含以下變更:

* 更改類型對應在項目設定中突出顯示。
* 使用者禁用遙測功能。

## <a name="ssma-v77"></a>SSMA v7.7

SSMA 的 v7.7 版本包含以下變更:

* 提高品質和轉化指標的針對性修復。
* 根據大眾需求,32 位版本的 SSMA 表示訪問。 與以前的實現(在 v7.4 之前)相比,有兩個安裝程式包,但不能並排安裝。 因此,您必須根據擁有的連接元件選擇最合適的版本。 如果可能,最好使用 64 位元版本。

## <a name="ssma-v76"></a>SSMA v7.6

SSMA 的 v7.6 版本透過提高品質和轉換指標的針對性修補程式以及支援 SQL Server 2017(公共預覽)來增強。 Windows 和 Linux 上對 SQL Server 2017 的支援處於公共預覽版,不應用於生產遷移。

## <a name="ssma-v75"></a>SSMA v7.5

通過多項改進,增強了 SSMA 的 v7.5 版本,以確保殘疾人獲得更大的可訪問性。

## <a name="ssma-v74"></a>SSMA v7.4

SSMA 的 v7.4 版本包含以下變更:

* **查詢超時**選項現在在源和目標架構對象發現期間可用。

  ![查詢逾時選項](../media/query-timeout_red.png)

* 品質和轉化指標已根據客戶反饋通過有針對性的修復得到了改進。

  > [!IMPORTANT]
  > .NET 4.5.2 是安裝 SSMA v7.4 的先決條件。 此外,從 v7.4 開始,SSMA 的 32 位版本已停產。

## <a name="ssma-v73"></a>SSMA v7.3

SSMA 的 v7.3 版本包含以下變更:

* 根據客戶反饋有針對性地修復,提高品質和轉化指標。
* 透過以下項目公開的 SSMA 可擴充性框架:
  * 將功能匯出到 SQL 伺服器資料工具 (SSDT) 專案。
    * 現在,您可以將架構腳本從 SSMA 匯出到 SSDT 專案。 您可以使用架構腳本進行其他架構更改並部署資料庫。

        ![另存為 SSDT 專案指令](../media/export-schema-scripts_red.png)
  * SSMA 可使用用於執行自定義轉換的庫。
    * 現在,您可以建構可以處理 SSMA 以前未處理的自訂語法轉換和轉換的代碼。
      * 有關如何建構自訂轉換器的說明以及用於轉換的範例專案,可在部落格文章['擴展 SQL Server 遷移助手的轉換功能](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Extending-SQL-Server-Migration-Assistant-s-conversion/ba-p/1004181)"中提供。

## <a name="ssma-v72"></a>SSMA v7.2

SSMA 的 v7.2 版本包含以下變更:

* 根據客戶反饋有針對性地修復,提高品質和轉化指標。
* 遙測增強功能,以提供更好的數據點,以解決客戶問題並提高 SSMA 的轉化率。

## <a name="ssma-v71"></a>SSMA v7.1

SSMA 的 v7.1 版本包含以下變更:

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援遷移的目標平臺。 此功能處於技術預覽中,支援針對 SQL 伺服器的架構和數據移動。
* SSMA 現在支援自動更新,以便一旦 SSMA 可用,立即下載。
* SSMA 可安裝二進位檔案現在透過 Windows 安裝套件檔 (.msi) 傳遞。

## <a name="may-2016"></a>2016 年 5 月

2016 年 5 月版本的 SSMA 存取包含以下變更:

* 添加了對 SQL Server 2016 的官方支援。
* 已刪除的安裝程式檢查 .NET 2.0。
* SSMA 主控台`save-project`的`open-project`固定和命令。
* SSMA 主控台`securepassword`的固定 命令。
* 修復了初始載入的物件計數。
* 修復了用於存取 UI 選項卡的表數據載入。
* 修復了全域設置中的 Bug。

## <a name="march-2016"></a>2016 年 3 月

2016 年 3 月用於存取的 SSMA 預覽版增加了對遷移到 SQL Server 2016 的支援。

## <a name="january-2016"></a>2016 年 1 月

SSMA 的 2016 年 1 月維護版本包含以下變更:

* 修復了 GUID 欄位預設值(RFC 3894811)的無效函數。
* 修復了將記錄導入到 SQL 資料庫 (Azure) (RFC 4919573) 上的掛起。
* 將檢視日誌功能表項添加到 SSMA (RFC 5706203)。
* 添加了遙測。

## <a name="july-2014"></a>2014 年 7 月

2014 年 7 月版本的 SSMA 存取包含以下變更:

* 改進了 Azure SQL DB 代碼轉換。
* 將擴展包功能移動到架構以支援 Azure SQL DB。
* 測試了具有 10k 個對象資料庫的性能改進。
* 添加了用於處理大量物件的UI改進。
* 添加了對突出顯示"眾所周知"LOB 架構的支援(以便在轉換中可以忽略它們)。
* 添加了轉換速度改進。
* 添加了對在 UI 中顯示物件計數的支援。
* 報表大小減少 25% 以上。
* 改進了未解析構造的錯誤消息。

## <a name="april-2014"></a>2014 年 4 月

2014 年 4 月版本的 SSMA 存取包含以下變更:

* 添加了對 MS SQL Server 2014 的支援。
* 修復了與轉換為 Azure 相關的 Bug。
* 修復了 IE 10 中與不可見報表頁相關的 Bug。

## <a name="january-2012"></a>2012 年 1 月

2012 年 1 月版本的 SSMA 用於存取包含以下變更:

* 提供了在遷移後不保留 MS Access 連結表的使用者名和密碼的選項。
* 為迴圈引用設置為"無操作"設置級聯操作。
* 提供的正確消息,指示迴圈引用的級聯操作已設置為"無操作"。

## <a name="july-2011"></a>2011 年 7 月

2011 年 7 月版本的 SSMA 用於訪問增加了數據遷移期間改進的錯誤報告。

## <a name="april-2011"></a>2011年4月

2011 年 4 月版本的 SSMA 用於存取包含以下變更:

* 新增了"SSMA 用於存取'的單一可安裝,[!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)]該[!INCLUDE [ssSQL10](../../includes/sssql10-md.md)][!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]安裝 支援與 。
* 添加了連接到[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]的功能。
* 添加了用於存取控制台版本的 SSMA,支援向後相容性。 您可以打開早期版本創建的專案 SSMA v5.0。
* 添加了使用舊版本的 SSMA 產品並排安裝 SSMA v5.0 產品 (SxS) 的能力。

## <a name="july-2010"></a>2010 年 7 月

2010 年 7 月版本的 SSMA 表示存取包含以下變更:

* 添加了對遷移到 SQL Server 2008 R2 和 Azure SQL 的支援。
* 向 SQL 伺服器和 Azure SQL 添加了安全連接。
* 添加了對 Access 2010 資料庫的支援。
* 添加了用於命令行執行的新 SSMA 主控台應用程式。
* 添加了對 SQL Server`DateTime2`數據類型的支援。

## <a name="june-2008"></a>2008 年 6 月

2008 年 6 月版本的 SSMA 訪問增加了對 Access 2007 資料庫的支援。

## <a name="may-2007"></a>2007 年 5 月

2007 年 5 月版本的 SSMA 用於存取包含以下變更:

* 添加了對使用工作組策略的 Access 資料庫的支援。
* 提供了從 SQL Server 中資料資源管理員中刪除轉換物件的功能。
* 在 SQL Server 格式化的 SQL 模式下添加了對使用者輸入的註釋的支援。
* 添加了物件轉換的改進。

## <a name="november-2006"></a>2006年11月

2006 年 11 月版本的 SSMA 用於造訪包含以下變更:

* 新增了新的資料庫遷移嚮導,用於指導您完成單個資料庫從 Access 遷[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]移到的遷移過程。
* 添加了新的「轉換、載入」和「遷移」命令,該命令將 Access[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]資料庫轉換 、將轉換的物件[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]載入中,並在一個步驟中將資料遷移到所有。
* 改進了查詢遷移。 查詢遷移現在將更多 SELECT 查詢轉換為檢視。 有關詳細資訊,請參考[轉換資料庫物件](converting-access-database-objects-accesstosql.md)。
* 添加了在[!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]**「表」** 選項卡上編輯表和索引屬性的能力。
* 新增新的全域設定:
  * 您可以選擇在編輯器視窗中顯示行號。
  * 您可以將 SSMA 設定為提示替換重複的物件,或者始終或從不在架構轉換期間替換重複的物件。
* 添加了一個新的轉換選項,用於指定當複雜查詢包含通配符時 SSMA 是否顯示警告。

## <a name="july-2006"></a>2006年7月

2006 年 7 月版本的 SSMA 用於訪問是初始版本。
