---
title: Azure SQL 受控執行個體延伸模組
description: 搭配 Azure SQL 受控執行個體使用 Azure Data Studio
ms.custom: seodec18
ms.date: 10/07/2019
ms.reviewer: alanyu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
manager: alanyu
ms.openlocfilehash: dd1b610c5c8e99fcda446688d0dbdffe0a9dc51e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778477"
---
# <a name="azure-sql-managed-instance-dashboard-for-azure-data-studio-preview"></a>適用於 Azure Data Studio 的 Azure SQL 受控執行個體儀表板 (預覽)

Azure SQL 受控執行個體延伸模組提供一個儀表板，以便在 [Azure Data Studio](https://github.com/Microsoft/azuredatastudio) 中使用 [Azure SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance-index)。 此延伸模組提供下列功能：

- 顯示 SQL 受控執行個體屬性，包括虛擬核心與已使用的儲存體
- 監視過去兩小時內的 CPU 和儲存體使用量
- 顯示設定警告與調整建議
- 顯示資料庫複本的狀態
- 顯示已篩選的錯誤記錄

## <a name="install"></a>安裝

您可以安裝此延伸模組的正式發行版本。 依照 [Azure Data Studio 文件](./extensions.md)中的步驟進行。
在 [延伸模組] 窗格中，搜尋「受控執行個體」，然後在該處進行安裝。 安裝完成之後，您會自動收到任何延伸模組未來更新的相關通知。

安裝延伸模組之後，您會在 Azure Data Studio 中看到 [受控執行個體]  索引標籤。 您可以在這裡找到受控執行個體的特定資訊。

## <a name="properties"></a>屬性

此延伸模組會顯示受控執行個體的技術特性和一些資源使用狀況。

[ ![受控執行個體屬性](media/azure-sql-mi-extension/ads-mi-tab1.png )](media/azure-sql-mi-extension/ads-mi-tab1.png#lightbox)

上方窗格會顯示下列詳細資料：

- **屬性**。 取得受控執行個體的基本資訊，包括可用的虛擬核心、記憶體和儲存體。 同時尋找您目前的服務層級、硬體世代和 IO 特性，例如執行個體記錄寫入輸送量或檔案 I/O 輸送量特性。
- **本機 SSD 儲存體**。 在一般用途服務層級上，**TempDB** 檔案會儲存在本機。 在業務關鍵服務層級上，所有  資料庫檔案都存放在本機 SSD 儲存體上。 在此節中，您可以看到本機儲存體上有多少空間是由您的受控執行個體使用的。
- **Azure 進階磁碟儲存體**。 如果您具有一般用途服務層級，則使用者和系統資料庫檔案都將存放在 Azure 進階儲存體上。 在本節中，您可以看到所使用的資料量、檔案數目和可用的儲存體。 在業務關鍵服務層級上，此區段是空的。
- **資源使用狀況**。 查看您的受控執行個體在過去兩小時內所使用的儲存體和 CPU 百分比。 如此一來，如果接近限制，您就可以增加執行個體大小。

## <a name="recommendations"></a>建議

當您選取 [受控執行個體]  索引標籤中的第二個窗格時，您會取得建議和警示，以協助最佳化您的受控執行個體。

[ ![受控執行個體建議](media/azure-sql-mi-extension/ads-mi-tab2.png )](media/azure-sql-mi-extension/ads-mi-tab2.png#lightbox)

您可能會看到下列一些建議：

- **達到儲存空間限制**。 請刪除不必要的資料，或增加執行個體儲存體大小。 達到儲存空間限制的資料庫可能無法處理甚至讀取查詢。
- **達到執行個體輸送量限制**。 在載入接近服務層級的限制時通知您：一般用途為 22 MB/秒，關鍵業務為 48 MB/秒。 請注意，您的受控執行個體會限制您的負載，以確保可以執行備份。
- **記憶體不足的壓力**。 頁面的預期壽命太低或大量 `PAGEIOLATCH` 等候統計資料可能指出您的執行個體正在將分頁從記憶體撤出並持續嘗試從磁碟載入分頁。
- **記錄檔限制**。 若您的記錄檔達到[一般用途服務層級的檔案 IO 限制](/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier)，您可能必須增加記錄檔大小以取得更好的效能。
- **資料檔限制**。 若您的資料檔達到[一般用途服務層級的檔案 IO 限制](/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier)，您可能必須增加檔案大小以取得更好的效能。 此問題可能會導致記憶體壓力並導致備份效能降低。
- **可用性問題**。 大量的虛擬記錄檔可能會影響效能。 如果發生程序失敗，這類問題可能會導致一般用途服務層級的資料庫復原時間變長。

請定期檢閱這些建議、調查根本原因，並採取矯正問題的措施。 SQL 受控執行個體延伸模組提供指令碼讓您執行，以減輕一些回報的問題。

## <a name="replicas"></a>複本數

[受控執行個體]  索引標籤中的第三個窗格會顯示您受控執行個體中的資料庫複本狀態。

[ ![受控執行個體複本](media/azure-sql-mi-extension/ads-mi-tab3.png )](media/azure-sql-mi-extension/ads-mi-tab3.png#lightbox)

在一般用途服務層級上，每個資料庫都有單一 (主要) 複本。 在業務關鍵層級執行個體上，每個資料庫都有一個主要複本和三個次要複本，其中一個是用於唯讀工作負載。 在 [複本]  窗格上，您可以監視同步程序並確認所有次要複本都與主要複本同步。

## <a name="logs"></a>記錄

[受控執行個體]  的第四個窗格會顯示最新和最相關的 SQL 錯誤記錄檔項目。

[ ![受控執行個體記錄項目](media/azure-sql-mi-extension/ads-mi-tab4.png )](media/azure-sql-mi-extension/ads-mi-tab4.png#lightbox)

雖然您的受控執行個體會發出大量記錄項目，但它們大部分都是內部/系統資訊。 此外，某些記錄項目會顯示實體資料庫名稱 (`GUID` 值)，而非實際邏輯資料庫名稱。

SQL 受控執行個體延伸模組會根據 [Dimitri Furman 方法](https://techcommunity.microsoft.com/t5/DataCAT/Azure-SQL-DB-Managed-Instance-sp-readmierrorlog/ba-p/305506)篩選掉不必要的記錄項目。 延伸模組也會顯示實際的邏輯檔案名稱，而不是實體名稱。

## <a name="reporting-problems"></a>回報問題

若您遇到 SQL 受控執行個體延伸模組的任何問題，請移至[延伸模組 GitHub 專案](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/issues) \(英文\) 並回報您的問題。

## <a name="code-of-conduct"></a>管理辦法

此專案採用了 [Microsoft 開放原始碼管理辦法][conduct-code]。

如需詳細資訊，請參閱[管理辦法常見問題集][conduct-FAQ]，如有其他問題或意見，請連絡 [opencode@microsoft.com][conduct-email]。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請造訪 [GitHub 專案](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/)。

[conduct-code]: https://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: https://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com