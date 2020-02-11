---
title: Data Migration Assistant （SQL Server）總覽 |Microsoft Docs
description: 瞭解如何使用 Data Migration Assistant 將 SQL Server 資料庫移轉至其他 SQL Server 或 Azure 資料庫
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: 64c8416a15afd685559fe2d05c436c2e5fc1382d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73632857"
---
# <a name="overview-of-data-migration-assistant"></a>Data Migration Assistant 總覽

Data Migration Assistant （DMA）會偵測可能影響新版本 SQL Server 或 Azure SQL Database 中資料庫功能的相容性問題，以協助您升級至新式資料平臺。 DMA 可為您的目標環境提供效能和可靠性改善的建議，並可讓您將結構描述、資料和非內含的物件從來源伺服器移至目標伺服器。

> [!NOTE]
> 針對大型遷移（根據資料庫的數量和大小），我們建議您使用[Azure 資料庫移轉服務](/azure/dms/dms-overview)，其可大規模地遷移資料庫。
  
## <a name="get-data-migration-assistant"></a>取得 Data Migration Assistant

若要安裝 DMA，請從[Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=53595)下載最新版本的工具，然後執行**DataMigrationAssistant .msi**檔案。

## <a name="capabilities"></a>功能

- 評估內部部署 SQL Server 實例遷移至 Azure SQL database。評估工作流程可協助您偵測下列可能會影響 Azure SQL database 遷移的問題，並提供如何解決這些問題的詳細指引。

  - 遷移封鎖問題：探索封鎖將內部部署 SQL Server 資料庫移轉至 Azure SQL Database 的相容性問題。DMA 提供的建議可協助您解決這些問題。

  - 部分支援或不支援的功能：偵測目前在來源 SQL Server 實例上使用的部分支援或不支援的功能。DMA 提供一組完整的建議、Azure 中可用的替代方法，以及減少步驟，讓您可以將它們併入您的遷移專案。

- 找出可能影響升級至內部部署 SQL Server 的問題。這些會描述為相容性問題，並以下列類別進行組織：

  - 重大變更
  - 行為變更
  - 即將淘汰的功能

- 探索目標 SQL Server 平臺中，資料庫在升級後可受益的新功能。 這些會描述為功能建議，並以下列類別進行組織：

  - 效能
  - 安全性
  - 儲存體

- 將內部部署 SQL Server 實例遷移至裝載于內部部署或 Azure 虛擬機器（VM）且可從內部部署網路存取的新式 SQL Server 實例。 您可以使用 VPN 或其他技術來存取 Azure VM。 遷移工作流程可協助您遷移下列元件：

  - 資料庫的架構
  - 資料和使用者
  - 伺服器角色
  - SQL Server 和 Windows 登入

- 成功遷移之後，應用程式就可以順暢地連接到目標 SQL Server 資料庫。

- 評估內部部署 SQL Server Integration Services （SSIS）封裝遷移至 Azure SQL Database 或 Azure SQL Database 受控實例。 評量有助於找出可能影響遷移的問題。 這些會描述為相容性問題，並以下列類別進行組織：

  - 遷移封鎖程式：探索阻止將來源套件遷移至 Azure 的相容性問題。 DMA 提供的建議可協助您解決這些問題。

  - 資訊問題：偵測在來源套件中使用的部分支援或已淘汰的功能。

## <a name="prerequisites"></a>Prerequisites

若要執行評量，您必須是 SQL Server**系統管理員（sysadmin** ）角色的成員。

## <a name="supported-source-and-target-versions"></a>支援的來源和目標版本

DMA 會取代所有舊版的 SQL Server Upgrade Advisor，而且應該用於大部分 SQL Server 版本的升級。 支援的來源和目標版本包括：

**根源**

- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
-  Windows 上的 SQL Server 2017

**目標**

- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Windows 和 Linux 上的 SQL Server 2017
- SQL Server 2019
- Azure SQL Database 單一資料庫
- Azure SQL Database 受控執行個體
- 在 Azure 虛擬機器上執行的 SQL server

## <a name="see-also"></a>另請參閱

[評估您的 SQL Server 遷移](../dma/dma-assesssqlonprem.md)

[Data Migration Assistant：設定](../dma/dma-configurationsettings.md)

[使用 Data Migration Assistant 遷移內部部署 SQL Server](../dma/dma-migrateonpremsql.md)

[Data Migration Assistant：最佳做法](../dma/dma-bestpractices.md)
