---
title: SSMA for Access 的新功能（AccessToSQL） |Microsoft Docs
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/27/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
ms.author: jtoland;alexiva
ms.openlocfilehash: e1bc77c0fac3698d7d36ebfb47dde547d475142e
ms.sourcegitcommit: 9afb612c5303d24b514cb8dba941d05c88f0ca90
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2020
ms.locfileid: "82220253"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>SSMA for Access 的新功能（AccessToSQL）

本文列出每個版本中的存取變更 SQL Server 移轉小幫手（SSMA）。

## <a name="ssma-v89"></a>SSMA v 8。9

SSMA for Access 的 v 8.9 版本包含下列變更：

* 改善自我參考查詢的轉換
* 修正專案名稱中特殊字元的問題

## <a name="ssma-v88"></a>SSMA v 8。8

SSMA for Access 的 v 8.8 版本包括：

* SQL Server 物件同步處理穩定性改善
* 在評定和轉換期間的 GUI 效能改進
* 全新的存取語法剖析器，以進一步改善轉換效能

## <a name="ssma-v87"></a>SSMA v 8。7

SSMA for Access 的8.7 版本已改善查詢中函式的轉換 `IIF` ，以及圖形化使用者介面中的次要修正和效能改進。

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝此版本，您可以從[這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v86"></a>SSMA v 8。6

除了為了改善可用性和效能而設計的一組目標修正程式之外，也新增了可讓使用者在轉換後的程式碼中省略 SSMA 擴充屬性的設定，以增強 SSMA for Access 的 v 8.6 版本。

若要利用這項設定，請在 SSMA 中，流覽至 [**工具**  >  ] [**專案設定**]  >  **[一般**  >  **轉換**]，然後在 [**其他**] 下，將 [**省略擴充屬性**] 設定的值更新為 **[是]**。

![省略擴充屬性設定](../access/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝此版本，您可以從[這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v85"></a>SSMA v 8。5

SSMA for Access 的第8.5 版已增強，並支援 SQL server 中的 Azure Active Directory 驗證和 JSON 功能的基本支援，以及一組專為改善可用性和效能而設計的目標修正程式。

此外，SSMA for Access 現在支援轉換多個標準函式（ `ISNULL` 、 `IIF` 等）。

> [!IMPORTANT]
> 使用 SSMA v 8.5 時，.NET 4.7.2 是必要的安裝。 如果您需要安裝此版本，您可以從[這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v84"></a>SSMA v 8。4

SSMA for Access 的 v2.0 版本增強了目標修正程式，其設計目的是為了解決協助工具問題，並修正與最大索引資料行（允許32，而不是16）有關 SQL Server 2016 和更新版本的錯誤。

> [!IMPORTANT]
> 透過8.4 的 SSMA 版本7.4，.NET 4.5.2 是必要的安裝。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for Access 的 v 8.3 版本已透過專為改善品質和轉換計量而設計的目標修正來增強。 此外，這一版的 SSMA for Access 會提供下列修正：

* 解決協助工具問題。
* `hierarchyid`在 SQL Server 中新增類型的基本支援。

## <a name="ssma-v82"></a>SSMA 8。2

SSMA for Access 的8.2 版已透過專為改善品質和轉換計量而設計的目標修正來增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA 8.1 到 v4.0 的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA 8。1

SSMA for Access 的8.1 版已透過專為改善品質和轉換計量而設計的目標修正來增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v4.0 到8.1 版的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA v 8。0

SSMA for Access 的8.0 版已透過專為改善品質和轉換計量而設計的目標修正來增強。 此版本也提供下列新功能：

* 支援做為目標**Azure SQL Database 受控執行個體**。 您現在可以建立以 Azure SQL Database 受控執行個體為目標的新專案：

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後的**修正建議程式**。 [在這裡](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Accelerate-your-Oracle-migrations-with-new-machine-learning/ba-p/368733)深入瞭解。

* 初步的資料庫/架構選擇。

    當連接到來源時，使用者現在可以選取想要的資料庫/架構。 只選取您打算遷移的架構，會在初始連接期間節省時間，並改善整體 SSMA 效能。

   ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

SSMA for Access 的 v 7.10 版本已增強，其目標修正旨在提供額外的安全性和隱私權保護，以符合全球需求的變更。

## <a name="ssma-v79"></a>SSMA v 7。9

SSMA for Access 的 v 7.9 版本包含下列變更：

* 改善品質和轉換計量的目標修正程式。
* 支援 SSMA 命令列來改變資料類型對應和專案喜好設定。
* SSMA 中的 [Azure SQL Database 連接] 對話方塊也已更改為指定完整的伺服器名稱。 在舊版的 SSMA 中，必須在專案設定中明確提及 Azure SQL Database 前置詞。

## <a name="ssma-v78"></a>SSMA 7.8 版

Access 的 SSMA 的7.8 版包含下列變更：

* 變更 [專案設定] 中反白顯示的類型對應。
* 使用者停用遙測的能力。

## <a name="ssma-v77"></a>SSMA 7。7

SSMA for Access 的7.7 版包含下列變更：

* 改善品質和轉換計量的目標修正程式。
* 根據受歡迎的需求，32位版本的 SSMA 可供存取。 相較于先前的執行（在7.4 之前），有兩個安裝程式套件，但無法並存安裝。 因此，您必須根據您擁有的連線元件來選擇最適當的版本。 最好是盡可能使用64位版本。

## <a name="ssma-v76"></a>SSMA v 7。6

SSMA for Access 的7.6 版已藉由改善品質和轉換計量，以及支援 SQL Server 2017 （公開預覽）的目標修正來增強。 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，不應用於生產環境遷移。

## <a name="ssma-v75"></a>SSMA v 7。5

SSMA for Access 的7.5 版已增強了數項改良功能，以確保更方便殘障人士使用。

## <a name="ssma-v74"></a>SSMA 7。4

SSMA for Access 的7.4 版包含下列變更：

* 在來源和目標的架構物件探索期間，現在可以使用 [**查詢超時**] 選項。

  ![查詢超時選項](../media/query-timeout_red.png)

* 品質和轉換度量已根據客戶的意見反應，以目標修正進行改善。

  > [!IMPORTANT]
  > .NET 4.5.2 是安裝 SSMA 7.4 的必要條件。 此外，從7.4 版開始，已停止32位版本的 SSMA。

## <a name="ssma-v73"></a>SSMA 7.3 版

SSMA for Access 的7.3 版包含下列變更：

* 改善品質和轉換計量，並根據客戶的意見反應進行目標修正。
* 透過下列專案公開的 SSMA 擴充性架構：
  * 將功能匯出至 SQL Server Data Tools （SSDT）專案。
    * 您現在可以將架構腳本從 SSMA 匯出至 SSDT 專案。 您可以使用架構腳本來進行其他架構變更，並部署您的資料庫。

        ![另存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  * 可供 SSMA 用來執行自訂轉換的程式庫。
    * 您現在可以建立可處理自訂語法轉換的程式碼，以及 SSMA 先前未處理的轉換。
      * 如需有關如何建立自訂轉換器的指示，以及用於轉換的範例專案，請前往[延伸 SQL Server 移轉小幫手的轉換功能](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Extending-SQL-Server-Migration-Assistant-s-conversion/ba-p/1004181)的 blog 文章。

## <a name="ssma-v72"></a>SSMA 7.2 版

SSMA for Access 的7.2 版包含下列變更：

* 改善品質和轉換計量，並根據客戶的意見反應進行目標修正。
* 遙測增強功能，可提供更好的資料點來疑難排解客戶問題，並改善 SSMA 的轉換率。

## <a name="ssma-v71"></a>SSMA 7。1

SSMA for Access 的7.1 版包含下列變更：

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援的目標平臺，可進行遷移。 這項功能在 technical preview 中，支援以 SQL server 為目標的架構和資料移動。
* SSMA 現在支援自動更新，以在最新版本的 SSMA 推出時立即下載。
* SSMA 可安裝的二進位檔現在會透過 Windows Installer 套件檔案（.msi）傳遞。

## <a name="may-2016"></a>2016 年 5 月

SSMA for Access 的2016年5月發行版本包含下列變更：

* 已新增 SQL Server 2016 的正式支援。
* 已移除 .NET 2.0 的安裝程式檢查。
* 已 `save-project` 修正 `open-project` SSMA 主控台的命令。
* 已修正 `securepassword` SSMA 主控台的命令。
* 已修正初始載入物件的計數。
* 已修正用於存取的 UI 索引標籤的資料表資料載入。
* 已修正全域設定中的 bug。

## <a name="march-2016"></a>2016 年 3 月

SSMA for Access 的2016年3月預覽版本將支援遷移至 SQL Server 2016。

## <a name="january-2016"></a>2016 年 1 月

SSMA for Access 的2016年1月維護版本包含下列變更：

* 已修正 GUID 欄位的預設無效函式（RFC 3894811）。
* 已修正將記錄匯入至 SQL Database （Azure）（RFC 4919573）時停止回應的問題。
* 已將 [查看記錄] 功能表項目新增至 SSMA （RFC 5706203）。
* 已新增遙測。

## <a name="july-2014"></a>2014 年 7 月

2014年7月發行的 SSMA for Access 包含下列變更：

* 改良的 Azure SQL DB 程式碼轉換。
* 已將延伸模組套件功能移至架構，以支援 Azure SQL DB。
* 已針對具有超過10k 物件的資料庫測試效能改進。
* 新增了處理大量物件的 UI 改良功能。
* 新增反白顯示「已知的」 LOB 架構的支援（以便在轉換時予以忽略）。
* 已新增轉換速度改進。
* 已新增在 UI 中顯示物件計數的支援。
* 減少超過25% 的報表大小。
* 已改善未分析之結構的錯誤訊息。

## <a name="april-2014"></a>2014 年 4 月

2014年4月發行的 SSMA for Access 包含下列變更：

* 已新增 MS SQL Server 2014 的支援。
* 已修正與轉換至 Azure 相關的 bug。
* 已修正 IE 10 中與隱藏報表頁面相關的錯誤。

## <a name="january-2012"></a>2012 年 1 月

SSMA for Access 的2012年1月版本包含下列變更：

* 提供了在遷移之後，不保存 MS Access 連結資料表之使用者名稱和密碼的選項。
* 將迴圈參考的 cascade 動作設定為 [無動作]。
* 提供適當的訊息，指出迴圈參考的串聯動作已設定為 [無動作]。

## <a name="july-2011"></a>2011 年 7 月

2011年7月發行的 SSMA for Access 在資料移轉期間加入了改良的錯誤報表。

## <a name="april-2011"></a>2011年4月

2011年4月發行的 SSMA for Access 包含下列變更：

* 已新增可供存取的「SSMA for Access」的單一安裝，其支援 [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] 、 [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 和 Azure SQL。
* 已新增連接到的能力 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 。
* 已新增 SSMA，以取得回溯相容性的 Access 主控台版本支援。 您可以開啟先前版本所建立的專案，以 SSMA 5.0 版。
* 新增了將 SSMA v 5.0 產品與舊版 SSMA 產品並存安裝的能力（SxS）。

## <a name="july-2010"></a>2010 年 7 月

2010年7月發行的 SSMA for Access 包含下列變更：

* 已新增遷移至 SQL Server 2008 R2 和 Azure SQL 的支援。
* 已將安全連線新增至 SQL Server 和 Azure SQL。
* 已新增存取2010資料庫的支援。
* 已新增新的 SSMA 主控台應用程式來執行命令列。
* 已新增 SQL Server `DateTime2` 資料類型的支援。

## <a name="june-2008"></a>2008年6月

2008年6月版的 SSMA for Access 新增了存取2007資料庫的支援。

## <a name="may-2007"></a>5月2007

SSMA for Access 的2007年5月發行版本包含下列變更：

* 已新增使用工作組原則之 Access 資料庫的支援。
* 提供從 SQL Server 的中繼資料瀏覽器刪除已轉換物件的功能。
* 已在 SQL Server 格式化的 SQL 模式中新增使用者輸入批註的支援。
* 已在物件轉換中新增改良功能。

## <a name="november-2006"></a>2006年11月

2006年11月發行的 SSMA for Access 包含下列變更：

* 新增了新的資料庫移轉嚮導，引導您將單一資料庫從的存取權遷移到 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] 。
* 新增了新的轉換、載入和遷移命令，以轉換 Access 資料庫、將轉換的物件載入 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] ，並 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] 在一個步驟中將資料移轉至全部。
* 改良的查詢遷移。 查詢遷移現在會將更多的 SELECT 查詢轉換成 views。 如需詳細資訊，請參閱[轉換 Access 資料庫物件](converting-access-database-objects-accesstosql.md)。
* 已在 [資料表] 索引標籤上新增編輯資料表和索引屬性的功能 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] **Table** 。
* 已新增通用設定：
  * 您可以選擇在編輯器視窗中顯示行號。
  * 您可以設定 SSMA，以提示取代重複的物件，或一律或永遠不在架構轉換期間取代重複的物件。
* 已加入新的轉換選項，可讓您指定當複雜查詢包含萬用字元時，SSMA 是否會顯示警告。

## <a name="july-2006"></a>2006年7月

2006年7月發行的 SSMA for Access 是初始版本。
