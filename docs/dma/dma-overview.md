---
title: Data Migration Assistant (SQL Server) 概觀 |Microsoft Docs
description: 了解如何使用 Data Migration Assistant 將 SQL Server 資料庫移轉至其他 SQL Server 或 Azure 資料庫
ms.custom: ''
ms.date: 03/12/2019
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
ms.author: rajpo
manager: jroth
ms.openlocfilehash: 2766005287a522a84d209d995be0de9a94e45c02
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794353"
---
# <a name="overview-of-data-migration-assistant"></a>Data Migration Assistant 的概觀
Data Migration Assistant (DMA) 可協助您升級至新式資料平台，藉由偵測可能會影響資料庫功能的新版本的 SQL Server 或 Azure SQL Database 的相容性問題。 DMA 建議的效能和可靠性的改進目標環境，並可讓您將您的結構描述、 資料和非內含性的物件從來源伺服器移至您的目標伺服器。

> [!NOTE] 
> （以數字和資料庫的大小） 的大型移轉，我們建議您使用[Azure 資料庫移轉服務](/azure/dms/dms-overview)，這可以大規模移轉資料庫。
  
## <a name="get-data-migration-assistant"></a>取得 Data Migration Assistant
若要安裝 DMA，下載最新版的工具，從[Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=53595)，然後執行**DataMigrationAssistant.msi**檔案。

## <a name="capabilities"></a>Capabilities
- 評估內部部署 SQL Server 執行個體移轉到 Azure SQL 資料庫。 評估工作流程可協助您偵測到下列問題，可能會影響 Azure SQL database 移轉，並提供有關如何解決這些問題的詳細指導方針。

  - 阻礙移轉的問題： 探索封鎖移轉內部部署 SQL Server 資料庫移轉到 Azure SQL database 的相容性問題。 DMA 會提供建議，協助您解決這些問題。

  - 部分支援或不受支援的功能： 偵測到目前正在使用來源 SQL Server 執行個體中的部分支援或不受支援的功能。 DMA 會提供一組完整的建議，Azure，以及補救步驟中可用的替代方法，以便將它們併入您的移轉專案。

- 找出可能會影響到在內部部署 SQL Server 升級的問題。 這些之所以被形容為相容性問題，並分成下列類別：

  - 重大變更
  - 行為變更
  - 即將淘汰的功能

- 探索資料庫可受益於在升級後的目標 SQL Server 平台的新功能。 這些會被稱為功能建議，並分成下列類別：

  - 效能
  - 安全性
  - 儲存體

- 最新 SQL Server 執行個體裝載內部部署或 Azure 虛擬機器 (VM) 可從您的內部部署網路存取，請移轉內部部署 SQL Server 執行個體。 Azure VM，可以使用 VPN 或其他技術來存取。 移轉工作流程可協助您移轉下列元件：

  - 資料庫的結構描述
  - 資料和使用者
  - 伺服器角色
  - SQL Server 和 Windows 登入

- 成功移轉之後，應用程式可以連接到目標 SQL Server 資料庫順暢地。

## <a name="prerequisites"></a>先決條件
若要進行評量，您必須是 SQL Server 的成員**sysadmin**角色。

## <a name="supported-source-and-target-versions"></a>支援的來源和目標版本
DMA 會取代所有舊版的 SQL Server Upgrade Advisor，並應用於大部分的 SQL Server 版本升級。 支援的來源和目標版本為：

**來源**
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016
- Windows 上的 SQL Server 2017

**目標**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- 在 Windows 和 Linux 上的 SQL Server 2017
- Azure SQL Database
- Azure SQL Database 受控執行個體

## <a name="see-also"></a>另請參閱
[評估您的 SQL Server 移轉](../dma/dma-assesssqlonprem.md)     
[資料移轉小幫手：組態設定](../dma/dma-configurationsettings.md)     
[使用 Data Migration Assistant 移轉內部部署 SQL Server](../dma/dma-migrateonpremsql.md)     
[資料移轉小幫手：最佳作法](../dma/dma-bestpractices.md)     
