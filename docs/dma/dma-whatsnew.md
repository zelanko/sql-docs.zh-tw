---
title: Data Migration Assistant (SQL Server) 的新功能 |Microsoft Docs
description: 瞭解 SQL Server 和 Azure SQL Database 的每個 Data Migration Assistant 版本中的新功能。
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
ms.openlocfilehash: 2becdd3e5ab0c6980ffbb4b4f4a5d50584f6fd35
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864895"
---
# <a name="whats-new-in-data-migration-assistant"></a>資料移轉小幫手的新功能

本文列出每個 Data Migration Assistant 版本中的新增專案。

## <a name="data-migration-assistant-v-52"></a>Data Migration Assistant v 5。2
Data Migration Assistant 的 v5.2 版本提供下列支援：
- 將評量上傳至 Azure Migrate，並支援 Azure Government 和國家雲端 (主權供應專案) 。  這項功能可讓評估遷移至 Azure SQL 之 SQL Server 資料資產的就緒程度。
- 支援 Azure Government 和國家雲端上傳評量至 Azure Migrate 的命令列支援。  現在，您可以完全自動將評量上傳至 Azure 遷移專案，以取得匯總的 Azure SQL 就緒報告。 

## <a name="data-migration-assistant-v-50"></a>Data Migration Assistant v 5。0

5.0 版的 Data Migration Assistant 提供下列支援：

- 適用于 Windows 的 SQL Server 2019 和 SQL Server 2019 做為評估和升級目標的 Linux。
- 儲存和載入評量，包括支援儲存和載入在舊版 Data Migration Assistant 中建立的評估。
- 評估裝載于封裝存放區之 SSISDB 和 SSIS 套件中裝載的 SQL Server Integration Services (SSIS) 專案。 資料庫移轉小幫手會偵測來源套件中所使用的不支援、部分支援或已淘汰的功能和相容性問題，並提供可協助您解決這些問題的建議。
- 從外部應用程式評估 SQL 查詢，例如 c # 原始程式碼中的 SQL 查詢。 使用者可以使用資料存取遷移工具組，針對 c # 原始程式碼中使用的 SQL 查詢產生完整的 JSON 報告，然後將報表上傳至 Data Migration Assistant。

此外，此版本的 Data Migration Assistant 還提供額外的增強功能和 bug 修正，而此工具已更新為 .Net 4.7.2。

## <a name="data-migration-assistant-v45"></a>Data Migration Assistant 4.5 版

Data Migration Assistant 的4.5 版支援將 (SQL Server Integration Services 檔案系統中所裝載的 SSIS) 套件遷移至 Azure SQL Database 或 SQL 受控執行個體的評估。

## <a name="data-migration-assistant-v44"></a>Data Migration Assistant 4。4

Data Migration Assistant 的4.4 版提供將評量上傳至 Azure Migrate 的支援。

## <a name="data-migration-assistant-v43"></a>Data Migration Assistant 4。3

Data Migration Assistant 的4.3 版提供下列支援：

- 以工作負載評估為基礎的 Azure SQL 受控執行個體 SKU 建議。
- RDS SQL Server 做為評量的來源。
- Azure SQL 受控執行個體的代理程式作業評量做為目標。
- 忽略特定評估規則的能力;dma 中設定的 ' ignoreErrorCodes ' 屬性中指定的錯誤碼清單不會顯示在 DMA 評估結果中。
- 評估作業活動步驟中的 T-SQL 查詢，並提供適當的建議
- 擴充事件評量 (公開預覽) 。

此外，這一版的 DMA 提供了在資料庫中處理大量架構物件的改良效能，以及與相關的錯誤修正：

- 在某些情況下，使用原生編譯編譯的程式。
- 複雜的資料庫架構。

## <a name="data-migration-assistant-v42"></a>Data Migration Assistant 4.2 版

當從內部部署 SQL Server 遷移至 SQL 受控執行個體時，Data Migration Assistant 的4.2 版會針對一或多個伺服器實例的目標就緒程度評估提供命令列支援。 客戶現在可以使用 Data Migration Assistant 命令列來收集其資料庫架構的中繼資料、偵測封鎖程式，並瞭解影響遷移至 SQL 受控執行個體的部分支援或不支援的功能。 然後，可以使用提供的 Power BI 範本來呈現結果。

## <a name="data-migration-assistant-v41"></a>Data Migration Assistant 4.1 版

4.1 版的 Data Migration Assistant 引進全面評估內部部署 SQL Server 資料庫移轉至 SQL 受控執行個體的支援。

評估工作流程可協助您偵測下列問題，這可能會影響您遷移至 SQL 受控執行個體：

- **不支援或部分支援的功能**。 Data Migration Assistant 會針對目標 SQL 受控執行個體上部分支援或不支援的使用功能，評估您的來源 SQL Server 資料庫。 然後，此工具會提供一組完整的建議、Azure 中可用的替代方法，以及減少步驟，讓客戶在規劃其遷移專案時可以將這項資訊列入考慮。

- **相容性問題**。 Data Migration Assistant 也會識別與下列領域相關的相容性問題：

  - 重大變更：可能會中斷遷移至目標資料庫之功能的特定架構物件。  我們建議在資料庫移轉之後修正這些架構物件。
  - 行為變更：所報告的架構物件可能會繼續運作，但它們可能會表現出不同的行為，例如效能降低。
  - 資訊問題：這些物件不會影響遷移，但可能已從功能 SQL Server 版本中淘汰。

評量完成之後，請使用我們的[Azure 資料庫移轉服務](https://azure.microsoft.com/services/database-migration/) (DMS) ，將 SQL Server 資料庫移轉至 SQL 受控執行個體。  DMS 同時支援[離線](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance) (一次性) 和[線上](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online) (最短停機時間) 資料庫移轉至 SQL 受控執行個體。

## <a name="data-migration-assistant-v40"></a>Data Migration Assistant v4。0

4.0 版的 Data Migration Assistant 引進了 Azure SQL Database SKU 建議功能，可讓使用者根據從) 裝載資料庫的 (電腦所收集的效能計數器，識別最小的建議 Azure SQL Database SKU。 這項功能會提供與定價層、計算層級和最大資料大小的相關建議，以及每個月的預估成本。 它也能讓您將所有資料庫大量布建至 Azure。

> [!NOTE]
> 此功能目前僅透過命令列介面 (CLI) 提供。

如需其他詳細資訊，請參閱為[您的內部部署資料庫識別正確的 AZURE SQL DATABASE SKU 一](dma-sku-recommend-sql-db.md)文。

## <a name="data-migration-assistant-v36"></a>Data Migration Assistant 3.6 版

3.6 版的 Data Migration Assistant 針對受最常見的遷移封鎖程式所影響的架構物件，引進了「自動修正」。

此版本提供下列遷移封鎖程式和行為變更問題的 autofix：

- 使用不合格聯結語法的架構物件。
- 使用舊版 RAISEERROR 語句的架構物件。
- 使用 Order By 整數常值的 SQL 語句。

Data Migration Assistant 會針對列出的問題所影響的物件執行自動架構轉換，並在繼續進行架構轉換之前提示使用者確認。 使用者可以檢查建議的程式碼變更，然後接受或拒絕任何指定資料庫物件的所有轉換。

Data Migration Assistant 使用 Microsoft 程式合成 (PROSE) 技術來建議程式碼修正。 深入瞭解[PROSE](https://microsoft.github.io/prose/)。

## <a name="data-migration-assistant-v35"></a>Data Migration Assistant v 3。5

Data Migration Assistant 的3.5 版包含下列新增專案：

- 遷移至 Azure SQL Database (基準測試的顯著效能改進，指出進程的速度比先前版本的 Data Migration Assistant) 快四倍。
- 記憶體使用量會進一步優化，以改善遷移工作流程的穩定性。
- 在架構和資料移轉期間略過評量的功能 (如果您已經執行評量，並在遷移) 之前解決任何中斷的架構物件。
- 修正以解決當為備份檔案提供了不正確網路共用路徑時，此工具會損毀的問題、將舊版 SQL Server 內部部署升級至較新版本，或在 Azure Vm 上 SQL Server。

## <a name="data-migration-assistant-v34"></a>Data Migration Assistant 3.4 版

Data Migration Assistant 的3.4 版包含下列新增專案：

- 支援 SQL Server 2017 做為 Azure SQL Database 遷移的來源。
- 穩定性、效能及評估規則正確性的增強功能。

## <a name="data-migration-assistant-v33"></a>Data Migration Assistant 3.3 版

3.3 版的 Data Migration Assistant 可將內部部署 SQL Server 實例遷移至 Windows 和 Linux 上的新版本 SQL Server 2017。 雖然 Windows 和 Linux 的整體遷移工作流程相同，但移至適用于 Linux 的 SQL Server 2017 需要一些額外的考慮。

### <a name="specifying-the-back-up-path"></a>指定備份路徑

Linux 和 Windows 使用不同的路徑格式。 因此，若要在 Linux 上遷移至 SQL Server 2017，使用者必須同時將 Windows 和 Linux 版本的路徑提供給實體檔案的位置。 您可以根據實體檔案的位置，以不同的方式提供兩種版本的路徑。
如果實體備份檔案在執行的電腦上：

- Linux，請使用 ' samba ' 共用來與網路上的其他電腦共用檔案。
- Windows，請使用 ' mnt ' 命令將共用掛接到執行 Linux 的電腦上。

> [!NOTE]
> 使用 ' samba ' 共用或 ' mnt ' 命令的詳細資料已超出本文的範圍。

### <a name="migrating-windows-logins"></a>遷移 Windows 登入

雖然 Linux 上的 SQL Server 2017 已正式支援 Active Directory (AD) 登入的遷移，但它需要額外的設定才能順利執行。 如需在 Linux 上的 SQL Server 2017 上設定 Active Directory 登入的詳細資訊，請參閱[使用 Linux 上的 SQL Server Active Directory 驗證](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication)一文。 執行必要的設定之後，安裝已完成，您可以照常遷移 Active Directory 登入。 標準 SQL 驗證會如預期般運作，而不需要任何額外的設定。

## <a name="data-migration-assistant-v32"></a>Data Migration Assistant 3.2 版

Data Migration Assistant 的3.2 版包含下列新增專案：

- 架構和資料移轉會從內部部署 SQL Server 資料庫啟用，以使用新的遷移工作流程來 Azure SQL Database。
- 在架構遷移至 Azure SQL Database 中，DMA 會編寫您的源資料庫物件的腳本，提供如何修正任何潛在相容性問題的指引，然後將您的架構部署至 Azure。

## <a name="data-migration-assistant-v31"></a>Data Migration Assistant 3.1 版

Data Migration Assistant 的3.1 版包含下列新增專案：

- 已改善 Azure SQL database 的評估建議（根據資料庫定序）、使用不支援的系統預存程式和 CLR 物件。
- 遷移至 Azure SQL 資料庫時，相容性層級130、120、110和100的評估指南。

## <a name="data-migration-assistant-v30"></a>Data Migration Assistant v3。0

Data Migration Assistant 的3.0 版會擴充 Azure SQL Database 評量，以提供完整的建議來協助修正與下列相關的問題：

- 遷移封鎖問題。
- 部分或不支援的功能和功能。

## <a name="data-migration-assistant-v21"></a>Data Migration Assistant v 2。1

Data Migration Assistant 的2.1 版包含下列新增專案：

- 以自動模式執行評量的命令列支援，可協助大規模執行評估。 如需其他詳細資料，請參閱[從命令列執行 Data Migration Assistant](dma-commandline.md)一文。
- 使用者啟動和關閉 DMA 時的效能改進。
- 設定 SQL 連接逾時的能力。如需其他詳細資料，請參閱[Data Migration Assistant 的設定](dma-configurationsettings.md)一文。

## <a name="data-migration-assistant-v20"></a>Data Migration Assistant v2。0

V2.0 版本的 Data Migration Assistant 包括改良的 Stretch database 功能建議，以提供適當的優先順序資料表來最大化儲存空間。

## <a name="data-migration-assistant-v10"></a>Data Migration Assistant v1。0

1.0 版的 Data Migration Assistant 是初始版本，它提供下列功能：

- 探索可能會影響升級至內部部署版本 SQL Server 的問題。 所有的發現都會描述為相容性問題，而且會分類成下列領域：
  - 重大變更
  - 行為變更
  - 已淘汰的功能
- 探索目標 SQL Server 平臺中，資料庫在升級後可受益的新功能。 所有的發現都會描述為功能建議，且會分類為下欄區域：
  - 效能
  - 安全性
  - 儲存體
- 執行評量的現代化使用者體驗。

## <a name="see-also"></a>另請參閱

[Data Migration Assistant 概觀](../dma/dma-overview.md) (機器翻譯)
