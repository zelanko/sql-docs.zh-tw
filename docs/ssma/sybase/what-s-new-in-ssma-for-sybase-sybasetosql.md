---
title: SSMA for SAP ASE 的新功能（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 12/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 094db4e2d374f79e8102d111d0a9f9bfda22e6b7
ms.sourcegitcommit: 26868c8ac3217176b370d972a26d307598a10328
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "74834265"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>SSMA for SAP ASE 的新功能（SybaseToSQL）

本文列出每個版本中 SAP ASE （先前稱為 SSMA for Sybase）變更的 SQL Server 移轉小幫手（SSMA）。

## <a name="ssma-v85"></a>SSMA v 8。5

SSMA for SAP ASE 的第8.5 版已增強，並支援 SQL server 中的 Azure Active Directory 驗證和 JSON 功能的基本支援，以及一組專為改善可用性和效能而設計的目標修正程式。

此外，SSMA for SAP ASE 現在可讓您隱藏系統資料表和視圖（將其排除在轉換之外）。

> [!IMPORTANT]
> 使用 SSMA v 8.5 時，.Net 4.7.2 是必要的安裝。 如果您需要安裝此版本，您可以從[這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v84"></a>SSMA v 8。4

SSMA for SAP ASE 的 v2.0 版本已透過專為處理協助工具問題而設計的目標修正來增強，並修正適用于 SQL Server 2016 和更新版本的最大索引資料行（允許32，而不是16）的相關錯誤。

> [!IMPORTANT]
> 在 SSMA 版本7.4 到8.4 的情況下，.Net 4.5.2 是必要的安裝。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for SAP ASE 的 v 8.3 版本已透過專為改善品質和轉換計量而設計的目標修正來增強。 此外，這一版的 SSMA for SAP ASE 提供了下列修正：

* 解決協助工具問題
* 在 SQL Server 中新增 ' hierarchyid ' 類型的基本支援

## <a name="ssma-v82"></a>SSMA 8。2

SSMA for SAP ASE 的：8.2 版已透過一組目標修正來增強，其設計目的是要改善品質和轉換計量，以及的修正：

* 資料移轉後停用非叢集索引的問題。
* 在無訊息安裝期間偵測 .NET Framework。
* 下載新版本時，會發生間歇性損毀。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA 8.1 到 v4.0 的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA 8。1

SSMA for SAP ASE 的8.1 版已透過專為改善品質和轉換計量而設計的目標修正來增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v4.0 到8.1 版的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA v 8。0

SSMA for SAP ASE 的8.0 版已透過專為改善品質和轉換計量而設計的目標修正來增強。 此外，此版本還提供下列新功能：

* 支援做為目標**Azure SQL Database 受控執行個體**。 您現在可以建立以 Azure SQL Database 受控執行個體為目標的新專案：

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後的**修正建議程式**。 [在這裡](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)深入瞭解。

* 初步的資料庫/架構選擇。

  當連接到來源時，使用者現在可以選取想要的資料庫/架構。 只選取您打算遷移的架構，會在初始連接期間節省時間，並改善整體 SSMA 效能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

SSMA for SAP ASE 的 v3.0 版本已透過專為提供額外安全性和隱私權保護而設計的目標修正來增強，以符合全球需求的變更。

## <a name="ssma-v79"></a>SSMA v 7。9

SSMA for SAP ASE 的 v 7.9 版本包含下列變更：

* 改善品質和轉換計量的目標修正程式。
* 支援 SSMA 命令列來改變資料類型對應和專案喜好設定。
* 支援使用 SQL Server Integration Services （SSIS）來遷移資料。 轉換架構之後，您可以使用滑鼠右鍵內容功能表選項來建立 SSIS 封裝。
* SSMA 中的 [Azure SQL Database 連接] 對話方塊也已更改為指定完整的伺服器名稱。 在舊版的 SSMA 中，必須在專案設定中明確提及 Azure SQL Database 前置詞。

## <a name="ssma-v78"></a>SSMA 7.8 版

SSMA for SAP ASE 的7.8 版包含下列變更：

* 變更 [專案設定] 中反白顯示的類型對應。
* 使用者停用遙測的能力。

## <a name="ssma-v77"></a>SSMA 7。7

SSMA for SAP ASE 的7.7 版包含下列變更：

* SSMA for SAP ASE 已透過改善品質和轉換計量的目標修正來加強。
* 根據熱門需求，適用于 SAP ASE 的32位版本 SSMA 已恢復。 相較于先前的執行（在 v4.0 之前），有兩個安裝程式套件，但無法並存安裝。 因此，您必須根據您擁有的連線元件來選擇最適當的版本。 最好是盡可能使用64位版本。

## <a name="ssma-v76"></a>SSMA v 7。6

SSMA for SAP ASE 的7.6 版包含下列變更：

* 改善品質和轉換計量的目標修正，並支援 SQL Server 2017 （公開預覽）。 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，不應用於生產環境遷移。
* 支援轉換 Sybase 函數。

## <a name="ssma-v75"></a>SSMA v 7。5

SSMA for SAP ASE 的7.5 版（先前稱為 Sybase 的 SSMA）包含下列變更：

* 有數項改良功能可確保更方便殘障人士使用。
* 支援 CREATE 或 REPLACE 語法。

## <a name="ssma-v74"></a>SSMA 7。4

SSMA for Sybase 的7.4 版包含下列變更：

* 在來源和目標的架構物件探索期間，現在可以使用 [**查詢超時**] 選項。

  ![查詢超時選項](../media/query-timeout_red.png)
* 品質和轉換度量已根據客戶的意見反應，以目標修正進行改善。

  > [!IMPORTANT]
  > .Net 4.5.2 是安裝 SSMA 7.4 的必要條件。 此外，從7.4 開始，32位版本的 SSMA 即將中止。  

## <a name="ssma-v73"></a>SSMA 7.3 版

SSMA for Sybase 的7.3 版包含下列變更：

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

SSMA for Sybase 的7.2 版包含下列變更：

* 改善品質和轉換計量，並根據客戶的意見反應進行目標修正。
* 遙測增強功能，可提供更好的資料點來疑難排解客戶問題，並改善 SSMA 的轉換率。

## <a name="ssma-v71"></a>SSMA 7。1

SSMA for Sybase 的7.1 版包含下列變更：

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援的目標平臺，可進行遷移。 這項功能在 technical preview 中，支援以 SQL server 為目標的架構和資料移動。
* 支援自動更新，以在最新版本的 SSMA 可用時立即下載。
* SSMA 可安裝的二進位檔現在會透過 Windows installer 封裝檔案（.msi）傳遞。

## <a name="may-2016"></a>2016 年 5 月

適用于 Sybase 的 SSMA 年5月2016版本包含下列變更：  

* 已新增 SQL Server 2016 的支援。
* 已移除 .Net 2.0 的安裝程式檢查。
* 已將延伸模組套件相依性從 .Net 3.5 更新為 .Net 4.0。
* 已修正 SSMA 主控台的 [儲存專案] 和 [開啟專案] 命令。
* 已修正 SSMA 主控台的 "securepassword" 命令。
* 已修正初始載入物件的計數。
* 已修正全域設定中的 bug。

## <a name="march-2016"></a>2016 年 3 月

SSMA for Sybase 的2016年3月預覽版本新增了遷移至 SQL Server 2016 的支援。  
  
## <a name="january-2016"></a>2016 年 1 月

SSMA for Sybase 的2016年1月維護版本包含下列變更：  
  
* 已將 [查看記錄] 功能表項目新增至 SSMA （RFC 5706203）。  
* 已新增遙測。

## <a name="july-2014"></a>2014年7月

2014年7月版的 SSMA for Sybase 包含下列變更：  
  
* 改良的 Azure SQL DB 程式碼轉換。  
* 已將延伸模組套件功能移至架構，以支援 Azure SQL DB。  
* 已針對具有超過10k 物件的資料庫測試過的效能改進。  
* 新增了處理大量物件的 UI 改良功能。  
* 新增反白顯示「知名的」 LOB 架構的功能（因此可以在轉換時予以忽略）。  
* 已新增轉換速度改進。  
* 已新增在 UI 中顯示物件計數的功能。
* 減少超過25% 的報表大小。  
* 已改善未分析之結構的錯誤訊息。  
  
## <a name="april-2014"></a>2014 年 4 月

2014年4月版的 SSMA for Sybase 包含下列變更：  
  
* 已新增 MS SQL Server 2014 的支援。  
* 已修正關於轉換至 Azure 的 bug。  
* 已修正 IE 10 中不可見報表頁面的相關 bug。  
  
## <a name="january-2012"></a>2012 年 1 月

2012年1月版的 SSMA for Sybase 包含下列變更：  
  
* 已新增復原觸發程式轉換的支援。
* 已提供在同一個@ROWCOUNT SET 語句@ERROR中轉換 @ 和 @ 的修正程式。  
  
## <a name="july-2011"></a>2011 年 7 月

2011年7月版的 SSMA for Sybase 會在資料移轉期間提供改良的錯誤報表。  
  
## <a name="april-2011"></a>2011年4月

2011年4月版的 SSMA for Sybase 包含下列變更：  
  
* 合併「Sybase 的 SSMA」產品，其支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" 和 Azure SQL。  
* 已新增連接和遷移至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" 的支援。  
* 已新增可將 Sybase 資料庫轉換和遷移至 Azure SQL 的新功能。  
* 加強的用戶端資料移轉引擎，支援資料的平行遷移。  
* 使用簡單和大量記錄復原模式來改善資料移轉效能。
* 新增了將區分大小寫的 Sybase 資料庫適當轉換和遷移至區分大小寫 SQL Server 的功能。  
* 已將 Sybase ASE 非 ANSI 聯結語句轉換的支援新增至 SQL Server ANSI 聯結語句，並已擴充至 DELETE 和 UPDATE 語句。  
* 針對使用 Sybase ASE ODBC 提供者和 Sybase ASE ADO.Net 提供者連接到 Sybase ASE 伺服器，提供其他連線選項。
* 已移除另一個名為**SysDB**之資料庫的相依性，其中包含 Sybase 模擬函式（安裝為延伸模組套件的一部分）。
* 已新增在叢集上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝 SSMA For Sybase 延伸模組套件的能力。
* 已新增舊版 SSMA （v4.0 和4.2 版）所建立之專案的回溯相容性。  
* 已新增安裝 SSMA for Sybase v 5.0 產品（SxS）與舊版 SSMA （v4.0 和4.2 版）的功能。  
  
## <a name="july-2010"></a>2010 年 7 月

2010年7月版的 SSMA for Sybase 已加入：

* 支援遷移至 SQL Server 2008 R2。  
* 用於命令列執行的新 SSMA 主控台應用程式。  
* 支援使用伺服器端和用戶端資料移轉引擎來進行資料移轉。  
* 支援資料移轉中的「自訂 SELECT」語句。  
* 支援從 Sybase ASE 15.0.3 版和15.5 進行遷移。  
  
## <a name="june-2008"></a>2008年6月

2008年6月版的 SSMA for Sybase 包含下列變更：  
  
* 已新增 SSMA 測試器，其會自動測試資料庫物件轉換和 SSMA 所進行的資料移轉。 完成所有 SSMA 的遷移步驟之後，請使用 SSMA 測試人員來驗證轉換的物件是否以相同的方式運作，以及是否已正確傳輸所有資料。
* 已新增 SQL 前轉換。 使用者現在可以針對要用於轉換的每個來來源程式，指定臨時表（和其他物件）宣告。
* 已在物件轉換中新增改良功能：  
  * 已修訂聯結轉換。  
  * 不含/group by 子句的匯總和非匯總。  
  * 具有 SELECT INTO 語句的 IDENTITY 函數。  
  * 僅限資料鎖定的叢集條件約束和索引。  
  * 由 SELECT INTO 所建立的臨時表。  
  * 臨時表的條件約束/索引。  
  * 支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]新的2008日期時間類型。  
  * Sybase 15.0 連線性和資料類型支援。  
  
## <a name="may-2007"></a>5月2007

2007年5月發行的 SSMA for Sybase 已加入：  
  
* 儲存專案時，能夠更快速地載入資料庫內容。  
* 支援 SQL Server 格式化的 SQL 模式中的使用者輸入批註。  
* 改進物件轉換。  

## <a name="november-2006"></a>2006年11月

2006年11月版的 SSMA for Sybase 包含下列變更：  
  
* 已新增通用設定：  
  * 您可以選擇在編輯器視窗中顯示行號。  
  * 您可以設定 SSMA，以提示取代重複的物件，或一律或永遠不在架構轉換期間取代重複的物件。  
* 已新增可讓您設定 SSMA 如何處理下列情況的新轉換選項：  
  * 包含二進位字串的 CAST 或 CONVERT 語句。  
  * 檢查相等運算式中的 null 值。  
  * Proxy 資料表。  
  * RAISERROR 的使用者訊息錯誤號碼。  
  * 包含未解析識別碼的 UPDATE 語句。  
* 新增了新的遷移選項，讓您指定 SSMA 應如何處理[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日期範圍外的日期。  
* 已在 [ **sql** ] 索引標籤上新增**格式化的 SQL**設定，其會格式化程式碼以改善可讀性。  
* 錯誤修正，包括：
  * SSMA 現在會轉換 {SHARED | 中的鎖定資料表*資料表*EXCLUSIVE} 模式語句，方法是在資料表的後續 SELECT 查詢中加入 TABLOCK 或 TABLOCKX 提示。  
  * 現在在字元運算式中使用二進位類型時，會新增必要的轉換。  
  * 記憶體和效能改進。  
  
## <a name="july-2006"></a>2006年7月

2006 年 7 月版的 SSMA for Sybase 是最早的版本。  
  
## <a name="see-also"></a>另請參閱

[適用于 Sybase &#40;SybaseToSQL 的 SSMA 消費者入門&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
