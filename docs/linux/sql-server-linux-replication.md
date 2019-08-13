---
title: Linux 上的 SQL Server 複寫
description: 本文描述 Linux 上的 SQL Server 複寫。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 10/17/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b049866d9752485cb1b9eb609404a3bd86f28a41
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68065188"
---
# <a name="sql-server-replication-on-linux"></a>Linux 上的 SQL Server 複寫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 引進對 Linux 上 SQL Server 執行個體進行 SQL Server 複寫的功能。

使用 SQL Server Management Studio (SSMS) [複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)在 Linux 上設定複寫。

SQL Server 的執行個體可以參與任何複寫角色：

* 發行者
* 散發者
* 訂閱者

複寫結構描述可以混合使用作業系統平台。 例如，複寫結構描述可包含發行者和散發者的 Linux SQL Server 執行個體，而訂閱者則包含 Windows 和 Linux 的 SQL Server 執行個體。

Linux 上的 SQL Server 執行個體可以參與任何類型的複寫。

* 異動
* 合併式
* 快照式

如需複寫的詳細資訊，請參閱 [SQL Server 複寫文件](../relational-databases/replication/sql-server-replication.md)。

## <a name="supported-features"></a>支援的功能

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 支援下列複寫功能：

* 快照式複寫
* 異動複寫
* 合併式複寫
* 點對點複寫
* 使用非預設連接埠進行複寫 <!--Add link to explanation-->
* 使用 AD 驗證進行複寫
* 跨 Windows 和 Linux 的複寫設定
* 異動複寫的立即更新

## <a name="limitations"></a>限制

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 不支援下列功能：

* 立即更新訂閱者
* Oracle 發行

## <a name="next-steps"></a>後續步驟

[設定 Linux 上的 SQL Server 複寫](sql-server-linux-replication-tutorial-tsql.md)

[範例：設定 Linux 上的 SQL Server 複寫](sql-server-linux-replication-configure.md)
