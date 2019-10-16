---
title: Azure SQL 受控執行個體延伸模組
titleSuffix: Azure Data Studio
description: 搭配 Azure SQL 受控執行個體使用 Azure Data Studio
ms.custom: seodec18
ms.date: 10/07/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
manager: alanyu
ms.openlocfilehash: d443292fb091679d3d6a18d557a5a7aac464fdec
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041137"
---
# <a name="managed-instance-support-for-azure-data-studio-preview"></a>Azure Data Studio 的受控執行個體支援 (預覽)

此延伸模組可讓您在 [Azure Data Studio](https://github.com/Microsoft/azuredatastudio) 中使用 [Azure SQL 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index) \(部分機器翻譯\)。 此延伸模組提供下列功能：

- 檢視受控執行個體 (vCores、已使用的儲存體) 的屬性。
- 監視過去兩小時內的 CPU 與儲存體使用狀況。
- 顯示設定警告與調整建議。
- 顯示資料庫複本的狀態。
- 顯示已篩選的錯誤記錄。

## <a name="installations"></a>安裝

您可以遵循 [Azure Data Studio 文件](https://docs.microsoft.com/sql/azure-data-studio/extensions)中的步驟，安裝受控執行個體延伸模組的正式版本。
在 [延伸模組] 窗格中搜尋「受控執行個體」延伸模組，然後在該處進行安裝。  您會自動收到任何延伸模組未來更新的相關通知！

一旦安裝受控執行個體延伸模組，您將會在 Azure Data Studio 中看到 `Managed Instance` 索引標籤。 在此索引標籤上，您可以找到受控執行個體的特定資訊。

## <a name="properties"></a>屬性

此延伸模組可讓您查看受控執行個體與一些資源使用狀況的技術特性。

![受控執行個體屬性](media/azure-sql-mi-extension/ads-mi-tab1.png)

在第一個刀鋒視窗上，您可以看到下列詳細資料：

- **基本屬性**，例如可用 vCores 數目、記憶體、儲存體、目前服務層級與硬體世代，以及 IO 特性 (如執行個體記錄寫入輸送量或檔案 IO/throughput 特性)。
- **本機 SSD 儲存體使用量**. 在一般用途服務層級，只有 **TEMPDB** 檔案會放在本機，而菜業務關鍵層級，所有資料庫檔案都會放在綁機 SSD 儲存體。 在此節中，您可以看到本機儲存體上有多少空間是由受控執行個體使用的。
- **Azure 進階磁碟儲存體使用狀況** - 一般用讀服務層級中的使用者與系統資料庫是放在 Azure 進階儲存體上。 您可以在這裡找到已使用的資料量，以及剩餘儲存體空間和檔案數目。 在業務關鍵服務層級上，此區段是空的。
- **資源使用狀況** - 將會顯示過去兩小時有多少儲存體與 CPU 是由您的執行個體使用的。 若達到限制，請增加執行個體大小。

## <a name="recommendations"></a>建議

此延伸模組提供一些建議與警示，可協助您最佳化您的受控執行個體。

![受控執行個體建議](media/azure-sql-mi-extension/ads-mi-tab2.png)

此表格中顯示的一些建議為：

- 達到儲存體空間限制 - 您應該刪除不必要的檔案或增加執行個體儲存體大小，因為達到儲存體限制的資料庫會甚至可能無法處理讀取查詢。
- 達到執行個體輸送量限制 - 若您在 GP 上載入速率為 ~22MB/秒或在 BC 上載入速率為 ~48 MB/秒，受控執行個體將會現在您的負載，以確保可以建立備份。
- 記憶體壓力 - 低分頁生命週期預期或大量 `PAGEIOLATCH` 等候統計資料可能指出您的執行個體正在將分頁從記憶體撤出並持續嘗試從磁碟載入分頁。
- 記錄檔限制 - 若您的記錄檔達到[一般用途服務階層的檔案 IO 限制](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier)，您可能必須增加檔案大小以取得更好的效能。
- 資料檔限制 - 若您的資料檔達到[一般用途服務階層的檔案 IO 限制](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier)，您可能必須增加檔案大小以取得更好的效能。 此問題可能會導致記憶體壓力並導致備份效能降低。
- 可用性問題 - 在發生處理序失敗時，大量的虛擬記錄檔可能會導致效能影響與潛在的較長資料庫復原 (在一般用途服務階層上)。

您應該定期檢閱這些建議、調查根本原因，並採取矯正措施。 受控執行個體延伸個體提供指令碼讓您執行，以減輕一些回報的問題。

## <a name="replicas"></a>複本

受控執行個體延伸模組可讓您查看受控執行個體中的資料庫複本狀態。

![受控執行個體複本](media/azure-sql-mi-extension/ads-mi-tab3.png)

在一般用途服務階層上，每個資料庫都有單一 (主要) 複本，而在業務關鍵執行個體上，每個資料庫都有一個主要與三個次要複本 (一個用於唯讀工作負載)。 您可以在這裡監視同步程序並確認所有次要複本都與主要複本同步。

## <a name="logs"></a>記錄檔

受控執行個體延伸模組會顯示最相關的最新 SQL 錯誤記錄項目。

![受控執行個體記錄項目](media/azure-sql-mi-extension/ads-mi-tab4.png)

受控執行個體會發出大量記錄項目，而且它們大部分都是內部/系統資訊。 某些記錄項目會顯示實體資料庫名稱 (`GUID` 值)，而非實際邏輯資料庫名稱。

受控執行個體延伸模組會根據 [Dimitri Furman 方法](https://techcommunity.microsoft.com/t5/DataCAT/Azure-SQL-DB-Managed-Instance-sp-readmierrorlog/ba-p/305506) \(英文\) 篩出不必要的記錄項目，並顯示實際邏輯檔案名稱，而非實體名稱。

## <a name="reporting-problems"></a>回報問題

若您遇到受控執行個體延伸模組的任何問題，請在[延伸模組 GitHub 專案](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/issues) \(英文\) 回報問題。

## <a name="maintainers"></a>維護人員

- [Jovan Popovic(MSFT)](https://github.com/jovanpop_msft) - [@jovanpop_msft](https://twitter.com/JovanPop_MSFT)

## <a name="code-of-conduct"></a>管理辦法

此專案採用了 [Microsoft 開放原始碼管理辦法][conduct-code]。
如需詳細資訊，請參閱[管理辦法常見問題集][conduct-FAQ]，如有其他問題或意見，請連絡 [opencode@microsoft.com][conduct-email]。

[conduct-code]: http://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: http://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[conduct-md]: https://github.com/PowerShell/vscode-powershell/blob/master/CODE_OF_CONDUCT.md
