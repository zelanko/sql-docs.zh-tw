---
title: Linux 上的 SQL Server 2017 新功能
description: 本文特別介紹 Linux 上的 SQL Server 2017 新功能。
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 6874c34c70b562ef726bda5abbda2aebe615cc08
ms.sourcegitcommit: bb56808dd81890df4f45636b600aaf3269c374f2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2019
ms.locfileid: "72890548"
---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>Linux 上的 SQL Server 2017 新功能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文描述適用於在 Linux 上執行的 SQL Server 2017 主要功能和服務。

> [!NOTE]
> 除了本文中的功能，之後還會定期發行累積更新。 這些累積更新提供許多改善和修正程式。 如需最新 CU 版本的詳細資訊，請參閱 [https://aka.ms/sql2017cu](https://aka.ms/sql2017cu)。 如需套件下載和已知問題，請參閱[版本資訊](sql-server-linux-release-notes.md)。

## <a name="sql-server-database-engine"></a>SQL Server Database Engine

- 已啟用核心 SQL Server 資料庫引擎功能。
- 支援原生 Linux 路徑。
- 支援 IPv6。
- 支援 NFS 上的資料庫檔案。
- 已啟用[傳輸層安全性](sql-server-linux-encrypted-connections.md) (TLS) 加密。
- 已啟用 [Azure Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。
- 可確保高可用性的[可用性群組功能](sql-server-linux-availability-group-overview.md)。
- 支援[全文檢索搜尋](sql-server-linux-setup-full-text-search.md)。

## <a name="sql-server-agent"></a>SQL Server Agent

- 已啟用下列工作的 [SQL Server Agent](sql-server-linux-setup-sql-agent.md) 支援：
  - [Transact-SQL 工作](sql-server-linux-run-sql-server-agent-job.md)
  - [DB 郵件](sql-server-linux-db-mail-sql-agent.md)
  - [記錄傳送](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- 可在 Linux 上執行 SSIS 套件。 如需詳細資訊，請參閱[使用 ssis-conf 設定 Linux 上的 SQL Server Integration Services](sql-server-linux-configure-ssis.md)。

## <a name="other-improvements"></a>其他改善

- 命令列設定工具 [mssql-conf](sql-server-linux-configure-mssql-conf.md)。
- 支援[環境變數](sql-server-linux-configure-environment-variables.md)的自動安裝。
- 跨平台 [Visual Studio Code mssql-server 延伸模組](sql-server-linux-develop-use-vscode.md)。
- 跨平台指令碼產生器 [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md)。
- 跨平台動態管理檢視 (DMV) 監視器 [DBFS 工具](https://github.com/Microsoft/dbfs)。

## <a name="next-steps"></a>後續步驟

若要在 Linux 上安裝 SQL Server，請使用下列其中一個教學課程：

- [在 Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [在 Docker 上執行](quickstart-install-connect-docker.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

如需常見問題的解答，請參閱 [Linux 上的 SQL Server 常見問題集](sql-server-linux-faq.md)。 若要查看 SQL Server 2017 中引進的其他改善，請參閱 [SQL Server 2017 的新功能](../sql-server/what-s-new-in-sql-server-2017.md)。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
