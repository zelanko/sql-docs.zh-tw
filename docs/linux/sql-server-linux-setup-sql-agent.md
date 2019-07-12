---
title: 在 Linux 上安裝 SQL Server 代理程式
description: 本文說明如何在 Linux 上安裝 SQL Server Agent。
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: 09751465dded818a51ca36df5a4328623b0b0a0a
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834687"
---
# <a name="install-sql-server-agent-on-linux"></a>在 Linux 上安裝 SQL Server 代理程式

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

 [SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)執行 SQL Server 的排程的工作。 從 SQL Server 2017 CU4 開始，SQL Server Agent 是隨附**mssql server**封裝，並預設為停用。 如需此版本的版本資訊以及 SQL Server Agent 支援的功能資訊，請參閱[Release Notes](sql-server-linux-release-notes.md)。

 安裝/啟用 SQL Server 代理程式：
- [針對 版本 2017 CU4 和更新版本中，啟用 SQL Server Agent](#EnableAgentAfterCU4)
- [針對版本 2017 cu3 開始 （含） 以下，安裝 SQL Server Agent](#InstallAgentBelowCU4)


## <a name="EnableAgentAfterCU4">針對 版本 2017 CU4 和更新版本中，啟用 SQL Server Agent</a>

 若要啟用 SQL Server Agent，請遵循下列步驟。

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> 如果您從 2017 CU3 升級，或下列代理程式安裝，SQL Server Agent 會自動啟用和前一個將會解除安裝代理程式套件。  

## <a name="InstallAgentBelowCU4">針對版本 2017 cu3 開始 （含） 以下，安裝 SQL Server Agent</a>

> [!NOTE]
> 安裝指示適用於 SQL Server 版本 2017 CU3 和以下版本。 然後再安裝 SQL Server Agent，第一次[安裝 SQL Server](sql-server-linux-setup.md#platforms)。 這會設定索引鍵和您在安裝時使用的儲存機制**mssql server agent**封裝。

安裝 SQL Server 代理程式，您的平台：
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name="RHEL">在 RHEL 上安裝</a>

使用下列步驟來安裝**mssql server agent** Red Hat Enterprise Linux 上。 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

如果您已經有**mssql server agent**安裝，您可以更新為最新的版本，使用下列命令：

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

如果您需要離線安裝時，找出在 SQL Server 代理程式套件下載[版本資訊](sql-server-linux-release-notes.md)。 然後使用[安裝 SQL Server](sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。

### <a name="ubuntu">在 Ubuntu 上安裝</a>

使用下列步驟來安裝**mssql server agent**在 Ubuntu 上。 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

如果您已經有**mssql server agent**安裝，您可以更新為最新的版本，使用下列命令：

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

如果您需要離線安裝時，找出在 SQL Server 代理程式套件下載[版本資訊](sql-server-linux-release-notes.md)。 然後使用[安裝 SQL Server](sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。

### <a name="SLES">在 SLES 上安裝</a>

使用下列步驟來安裝**mssql server agent** SUSE Linux Enterprise Server 上。 

安裝**mssql server 代理程式** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

如果您已經有**mssql server agent**安裝，您可以更新為最新的版本，使用下列命令：

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

如果您需要離線安裝時，找出在 SQL Server 代理程式套件下載[版本資訊](sql-server-linux-release-notes.md)。 然後使用[安裝 SQL Server](sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。

## <a name="next-steps"></a>後續步驟
如需有關如何使用 SQL Server Agent 來建立、 排程及執行工作的詳細資訊，請參閱 <<c0> [ 在 Linux 上執行的 SQL Server Agent 作業](sql-server-linux-run-sql-server-agent-job.md)。
