---
title: Linux 上的 SQL Server 複寫
description: 本文描述 Linux 上的 SQL Server 複寫。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/09/2019
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: f0e1acd5af76f5b0b075879fc1c5122713caed55
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75002022"
---
# <a name="sql-server-replication-on-linux"></a>Linux 上的 SQL Server 複寫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2017](../includes/sssqlv14-md.md)] ([CU18](https://support.microsoft.com/help/4527377)) 和更新版本支援 Linux 上 SQL Server 執行個體的 SQL Server 複寫。

使用 SQL Server Management Studio (SSMS) [複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)在 Linux 上設定複寫。

SQL Server 的執行個體可以參與任何複寫角色：

* 發行者
* 散發者
* 用戶

複寫結構描述可以混合使用作業系統平台。 例如，複寫結構描述可包含發行者和散發者的 Linux SQL Server 執行個體，而訂閱者則包含 Windows 和 Linux 的 SQL Server 執行個體。

Linux 上的 SQL Server 執行個體可以參與任何類型的複寫。

* 交易式
* 快照式

如需複寫的詳細資訊，請參閱 [SQL Server 複寫文件](../relational-databases/replication/sql-server-replication.md)。

## <a name="supported-features"></a>支援的功能

支援下列複寫功能：

* 快照式複寫
* 異動複寫
* 使用非預設連接埠進行複寫 <!--Add link to explanation-->
* 使用 AD 驗證進行複寫
* 跨 Windows 和 Linux 的複寫設定
* 異動複寫的立即更新

## <a name="limitations"></a>限制

不支援下列功能：

* 合併式複寫
* 點對點複寫
* Oracle 發行

## <a name="next-steps"></a>後續步驟

[設定 Linux 上的 SQL Server 複寫](sql-server-linux-replication-tutorial-tsql.md)

[範例：設定 Linux 上的 SQL Server 複寫](sql-server-linux-replication-configure.md)
