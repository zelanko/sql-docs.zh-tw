---
title: 在 Linux 上的 SQL Server 複寫 |Microsoft Docs
description: 本文說明在 Linux 上的 SQL Server 複寫。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 10/17/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ac812b8f39e9332f8bfcc22e91a6f575ef2873d7
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705105"
---
# <a name="sql-server-replication-on-linux"></a>在 Linux 上的 SQL Server 複寫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 介紹 SQL Server 複寫的 Linux 上的 SQL Server 執行個體。

使用 SQL Server Management Studio (SSMS) 在 Linux 上設定複寫[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

SQL Server 的執行個體可以參與任何複寫角色：

* 發行者
* 散發者
* 訂閱者

複寫結構描述可以混搭作業系統平台。 例如，複寫結構描述可能包括發行者和散發者上，在 Linux 上的 SQL Server 的執行個體，以及訂閱者包含在 Windows 與 Linux 上的 SQL Server 執行個體。

Linux 上的 SQL Server 執行個體可以參與任何類型的複寫。

* 異動
* 合併式
* 快照式

如需複寫的詳細資訊，請參閱 < [SQL Server 複寫的文件](../relational-databases/replication/sql-server-replication.md)。

## <a name="supported-features"></a>支援的功能

針對[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]下列複寫功能支援：

* 快照式複寫
* 異動複寫
* 合併式複寫
* 對等項目-複寫
* 使用非預設連接埠的複寫 <!--Add link to explanation-->
* 使用 AD 驗證的複寫
* 跨 Windows 與 Linux 的複寫設定
* 對於異動複寫的立即更新

## <a name="limitations"></a>限制

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 不支援下列功能：

* 立即更新訂閱者
* Oracle 發行

## <a name="next-steps"></a>後續步驟

[在 Linux 上設定 SQL Server 複寫](sql-server-linux-replication-tutorial-tsql.md)

[範例：在 Linux 上設定 SQL Server 複寫](sql-server-linux-replication-configure.md)
