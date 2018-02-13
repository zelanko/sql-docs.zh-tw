---
title: "Linux 上安裝 SQL Server Agent |Microsoft 文件"
description: "本文說明如何在 Linux 上安裝 SQL Server 代理程式。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.workload: On Demand
ms.openlocfilehash: 7db50a59a4a6ce9ab7aa416e4ac8d597449541b7
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2018
---
# <a name="install-sql-server-agent-on-linux"></a>Linux 上安裝 SQL Server 代理程式

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

下列步驟安裝 SQL Server Agent (**mssql server agent**) 在 Linux 上。 [SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent)執行 SQL Server 的排程的工作。 在這一版的 SQL Server 代理程式所支援之功能的資訊，請參閱[Release Notes](sql-server-linux-release-notes.md)。

> [!NOTE]
> 之前先安裝 SQL Server Agent，[安裝 SQL Server 2017](sql-server-linux-setup.md#platforms)。 這會設定索引鍵和您在安裝時使用的儲存機制**mssql server agent**封裝。

安裝 SQL Server 代理程式，您為平台：

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">RHEL 上安裝</a>

使用下列步驟來安裝**mssql server agent** Red Hat Enterprise Linux 上。 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

如果您已經有**mssql server agent**安裝，您可以更新為最新版本，並輸入下列命令：

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

如果您需要離線安裝，找出在 SQL Server 代理程式套件下載[版本資訊](sql-server-linux-release-notes.md)。 然後使用 文件中所述的相同離線安裝步驟[安裝 SQL Server](sql-server-linux-setup.md#offline)。

## <a name="ubuntu">在 Ubuntu 上安裝</a>

使用下列步驟來安裝**mssql server agent** Ubuntu 上。 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

如果您已經有**mssql server agent**安裝，您可以更新為最新版本，並輸入下列命令：

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

如果您需要離線安裝，找出在 SQL Server 代理程式套件下載[版本資訊](sql-server-linux-release-notes.md)。 然後使用 文件中所述的相同離線安裝步驟[安裝 SQL Server](sql-server-linux-setup.md#offline)。

## <a name="SLES">SLES 上安裝</a>

使用下列步驟來安裝**mssql server agent** SUSE Linux Enterprise Server 上。 

Install **mssql-server-agent** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

如果您已經有**mssql server agent**安裝，您可以更新為最新版本，並輸入下列命令：

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

如果您需要離線安裝，找出在 SQL Server 代理程式套件下載[版本資訊](sql-server-linux-release-notes.md)。 然後使用 文件中所述的相同離線安裝步驟[安裝 SQL Server](sql-server-linux-setup.md#offline)。

## <a name="next-steps"></a>後續的步驟
如需有關如何使用 SQL Server Agent 來建立、 排程及執行工作的詳細資訊，請參閱[在 Linux 上執行的 SQL Server Agent 作業](sql-server-linux-run-sql-server-agent-job.md)。
