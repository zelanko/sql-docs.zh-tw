---
title: 開始使用 Red Hat Enterprise Linux 上的 SQL Server |Microsoft Docs
description: 本快速入門示範如何在 Red Hat Enterprise Linux 上安裝 SQL Server 2017 或 SQL Server 2019 然後建立並查詢資料庫，以使用 sqlcmd。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/16/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.custom: sql-linux
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: 8d5b044adbdc0e5a846013aff1922b3cb1cb5dc8
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51669447"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>快速入門： 安裝 SQL Server 和 Red Hat 上建立資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

在本快速入門中，您安裝 SQL Server 2017 或 SQL Server 2019 上 Red Hat Enterprise Linux (RHEL) 7.3 +。 然後交流**sqlcmd**來建立您的第一個資料庫和執行查詢。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

在本快速入門中，您安裝 SQL Server 2019 preview 上 Red Hat Enterprise Linux (RHEL) 7.3 +。 然後交流**sqlcmd**來建立您的第一個資料庫和執行查詢。

::: moniker-end

> [!TIP]
> 本教學課程需要使用者輸入和網際網路連線。 如果您有興趣[無人看管](sql-server-linux-setup.md#unattended)或是[離線](sql-server-linux-setup.md#offline)安裝程序，請參閱[的 Linux 上的 SQL Server 的安裝指引](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>先決條件

您必須擁有 RHEL 7.3 或 7.4 的電腦，具有**至少 2 GB**的記憶體。

若要安裝在您自己的電腦上的 Red Hat Enterprise Linux，請前往[ https://access.redhat.com/products/red-hat-enterprise-linux/evaluation ](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)。 您也可以在 Azure 中建立 RHEL 虛擬機器。 請參閱[建立和使用 Azure CLI 管理 Linux Vm](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)，並使用`--image RHEL`呼叫中`az vm create`。

如果您先前已安裝 CTP 或 RC 版本的 SQL Server 2017，您必須先移除舊的存放庫，才能執行這些步驟。 如需詳細資訊，請參閱 <<c0> [ 設定 Linux SQL Server 2017 和 2019年的存放庫](sql-server-linux-change-repo.md)。

如需其他系統需求，請參閱[在 Linux 上的 SQL Server 的系統需求](sql-server-linux-setup.md#system)。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>安裝 SQL Server

若要在 RHEL 上設定 SQL Server，請執行下列命令來安裝終端機中**mssql server**封裝：

1. 下載 Microsoft SQL Server 2017 Red Hat 存放庫的組態檔：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!TIP]
   > 如果您想要試用 SQL Server 2019，則改為必須登錄**預覽 (2019)** 存放庫。 SQL Server 2019 安裝中使用下列命令：
   >
   > ```bash
   > sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo
   > ```

2. 執行下列命令來安裝 SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

3. 在 執行套件安裝完成後**mssql conf 安裝**並遵循提示來設定 SA 密碼，然後選擇您的版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 免費授權下列的 SQL Server 2017 版本： Evaluation、 Developer 和 Express。

   > [!NOTE]
   > 請務必指定 SA 帳戶 （最小長度為 8 個字元，包括大寫和小寫字母、 10 進位數字和/或非英數符號） 的強式密碼。

4. 完成設定之後，請確認服務正在執行：

   ```bash
   systemctl status mssql-server
   ```

5. 若要允許遠端連線，請開啟 RHEL 上的防火牆上的 SQL Server 連接埠。 預設 SQL Server 連接埠為 TCP 1433。 如果您使用**FirewallD**防火牆，您可以使用下列命令：

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

此時，SQL Server RHEL 機器上執行，並可供使用 ！

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>安裝 SQL Server

若要在 RHEL 上設定 SQL Server，請執行下列命令來安裝終端機中**mssql server**封裝：

1. 下載 Microsoft SQL Server 2019 預覽版 Red Hat 存放庫設定檔：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo
   ```

2. 執行下列命令來安裝 SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

3. 在 執行套件安裝完成後**mssql conf 安裝**並遵循提示來設定 SA 密碼，然後選擇您的版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > 請務必指定 SA 帳戶 （最小長度為 8 個字元，包括大寫和小寫字母、 10 進位數字和/或非英數符號） 的強式密碼。

4. 完成設定之後，請確認服務正在執行：

   ```bash
   systemctl status mssql-server
   ```

5. 若要允許遠端連線，請開啟 RHEL 上的防火牆上的 SQL Server 連接埠。 預設 SQL Server 連接埠為 TCP 1433。 如果您使用**FirewallD**防火牆，您可以使用下列命令：

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

此時，SQL Server 2019 預覽 RHEL 機器上執行，並可供使用 ！

::: moniker-end

## <a id="tools"></a>安裝 SQL Server 命令列工具

若要建立資料庫，您需要連線工具，可以在 SQL Server 上執行 TRANSACT-SQL 陳述式。 下列步驟會安裝 SQL Server 命令列工具： [sqlcmd](../tools/sqlcmd-utility.md)並[bcp](../tools/bcp-utility.md)。

1. 下載 Microsoft Red Hat 存放庫的組態檔。

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. 如果您有舊版**mssql 工具**安裝，請移除任何舊版 unixODBC 套件。

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 執行下列命令來安裝**mssql 工具**unixODBC 開發人員套件。

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. 為了方便起見，新增`/opt/mssql-tools/bin/`至您**路徑**環境變數。 這可讓您執行工具，而不指定完整路徑。 執行下列命令來修改**路徑**登入工作階段和互動式/非登入工作階段：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
