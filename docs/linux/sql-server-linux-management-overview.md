---
title: 管理 Linux 上的 SQL Server |Microsoft Docs
description: 本文提供一般管理工作和工具的連結適用於 SQL Server 在 Linux 上執行。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.custom: sql-linux
ms.openlocfilehash: c87533096357117fda518794d961dfacca2ce481
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "46712910"
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>選擇正確的工具來管理 SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

有幾種方式來管理 SQL Server on Linux。 下一節提供不同的管理工具和技術，具有更多資源的指標的快速概觀。

## <a name="mssql-conf"></a>mssql-conf 

**Mssql conf**工具在 Linux 上設定 SQL Server。 如需詳細資訊，請參閱 <<c0> [ 設定 SQL Server on Linux 使用 mssql-conf](sql-server-linux-configure-mssql-conf.md)。

## <a name="transact-sql"></a>Transact-SQL

幾乎能夠進行的所有用戶端工具也可以使用 TRANSACT-SQL 陳述式完成。 SQL Server 提供[動態管理檢視 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) ，查詢 [狀態] 和 SQL Server 的組態。 另外還有[TRANSACT-SQL 命令](../t-sql/language-reference.md)資料庫管理工作。 您可以執行下列命令中支援連接到 SQL Server 和執行 TRANSACT-SQL 查詢，例如任何用戶端工具[sqlcmd](sql-server-linux-setup-tools.md)或是[Visual Studio Code](sql-server-linux-develop-use-vscode.md)。

## <a name="azure-data-studio-preview"></a>Azure Data Studio （預覽）

新的 Azure Data Studio （預覽） 是用於管理 SQL Server 的跨平台工具。 如需詳細資訊，請參閱 < [Azure Data Studio （預覽）](../azure-data-studio/what-is.md)。

## <a name="sql-server-management-studio-on-windows"></a>在 Windows 上的 SQL Server Management Studio

SQL Server Management Studio (SSMS) 是用於管理 SQL Server 提供圖形化使用者介面的 Windows 應用程式。 雖然它目前只能在 Windows 上執行，您可以從遠端連線到您的 Linux SQL Server 執行個體中使用它。 如需有關如何使用 SSMS 管理 SQL Server 的詳細資訊，請參閱 <<c0> [ 使用 SSMS 管理 SQL Server on Linux](sql-server-linux-manage-ssms.md)。

## <a name="mssql-cli-preview"></a>mssql cli （預覽）

Microsoft 已發行新的跨平台指令碼工具，適用於 SQL Server [mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)。 這項工具目前為預覽狀態。

## <a name="powershell"></a>PowerShell

PowerShell 提供豐富的命令列環境，來管理 SQL Server on Linux。 如需詳細資訊，請參閱 <<c0> [ 使用 PowerShell 管理 SQL Server on Linux](sql-server-linux-manage-powershell.md)。

## <a name="next-steps"></a>後續步驟

在 Linux 上 SQL Server 的相關資訊，請參閱[在 Linux 上的 SQL Server](sql-server-linux-overview.md)。
