---
title: "管理 SQL Server on Linux |Microsoft 文件"
description: "本主題提供連結的一般管理工作和工具適用於 SQL Server 在 Linux 上執行。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 5f7c0f61cf9f441c56529ddaaddc96a0c318ce59
ms.contentlocale: zh-tw
ms.lasthandoff: 09/21/2017

---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>選擇正確的工具來管理 SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

有幾種方式來管理 Linux 上的 SQL Server 2017 RC2。 下節提供不同的管理工具和技術的更多資源指標的快速概觀。

## <a name="mssql-conf"></a>mssql conf 
**Mssql conf**工具設定 SQL Server on Linux。 如需詳細資訊，請參閱[設定 SQL Server on Linux 與 mssql conf](sql-server-linux-configure-mssql-conf.md)。

## <a name="transact-sql"></a>Transact-SQL

幾乎所有項目您可以在用戶端工具中也可以使用 TRANSACT-SQL 陳述式完成。 SQL Server 提供[動態管理檢視 (Dmv)](/sql-docs/docs/relational-databases/system-dynamic-management-views/system-dynamic-management-views) ，查詢 SQL Server 的組態與狀態。 另外還有[TRANSACT-SQL 命令](https://msdn.microsoft.com/library/bb510741.aspx)資料庫管理工作。 您可以在任何支援連接至 SQL Server 和執行 TRANSACT-SQL 查詢的用戶端工具來執行這些命令。 範例包括[sqlcmd](sql-server-linux-setup-tools.md)， [Visual Studio Code](sql-server-linux-develop-use-vscode.md)，和[SQL Server Management Studio](sql-server-linux-manage-ssms.md)。

## <a name="sql-server-management-studio-on-windows"></a>在 Windows 上的 SQL Server Management Studio

SQL Server Management Studio (SSMS) 是提供圖形化使用者介面來管理 SQL Server 的 Windows 應用程式。 雖然它目前只會在執行 Windows，您可以使用它來從遠端連線到您的 Linux SQL Server 執行個體。 如需使用 SSMS 管理 SQL Server 的詳細資訊，請參閱[使用 SSMS 管理 SQL Server on Linux](sql-server-linux-manage-ssms.md)。

## <a name="powershell"></a>PowerShell

PowerShell 提供豐富的命令列環境，來管理 SQL Server on Linux。 如需詳細資訊，請參閱[使用 PowerShell 來管理 SQL Server on Linux](sql-server-linux-manage-powershell.md)。

## <a name="next-steps"></a>後續的步驟

如需有關 SQL Server on Linux，請參閱[SQL Server on Linux](sql-server-linux-overview.md)。
