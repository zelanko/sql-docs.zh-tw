---
title: 安裝 SQL Server 文件以離線檢視
description: 了解如何安裝 SQL Server 2019、2017、2016、2014 與 2012 的離線文件。 使用 SQL Server Management Studio (SSMS) 來檢視離線內容。
ms.prod: sql
ms.technology: install
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: markingmyname
ms.author: maghan
ms.date: 08/12/2020
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017'
ms.openlocfilehash: 5af6eff12d81ea028247f146842d3a5eed0e2eba
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97409724"
---
# <a name="install-sql-server-documentation-to-view-offline-in-ssms"></a>安裝 SQL Server 文件以在 SSMS 中離線檢視

[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

此文章說明如何在 [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) 中下載及檢視離線 SQL Server 內容。 離線內容可讓您在沒有網際網路連線的情況下存取文件 (但是一開始需要網際網路連線來下載文件)。

離線文件適用於 SQL Server 2012 版及更新版本。 雖然您可[線上檢視舊版內容](/previous-versions/sql/)，但離線選項提供一種存取舊版內容的便利方式。

- [SQL Server 2016 及更新版本](#sql-server-2016-and-later-offline-content)
- [SQL Server 2014](#sql-server-2014-offline-content)
- [SQL Server 2012](#sql-server-2012-offline-content)

## <a name="sql-server-2016-and-later-offline-content"></a>SQL Server 2016 及更新版本的離線內容

下列步驟說明如何載入 SQL Server 2016 及更新版本的離線內容。

1. 在 SSMS 中，選取 [說明] 功能表上的 [加入和移除說明內容]。

   ![新增和移除說明內容](../sql-server/media/sql-server-offline-documentation/add-remove-content.png)

   說明檢視器會開啟至 [管理內容] 索引標籤。

2. 若要尋找 SQL Server 2016 及更新版本的最新說明內容，請在 [管理內容] 索引標籤底下的 [安裝來源] 下選擇 [線上]，然後在搜尋列中輸入 *SQL Server*。

   ![SQL Server 叢書搜尋](../sql-server/media/sql-server-offline-documentation/sql-online-search.png)

   > [!Note]
   > [管理內容] 索引標籤上的 [本機存放區路徑] 會顯示內容在本機電腦上的安裝位置。 若要變更位置，請選取 [移動]，並在 [到] 欄位中輸入不同資料夾路徑，然後選取 [確定]。 如果在變更本機存放區路徑後，說明安裝失敗，請關閉並重新開啟 [說明檢視器]。 請確定新的位置出現在本機存放區路徑中，然後再次嘗試安裝。

3. 若要安裝 SQL Server 2016 及更新版本的最新說明內容，請選取所要安裝其每個內容套件 (書籍) 旁邊的 [新增]，然後選取右下方的 [更新]。

   ![SQL Server 線上叢書新增與更新](../sql-server/media/sql-server-offline-documentation/sql-add-update.png)

   > [!NOTE]
   > 如果說明檢視器在新增內容時凍結 (停止回應)，請將 %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings or HlpViewer_VisualStudiox_en-US.settings 檔案中的 Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" 行變更為未來的某個日期。 如需此問題的詳細資訊，請參閱 [Visual Studio 說明檢視器凍結在啟動顯示畫面上](/visualstudio/welcome-to-visual-studio)。

4. 您可在左側內容窗格底下搜尋 *SQL Server 2016*，以確認是否已載入 SQL Server 2016 及更新版本的內容。

   ![SQL Server 2016 書籍已自動更新](../sql-server/media/sql-server-offline-documentation/sql-2016-content.png)

## <a name="sql-server-2014-offline-content"></a>SQL Server 2014 離線內容

> [!IMPORTANT]
> SQL 2014 Transact-SQL 內容僅供離線使用。

下列步驟說明如何載入 SQL Server 2014 的離線內容。

1. 從下載中心下載 [Microsoft SQL Server 2014 的防火牆和 Proxy 受限環境產品文件](https://www.microsoft.com/download/details.aspx?id=42557) \(英文\) 內容，並將其儲存到資料夾。

2. 將該檔案解壓縮以檢視 *.msha* 檔案。

   ![SQL Server 2014 說明文件安裝檔](../sql-server/media/sql-server-offline-documentation/sql-2014-help-content-setup-msha.png)

3. 在 SSMS 中，選取 [說明] 功能表上的 [加入和移除說明內容]。

   ![說明檢視器新增移除內容](../sql-server/media/sql-server-offline-documentation/add-remove-content.png)

   說明檢視器會開啟至 [管理內容] 索引標籤。

4. 若要安裝最新說明內容，請選擇 [安裝來源] 底下的 [磁碟]，然後選擇省略符號 (...)。

   ![說明檢視器管理內容磁碟來源](../sql-server/media/sql-server-offline-documentation/install-source-disk.png)

   > [!NOTE]
   > [管理內容] 索引標籤上的 [本機存放區路徑] 會顯示內容在本機電腦上的所在位置。 若要變更位置，請選取 [移動]，並在 [到] 欄位中輸入不同資料夾路徑，然後選取 [確定]。
   如果變更本機存放區路徑後，說明安裝失敗，請關閉並重新開啟 Help Viewer。 請確定新的位置出現在本機存放區路徑中，然後再次嘗試安裝。

5. 尋找已解壓縮內容所在的資料夾。 選取資料夾中的 [HelpContentSetup.msha] 檔案，然後選取 [開啟]。

   ![開啟 SQL Server 2014 Help Content Setup.msha 檔案](../sql-server/media/sql-server-offline-documentation/sql-2014-open-msha.png)

6. 在搜尋列中輸入 *sql server 2014*。 當您看到有 2014 內容可供使用之後，選取您想要安裝至 [說明檢視器] 之每個內容套件 (書籍) 旁邊的 [新增]，然後選取 [更新]。

   ![[說明檢視器] 中的 SQL Server 2014 書籍搜尋](../sql-server/media/sql-server-offline-documentation/sql-2014-search.png)

   ![[說明檢視器] 中的 SQL Server 2014 書籍新增與更新](../sql-server/media/sql-server-offline-documentation/sql-2014-add-update.png)

    > [!NOTE]
    > 如果說明檢視器在新增內容時凍結 (停止回應)，請將 %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings or HlpViewer_VisualStudiox_en-US.settings 檔案中的 Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" 行變更為未來的某個日期。 如需此問題的詳細資訊，請參閱 [Visual Studio 說明檢視器凍結在啟動顯示畫面上](/visualstudio/welcome-to-visual-studio)。

7. 您可以在左側內容窗格底下搜尋 *sql server 2014*，以確認是否已安裝 SQL Server 2014 內容。

   ![SQL Server 2014 書籍已自動更新](../sql-server/media/sql-server-offline-documentation/sql-2014-content.png)

## <a name="sql-server-2012-offline-content"></a>SQL Server 2012 離線內容

下列步驟說明如何載入 SQL Server 2012 的離線內容

1. 從下載中心下載 [Microsoft SQL Server 2012 的防火牆和 Proxy 受限環境產品文件](https://www.microsoft.com/download/details.aspx?id=35750) \(英文\) 內容，並將其儲存到資料夾。

2. 將該檔案解壓縮以檢視 *.msha* 檔案。

   ![SQL Server 2012 說明內容安裝程式檔案](../sql-server/media/sql-server-offline-documentation/sql-2012-help-content-setup-msha.png)

3. 在 SSMS 中，選取 [說明] 功能表上的 [加入和移除說明內容]。

   ![說明檢視器新增移除內容](../sql-server/media/sql-server-offline-documentation/add-remove-content.png)

   說明檢視器會開啟至 [管理內容] 索引標籤。

4. 若要安裝最新說明內容，請選擇 [安裝來源] 底下的 [磁碟]，然後選擇省略符號 (...)。

   ![說明檢視器管理內容磁碟來源](../sql-server/media/sql-server-offline-documentation/install-source-disk.png)

   > [!NOTE]
   > [管理內容] 索引標籤上的 [本機存放區路徑] 會顯示內容在本機電腦上的所在位置。 若要變更位置，請選取 [移動]，並在 [到] 欄位中輸入不同資料夾路徑，然後選取 [確定]。
   如果變更本機存放區路徑後，說明安裝失敗，請關閉並重新開啟 Help Viewer。 請確定新的位置出現在本機存放區路徑中，然後再次嘗試安裝。

5. 尋找已解壓縮內容所在的資料夾。 選取資料夾中的 [HelpContentSetup.msha] 檔案，然後選取 [開啟]。

   ![開啟 SQL Server 2012 Help Content Setup.msha 檔案](../sql-server/media/sql-server-offline-documentation/sql-2012-open-msha.png)

6. 在搜尋列中輸入 *sql server 2012*。 當您看到有 2012 內容可供使用之後，選取您想要安裝至 [說明檢視器] 之每個內容套件 (書籍) 旁邊的 [新增]，然後選取 [更新]。

   ![[說明檢視器] 中的 SQL Server 2012 書籍搜尋](../sql-server/media/sql-server-offline-documentation/sql-2012-search.png)

   ![[說明檢視器] 中的 SQL Server 2012 書籍新增與更新](../sql-server/media/sql-server-offline-documentation/sql-2012-add-update.png)

    > [!NOTE]
    > 如果說明檢視器在新增內容時凍結 (停止回應)，請將 %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings or HlpViewer_VisualStudiox_en-US.settings 檔案中的 Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" 行變更為未來的某個日期。 如需此問題的詳細資訊，請參閱 [Visual Studio 說明檢視器凍結在啟動顯示畫面上](/visualstudio/welcome-to-visual-studio)。

7. 您可以在左側內容窗格底下搜尋 *sql server 2012*，以確認是否已載入 SQL Server 2012 內容。

   ![SQL Server 2012 文件已自動更新](../sql-server/media/sql-server-offline-documentation/sql-2012-content.png)

## <a name="view-offline-documentation"></a>檢視離線文件

您可以使用最新版 [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) 中的 [說明] 功能表，來檢視 SQL Server 說明內容。

### <a name="view-offline-help-content-in-ssms"></a>在 SSMS 中檢視離線說明內容

若要在 SSMS 中檢視已安裝的說明，請從 [說明] 功能表中選取 [在說明檢視器中啟動]，以啟動 [說明檢視器]。

   ![在說明檢視器中啟動](../sql-server/media/sql-server-offline-documentation/helpviewer-view-offline.png)  

[說明檢視器] 會開啟至 [管理內容] 索引標籤，並在左窗格中顯示已安裝的說明目錄。 選取目錄中的文章以在右方窗格中顯示該文章。

> [!Important]
> 如果看不到內容窗格，請選取左邊界上的 [內容]。 選取圖釘圖示以將內容窗格保持開啟。  

   ![含內容的 [說明檢視器]](../sql-server/media/sql-server-offline-documentation/view-offline-all.png)

## <a name="life-cycle-policy"></a>生命週期原則

如需有關特定產品、服務或技術之支援方式的詳細資訊，請檢閱「Microsoft 產品生命週期」：

- [Microsoft 週期原則](https://support.microsoft.com/lifecycle/selectindex)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="next-steps"></a>後續步驟

若要深入了解封存的內容和 [說明檢視器]，請參考下方連結。

- [SQL Server 線上文件](../sql-server/index.yml?view=sql-server-2016&preserve-view=true)
- [SQL Server 2014 線上文件](/previous-versions/sql/2014)
- [舊版的 SQL Server 線上文件](previous-versions-sql-server.md)
- [SQL 文件的版本控制系統](../sql-server/versioning-system-monikers-ui-sql-server.md?view=sql-server-2016&preserve-view=true)