---
title: "新功能 SQL Server on Linux 2017 |Microsoft 文件"
description: "本文章重點說明在 Linux 上的 SQL Server 2017 的新功能。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.workload: On Demand
ms.openlocfilehash: fd7f69a8cb21fa8aaabb518f9b3d1d178606a685
ms.sourcegitcommit: f0c5e37c138be5fb2cbb93e9f2ded307665b54ea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/24/2018
---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>在 Linux 上的 SQL Server 2017 的新功能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文描述在 Linux 上執行的 SQL Server 2017 可用服務的主要功能。

> [!NOTE]
> 除了在本文中的這些功能，累計更新定期發行後發行 GA 版本。 這些累積更新提供許多改善和修正程式。 如需最新 CU 版本資訊，請參閱[http://aka.ms/sql2017cu](http://aka.ms/sql2017cu)。 如需下載套件和已知的問題，請參閱[版本資訊](sql-server-linux-release-notes.md)。

## <a name="sql-server-database-engine"></a>SQL Server Database Engine

- 啟用核心 SQL Server Database Engine 功能。
- 支援原生 Linux 路徑。
- IPV6 支援。
- 支援 NFS 上資料庫檔案。
- 啟用[透明的層級安全性](sql-server-linux-encrypted-connections.md)(TLS) 加密。
- 啟用[Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。
- [可用性群組功能](sql-server-linux-availability-group-overview.md)高可用性。
- [全文檢索搜尋](sql-server-linux-setup-full-text-search.md)支援。

## <a name="sql-server-agent"></a>SQL Server Agent

- 啟用[SQL Server Agent](sql-server-linux-setup-sql-agent.md)支援下列工作：
  - [Transact SQL 作業](sql-server-linux-run-sql-server-agent-job.md)
  - [DB 郵件](sql-server-linux-db-mail-sql-agent.md)
  - [記錄傳送](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- 在 Linux 上執行 SSIS 封裝的功能。 如需詳細資訊，請參閱[ssis conf 與 Linux 上設定 SQL Server Integration Services](sql-server-linux-configure-ssis.md)。

## <a name="other-improvements"></a>其他改進功能

- 命令列組態工具、 [mssql conf](sql-server-linux-configure-mssql-conf.md)。
- 使用自動的安裝支援[環境變數](sql-server-linux-configure-environment-variables.md)。
- 跨平台[Visual Studio Code mssql 伺服器延伸模組](sql-server-linux-develop-use-vscode.md)。
- 跨平台指令碼產生器， [mssql scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md)。
- 跨平台的動態管理檢視 (DMV) 監視， [DBFS 工具](https://github.com/Microsoft/dbfs)。

## <a name="next-steps"></a>後續的步驟

若要安裝 SQL Server on Linux，使用下列教學課程之一：

- [Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [執行 docker](quickstart-install-connect-docker.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

若要查看其他 SQL Server 2017 中導入的增強功能，請參閱[What's New in SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)。

> [!TIP]
> 常見問題的解答，請參閱[Linux 常見問題集 > 的 SQL Server](sql-server-linux-faq.md)。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
