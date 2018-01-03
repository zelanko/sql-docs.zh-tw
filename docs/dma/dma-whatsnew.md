---
title: "在資料移轉小幫手 (SQL Server) 的新 |Microsoft 文件"
ms.custom: 
ms.date: 10/03/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, new features
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 07d72eb6c4d40c3e61f4292616f9eda99d6d4742
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="whats-new-in-data-migration-assistant"></a>在資料移轉小幫手最新消息

本主題列出新增的項目在每個版本中的資料移轉小幫手 (DMA)。

## <a name="dma-v33"></a>DMA v3.3
DMA v3.3 發行可讓移轉至新版的 SQL Server 2017，在 Windows 和 Linux 上的內部部署 SQL Server 執行個體。 雖然 Windows 和 Linux 的整體移轉工作流程中都相同，適用於 Linux 移至 SQL Server 2017 會需要幾個額外的考量。

### <a name="specifying-the-back-up-path"></a>指定備份路徑
Linux 和 Windows 使用不同的路徑格式。 如此一來，若要在 Linux 上的 SQL Server 2017 移轉會要求使用者提供的實體檔案的位置路徑的 Windows 和 Linux 版本。 這是根據實體檔案的位置不同的方式達成。
如果實體備份檔案是執行的電腦上：
- Linux，請使用 'samba' 共用與網路上的其他電腦共用檔案。
-   Windows 中，使用 'mnt' 命令來掛接到執行 Linux 的電腦上的共用。

> [!NOTE]
> 請使用 'samba' 共用或 'mnt' 命令的詳細資料已超出本文的範圍。

### <a name="migrating-windows-logins"></a>移轉的 Windows 登入
雖然在 Linux 上的 SQL Server 2017 正式支援的 Active Directory (AD) 登入移轉，它會需要額外設定才能順利運作。 請參閱主題[Active Directory 驗證與 SQL Server on Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-active-directory-authentication)針對設定 SQL Server 2017 on Linux 上的 Active Directory 登入的詳細資訊。 在此之後安裝程式完成時，您可以如往常般在移轉 Active Directory 登入。 使用標準 SQL 驗證的運作方式如預期般無須進行任何額外的設定。

## <a name="dma-v32"></a>DMA v3.2
DMA 的 v3.2 版本包含下列功能：

- 結構描述和資料移轉會啟用內部部署 SQL Server 資料庫從 Azure SQL Database 與新的移轉工作流程。

- 在結構描述移轉至 Azure SQL Database 時，DMA 指令碼來源資料庫物件、 如何修正任何可能發生的相容性問題，提供指引，並將您的結構描述部署到 Azure。

## <a name="dma-v31"></a>DMA v3.1
DMA 的 v3.1 版本包含下列功能：

- Azure SQL Database 資料庫定序，以改善的評估建議使用不支援的系統預存程序和 CLR 物件。

- 相容性層級 130、 120、 110 和 100 移轉到 Azure SQL Database 時的評估指引。

## <a name="dma-v30"></a>DMA v3.0
DMA v3.0 發行擴充 Azure SQL 資料庫評估，以提供完整的建議來協助修正的相關問題：

- 移轉封鎖問題。

- 部分或不支援的功能和函式。

## <a name="dma-v21"></a>DMA v2.1
DMA 的 v2.1 版本包含下列功能：
- 支援命令列執行自動安裝模式，這樣可協助您評估執行大規模的評估。 如需詳細資料，請參閱主題[執行資料移轉小幫手從命令列](dma-commandline.md)。

- 當使用者啟動並關閉 DMA 的效能改進。

- 設定 SQL 連接逾時的能力。如需詳細資料，請參閱主題[組態設定，資料移轉小幫手](dma-configurationsettings.md)。

## <a name="dma-v20"></a>DMA v2.0
DMA 的 v2.0 發行版本包含改良的 Stretch 資料庫功能建議，以提供最大化的存放裝置節省的適當優先順序的資料表。

## <a name="dma-v10"></a>DMA v1.0
DMA 的 v1.0 版本是初始版本中，並提供：
- 探索可能會影響升級為 SQL Server 的內部部署版本的問題。 相容性問題，以描述任何發現與它們分成下列領域：
    -   重大變更
    - 行為變更
    - 已被取代的功能

- 探索的資料庫可以受益於升級的目標 SQL Server 平台的新功能。 功能的建議事項，以描述任何發現與它們分成下列領域：
    - [效能]
    - Security
    - Storage

-   若要執行評估的現代化使用者體驗。

## <a name="see-also"></a>另請參閱

[資料移轉小幫手的概觀](../dma/dma-overview.md)
