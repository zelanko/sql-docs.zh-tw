---
title: "管理 SQL Server on Linux |Microsoft 文件"
description: "本主題提供連結的一般管理工作和工具適用於 SQL Server 在 Linux 上執行。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: 
ms.workload: On Demand
ms.openlocfilehash: f6710b3e7bd40a2589333cebbf94c8b07f9aaa5d
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2018
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>選擇正確的工具來管理 SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

有幾種方式來管理 Linux 上的 SQL Server 2017。 下節提供不同的管理工具和技術的更多資源指標的快速概觀。

## <a name="mssql-conf"></a>mssql-conf 
**Mssql conf**工具設定 SQL Server on Linux。 如需詳細資訊，請參閱[設定 SQL Server on Linux 與 mssql conf](sql-server-linux-configure-mssql-conf.md)。

## <a name="transact-sql"></a>Transact-SQL

幾乎所有項目您可以在用戶端工具中也可以使用 TRANSACT-SQL 陳述式完成。 SQL Server 提供[動態管理檢視 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) ，查詢 SQL Server 的組態與狀態。 另外還有[TRANSACT-SQL 命令](https://msdn.microsoft.com/library/bb510741.aspx)資料庫管理工作。 您可以在任何支援連接至 SQL Server 和執行 TRANSACT-SQL 查詢，例如用戶端工具中執行這些命令[sqlcmd](sql-server-linux-setup-tools.md)或[Visual Studio Code](sql-server-linux-develop-use-vscode.md)。

## <a name="sql-server-operations-studio-preview"></a>SQL Server 作業 Studio （預覽）

新的 Microsoft SQL 作業 Studio （預覽） 是用來管理 SQL Server 的跨平台工具。 如需詳細資訊，請參閱[什麼是 Microsoft SQL 作業 Studio （預覽）](../sql-operations-studio/what-is.md)。

## <a name="sql-server-management-studio-on-windows"></a>在 Windows 上的 SQL Server Management Studio

SQL Server Management Studio (SSMS) 是提供圖形化使用者介面來管理 SQL Server 的 Windows 應用程式。 雖然它目前只會在執行 Windows，您可以使用它來從遠端連線到您的 Linux SQL Server 執行個體。 如需使用 SSMS 管理 SQL Server 的詳細資訊，請參閱[使用 SSMS 管理 SQL Server on Linux](sql-server-linux-manage-ssms.md)。

## <a name="mssql-cli-preview"></a>mssql cli （預覽）

Microsoft 已針對 SQL Server 發行新的跨平台指令碼工具[mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)。 這項工具目前為預覽狀態。

## <a name="powershell"></a>PowerShell

PowerShell 提供豐富的命令列環境，來管理 SQL Server on Linux。 如需詳細資訊，請參閱[使用 PowerShell 來管理 SQL Server on Linux](sql-server-linux-manage-powershell.md)。

## <a name="next-steps"></a>後續的步驟

如需有關 SQL Server on Linux，請參閱[SQL Server on Linux](sql-server-linux-overview.md)。
