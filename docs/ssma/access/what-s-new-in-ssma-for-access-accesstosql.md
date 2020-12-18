---
title: SSMA for Access 的新功能 (AccessToSQL) |Microsoft Docs
description: 瞭解每個版本的 SQL Server 移轉小幫手 (SSMA) 存取 (AccessToSQL) 的變更。
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 12/17/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
ms.author: alexiva
ms.openlocfilehash: 1482ec079e0410fd7713ac183f6181c2a8793a11
ms.sourcegitcommit: a16b98d3bf3eeb58f5d2aeece2464f8a96e2b4a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2020
ms.locfileid: "97665850"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>SSMA for Access 的新功能 (AccessToSQL) 

本文列出每個版本的 SQL Server 移轉小幫手 (SSMA) 存取變更。

## <a name="ssma-v816"></a>SSMA v 8.16

適用于 Access 的 SSMA v 8.16 版本包含下列變更：

* 在 HTML 轉換報表中顯示查詢的 SQL 文字
* 移除舊版剖析器的支援
* 修正無法從資料庫重新整理之物件的問題

## <a name="ssma-v815"></a>SSMA v 8.15

除了許多協助工具改進之外，SSMA for Access 的8.15 版本也包含下列變更：

* 忽略針對外鍵自動建立的索引
* 改造評量報告以在新式瀏覽器中工作
* 使用資料庫提供的授權單位進行 Azure AD authentication
* 改善從檔案載入之語句的命名

## <a name="ssma-v814"></a>SSMA v 8.14

除了許多改進以確保殘障人士能獲得更高的協助工具，8.14 版的 SSMA for Access 需要專案升級，因為它現在會在專案中繼資料中儲存完整的來源/目標伺服器版本。

## <a name="ssma-v813"></a>SSMA v 8.13

適用于 Access 的 SSMA v 8.13 版本包含下列變更：

* 修正 `ORDER BY` 轉換 with `UNION` 子句
* 支援篩選的唯一索引
* 轉換程式和函式呼叫時，請考慮隱含類型轉換

## <a name="ssma-v812"></a>SSMA v 8.12

適用于 Access 的 SSMA v 8.12 版本包含下列變更：

* `BigInt` (`Large Number`) 資料類型的支援
* 改良的資料行類型解析
* 改善資料行驗證規則的轉換
* 使用最新的可用 ACE OLE DB 提供者進行資料移轉

## <a name="ssma-v811"></a>SSMA v 8.11

適用于 Access 的 SSMA v 8.11 版本包含下列變更：

* 使用 MSAL.NET 程式庫進行互動式 Azure Active Directory 驗證

## <a name="ssma-v810"></a>SSMA v 8.10

SSMA for Access 的 v5.2 版本包含次要效能改進和 bug 修正。

## <a name="ssma-v89"></a>SSMA v 8。9

SSMA for Access 的8.9 版本包含下列變更：

* 改進自我參考查詢的轉換
* 修正專案名稱中特殊字元的問題

## <a name="ssma-v88"></a>SSMA v 8。8

SSMA for Access 的8.8% 版本包括：

* SQL Server 物件同步處理穩定性改進
* 評估和轉換期間的 GUI 效能改進
* 全新的存取語法剖析器，以進一步改善轉換效能

## <a name="ssma-v87"></a>SSMA v 8。7

SSMA for Access 的8.7 版本已改善查詢中函式的轉換 `IIF` ，以及圖形化使用者介面中的次要修正和效能改進。

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v86"></a>SSMA v 8。6

除了針對改善可用性和效能而設計的一組目標修正之外，也藉由新增可讓使用者在轉換的程式碼中省略 SSMA 擴充屬性的設定，來增強 SSMA for Access 的 v 8.6 版本。

若要利用這項設定，請在 SSMA 中，流覽至 [**工具**  >  **專案設定**  >  **一般**  >  **轉換**]，然後在 [**其他**] 下，將 [**省略擴充屬性**] 設定的值更新為 **[是]**。

![省略擴充屬性設定](../access/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v85"></a>SSMA v 8。5

SSMA for Access 的8.5 版可透過支援 SQL server 中的 Azure Active Directory authentication 和 JSON 功能的基本支援，以及專為改善可用性和效能而設計的一組目標修正來增強。

此外，SSMA for Access 現在支援將多個標準函式轉換 (`ISNULL` 、等 `IIF` ) 。

> [!IMPORTANT]
> 使用 SSMA v 8.5 時，.NET 4.7.2 是必要的安裝程式。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v84"></a>SSMA v 8。4

SSMA for Access 的8.4 版可利用專為解決協助工具問題而設計的目標修正來修正，並修正與 max index 資料行相關的錯誤 (，以允許 SQL Server 2016 和更新版本的32而非 16) 。

> [!IMPORTANT]
> 使用 SSMA 版本7.4 至8.4，.NET 4.5.2 是必要條件的安裝。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for Access 的 v 8.3 發行版本已利用專為改善品質和轉換度量而設計的目標修正來增強。 此外，此版本的 SSMA for Access 提供下列修正：

* 解決協助工具問題。
* `hierarchyid`在 SQL Server 中加入類型的基本支援。

## <a name="ssma-v82"></a>SSMA v 8。2

SSMA for Access 的8.2 版可利用專為改善品質和轉換度量而設計的目標修正來增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v4.0 至8.2 版的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA v 8。1

SSMA for Access 的8.1 版可利用專為改善品質和轉換度量而設計的目標修正來增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA 8.0 版更新為 v4.0 的失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA 8.0 版

SSMA for Access 的8.0 版可利用專為改善品質和轉換度量而設計的目標修正來增強。 此版本也提供下列新功能：

* 支援以 **AZURE SQL 受控執行個體** 作為目標。 您現在可以建立以 Azure SQL 受控執行個體為目標的新專案：

  ![SQL MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後的 **修正程式**。 若要深入瞭解[，請參閱。](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Accelerate-your-Oracle-migrations-with-new-machine-learning/ba-p/368733)

* 初步的資料庫/架構選取。

    連接到來源時，使用者現在可以選取想要的資料庫/架構。 只選取您打算遷移的架構，可在初始連接期間節省時間，並改善整體 SSMA 效能。

   ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

SSMA for Access 的 v3.0 版本增強了目標修正程式，其設計目的是為了提供額外的安全性和隱私權保護，以符合全球需求的變更。

## <a name="ssma-v79"></a>SSMA v 7。9

SSMA for Access 的 v 7.9 版本包含下列變更：

* 改善品質和轉換度量的目標修正。
* 支援 SSMA 命令列來改變資料類型對應和專案喜好設定。
* SSMA 中的 [Azure SQL Database 連接] 對話方塊也已經改變，以指定完整的伺服器名稱。 在舊版 SSMA 中，必須在專案設定內明確提及 Azure SQL Database 前置詞。

## <a name="ssma-v78"></a>SSMA v 7。8

SSMA for Access 的7.8 版版本包含下列變更：

* 在 [專案設定] 中反白顯示變更類型對應。
* 使用者停用遙測的能力。

## <a name="ssma-v77"></a>SSMA 7。7

SSMA for Access 的7.7 版中包含下列變更：

* 改善品質和轉換度量的目標修正。
* 根據受歡迎的需求，SSMA 的32位版本可供存取。 相較于前一次的執行 (在 7.4) 之前，有兩個安裝程式套件，但無法並存安裝。 因此，您必須根據您擁有的連線元件，選擇最適當的版本。 如果可能的話，最好使用64位版本。

## <a name="ssma-v76"></a>SSMA v 7。6

SSMA for Access 的 v 7.6 版本已透過改善品質和轉換度量的目標修正來增強，並支援 SQL Server 2017 (公開預覽) 。 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，不應該用於生產環境的遷移。

## <a name="ssma-v75"></a>SSMA v 7。5

SSMA for Access 的 v1.0 版本增強了許多改進功能，可確保更適合殘障人士的協助工具。

## <a name="ssma-v74"></a>SSMA 7。4

SSMA for Access 的7.4 版包含下列變更：

* **查詢超時** 選項現在可在來源和目標的架構物件探索期間使用。

  ![query timeout 選項](../media/query-timeout_red.png)

* 根據客戶的意見反應，已改善目標修正的品質和轉換度量。

  > [!IMPORTANT]
  > .NET 4.5.2 是安裝 SSMA 7.4 的先決條件。 此外，從7.4 版開始，32位版本的 SSMA 已中止。

## <a name="ssma-v73"></a>SSMA v 7。3

SSMA for Access 的7.3 版包含下列變更：

* 根據客戶的意見反應，以目標修正改善品質和轉換度量。
* 透過下列專案公開的延伸架構 SSMA：
  * 將功能匯出至 SQL Server Data Tools (SSDT) 專案。
    * 您現在可以將架構腳本從 SSMA 匯出至 SSDT 專案。 您可以使用架構腳本進行額外的架構變更，並部署您的資料庫。

        ![另存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  * SSMA 可使用的程式庫，以執行自訂轉換。
    * 您現在可以建立程式碼，該程式碼可以處理 SSMA 先前未處理的自訂語法轉換和轉換。
      * 如需有關如何建立自訂轉換器的指示，以及用於轉換的範例專案，請前往 [延伸 SQL Server 移轉小幫手的轉換功能](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Extending-SQL-Server-Migration-Assistant-s-conversion/ba-p/1004181)的 blog 文章。

## <a name="ssma-v72"></a>SSMA 7.2 版

SSMA for Access 的7.2 版包含下列變更：

* 根據客戶的意見反應，以目標修正改善品質和轉換度量。
* 遙測增強功能，可提供更好的資料點來對客戶問題進行疑難排解，並改善 SSMA 的轉換率。

## <a name="ssma-v71"></a>SSMA 7。1

SSMA for Access 的7.1 版本包含下列變更：

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援遷移的目標平臺。 這項功能在 technical preview 中，支援以 SQL server 為目標的架構和資料移動。
* SSMA 現在支援自動更新，以在最新版本的 SSMA 可用時立即下載。
* SSMA 可安裝的二進位檔現在會透過 Windows Installer 套件檔案傳遞 ( .msi) 。

## <a name="may-2016"></a>2016 年 5 月

SSMA 的2016版可供存取包含下列變更：

* 已新增 SQL Server 2016 的官方支援。
* 已移除 .NET 2.0 的安裝程式檢查。
* Fixed `save-project` 和 `open-project` SSMA 主控台的命令。
* 已修正 `securepassword` SSMA 主控台的命令。
* 修正初始載入的物件計數。
* 固定的資料表資料載入，用於存取的 UI 索引標籤。
* 修正全域設定中的 bug。

## <a name="march-2016"></a>2016 年 3 月

SSMA for Access 的2016年3月預覽版本新增了遷移至 SQL Server 2016 的支援。

## <a name="january-2016"></a>2016 年 1 月

SSMA for Access 的2016年1月維護版本包含下列變更：

* 修正 (RFC 3894811) 的 GUID 欄位預設為不正確函式。
* 已修正將記錄匯入至 SQL Database (Azure)  (RFC 4919573) 時，系統停止回應的問題。
* 將 View Log 功能表項目新增至 SSMA (RFC 5706203) 。
* 已新增遙測。

## <a name="july-2014"></a>2014 年 7 月

SSMA for Access 的2014年7月版本包含下列變更：

* 改良的 Azure SQL Database 程式碼轉換。
* 已將擴充功能套件功能移至架構，以支援 Azure SQL Database。
* 針對具有超過10k 個物件的資料庫測試效能改進。
* 新增了處理大量物件的 UI 改進。
* 已新增反白顯示「已知」 LOB 架構的支援， (因此可以在轉換) 中忽略。
* 新增轉換速度改進。
* 已新增在 UI 中顯示物件計數的支援。
* 減少超過25% 的報表大小。
* 已改善未剖析之結構的錯誤訊息。

## <a name="april-2014"></a>2014 年 4 月

SSMA for Access 的2014年4月版本包含下列變更：

* 已新增 MS SQL Server 2014 的支援。
* 已修正與轉換至 Azure 相關的錯誤。
* 修正了與 IE 10 中不可見報表頁面相關的 bug。

## <a name="january-2012"></a>2012 年 1 月

SSMA for Access 的2012年1月版本包含下列變更：

* 提供在遷移後不保存 MS Access 連結資料表的使用者名稱和密碼的選項。
* 將迴圈參考的串聯動作設定為無動作。
* 提供適當的訊息，指出迴圈參考的串聯動作已設定為沒有動作。

## <a name="july-2011"></a>2011 年 7 月

SSMA for Access 的2011年7月版本會在資料移轉期間新增改良的錯誤報表。

## <a name="april-2011"></a>2011年4月

SSMA for Access 的2011年4月版本包含下列變更：

* 新增了一個可安裝的「SSMA for Access」，其 [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] 支援 [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] 、 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 和 Azure SQL。
* 已新增連接至的能力 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 。
* 已新增 SSMA 以取得存取主控台版本的回溯相容性支援。 您可以開啟之前版本所建立的專案至 SSMA v 5.0。
* 已新增將 SSMA 5.0 版產品與舊版 SSMA 產品並存安裝 (SxS) 的功能。

## <a name="july-2010"></a>2010 年 7 月

SSMA for Access 的2010年7月版本包含下列變更：

* 已新增遷移至 SQL Server 2008 R2 和 Azure SQL 的支援。
* 將安全連線新增至 SQL Server 和 Azure SQL。
* 已新增存取2010資料庫的支援。
* 已新增新的 SSMA 主控台應用程式以進行命令列執行。
* 已新增 SQL Server `DateTime2` 資料類型的支援。

## <a name="june-2008"></a>2008年6月

2008年6月發行的 SSMA for Access 新增了存取2007資料庫的支援。

## <a name="may-2007"></a>5月2007

SSMA 的2007版可供存取包含下列變更：

* 已新增使用工作組原則之 Access 資料庫的支援。
* 提供從 SQL Server metadata explorer 刪除已轉換物件的功能。
* 在 SQL Server 格式化的 SQL 模式中新增使用者輸入批註的支援。
* 新增物件轉換的增強功能。

## <a name="november-2006"></a>2006年11月

SSMA for Access 的2006年11月版本包含下列變更：

* 加入新的資料庫移轉嚮導，引導您將單一資料庫從存取權遷移至 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] 。
* 加入新的轉換、載入和遷移命令，可轉換 Access 資料庫、將轉換的物件載入 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] ，並 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] 在一個步驟中將資料移轉至全部。
* 改進的查詢遷移。 查詢遷移現在會將更多的選取查詢轉換成 views。 如需詳細資訊，請參閱 [轉換 Access 資料庫物件](converting-access-database-objects-accesstosql.md)。
* 新增在 [資料表] 索引標籤上編輯資料表和索引屬性的功能 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)]  。
* 新增通用設定：
  * 您可以選擇在編輯器視窗中顯示行號。
  * 您可以設定 SSMA 以提示取代重複的物件，或在架構轉換期間一律或永遠取代重複的物件。
* 加入新的轉換選項，可讓您指定當複雜查詢包含萬用字元時，SSMA 是否會顯示警告。

## <a name="july-2006"></a>2006年7月

SSMA for Access 的2006年7月版本是初始發行版本。
