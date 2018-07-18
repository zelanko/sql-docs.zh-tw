---
title: 什麼是新 Data Migration Assistant (SQL Server) |Microsoft 文件
ms.custom: ''
ms.date: 07/09/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, new features
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 620590f03bf429dbc1633a1f78bb921def5fd585
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982150"
---
# <a name="whats-new-in-data-migration-assistant"></a>在 Data Migration Assistant 中最新消息
本主題列出新增的項目在每個版本的 Data Migration Assistant (DMA)。

## <a name="dma-v36"></a>DMA 3.6 版
DMA 的 3.6 版版本導入了 「 自動修復 」 會受到最常見的移轉封鎖器的結構描述物件。

此版本中提供下列移轉封鎖程式自動修正和行為變更的問題：
- 使用未限定 Join 語法的結構描述物件。
- 使用舊版的 RAISEERROR 陳述式的結構描述物件。
- 使用順序的整數常值的 SQL 陳述式。

DMA 會自動結構描述轉換執行列出的問題所影響的物件，並會提示使用者進行確認，再繼續進行結構描述的轉換。 使用者可以檢閱建議的程式碼變更，然後選擇接受或拒絕任何給定的資料庫物件的所有轉換。

DMA 會使用 Microsoft 程式合成 （文字） 技術來提供建議的程式碼修正。 深入了解[PROSE](https://microsoft.github.io/prose/)。

## <a name="dma-v35"></a>DMA v3.5
DMA 的 v3.5 版本包含下列各項：
- 移轉至 Azure SQL Database （基準測試表示處理程序四次較快，與舊版 DMA） 的顯著效能改善。
- 記憶體使用量已進一步最佳化，改善移轉工作流程的穩定性。
- 能夠在結構描述和資料移轉期間略過評估，（如果您已經執行評估並解決任何重大結構描述物件，在移轉之前）。
- 若要解決與損毀時升級舊版的 SQL Server 的內部部署至更新版本，或在 Azure Vm 上的 SQL server 備份的檔案，提供不正確的網路共用路徑時，此工具的問題修正。

## <a name="dma-v34"></a>DMA 3.4 版
DMA 的 v3.4 版本包含下列各項：
- 做為來源移轉到 Azure SQL Database 的 SQL Server 2017 的支援。
- 穩定性、 效能及評估規則正確性增強功能。

## <a name="dma-v33"></a>DMA v3.3
DMA 的 v3.3 版本可讓移轉至新版本的 Windows 和 Linux 上的 SQL Server 2017 的內部部署 SQL Server 執行個體。 雖然 Windows 和 Linux 的整體移轉工作流程中都相同，移至 SQL Server 2017 linux 會需要幾個額外的考量。

### <a name="specifying-the-back-up-path"></a>指定的備份路徑
Linux 和 Windows 使用不同的路徑格式。 如此一來，移轉至 Linux 上的 SQL Server 2017 會要求使用者提供 Windows 與 Linux 兩種版本的實體檔案位置的路徑。 您可以根據實體檔案的位置不同的方式提供兩個版本的路徑。
如果實體的備份檔案是執行的電腦上：
- Linux，請使用 'samba' 會與網路上的其他電腦共用檔案共用。
- Windows 中，會使用 '/mnt' 命令來掛接到執行 Linux 的電腦上的共用。

> [!NOTE]
> 使用 'samba' 共用或 '/mnt' 命令的詳細資料已超出本文的範圍。

### <a name="migrating-windows-logins"></a>移轉的 Windows 登入
雖然在 Linux 上的 SQL Server 2017 正式支援的 Active Directory (AD) 登入移轉，它會需要額外的設定，才能順利運作。 請參閱主題[在 Linux 上的 SQL server 的 Active Directory 驗證](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-authentication)上 SQL Server 2017 Linux 上的 Active Directory 登入所設定的詳細資訊。 在執行之後所需的設定，設定完成後，您可以如往常般移轉 Active Directory 登入。 如預期般運作，而不需要任何額外的設定，適用於標準的 SQL 驗證。

## <a name="dma-v32"></a>DMA v3.2
DMA 的 v3.2 版本包含下列各項：

- 結構描述和資料移轉會啟用內部部署 SQL Server 資料庫從 Azure SQL Database 使用新的移轉工作流程。
- 在結構描述移轉至 Azure SQL Database 時，DMA 來源資料庫物件的指令碼、 如何修正任何潛在的相容性問題，提供指引，然後將您的結構描述部署至 Azure。

## <a name="dma-v31"></a>DMA v3.1
DMA 的 v3.1 版本包含下列各項：

- Azure SQL Database 資料庫的定序，以改善的評估建議使用的不受支援的系統預存程序和 CLR 物件。
- 相容性層級 130、 120、 110 和 100 在移轉到 Azure SQL Database 時的評估指引。

## <a name="dma-v30"></a>DMA v3.0
DMA v3.0 發行擴充 Azure SQL 資料庫評估，以提供完整的建議，可協助修正的相關問題：

- 阻礙移轉的問題。
- 部分或不支援的功能和函式。

## <a name="dma-v21"></a>DMA v2.1
DMA 的 v2.1 版本包含下列各項：
- 支援命令列以自動模式，以協助執行大規模的評定執行評定。 如需詳細資料，請參閱主題[執行 Data Migration Assistant 從命令列](dma-commandline.md)。
- 當使用者啟動，然後關閉 DMA 的效能改進。
- 設定 SQL 連線逾時的功能。如需詳細資料，請參閱主題[組態設定，Data Migration assistant](dma-configurationsettings.md)。

## <a name="dma-v20"></a>DMA v2.0
DMA 的 v2.0 發行版本包含改善的 Stretch database 功能建議，以提供最大化省下的儲存體的適當優先順序的資料表。

## <a name="dma-v10"></a>DMA v1.0
DMA v1.0 發行時的初始版本，並提供：
- 探索可能會影響升級至 SQL Server 的內部部署版本的問題。 任何所發現的錯誤會被稱為相容性問題，並分成下列領域：
    - 重大變更
    - 行為變更
    - 已被取代的功能
- 探索的資料庫可以受益於升級的目標 SQL Server 平台的新功能。 任何所發現的錯誤會被稱為功能建議，並分成下列領域：
    - 效能
    - Security
    - Storage
-   若要執行評估的現代化使用者體驗。

## <a name="see-also"></a>另請參閱
[Data Migration Assistant 的概觀](../dma/dma-overview.md)
