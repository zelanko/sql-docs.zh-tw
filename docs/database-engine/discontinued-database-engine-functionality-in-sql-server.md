---
title: SQL Server 中已中止的資料庫引擎功能 | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- VIA protocol
- unsupported features [SQL Server]
- SQL Mail
- discontinued functionality [SQL Server]
- RESTORE WITH DBO_ONLY
- BACKUP WITH PASSWORD
- user instances enabled
- BACKUP WITH MEDIAPASSWORD
- AWE
- SQL-DMO
- '*= and =*'
- 80 compatibility levels
- COMPUTE BY
- user instance timeout
- sp_dropalias
- COMPUTE
- SSL
- WITH APPEND
- sys.database_principal_aliases
- sp_dboption
- DATABASEPROPERTY
- FASTFIRSTROW hint
- SET DISABLE_DEF_CNST_CHK
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= sql-server-linux-2017  || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a708aad1d483eaf28d559ff04424e515ec9f6aa7
ms.sourcegitcommit: ffb87aa292fc9b545c4258749c28df1bd88d7342
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2019
ms.locfileid: "71816665"
---
# <a name="discontinued-database-engine-functionality-in-sql-server"></a>SQL Server 中已中止的資料庫引擎功能
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主題描述 [!INCLUDE[ssDE](../includes/ssde-md.md)] 中不再可用的 [!INCLUDE[ssCurrent](../includes/ssnoversion-md.md)]功能。  

## <a name="discontinued-features-in-includesssqlv15includessssqlv15-mdmd"></a>[!INCLUDE[ssSQLv15](../includes/sssqlv15-md.md)] 中已中止的功能  

- 下列資料庫範圍設定選項已中止：

  - `DISABLE_BATCH_MODE_ADAPTIVE_JOIN`
  - `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK`
  - `DISABLE_INTERLEAVED_EXECUTION_TVF`

如需目前的設定選項，請參閱 [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。

>[!NOTE]
>[!INCLUDE[ssSQLv14](../includes/sssqlv14-md.md)] 中沒有任何已中止的功能。

## <a name="discontinued-features-in-includesssql15includessssql15-mdmd"></a>[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 中已中止的功能

- [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 是 64 位元應用程式。 即使有些元素是以 32 位元元件的形式執行，32 位元安裝已然中止。  

- 已停止相容性層級 90。 如需詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  

- ActiveX 子系統已停止。 請改用命令列或 PowerShell 指令碼。

- 啟動參數 **-h** 與 **-g**。 如需詳細資訊，請參閱 [Database Engine Service Startup Options](https://docs.microsoft.com/sql/database-engine/configure-windows/database-engine-service-startup-options?view=sql-server-2014)。

- 已中止安全通訊端層 (SSL) 加密。 請改用傳輸層安全性 (TLS)。 如需詳細資訊，請參閱[啟用資料庫引擎的加密連線](../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。

## <a name="previous-versions"></a>先前版本

- [SQL Server 2014 中已停止的 Database Engine 功能](https://docs.microsoft.com/sql/database-engine/discontinued-database-engine-functionality-in-sql-server-2016?view=sql-server-2014)

## <a name="see-also"></a>另請參閱

- [SQL Server 2016 中已被取代的 Database Engine 功能](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)
- [SQL Server 複寫中已被取代的功能](../relational-databases/replication/deprecated-features-in-sql-server-replication.md)