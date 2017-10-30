---
title: "SQL Server on Linux 的安全性限制 |Microsoft 文件"
description: "本主題描述 SQL Server Linux 的限制。"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 45f88572804d236c209ab86884fc0fcbc432bc62
ms.contentlocale: zh-tw
ms.lasthandoff: 10/02/2017

---
# <a name="security-limitations-for-sql-server-on-linux"></a>SQL Server on Linux 的安全性限制

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

在 Linux 上的 SQL Server 目前有下列限制：

* 提供標準的密碼原則。 MUST_CHANGE 是唯一可設定的選項。  
* 不支援 「 可延伸金鑰管理。 
* 不支援使用儲存在 Azure 金鑰保存庫金鑰。
* SQL Server 會產生自己的自我簽署的憑證來加密連線。 目前，SQL Server 無法設定為使用使用者提供憑證以進行 SSL 或 TLS。 

如需 SQL Server 中可用的安全性功能的詳細資訊，請參閱[SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。

## <a name="next-steps"></a>後續的步驟

如需常見的安全性工作，請參閱[開始使用 Linux 上的 SQL Server 安全性功能](sql-server-linux-security-get-started.md)。   
指令碼來變更 TCP 連接埠號碼，SQL Server 目錄中，並設定 traceflag 或定序，請參閱[設定 SQL Server on Linux 與 mssql conf](sql-server-linux-configure-mssql-conf.md)。

