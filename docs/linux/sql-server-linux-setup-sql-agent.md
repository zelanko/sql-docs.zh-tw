---
title: 在 Linux 上設定 SQL Server Agent
description: 此文章描述如何在 Linux 上啟用或安裝 SQL Server Agent。
author: VanMSFT
ms.author: vanto
ms.date: 12/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: 85869c797e8f91ca28d468c6a4a52dd52ea45a92
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882531"
---
# <a name="install-sql-server-agent-on-linux"></a>在 Linux 上安裝 SQL Server Agent

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

此文章描述如何在 Linux 上啟用或安裝 SQL Server Agent。

[SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) 會執行已排程的 SQL Server 作業。 從 SQL Server 2017 CU4 開始，SQL Server Agent 已隨附於 **mssql-server** 套件，而且預設為停用。 如需此 SQL Server Agent 版本所支援功能的相關資訊及版本資訊，請參閱[版本資訊](sql-server-linux-release-notes.md)。

## <a name="instructions"></a>Instructions

在 Linux 上使用 SQL Server Agent 之前，請使用下列步驟來啟用或安裝它。

1. 在 `/etc/hosts` 檔案中新增您的主機名稱 (包含和不包含網域)。 下列行顯示這些項目格式的範例：

   ```bash
   "IP Address" "hostname"
   "IP Address" "hostname.domain.com"
   ```

1. 請根據您的 SQL Server 版本遵循下列其中一小節的指示：

   | 版本 | Instructions |
   |---|---|
   | SQL Server 2017 CU4 和更高版本</br>SQL Server 2019 | [啟用 SQL Server Agent](#EnableAgentAfterCU4) |
   | SQL Server 2017 CU3 和更低版本 | [安裝 SQL Server Agent](#InstallAgentBelowCU4) |

## <a name="enable-the-sql-server-agent"></a><a id="EnableAgentAfterCU4"></a>啟用 SQL Server Agent

針對 SQL Server 2019 和 SQL Server 2017 CU4 和更高版本，您只需要啟用 SQL Server Agent。 您不需要安裝個別套件。

若要啟用 SQL Server Agent，請遵循下列步驟。

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> 如果您從已安裝 Agent 的 2017 CU3 或較低版本升級，將自動啟用 SQL Server Agent，並將解除安裝先前的 Agent 套件。  

## <a name="install-the-sql-server-agent"></a><a name="InstallAgentBelowCU4"></a>安裝 SQL Server Agent

針對 SQL Server 2017 CU3 和更早版本，您必須安裝 SQL Server Agent 套件。

> [!NOTE]
> 以下的安裝指示適用於 SQL Server 版本 2017 CU3 和較低版本。 安裝 SQL Server Agent 之前，請先[安裝 SQL Server](sql-server-linux-setup.md#platforms)。 這會設定您在安裝 **mssql-server-agent** 套件時所使用的金鑰和存放庫。

安裝適用於您平台的 SQL Server Agent：
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name=""></a><a name="RHEL">在 RHEL 上安裝</a>

使用下列步驟，在 Red Hat Enterprise Linux 上安裝 **mssql-server-agent**。 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

如果您已經安裝 **mssql-server-agent**，則可使用下列命令更新為最新版本：

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

如果您需要離線安裝，請在[版本資訊](sql-server-linux-release-notes.md)中找到 SQL Server Agent 套件下載。 然後使用[安裝 SQL Server](sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。

### <a name=""></a><a name="ubuntu">在 Ubuntu 上安裝</a>

使用下列步驟，在 Ubuntu 上安裝 **mssql-server-agent**。 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

如果您已經安裝 **mssql-server-agent**，則可使用下列命令更新為最新版本：

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

如果您需要離線安裝，請在[版本資訊](sql-server-linux-release-notes.md)中找到 SQL Server Agent 套件下載。 然後使用[安裝 SQL Server](sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。

### <a name=""></a><a name="SLES">在 SLES 上安裝</a>

使用下列步驟，在 SUSE Linux Enterprise Server 上安裝 **mssql-server-agent**。 

安裝 **mssql-server-agent** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

如果您已經安裝 **mssql-server-agent**，則可使用下列命令更新為最新版本：

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

如果您需要離線安裝，請在[版本資訊](sql-server-linux-release-notes.md)中找到 SQL Server Agent 套件下載。 然後使用[安裝 SQL Server](sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。

## <a name="next-steps"></a>後續步驟
如需如何使用 SQL Server Agent 來建立、排程和執行作業的詳細資訊，請參閱[在 Linux 上執行 SQL Server Agent 作業](sql-server-linux-run-sql-server-agent-job.md)。
