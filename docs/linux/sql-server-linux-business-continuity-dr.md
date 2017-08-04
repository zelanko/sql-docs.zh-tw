---
title: "SQL Server on Linux 的災害復原 |Microsoft 文件"
description: 
author: mihaelab
ms.author: mihaelab
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: c75717c8-c677-4033-8ca6-d0ac93aee04d
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 86f41971e06efb767dde336cf93f9224a204176d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="business-continuity-and-database-recovery-sql-server-on-linux"></a>商務持續性和資料庫復原 SQL Server on Linux

在 Linux 上的 SQL Server 可讓組織達成各式各樣的服務等級協定以容納各種商務需求的目標。

最簡單的解決方案會運用虛擬化技術，以達到較高程度的恢復功能針對主機層級失敗容錯功能，針對硬體故障，以及彈性和資源極大化。 這些系統可以執行內部部署私人或公用雲端或混合式環境中。 保護的嚴重損壞修復的最簡單形式是資料庫備份。 SQL Server 2017 RC2 中可用的簡單解決方案包括：

- **VM 容錯移轉**
    - 針對客體和作業系統層級失敗的恢復功能
    - 未計劃及經過規劃的事件
    - 最小的修補和升級的停機時間
    - 以分鐘為單位的 RTO


- [**資料庫備份和還原**](sql-server-linux-backup-and-restore-database.md) 
    - 防止意外或惡意的資料損毀
    - 災害復原保護
    - RTO 小時以分鐘為單位

標準的高可用性和災害復原技術提供結合可靠的共用存放裝置基礎結構的執行個體層級保護。 SQL Server 2017 RC2 標準的高可用性包含：

- [**容錯移轉叢集**](sql-server-linux-shared-disk-cluster-configure.md)
    - 執行個體層級的保護
    - 自動偵測和容錯移轉
    - 針對作業系統和 SQL Server 故障的恢復功能
    - 以秒為單位為分鐘 RTO


## <a name="summary"></a>摘要

在 Linux 上的 SQL Server 2017 RC2 包含虛擬化、 備份和還原及容錯移轉叢集，以支援高可用性和災害復原。 
