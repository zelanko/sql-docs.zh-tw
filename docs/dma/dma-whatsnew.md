---
title: Data Migration Assistant (SQL Server 的新功能) |Microsoft Docs
description: 瞭解 SQL Server 和 Azure SQL Database 的每個 Data Migration Assistant 版本的新功能。
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.openlocfilehash: 11bbf0a39ed9a9bbaa19992f98e4e23d50d6fbe9
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727757"
---
# <a name="whats-new-in-data-migration-assistant"></a>資料移轉小幫手的新功能

本文列出 Data Migration Assistant 的每個版本中的新增專案。

## <a name="data-migration-assistant-v-52"></a>Data Migration Assistant v 5。2
Data Migration Assistant 的5.2 版提供下列支援：
- 將評量上傳至 Azure Migrate，並支援 Azure Government 和國家雲端 (主權提供) 。  這項功能可讓您評估將 SQL Server 資料資產遷移至 Azure SQL 的就緒程度。
- 將評量上傳至 Azure Migrate 並支援 Azure Government 和國家雲端的命令列支援。  現在，您可以完全自動將評量上傳至 Azure 遷移專案，以取得合併的 Azure SQL 就緒報告。 

## <a name="data-migration-assistant-v-50"></a>Data Migration Assistant v 5。0

Data Migration Assistant 的5.0 版提供下列支援：

- 適用于 Windows 的 SQL Server 2019 和適用于 Linux 的 SQL Server 2019，作為評量及升級目標。
- 儲存和載入評量，包括支援儲存和載入在舊版 Data Migration Assistant 中建立的評量。
- 評估 SQL Server Integration Services (SSIS) 裝載在封裝存放區中的 SSISDB 和 SSIS 套件中的專案。 資料庫 Migration Assistant 會偵測來源套件中所使用之不支援、部分支援或已淘汰的功能和相容性問題，並提供可協助您解決這些問題的建議。
- 從外部應用程式評估 SQL 查詢，例如 c # 原始程式碼中的 SQL 查詢。 使用者可以使用 Data Access Migration Toolkit 來產生 c # 原始程式碼中所使用之 SQL 查詢的完整 JSON 報表，然後將報表上傳至 Data Migration Assistant。

此外，這個版本的 Data Migration Assistant 也提供額外的增強功能和 bug 修正，而且工具已經更新為 .Net 4.7.2。

## <a name="data-migration-assistant-v45"></a>Data Migration Assistant 4。5

Data Migration Assistant 的4.5 版可支援將檔案系統中所裝載 SQL Server Integration Services (SSIS) 套件遷移至 Azure SQL Database 或 SQL 受控執行個體的評定。

## <a name="data-migration-assistant-v44"></a>Data Migration Assistant 4。4

Data Migration Assistant 的4.4 版提供將評量上傳至 Azure Migrate 的支援。

## <a name="data-migration-assistant-v43"></a>Data Migration Assistant 4。3

Data Migration Assistant 的4.3 版提供下列支援：

- Azure SQL 受控執行個體的 SKU 建議是以工作負載評估為基礎。
- RDS SQL Server 作為評量的來源。
- 作為目標的 Azure SQL 受控執行個體代理程式作業評量。
- 略過特定評估規則的能力;在 DMA 中設定的 ' ignoreErrorCodes ' 屬性所指定的錯誤碼清單，不會顯示在 DMA 評定結果中。
- 評估作業活動步驟中的 T-SQL 查詢並提供適當的建議
-  (公開預覽) 的擴充事件評量。

此外，這一版的 DMA 也改善了在資料庫中處理大量架構物件的效能，以及與相關的錯誤修正：

- 使用原生編譯編譯的程式（在某些情況下）。
- 複雜的資料庫架構。

## <a name="data-migration-assistant-v42"></a>Data Migration Assistant 4.2 版

Data Migration Assistant 的4.2 版可針對一或多個伺服器實例，在從內部部署 SQL Server 遷移至 SQL 受控執行個體時，提供命令列支援。 客戶現在可以使用 Data Migration Assistant 命令列來收集其資料庫架構的相關中繼資料、偵測封鎖程式，以及瞭解會影響遷移至 SQL 受控執行個體的部分支援或不支援功能。 然後，您可以使用提供的 Power BI 範本來呈現結果。

## <a name="data-migration-assistant-v41"></a>Data Migration Assistant 4.1 版

4.1 版的 Data Migration Assistant 導入了對遷移至 SQL 受控執行個體的內部部署 SQL Server 資料庫進行全面評量的支援。

評量工作流程可協助您偵測下列問題，這可能會影響您遷移至 SQL 受控執行個體：

- **不支援或部分支援的功能**。 Data Migration Assistant 會針對目標 SQL 受控執行個體上部分支援或不支援的使用功能，評估您的來源 SQL Server 資料庫。 然後，此工具會提供一組完整的建議、Azure 中提供的替代方法，以及可減輕的步驟，讓客戶能夠在規劃其遷移專案時將這項資訊納入考慮。

- **相容性問題**。 Data Migration Assistant 也會識別與下欄區域相關的相容性問題：

  - 中斷性變更：可能會中斷遷移至目標資料庫之功能的特定架構物件。  建議您在資料庫移轉之後，修正這些架構物件。
  - 行為變更：所報告的架構物件可能會繼續運作，但可能會顯示不同的行為，例如效能降低。
  - 參考問題：這些物件不會影響遷移，但功能 SQL Server 版本可能已淘汰。

評量完成後，請使用 [Azure 資料庫移轉服務](https://azure.microsoft.com/services/database-migration/) (DMS) ，以將您的 SQL Server 資料庫移轉至 SQL 受控執行個體。  DMS 同時支援 [離線](/azure/dms/tutorial-sql-server-to-managed-instance) (一次性) 和 [線上](/azure/dms/tutorial-sql-server-managed-instance-online) (將資料庫移轉至 SQL 受控執行個體) 的停機時間。

## <a name="data-migration-assistant-v40"></a>Data Migration Assistant v4。0

4.0 版的 Data Migration Assistant 引進了 Azure SQL Database SKU 建議功能，可讓使用者根據從電腦 () 裝載資料庫的效能計數器，來識別最低建議的 Azure SQL Database SKU。 這項功能會提供定價層、計算層級和最大資料大小的相關建議，以及每月預估成本。 它也可讓您將所有資料庫大量布建至 Azure。

> [!NOTE]
> 這項功能目前僅可透過命令列介面 (CLI) 取得。

如需其他詳細資訊，請參閱文章 [找出適合您內部部署資料庫的 AZURE SQL DATABASE SKU](dma-sku-recommend-sql-db.md)。

## <a name="data-migration-assistant-v36"></a>Data Migration Assistant 3.6 版

3.6 版的 Data Migration Assistant 引進了「自動修正」，適用于最常見的遷移封鎖器所影響的架構物件。

此版本提供下列遷移封鎖程式和行為變更問題的 >autofix 有效值：

- 使用不合格聯結語法的架構物件。
- 使用舊版 RAISEERROR 語句的架構物件。
- 使用 Order By 整數常值的 SQL 語句。

Data Migration Assistant 會針對所列出的問題影響的物件執行自動架構轉換，並提示使用者進行確認，再繼續進行架構轉換。 使用者可以查看建議的程式碼變更，然後接受或拒絕任何指定資料庫物件的所有轉換。

Data Migration Assistant 使用 Microsoft 程式合成 (PROSE) 技術來建議程式碼修正。 深入瞭解 [PROSE](https://microsoft.github.io/prose/)。

## <a name="data-migration-assistant-v35"></a>Data Migration Assistant v 3。5

Data Migration Assistant 的3.5 版包含下列新增專案：

- 遷移至 Azure SQL Database (基準測試的大幅效能改進，指出處理常式的速度比舊版 Data Migration Assistant) 快四倍。
- 記憶體使用量會進一步優化，以改善遷移工作流程的穩定性。
- 如果您已經執行評量，並在遷移) 之前解決任何中斷的架構物件，則在架構和資料移轉期間略過評量的功能 (。
- 當針對備份檔案提供不正確網路共用路徑、將舊版 SQL Server 內部部署升級至較新版本，或在 Azure Vm 上 SQL Server 時，可解決此問題的修正問題。

## <a name="data-migration-assistant-v34"></a>Data Migration Assistant 3.4 版

Data Migration Assistant 的3.4 版包含下列新增專案：

- 支援 SQL Server 2017 作為遷移至 Azure SQL Database 的來源。
- 穩定性、效能和評定規則正確性的增強功能。

## <a name="data-migration-assistant-v33"></a>Data Migration Assistant 3.3 版

Data Migration Assistant 的3.3 版可將內部部署 SQL Server 實例遷移至 Windows 和 Linux 上的新版本 SQL Server 2017。 雖然適用于 Windows 和 Linux 的整體遷移工作流程是相同的，但移至適用于 Linux 的 SQL Server 2017 需要一些額外的考慮。

### <a name="specifying-the-back-up-path"></a>指定備份路徑

Linux 和 Windows 使用不同的路徑格式。 因此，若要遷移至 Linux 上的 SQL Server 2017，使用者必須將 Windows 和 Linux 版本的路徑提供給實體檔案的位置。 您可以根據實體檔案的位置，以不同的方式提供兩個版本的路徑。
如果實體備份檔案在執行的電腦上：

- Linux，使用「samba」共用來與網路上的其他電腦共用檔案。
- Windows，請使用 ' mnt ' 命令將共用掛接到執行 Linux 的電腦上。

> [!NOTE]
> 使用 ' samba ' 共用或 ' mnt ' 命令的詳細資料已超出本文的範圍。

### <a name="migrating-windows-logins"></a>遷移 Windows 登入

雖然 Linux 上 SQL Server 2017 已正式支援 Active Directory (AD) 登入，但需要額外的設定才能順利運作。 如需有關在 Linux 上 SQL Server 2017 上設定 Active Directory 登入的詳細資訊，請參閱 [Active Directory 使用 Linux 上的 SQL Server 進行驗證](../linux/sql-server-linux-active-directory-authentication.md) 的文章。 執行必要的設定之後，安裝程式就會完成，您可以像平常一樣遷移 Active Directory 的登入。 標準 SQL 驗證可如預期般運作，而不需要任何額外的設定。

## <a name="data-migration-assistant-v32"></a>Data Migration Assistant 3.2 版

Data Migration Assistant 的3.2 版包含下列新增專案：

- 您可以使用新的遷移工作流程，從內部部署 SQL Server 資料庫啟用架構和資料移轉，以 Azure SQL Database。
- 在將架構遷移至 Azure SQL Database 時，DMA 會編寫您源資料庫物件的腳本，並提供如何修正任何潛在相容性問題的指引，然後將您的架構部署到 Azure。

## <a name="data-migration-assistant-v31"></a>Data Migration Assistant 3.1 版

Data Migration Assistant 的3.1 版包含下列新增專案：

- 改進對資料庫定序、使用不支援的系統預存程式和 CLR 物件的 Azure SQL Database 評估建議。
- 遷移至 Azure SQL Database 時，相容性層級130、120、110和100的評估指引。

## <a name="data-migration-assistant-v30"></a>Data Migration Assistant v3。0

3.0 版的 Data Migration Assistant 擴充了 Azure SQL Database 評量，以提供完整的建議來協助修正與相關的問題：

- 遷移封鎖問題。
- 部分或不支援的功能和功能。

## <a name="data-migration-assistant-v21"></a>Data Migration Assistant 2.1 版

Data Migration Assistant 的2.1 版包含下列新增專案：

- 以自動模式執行評量的命令列支援，有助於大規模執行評量。 如需其他詳細資訊，請參閱 [從命令列執行 Data Migration Assistant](dma-commandline.md)一文。
- 當使用者啟動及關閉 DMA 時的效能改進。
- 設定 SQL 連接逾時的能力。如需其他詳細資訊，請參閱 [Data Migration Assistant](dma-configurationsettings.md)的文章設定。

## <a name="data-migration-assistant-v20"></a>Data Migration Assistant 2.0 版

2.0 版的 Data Migration Assistant 包含改良的 Stretch database 功能建議，以提供適當的優先順序資料表，以將節省的儲存空間最大化。

## <a name="data-migration-assistant-v10"></a>Data Migration Assistant 1.0 版

1.0 版的 Data Migration Assistant 是初始版本，並提供下列功能：

- 探索可能會影響 SQL Server 的內部部署版本升級的問題。 任何發現都會被描述為相容性問題，而且會分類為下列領域：
  - 重大變更
  - 行為變更
  - 即將淘汰的功能
- 探索目標 SQL Server 平臺中的新功能，資料庫在升級之後可從中獲益。 系統會將任何結果描述為功能建議，並將其分類為下列領域：
  - 效能
  - 安全性
  - 儲存體
- 執行評量的新式使用者體驗。

## <a name="see-also"></a>另請參閱

[Data Migration Assistant 概觀](../dma/dma-overview.md) (機器翻譯)