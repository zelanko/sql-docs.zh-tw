---
title: RHEL：在 Linux 上安裝 SQL Server
titleSuffix: SQL Server
description: 此快速入門說明如何在 Red Hat Enterprise Linux (RHEL) 上安裝 SQL Server 2017 或 SQL Server 2019，然後使用 sqlcmd 建立及查詢資料庫。
author: VanMSFT
ms.custom: seo-lt-2019
ms.author: vanto
ms.date: 01/08/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: d94e90e67814ec2dd1541abdbd52b04152681d84
ms.sourcegitcommit: 76fb3ecb79850a8ef2095310aaa61a89d6d93afd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2020
ms.locfileid: "75776398"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>快速入門：在 Red Hat 上安裝 SQL Server 並建立資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

在本快速入門中，您會在 Red Hat Enterprise Linux (RHEL) 上安裝 SQL Server 2017 或 SQL Server 2019。 然後與 **sqlcmd** 連線，建立您的第一個資料庫並執行查詢。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

在本快速入門中，您會在 Red Hat Enterprise Linux (RHEL) 8 上安裝 SQL Server 2019。 然後與 **sqlcmd** 連線，建立您的第一個資料庫並執行查詢。

::: moniker-end

> [!TIP]
> 本教學課程需要使用者輸入和網際網路連線。 如果您對[自動](sql-server-linux-setup.md#unattended)或[離線](sql-server-linux-setup.md#offline)安裝程序感興趣，請參閱 [ Linux 上的 SQL Server 安裝指引](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>Prerequisites

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

RHEL 7.3、7.4、7.5、7.6 或 8 機器必須**至少有 2 GB** 的記憶體。

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

您的 RHEL 7.3、7.4、7.5 或 7.6 機器必須**至少有 2 GB** 的記憶體。

::: moniker-end

若您要在自己的機器上安裝 Red Hat Enterprise Linux，請前往 [https://access.redhat.com/products/red-hat-enterprise-linux/evaluation](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)。 您也可以在 Azure 中建立 RHEL 虛擬機器。 請參閱[使用 Azure CLI 建立和管理 Linux VM](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)，並於呼叫 `az vm create`時使用 `--image RHEL`。

如果您先前已安裝 SQL Server 的 CTP 或 RC 版本，您必須先移除舊的存放庫，然後遵循這些步驟進行。 如需詳細資訊，請參閱[為 SQL Server 2017 和 2019 設定 Linux 存放庫](sql-server-linux-change-repo.md)。

如需其他系統需求，請參閱 [SQL Server 在 Linux 上的系統需求](sql-server-linux-setup.md#system)。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>安裝 SQL Server

若要在 RHEL 上設定 SQL Server，請從終端執行下列命令，安裝 **mssql-server** 套件：

1. 下載 Microsoft SQL Server 2017 Red Hat 存放庫組態檔：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!TIP]
   > 如果您想要安裝 SQL Server 2019，則必須改為註冊 SQL Server 2019 存放庫。 請使用下列命令安裝 SQL Server 2019：
   >
   > ```bash
   > sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo
   > ```

2. 執行下列命令安裝 SQL Server：

   ```bash
   sudo yum install -y mssql-server
   ```

3. 套件安裝完成之後，請執行 **mssql-conf setup** 並遵循提示設定 SA 密碼，然後選擇您的版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 下列 SQL Server 2017 版本是免費授權的版本：Evaluation、Developer 和 Express。

   > [!NOTE]
   > 請務必為 SA 帳戶指定強式密碼 (最小長度為 8 個字元，包括大小寫字母、以 10 為基底的數字及/或非英數字元符號)。

4. 完成設定之後，請確認服務正在執行：

   ```bash
   systemctl status mssql-server
   ```

5. 若要允許遠端連線，請在 RHEL 的防火牆上開啟 SQL Server 連接埠。 SQL Server 連接埠預設為 TCP 1433。 如果您正在使用防火牆的 **FirewallD**，可以使用下列命令：

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

此時，SQL Server 正在您的 RHEL 機器上執行並可立即使用！

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>安裝 SQL Server

若要在 RHEL 上設定 SQL Server，請從終端執行下列命令，安裝 **mssql-server** 套件：

1. 下載 Microsoft SQL Server 2019 Red Hat 存放庫設定檔：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo
   ```

2. 執行下列命令安裝 SQL Server：

   ```bash
   sudo yum install -y mssql-server
   ```

3. 套件安裝完成之後，請執行 **mssql-conf setup** 並遵循提示設定 SA 密碼，然後選擇您的版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > 請務必為 SA 帳戶指定強式密碼 (最小長度為 8 個字元，包括大小寫字母、以 10 為基底的數字及/或非英數字元符號)。

4. 完成設定之後，請確認服務正在執行：

   ```bash
   systemctl status mssql-server
   ```

5. 若要允許遠端連線，請在 RHEL 的防火牆上開啟 SQL Server 連接埠。 SQL Server 連接埠預設為 TCP 1433。 如果您正在使用防火牆的 **FirewallD**，可以使用下列命令：

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

此時，SQL Server 2019 即已在您的 RHEL 機器上執行，並可立即使用！

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="tools"></a>安裝 SQL Server 命令列工具

若要建立資料庫，您必須與可在 SQL Server 上執行 Transact-SQL 陳述式的工具連線。 下列步驟會安裝 SQL Server 命令列工具：[sqlcmd](../tools/sqlcmd-utility.md) 和 [bcp](../tools/bcp-utility.md)。

1. 下載 Microsoft Red Hat 存放庫組態檔。

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. 如果您已安裝舊版的 **mssql-tools**，請移除所有舊版的 unixODBC 套件。

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 執行下列命令，使用 unixODBC 開發人員套件安裝 **mssql-tools**。

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. 方便起見，請將 `/opt/mssql-tools/bin/` 新增至您的 **PATH** 環境變數。 這可讓您不需要指定完整路徑，即可執行工具。 執行下列命令，修改登入工作階段和互動式/非登入工作階段的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="tools"></a>安裝 SQL Server 命令列工具

若要建立資料庫，您必須與可在 SQL Server 上執行 Transact-SQL 陳述式的工具連線。 下列步驟會安裝 SQL Server 命令列工具：[sqlcmd](../tools/sqlcmd-utility.md) 和 [bcp](../tools/bcp-utility.md)。

1. 下載 Microsoft Red Hat 存放庫組態檔。

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/8/prod.repo
   ```

1. 如果您已安裝舊版的 **mssql-tools**，請移除所有舊版的 unixODBC 套件。

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 執行下列命令，使用 unixODBC 開發人員套件安裝 **mssql-tools**。

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. 方便起見，請將 `/opt/mssql-tools/bin/` 新增至您的 **PATH** 環境變數。 這可讓您不需要指定完整路徑，即可執行工具。 執行下列命令，修改登入工作階段和互動式/非登入工作階段的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

::: moniker-end

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
