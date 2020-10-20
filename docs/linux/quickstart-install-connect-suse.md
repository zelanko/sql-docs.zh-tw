---
title: SUSE：在 Linux 上安裝 SQL Server
description: 本快速入門說明如何在 SUSE Linux Enterprise Server 上安裝 SQL Server 2017 或 SQL Server 2019，然後使用 sqlcmd 建立及查詢資料庫。
author: VanMSFT
ms.author: vanto
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.openlocfilehash: 8babcb8b849360ba4a025d62a8e89f5ad92175c2
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115935"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>快速入門：在 SUSE Linux Enterprise Server 上安裝 SQL Server 並建立資料庫

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

在本快速入門中，您會在 SUSE Linux Enterprise Server (SLES) v12 SP2 上安裝 SQL Server 2017 或 SQL Server 2019。 然後與 **sqlcmd** 連線，建立您的第一個資料庫並執行查詢。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

在本快速入門中，您會在 SUSE Linux Enterprise Server (SLES) v12 上安裝 SQL Server 2019。 然後與 **sqlcmd** 連線，建立您的第一個資料庫並執行查詢。

> [!IMPORTANT]
> SUSE Linux Server v12 SP2、SP3、SP4 或 SP5 上皆支援 SQL Server 2019。

::: moniker-end

> [!TIP]
> 本教學課程需要使用者輸入和網際網路連線。 如果您對[自動](sql-server-linux-setup.md#unattended)或[離線](sql-server-linux-setup.md#offline)安裝程序感興趣，請參閱 [ Linux 上的 SQL Server 安裝指引](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>Prerequisites

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

您的 SLES v12 SP2 機器必須**至少有 2 GB** 的記憶體。 檔案系統必須是 **XFS** 或 **EXT4**。 不支援其他檔案系統 (例如 **BTRFS**)。

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

您的 SLES v12 SP2、SP3、SP4 或 SP5 電腦必須**至少有 2 GB** 的記憶體。 檔案系統必須是 **XFS** 或 **EXT4**。 不支援其他檔案系統 (例如 **BTRFS**)。

::: moniker-end

若要在您自己的機器上安裝 SUSE Linux Enterprise Server，請前往 [https://www.suse.com/products/server](https://www.suse.com/products/server)。 您也可以在 Azure 中建立 SLES 虛擬機器。 請參閱[使用 Azure CLI 建立和管理 Linux VM](/azure/virtual-machines/linux/tutorial-manage-vm)，並於呼叫 `az vm create`時使用 `--image SLES`。

如果您先前已安裝 SQL Server 的 CTP 或 RC 版本，您必須先移除舊的存放庫，然後遵循這些步驟進行。 如需詳細資訊，請參閱[為 SQL Server 2017 和 2019 設定 Linux 存放庫](sql-server-linux-change-repo.md)。

> [!NOTE]
> 目前尚未支援在 Windows 10 上使用[適用於 Linux 的 Windows 子系統](/windows/wsl/about)作為安裝目標。

如需其他系統需求，請參閱 [SQL Server 在 Linux 上的系統需求](sql-server-linux-setup.md#system)。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a name="install-sql-server"></a><a id="install"></a>安裝 SQL Server

若要在 SLES 上設定 SQL Server，請從終端執行下列命令，安裝 **mssql-server** 套件：

1. 下載 Microsoft SQL Server 2017 SLES 存放庫組態檔：

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   ```

   > [!TIP]
   > 如果您想要安裝 SQL Server 2019，則必須改為註冊 SQL Server 2019 存放庫。 請使用下列命令安裝 SQL Server 2019：
   >
   > ```bash
   > sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo
   > ```

2. 重新整理您的存放庫。

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
   若要確定您的系統上已安裝 Microsoft 套件簽署金鑰，請使用下列命令將其匯入： 
   
   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```
   
3. 執行下列命令安裝 SQL Server：

   ```bash
   sudo zypper install -y mssql-server
   ```

4. 套件安裝完成之後，請執行 **mssql-conf setup** 並遵循提示設定 SA 密碼，然後選擇您的版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 下列 SQL Server 2017 版本是免費授權的版本：Evaluation、Developer 和 Express。

   > [!NOTE]
   > 請務必為 SA 帳戶指定強式密碼 (最小長度為 8 個字元，包括大小寫字母、以 10 為基底的數字及/或非英數字元符號)。

5. 完成設定之後，請確認服務正在執行：

   ```bash
   systemctl status mssql-server
   ```

6. 如果您想要進行遠端連線，可能還需要在防火牆上開啟 SQL Server TCP 通訊埠 (預設值 1433)。 如果您使用的是 SuSE 防火牆，需要編輯 **/etc/sysconfig/SuSEfirewall2** 組態檔。 請修改 **FW_SERVICES_EXT_TCP** 項目，納入 SQL Server 連接埠號碼。

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

此時，SQL Server 正在您的 SLES 機器上執行並可立即使用！

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="install-sql-server"></a><a id="install"></a>安裝 SQL Server

若要在 SLES 上設定 SQL Server，請從終端執行下列命令，安裝 **mssql-server** 套件：

1. 下載 Microsoft SQL Server 2019 SLES 存放庫設定檔：

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo
   ```

2. 重新整理您的存放庫。

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
   若要確定您的系統上是否已安裝 Microsoft 套件簽署金鑰，請使用下列命令來匯入金鑰： 
   
   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```
   
3. 執行下列命令安裝 SQL Server：

   ```bash
   sudo zypper install -y mssql-server
   ```

4. 套件安裝完成之後，請執行 **mssql-conf setup** 並遵循提示設定 SA 密碼，然後選擇您的版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > 請務必為 SA 帳戶指定強式密碼 (最小長度為 8 個字元，包括大小寫字母、以 10 為基底的數字及/或非英數字元符號)。

5. 完成設定之後，請確認服務正在執行：

   ```bash
   systemctl status mssql-server
   ```

6. 如果您想要進行遠端連線，可能還需要在防火牆上開啟 SQL Server TCP 通訊埠 (預設值 1433)。 如果您使用的是 SuSE 防火牆，需要編輯 **/etc/sysconfig/SuSEfirewall2** 組態檔。 請修改 **FW_SERVICES_EXT_TCP** 項目，納入 SQL Server 連接埠號碼。

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

此時，SQL Server 2019 正在 SLES 機器上執行並可立即使用！

::: moniker-end


## <a name="install-the-sql-server-command-line-tools"></a><a id="tools"></a>安裝 SQL Server 命令列工具

若要建立資料庫，您必須與可在 SQL Server 上執行 Transact-SQL 陳述式的工具連線。 下列步驟會安裝 SQL Server 命令列工具：[sqlcmd](../tools/sqlcmd-utility.md) 和 [bcp](../tools/bcp-utility.md)。

1. 將 Microsoft SQL Server 存放庫新增至 Zypper。

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. 使用 unixODBC 開發人員套件安裝 **mssql-tools**。 如需詳細資訊，請參閱安裝 [Microsoft ODBC Driver for SQL Server (Linux)](../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)。

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
   ```

1. 方便起見，請將 `/opt/mssql-tools/bin/` 新增至您的 **PATH** 環境變數。 這可讓您不需要指定完整路徑，即可執行工具。 執行下列命令，修改登入工作階段和互動式/非登入工作階段的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]