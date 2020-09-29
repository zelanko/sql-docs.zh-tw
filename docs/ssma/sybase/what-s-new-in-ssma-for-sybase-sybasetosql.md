---
title: 適用于 SAP ASE 的 SSMA 新功能 (SybaseToSQL) |Microsoft Docs
description: 瞭解針對每個版本的 Sybase (SybaseToSQL) SQL Server 移轉小幫手 (SSMA) 的變更。
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 9/28/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
ms.author: alexiva
ms.openlocfilehash: fdbe37ddb915e64c5f947a64078e574a8eed8bbd
ms.sourcegitcommit: b93beb4f03aee2c1971909cb1d15f79cd479a35c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/29/2020
ms.locfileid: "91497792"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>適用于 SAP ASE 的 SSMA 新功能 (SybaseToSQL) 

本文列出適用于 SAP ASE 的 SQL Server 移轉小幫手 (SSMA)  (先前針對 Sybase) 每個版本中變更的 SSMA。

## <a name="ssma-v814"></a>SSMA v 8.14

除了許多改進以確保殘障人士能獲得更高的協助工具，8.14 版的 SSMA for SAP ASE 需要專案升級，因為它現在會在專案中繼資料中儲存完整的來源/目標伺服器版本。

## <a name="ssma-v813"></a>SSMA v 8.13

適用于 SAP ASE 的 SSMA v 8.13 版包含下列變更：

* 轉換程式和函式呼叫時，請考慮隱含類型轉換
* 改善來源連接字串的記錄，以協助疑難排解連接問題

## <a name="ssma-v812"></a>SSMA v 8.12

適用于 SAP ASE 的 SSMA 8.12 版包含較小的效能改進和 bug 修正。

## <a name="ssma-v811"></a>SSMA v 8.11

適用于 SAP ASE 的 SSMA v 8.11 版包含下列變更：

* 修正臨時表的轉換
* 使用 MSAL.NET 程式庫進行互動式 Azure Active Directory 驗證

## <a name="ssma-v810"></a>SSMA v 8.10

適用于 SAP ASE 的 SSMA v4.0 版本包含次要效能改進和 bug 修正。

## <a name="ssma-v89"></a>SSMA v 8。9

SSMA for SAP ASE 的8.9 版包含下列變更：

* 改善日期和時間格式轉換
* 修正物件的 SQL 定義中遺失字元的問題

## <a name="ssma-v88"></a>SSMA v 8。8

適用于 SAP ASE 的 SSMA 8.8 版包含：

* SQL Server 物件同步處理穩定性改進
* 評估和轉換期間的 GUI 效能改進
* 修正物件的 SQL 定義中遺失字元的問題

## <a name="ssma-v87"></a>SSMA v 8。7

SSMA for SAP ASE 的8.7 版本在圖形化使用者介面中有輕微的修正和效能改進。

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v86"></a>SSMA v 8。6

除了針對改善可用性和效能而設計的一組目標修正之外，也藉由新增可讓使用者在轉換的程式碼中省略 SSMA 擴充屬性的設定，來增強 SSMA for SAP ASE 的 v 8.6 版本。

若要利用這項設定，請在 SSMA for SAP ASE 中，流覽至 [**工具**  >  **專案設定**  >  **一般**  >  **轉換**]，然後在 [**其他**] 下，將 [**省略擴充屬性**] 設定的值更新為 **[是]**。

![省略擴充屬性設定](../sybase/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v85"></a>SSMA v 8。5

適用于 SAP ASE 的 SSMA 8.5 版已透過支援 SQL server 中的 Azure Active Directory authentication 和 JSON 功能的基本支援來增強，並提供一組目標修正程式，其設計目的是要改善可用性和效能。

此外，SSMA for SAP ASE 現在可讓您隱藏系統資料表和 views， (將它們排除在轉換) 之外。

> [!IMPORTANT]
> 使用 SSMA v 8.5 時，.NET 4.7.2 是必要的安裝程式。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v84"></a>SSMA v 8。4

適用于 SAP ASE 的 SSMA 8.4 版已增強目標修正程式，其設計目的是要解決協助工具問題，並修正與最大索引資料行相關的錯誤 (以允許32（而非 16) SQL Server 2016 和更新版本）。

> [!IMPORTANT]
> 在 SSMA 7.4 至8.4 版中，.NET 4.5.2 是必要的安裝。

## <a name="ssma-v83"></a>SSMA v 8。3

適用于 SAP ASE 的 SSMA （8.3 版）已增強目標修正程式，其設計目的是要改善品質和轉換度量。 此外，此版本的 SSMA for SAP ASE 提供下列修正：

* 解決存取範圍問題
* `hierarchyid`在 SQL Server 中新增類型的基本支援

## <a name="ssma-v82"></a>SSMA v 8。2

適用于 SAP ASE 的 SSMA 8.2 版已增強，並提供一組目標修正程式，其設計目的是要改善品質和轉換度量，以及下列各項的修正：

* 資料移轉後停用非叢集索引的問題。
* 無訊息安裝期間的 .NET Framework 偵測。
* 下載新版本時所發生的間歇性損毀。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v4.0 至8.2 版的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA v 8。1

適用于 SAP ASE 的 SSMA 8.1 版已增強目標修正程式，其設計目的是要改善品質和轉換度量。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA 8.0 版更新為 v4.0 的失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA 8.0 版

適用于 SAP ASE 的 SSMA 8.0 版已增強目標修正程式，其設計目的是為了改善品質和轉換度量。 此外，此版本還提供下列新功能：

* 支援以 **AZURE SQL 受控執行個體** 作為目標。 您現在可以建立以 Azure SQL 受控執行個體為目標的新專案：

  ![SQL Database MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後的 **修正程式**。 若要深入瞭解[，請參閱。](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 初步的資料庫/架構選取。

  連接到來源時，使用者現在可以選取想要的資料庫/架構。 只選取您打算遷移的架構，可在初始連接期間節省時間，並改善整體 SSMA 效能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

適用于 SAP ASE 的 SSMA，已增強目標修正程式，其設計目的是為了提供額外的安全性和隱私權保護，以符合全球需求的變更。

## <a name="ssma-v79"></a>SSMA v 7。9

適用于 SAP ASE 的 SSMA 的 v 7.9 版本包含下列變更：

* 改善品質和轉換度量的目標修正。
* 支援 SSMA 命令列來改變資料類型對應和專案喜好設定。
* 支援使用 SQL Server Integration Services (SSIS) 來遷移資料。 轉換架構之後，您可以使用滑鼠右鍵內容功能表選項來建立 SSIS 封裝。
* SSMA 中的 [Azure SQL Database 連接] 對話方塊也已經改變，以指定完整的伺服器名稱。 在舊版 SSMA 中，必須在專案設定內明確提及 Azure SQL Database 前置詞。

## <a name="ssma-v78"></a>SSMA v 7。8

適用于 SAP ASE 的 SSMA 7.8 版包含下列變更：

* 在 [ **專案設定**] 中反白顯示變更類型對應。
* 使用者停用遙測的能力。

## <a name="ssma-v77"></a>SSMA 7。7

SSMA for SAP ASE 的7.7 版包含下列變更：

* 適用于 SAP ASE 的 SSMA 已透過可改善品質和轉換度量的目標修正來增強。
* 根據熱門需求，適用于 SAP ASE 的32位版本 SSMA 已恢復。 相較于先前的實施 (在7.4 版之前) ，有兩個安裝程式套件，但無法並存安裝。 因此，您必須根據您擁有的連線元件，選擇最適當的版本。 如果可能的話，最好使用64位版本。

## <a name="ssma-v76"></a>SSMA v 7。6

適用于 SAP ASE 的 SSMA v 7.6 版包含下列變更：

* 改善品質和轉換度量以及支援 SQL Server 2017 (公開預覽) 的目標修正。 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，不應該用於生產環境的遷移。
* 支援 Sybase 函數的轉換。

## <a name="ssma-v75"></a>SSMA v 7。5

適用于 SAP ASE 的 SSMA 7.5 版 (先前針對 Sybase) 的 SSMA 包含下列變更：

* 有幾項改良功能，可確保更適合殘障人士的協助工具。
* 語法的支援 `CREATE OR REPLACE` 。

## <a name="ssma-v74"></a>SSMA 7。4

SSMA for Sybase 的7.4 版包含下列變更：

* **查詢超時**選項現在可在來源和目標的架構物件探索期間使用。

  ![query timeout 選項](../media/query-timeout_red.png)
* 根據客戶的意見反應，已改善目標修正的品質和轉換度量。

  > [!IMPORTANT]
  > .NET 4.5.2 是安裝 SSMA 7.4 的先決條件。 此外，從 v4.0 開始，32位版本的 SSMA 將會中止。

## <a name="ssma-v73"></a>SSMA v 7。3

SSMA for Sybase 的7.3 版包含下列變更：

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

SSMA for Sybase 的7.2 版包含下列變更：

* 根據客戶的意見反應，以目標修正改善品質和轉換度量。
* 遙測增強功能，可提供更好的資料點來對客戶問題進行疑難排解，並改善 SSMA 的轉換率。

## <a name="ssma-v71"></a>SSMA 7。1

SSMA for Sybase 的7.1 版包含下列變更：

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援遷移的目標平臺。 這項功能在 technical preview 中，支援以 SQL server 為目標的架構和資料移動。
* 支援自動更新，以便在最新版的 SSMA 可供使用時立即下載。
* SSMA 可安裝的二進位檔現在會透過 Windows Installer 套件檔案傳遞 ( .msi) 。

## <a name="may-2016"></a>2016 年 5 月

SSMA for Sybase 的2016版可能包含下列變更：

* 已新增 SQL Server 2016 的支援。
* 已移除 .NET 2.0 的安裝程式檢查。
* 已將延伸模組套件相依性從 .NET 3.5 更新為 .NET 4.0。
* Fixed `save-project` 和 `open-project` SSMA 主控台的命令。
* 已修正 `securepassword` SSMA 主控台的命令。
* 修正初始載入的物件計數。
* 修正全域設定中的 bug。

## <a name="march-2016"></a>2016 年 3 月

SSMA for Sybase 的2016年3月預覽版本新增了遷移至 SQL Server 2016 的支援。

## <a name="january-2016"></a>2016 年 1 月

SSMA for Sybase 的2016年1月維護版本包含下列變更：

* 將 View Log 功能表項目新增至 SSMA (RFC 5706203) 。
* 已新增遙測。

## <a name="july-2014"></a>2014 年 7 月

SSMA for Sybase 的2014年7月版本包含下列變更：

* 改良的 Azure SQL Database 程式碼轉換。
* 已將擴充功能套件功能移至架構，以支援 Azure SQL Database。
* 針對具有超過1萬個物件的資料庫，增加了測試的效能改進。
* 新增了處理大量物件的 UI 改進。
* 新增了醒目提示已知 LOB 架構 (的功能，因此可以在轉換) 中忽略它們。
* 新增轉換速度改進。
* 新增了在 UI 中顯示物件計數的功能。
* 減少超過25% 的報表大小。
* 已改善未剖析之結構的錯誤訊息。

## <a name="april-2014"></a>2014 年 4 月

SSMA for Sybase 的2014年4月版本包含下列變更：

* 已新增 MS SQL Server 2014 的支援。
* 已修正有關轉換至 Azure 的 bug。
* 修正 IE 10 中有關不可見報表頁面的錯誤。

## <a name="january-2012"></a>2012 年 1 月

SSMA for Sybase 的2012年1月版本包含下列變更：

* 已新增復原觸發程式轉換的支援。
* 提供 `@@ROWCOUNT` `@@ERROR` 在相同的語句中轉換和的修正 `SET` 。

## <a name="july-2011"></a>2011 年 7 月

SSMA for Sybase 的2011年7月版本可在資料移轉期間提供改進的錯誤報表。

## <a name="april-2011"></a>2011年4月

SSMA for Sybase 的2011年4月版本包含下列變更：

* 合併「適用于 Sybase 的 SSMA」產品，可支援 [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] 、 [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] [!INCLUDE [ssSQL11](../../includes/ssSQL11-md.md)] 和 Azure SQL。
* 已新增連接和遷移至的支援 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 。
* 新增了一項新功能，可將 Sybase 資料庫轉換和遷移至 Azure SQL。
* 增強的用戶端資料移轉引擎，支援平行的資料移轉。
* 使用簡單和大量記錄復原模式來改善資料移轉效能。
* 已新增適當的功能，可將區分大小寫的 Sybase 資料庫正確轉換和遷移至區分大小寫的 SQL Server。
* 已將 Sybase ASE 非 ANSI 聯結語句的轉換支援新增至 SQL Server 的 ANSI 聯結語句已擴充至 DELETE 和 UPDATE 語句。
* 提供使用 Sybase ASE ODBC 提供者和 Sybase ASE ADO.NET 提供者連接到 Sybase ASE 伺服器的其他連接選項。
* 移除另一個資料庫的相依性 `SysDB` ，其中包含 (安裝為擴充功能套件) 一部分的 Sybase 模擬函數。
* 已新增在叢集上安裝 SSMA for Sybase 擴充功能的功能 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] 。
* 已為舊版 SSMA 所建立的專案提供回溯相容性 (v4.0 和4.2 版) 。
* 新增了一項功能，可安裝 SSMA for Sybase 5.0 版產品並存 (SxS) 舊版的 SSMA (v4.0 和4.2 版) 。

## <a name="july-2010"></a>2010 年 7 月

SSMA for Sybase 的2010年7月版本已新增：

* 支援遷移至 SQL Server 2008 R2。
* 用於命令列執行的新 SSMA 主控台應用程式。
* 支援使用伺服器端和用戶端資料移轉引擎進行資料移轉。
* 在資料移轉中支援「自訂 SELECT」語句。
* 支援從 Sybase ASE 15.0.3 版和15.5 進行遷移。

## <a name="june-2008"></a>2008年6月

SSMA for Sybase 的2008年6月版本包含下列變更：

* 已新增 SSMA 測試人員，其會自動測試資料庫物件轉換和 SSMA 所進行的資料移轉。 所有 SSMA 的遷移步驟都完成後，請使用 SSMA 測試人員確認轉換的物件以相同方式運作，而且所有資料都已正確傳輸。
* 已新增 SQL 之前的轉換。 使用者現在可以為每個要在轉換中使用的來來源程式，指定臨時表 (和其他物件) 宣告。
* 新增物件轉換的增強功能：
  * 已修訂聯結轉換。
  * 不含/group by 子句的匯總和非匯總。
  * 具有語句的函式 `IDENTITY` `SELECT INTO` 。
  * 僅限資料鎖定的叢集條件約束和索引。
  * 所建立的臨時表 `SELECT INTO` 。
  * 臨時表的條件約束/索引。
  * [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]支援新的日期時間類型。
  * Sybase 15.0 連線能力和資料類型支援。

## <a name="may-2007"></a>5月2007

適用于 Sybase 的 SSMA 2007 版可能已新增：

* 儲存專案時，能夠更快速地載入資料庫內容。
* 在 SQL Server 格式化的 SQL 模式下支援使用者輸入的批註。
* 改進物件轉換。

## <a name="november-2006"></a>2006年11月

SSMA for Sybase 的2006年11月版本包含下列變更：

* 新增通用設定：
  * 您可以選擇在編輯器視窗中顯示行號。
  * 您可以設定 SSMA 以提示取代重複的物件，或在架構轉換期間一律或永遠取代重複的物件。
* 加入新的轉換選項，可讓您設定 SSMA 處理下列情況的方式：
  * `CAST` `CONVERT` 包含二進位字串的或語句。
  * 檢查相等運算式中是否有 null 值。
  * Proxy 資料表。
  * 的使用者訊息錯誤號碼 `RAISERROR` 。
  * `UPDATE` 包含未解析識別碼的語句。
* 已加入新的遷移選項，可讓您指定 SSMA 處理日期範圍之外之日期的方式 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] 。
* 在 [ **sql** ] 索引標籤上新增**格式化的 sql**設定，以將程式碼格式化以改善可讀性。
* Bug 修正，包括：
  * SSMA 現在會在 `LOCK TABLE <table> IN { SHARED | EXCLUSIVE } MODE` `TABLOCK` 資料表的 `TABLOCKX` 後續查詢中加入或提示，以轉換語句 `SELECT` 。
  * 在字元運算式中使用二進位類型時，現在會新增必要的轉換。
  * 記憶體和效能改善。

## <a name="july-2006"></a>2006年7月

2006 年 7 月版的 SSMA for Sybase 是最早的版本。

## <a name="see-also"></a>另請參閱

[消費者入門適用于 Sybase &#40;SybaseToSQL&#41;的 SSMA ](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
