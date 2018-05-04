---
title: 資料移轉小幫手 (SQL Server) 的概觀 |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2018
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: d7349e266f1d16310bf32c3b4c0307ba5c46bf27
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="overview-of-data-migration-assistant"></a>資料移轉小幫手的概觀

資料移轉小幫手 (DMA) 可讓您升級至現代化資料平台，就會偵測相容性問題，可能會影響資料庫的新版本的 SQL Server 和 Azure SQL Database 的功能。 DMA 效能和可靠性的改進您的目標環境的建議，並可讓您將您的結構描述、 資料和非內含性的物件從來源伺服器移至您的目標伺服器。

> [!NOTE] 
> 為大型 （依據資料庫的大小和數量） 移轉，建議使用[Azure 資料庫移轉服務](https://docs.microsoft.com/en-us/azure/dms/dms-overview)，大規模的資料庫的移轉。
  
## <a name="capabilities"></a>Capabilities

- 評估在內部部署移轉至 Azure SQL 資料庫的 SQL Server 執行個體。 評估工作流程可協助您偵測到下列問題，可能會影響 Azure SQL database 移轉，並提供如何解決這些問題的詳細指導方針。

  - 移轉封鎖問題： 探索相容性問題，區塊移轉內部部署 SQL Server 資料庫以 Azure SQL 資料庫。 DMA 提供建議，協助您解決這些問題。

  - 部分支援或不支援的功能： 偵測到目前正在使用來源 SQL Server 執行個體中的部分支援或不受支援的功能。 DMA 提供完整設定的建議，可在 Azure 中和補救步驟的替代方法，讓您可以併入您的移轉專案。

- 探索可能會影響升級至內部部署 SQL Server 的問題。 這些所謂的相容性問題，並分成下列類別：

  - 重大變更
  - 行為變更
  - 已被取代的功能

- 探索目標 SQL Server 平台的資料庫可以受益於在升級後的新功能。 這些功能的建議形式被描述，並分成下列類別：

  - 效能
  - Security
  - 儲存空間

- 將內部部署 SQL Server 執行個體移轉至的現代的 SQL Server 執行個體，裝載在內部部署或在 Azure 虛擬機器 (VM) 可從您的內部部署網路存取。 可以使用 VPN 或其他技術來存取 Azure VM。 移轉工作流程可協助您移轉下列元件：

  - 資料庫的結構描述
  - 資料和使用者
  - 伺服器角色
  - SQL Server 和 Windows 登入

- 成功移轉之後，應用程式可以連接到目標 SQL server 資料庫順暢。

## <a name="supported-source-and-target-versions"></a>支援的來源和目標版本

DMA 取代所有舊版的 SQL Server Upgrade Advisor，並適用於大多數的 SQL Server 版本升級。 遵循支援的來源和目標版本。

**來源**
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016
- 在 Windows 上的 SQL Server 2017

**目標**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- 在 Windows 和 Linux 上的 SQL Server 2017
- Azure SQL Database

> [!NOTE] 
> DMA 目前不支援 Azure SQL Database 管理執行個體做為目標。

## <a name="installation"></a>安裝

若要安裝 DMA，下載最新版的工具，從[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595)，然後執行**DataMigrationAssistant.msi**檔案。

## <a name="see-also"></a>另請參閱

[評估您的 SQL Server 移轉](../dma/dma-assesssqlonprem.md)

[資料移轉小幫手： 組態設定](../dma/dma-configurationsettings.md)

[使用資料移轉小幫手移轉內部部署 SQL Server](../dma/dma-migrateonpremsql.md)

[資料移轉小幫手： 最佳作法](../dma/dma-bestpractices.md)



