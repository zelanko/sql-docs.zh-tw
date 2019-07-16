---
title: 什麼是新 Data Migration Assistant (SQL Server) |Microsoft 文件
ms.custom: ''
ms.date: 05/18/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: 5251b4da6334e8aeba1c467ff921f6f25b2ab26a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008374"
---
# <a name="whats-new-in-data-migration-assistant"></a>資料移轉小幫手的新功能
本文章列出新增的項目在每個版本的 Data Migration Assistant (DMA)。

## <a name="dma-v43"></a>DMA v4.3

DMA 的 v4.3 版本提供支援：

* SKU 建議為 Azure SQL Database 受控執行個體根據工作負載評估。
* RDS SQL Server 做為評量的來源。
* 代理程式作業評估為 Azure SQL Database 受控執行個體做為目標。
* 是能夠忽略特定的評估規則;在 DMA 評估結果，不會顯示在 DMA 中所設定的 'ignoreErrorCodes' 屬性中指定的錯誤碼的清單。
* 在 作業活動的步驟，並提供適當的建議的 T-SQL 查詢的評估
* 擴充的事件評定 （公開預覽狀態）。

此外，這一版的 DMA 提供改善的效能來處理大量的結構描述物件的資料庫，以及相關 bug 修正：

* 使用原生編譯，在某些情況下所編譯的程序。
* 複雜的資料庫結構描述。

## <a name="dma-v42"></a>DMA v4.2

DMA 的 4.2 版版本在從內部部署 SQL Server 移轉至 Azure SQL Database 受控執行個體時，會提供一或多個伺服器執行個體的目標整備性評估的命令列支援。 客戶現在可以收集關於其資料庫結構描述的中繼資料、 偵測阻礙，請使用 DMA 命令列，並了解影響移轉至 Azure SQL Database 受控執行個體的部分支援或不受支援的功能。 結果接著可以使用提供的 Power BI 範本來轉譯。

## <a name="dma-v41"></a>DMA v4.1

DMA 的 v4.1 版本引進了支援的內部部署 SQL Server 資料庫移轉至 Azure SQL Database 受控執行個體的全方位評估。

評估工作流程可協助您偵測可能會影響您移轉至 Azure SQL Database 受控執行個體的下列問題：

* **不支援，或僅部分支援功能**。 DMA 會評估來源 SQL Server 資料庫使用中或在目標 Azure SQL Database 受控執行個體上不支援部分支援的功能。 然後此工具會提供一組完整的建議，Azure，以及緩和步驟，以便規劃移轉專案時，客戶可以用這項資訊到帳戶中可用的替代方法。

* **相容性問題**。 DMA 也會識別下列領域的相關的相容性問題：

  * 重大變更：可能會中斷移轉到目標資料庫的功能特定的結構描述物件。  我們建議修正資料庫移轉後的這些結構描述物件。
  * 行為變更：報告的結構描述物件可能會繼續運作，但它們可能會出現不同的行為，例如效能降低。
  * 告知性問題：這些物件不會影響移轉，但可能已被取代的 SQL Server 版本的功能。

完成評估之後，使用我們[Azure 資料庫移轉服務](https://azure.microsoft.com/services/database-migration/)(DMS) 來執行的 SQL Server 資料庫到 Azure SQL Database 受控執行個體移轉。  同時支援 DMS[離線](https://docs.microsoft.com/azure/dms/tutorial-sql-server-to-managed-instance)（單次） 和[線上](https://docs.microsoft.com/azure/dms/tutorial-sql-server-managed-instance-online)（最少停機時間） 的資料庫移轉至 Azure SQL Database 受控執行個體。

## <a name="dma-v40"></a>DMA v4.0

DMA 的 v4.0 版本引進了 「 Azure SQL 資料庫 SKU 建議 」 功能，可讓使用者能夠識別建議從裝載資料庫的電腦收集效能計數器為基礎的 Azure SQL 資料庫 SKU 的最小。 這項功能提供定價層、 計算層級，和最大的資料大小，以及每月預估的成本的相關建議。 它也提供佈建所有資料庫到 Azure 中大量的能力。

> [!NOTE]
> 這項功能目前是只能透過命令列介面 (CLI)。

如需詳細資料，請參閱文章[找出您的內部部署資料庫正確的 Azure SQL 資料庫 SKU](dma-sku-recommend-sql-db.md)。

## <a name="dma-v36"></a>DMA v3.6

DMA 的 3.6 版版本導入了 「 自動修復 」 會受到最常見的移轉封鎖器的結構描述物件。

此版本中提供下列移轉封鎖程式 autofix 和行為變更的問題：

* 使用未限定 Join 語法的結構描述物件。
* 使用舊版的 RAISEERROR 陳述式的結構描述物件。
* 使用順序的整數常值的 SQL 陳述式。

DMA 會自動結構描述轉換執行列出的問題所影響的物件，並會提示使用者進行確認，再繼續進行結構描述的轉換。 使用者可以檢閱建議的程式碼變更，然後選擇接受或拒絕任何給定的資料庫物件的所有轉換。

DMA 會使用 Microsoft 程式合成 （文字） 技術來提供建議的程式碼修正。 深入了解[PROSE](https://microsoft.github.io/prose/)。

## <a name="dma-v35"></a>DMA v3.5

DMA 的 v3.5 版本包含下列各項：

* 移轉至 Azure SQL Database （基準測試表示處理程序四次較快，與舊版 DMA） 的顯著效能改善。
* 記憶體使用量已進一步最佳化，改善移轉工作流程的穩定性。
* 能夠在結構描述和資料移轉期間略過評估，（如果您已經執行評估並解決任何重大結構描述物件，在移轉之前）。
* 若要解決與損毀時升級舊版的 SQL Server 的內部部署至更新版本，或在 Azure Vm 上的 SQL server 備份的檔案，提供不正確的網路共用路徑時，此工具的問題修正。

## <a name="dma-v34"></a>DMA v3.4

DMA 的 v3.4 版本包含下列各項：

* 做為來源移轉到 Azure SQL Database 的 SQL Server 2017 的支援。
* 穩定性、 效能及評估規則正確性增強功能。

## <a name="dma-v33"></a>DMA v3.3

DMA 的 v3.3 版本可讓移轉至新版本的 Windows 和 Linux 上的 SQL Server 2017 的內部部署 SQL Server 執行個體。 雖然 Windows 和 Linux 的整體移轉工作流程中都相同，移至 SQL Server 2017 linux 會需要幾個額外的考量。

### <a name="specifying-the-back-up-path"></a>指定的備份路徑

Linux 和 Windows 使用不同的路徑格式。 如此一來，移轉至 Linux 上的 SQL Server 2017 會要求使用者提供 Windows 與 Linux 兩種版本的實體檔案位置的路徑。 您可以根據實體檔案的位置不同的方式提供兩個版本的路徑。
如果實體的備份檔案是執行的電腦上：

* Linux，請使用 'samba' 會與網路上的其他電腦共用檔案共用。
* Windows 中，會使用 '/mnt' 命令來掛接到執行 Linux 的電腦上的共用。

> [!NOTE]
> 使用 'samba' 共用或 '/mnt' 命令的詳細資料已超出本文的範圍。

### <a name="migrating-windows-logins"></a>移轉的 Windows 登入

雖然在 Linux 上的 SQL Server 2017 正式支援的 Active Directory (AD) 登入移轉，它會需要額外的設定，才能順利運作。 請參閱文章[在 Linux 上的 SQL server 的 Active Directory 驗證](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication)上 SQL Server 2017 Linux 上的 Active Directory 登入所設定的詳細資訊。 在執行之後所需的設定，設定完成後，您可以如往常般移轉 Active Directory 登入。 如預期般運作，而不需要任何額外的設定，適用於標準的 SQL 驗證。

## <a name="dma-v32"></a>DMA v3.2

DMA 的 v3.2 版本包含下列各項：

* 結構描述和資料移轉會啟用內部部署 SQL Server 資料庫從 Azure SQL Database 使用新的移轉工作流程。
* 在結構描述移轉至 Azure SQL Database 時，DMA 來源資料庫物件的指令碼、 如何修正任何潛在的相容性問題，提供指引，然後將您的結構描述部署至 Azure。

## <a name="dma-v31"></a>DMA v3.1

DMA 的 v3.1 版本包含下列各項：

* Azure SQL Database 資料庫的定序，以改善的評估建議使用的不受支援的系統預存程序和 CLR 物件。
* 相容性層級 130、 120、 110 和 100 在移轉到 Azure SQL Database 時的評估指引。

## <a name="dma-v30"></a>DMA v3.0

DMA v3.0 發行擴充 Azure SQL 資料庫評估，以提供完整的建議，可協助修正的相關問題：

* 阻礙移轉的問題。
* 部分或不支援的功能和函式。

## <a name="dma-v21"></a>DMA v2.1

DMA 的 v2.1 版本包含下列各項：

* 支援命令列以自動模式，以協助執行大規模的評定執行評定。 如需詳細資料，請參閱文章[執行 Data Migration Assistant 從命令列](dma-commandline.md)。
* 當使用者啟動，然後關閉 DMA 的效能改進。
* 設定 SQL 連線逾時的功能。如需詳細資料，請參閱文章[組態設定，Data Migration assistant](dma-configurationsettings.md)。

## <a name="dma-v20"></a>DMA v2.0

DMA 的 v2.0 發行版本包含改善的 Stretch database 功能建議，以提供最大化省下的儲存體的適當優先順序的資料表。

## <a name="dma-v10"></a>DMA v1.0

DMA v1.0 發行時的初始版本，並提供：

* 探索可能會影響升級至 SQL Server 的內部部署版本的問題。 任何所發現的錯誤會被稱為相容性問題，並加以分類成下列區域：
  * 重大變更
  * 行為變更
  * 即將淘汰的功能
* 探索的目標 SQL Server 平台的資料庫可以受益於在升級後的新功能。 任何所發現的錯誤會被稱為功能建議，並加以分類成下列區域：
  * 效能
  * 安全性
  * 儲存體
* 若要執行評估的現代化使用者體驗。

## <a name="see-also"></a>另請參閱

[Data Migration Assistant 的概觀](../dma/dma-overview.md)
