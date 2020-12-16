---
title: 在 Linux 上安裝 SQL Server Integration Services
description: 本文描述如何在 Linux 上安裝 SQL Server Integration Services (SSIS)。 您可以在 Ubuntu 16.04 和 Red Hat Enterprise Linux 上安裝 SSIS。
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: e34fd6c218950b86a46f43842c06408feefedfc9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471439"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>在 Linux 上安裝 SQL Server Integration Services (SSIS)

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

請遵循本文中的步驟，在 Linux 上安裝 SQL Server Integration Services (**mssql-server-is**)。 如需此版本 Integration Services for Linux 支援功能的資訊，請參閱[版本資訊](sql-server-linux-release-notes.md)。

您可以在下列平台上安裝 SQL Server Integration Services：

- [Ubuntu 16.04](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="install-ssis-on-ubuntu"></a><a name="ubuntu"></a> 在 Ubuntu 上安裝 SSIS

若要在 Ubuntu 上安裝 **mssql-server-is** 套件，請遵循下列步驟：

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 匯入公開存放庫 GPG 金鑰。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 註冊 SQL Server Ubuntu 存放庫。

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

1. 執行下列命令來安裝 SQL Server Integration Services。

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

1. 安裝 Integration Services 之後，請執行 **ssis-conf**。 如需詳細資訊，請參閱[使用 ssis-conf 設定 Linux 上的 SSIS](sql-server-linux-configure-ssis.md)。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 完成設定之後，請設定 PATH 環境變數。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

1. 匯入公開存放庫 GPG 金鑰。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 註冊 SQL Server Ubuntu 存放庫。

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
   ```

1. 執行下列命令來安裝 SQL Server Integration Services。

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

1. 安裝 Integration Services 之後，請執行 **ssis-conf**。 如需詳細資訊，請參閱[使用 ssis-conf 設定 Linux 上的 SSIS](sql-server-linux-configure-ssis.md)。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 完成設定之後，請設定 PATH 環境變數。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

### <a name="update-ssis"></a>更新 SSIS

如果您已經安裝 **mssql-server-is**，請使用下列命令更新為最新版本：

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>移除 SSIS

若要移除 **mssql-server-is**，請執行下列命令：

```bash
sudo apt-get remove mssql-server-is
```

## <a name="install-ssis-on-rhel"></a><a name="RHEL"></a> 在 RHEL 上安裝 SSIS
若要在 RHEL 上安裝 **mssql-server-is** 套件，請遵循下列步驟：

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 下載 SQL Server Red Hat 存放庫設定檔。

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. 執行下列命令來安裝 SQL Server Integration Services。

   ```bash
   sudo yum install -y mssql-server-is
   ```

1. 安裝後，請執行 **ssis-conf**。 如需詳細資訊，請參閱[使用 ssis-conf 設定 Linux 上的 SSIS](sql-server-linux-configure-ssis.md)。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 完成設定之後，請設定 PATH 環境變數。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

1. 下載 SQL Server Red Hat 存放庫設定檔。

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   ```

1. 執行下列命令來安裝 SQL Server Integration Services。

   ```bash
   sudo yum install -y mssql-server-is
   ```

1. 安裝後，請執行 **ssis-conf**。 如需詳細資訊，請參閱[使用 ssis-conf 設定 Linux 上的 SSIS](sql-server-linux-configure-ssis.md)。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 完成設定之後，請設定 PATH 環境變數。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

::: moniker-end

### <a name="update-ssis"></a>更新 SSIS

如果您已經安裝 **mssql-server-is**，請使用下列命令更新為最新版本：

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>移除 SSIS
若要移除 **mssql-server-is**，請執行下列命令：

```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>自動安裝

若要以自動安裝的形式執行 **ssis-conf setup**，請執行下列步驟：

1. 指定 **-n** (無提示) 選項。
1. 設定環境變數，以提供必要的值。

下列範例會執行這些動作：

- 安裝 SSIS
- 提供 SSIS_PID 環境變數的值，以指定 Developer 版本
- 提供 ACCEPT_EULA 環境變數的值，以接受 Microsoft 軟體授權條款
- 指定 **-n** (無提示) 選項，以執行自動安裝

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>自動安裝的環境變數

| 環境變數 | 描述 |
|---|---|
| ACCEPT_EULA | 當設定為任何值 (例如 "Y") 時，即接受 SQL Server 授權條款。|
| SSIS_PID | 設定 SQL Server 版本或產品金鑰。 下列為可能的值：<ul><li>評估</li><li>開發人員</li><li>Express</li><li>Web</li><li>Standard</li><li>企業</li><li>產品金鑰</li></ul>如果您指定產品金鑰，則其格式必須為 *#####* - *#####* - *#####* - *#####* - *#####* ，其中 *#* 是字母或數字。  |
| | |

## <a name="next-steps"></a>接下來的步驟

若要在 Linux 上執行 SSIS 套件，請參閱[使用 SSIS 在 Linux 上的 SQL Server 擷取、轉換和載入資料](sql-server-linux-migrate-ssis.md)。

若要在 Linux 上設定其他 SSIS 設定，請參閱[使用 ssis-conf 設定 Linux 上的 SQL Server Integration Services](sql-server-linux-configure-ssis.md)。

## <a name="related-content-about-ssis-on-linux"></a>Linux 上的 SSIS 相關內容

- [使用 SSIS 在 Linux 上擷取、轉換和載入資料](sql-server-linux-migrate-ssis.md)
- [使用 ssis-conf 設定 Linux 上的 SQL Server Integration Services](sql-server-linux-configure-ssis.md)
- [Linux 上的 SSIS 限制和已知問題](sql-server-linux-ssis-known-issues.md)
- [使用 cron 排程 Linux 上的 SQL Server Integration Services 套件執行](sql-server-linux-schedule-ssis-packages.md)
