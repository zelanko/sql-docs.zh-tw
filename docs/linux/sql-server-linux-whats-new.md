---
title: 有關 Linux 上的 SQL Server 2017 的新功能 |Microsoft Docs
description: 這篇文章強調有關 Linux 上的 SQL Server 2017 的新功能。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.openlocfilehash: 266982731cc98121e6456d10fb93c7ccffaa4b22
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719337"
---
# <a name="whats-new-for-sql-server-on-linux"></a>在 Linux 上的 SQL Server 的最新消息

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章描述在 Linux 上執行的 SQL Server 2017 的主要功能和可用的服務。

SQL Server 2019 預覽已發行。 這篇文章並未涵蓋 SQL Server 2019 預覽版本。 若要深入了解 SQL Server 2019 預覽，請參閱[什麼是適用於 Linux 的 SQL Server 2019 preview 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux)。

> [!NOTE]
> 除了這篇文章中的這些功能，累計更新會定期發行後 GA 版本。 這些累積更新提供許多改善和修正程式。 如需最新 CU 版本資訊，請參閱[ https://aka.ms/sql2017cu ](https://aka.ms/sql2017cu)。 下載套件及已知的問題，請參閱[版本資訊](sql-server-linux-release-notes.md)。

## <a name="sql-server-database-engine"></a>SQL Server Database Engine

- 啟用核心 SQL Server Database Engine 功能。
- 原生 Linux 路徑的支援。
- IPV6 支援。
- 支援在 NFS 上的資料庫檔案。
- 已啟用[傳輸層安全性](sql-server-linux-encrypted-connections.md)(TLS) 加密。
- 已啟用[Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。
- [可用性群組功能](sql-server-linux-availability-group-overview.md)以獲得高可用性。
- [全文檢索搜尋](sql-server-linux-setup-full-text-search.md)支援。

## <a name="sql-server-agent"></a>SQL Server Agent

- 已啟用[SQL Server Agent](sql-server-linux-setup-sql-agent.md)支援下列工作：
  - [Transact SQL 作業](sql-server-linux-run-sql-server-agent-job.md)
  - [DB 郵件](sql-server-linux-db-mail-sql-agent.md)
  - [記錄傳送](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- 在 Linux 上執行 SSIS 套件的能力。 如需詳細資訊，請參閱 <<c0> [ 在 Linux 上使用 ssis conf 設定 SQL Server Integration Services](sql-server-linux-configure-ssis.md)。

## <a name="other-improvements"></a>其他改進功能

- 命令列組態工具[mssql conf](sql-server-linux-configure-mssql-conf.md)。
- 自動的安裝支援[環境變數](sql-server-linux-configure-environment-variables.md)。
- 跨平台[Visual Studio Code 的 mssql server 延伸模組](sql-server-linux-develop-use-vscode.md)。
- 跨平台指令碼產生器中， [mssql scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md)。
- 跨平台的動態管理檢視 (DMV) 監視[DBFS 工具](https://github.com/Microsoft/dbfs)。

## <a name="next-steps"></a>後續步驟

若要在 Linux 上安裝 SQL Server，使用下列的教學課程中的其中一個：

- [在 Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [在 Docker 上執行](quickstart-install-connect-docker.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

若要查看其他 SQL Server 2017 中導入的增強功能，請參閱[What's New in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)。

> [!TIP]
> 如需常見問題的解答，請參閱[Linux 常見問題集 > 的 SQL Server](sql-server-linux-faq.md)。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
