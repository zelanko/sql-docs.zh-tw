---
title: 在 Ubuntu 上的 SQL Server 入門
titleSuffix: SQL Server
description: 本快速入門示範如何在 Ubuntu 上安裝 SQL Server 2017 或 SQL Server 2019 然後建立並查詢資料庫，以使用 sqlcmd。
author: VanMSFT
ms.author: vanto
ms.date: 05/28/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 23597e4937f279694d7e4286e5aec3d714b54afa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910459"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>快速入門：安裝 SQL Server，並在 Ubuntu 上建立資料庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]


<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

在本快速入門中，您在 Ubuntu 16.04 上安裝 SQL Server 2017 或 SQL Server 2019 預覽。 然後交流**sqlcmd**來建立您的第一個資料庫和執行查詢。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

在本快速入門中中,，您可以安裝 SQL Server 2019 preview Ubuntu 16.04 上。 然後交流**sqlcmd**來建立您的第一個資料庫和執行查詢。

::: moniker-end

> [!TIP]
> 本教學課程需要使用者輸入和網際網路連線。 如果您想要自動或離線安裝程序中，請參閱[在 Linux 上的 SQL Server 的安裝指引](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>必要條件

您必須有一個 Ubuntu 16.04 的機器**至少 2 GB**的記憶體。

若要在您自己的電腦上安裝 Ubuntu 16.04，請前往[ http://releases.ubuntu.com/xenial/ ](http://releases.ubuntu.com/xenial/)。 您也可以在 Azure 中建立 Ubuntu 虛擬機器。 請參閱[建立和管理 Linux Vm 使用 Azure CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)。

> [!NOTE]
> 在此階段中，[適用於 Linux 的 Windows 子系統](https://msdn.microsoft.com/commandline/wsl/about)Windows 10 不支援做為安裝目標。

如需其他系統需求，請參閱[在 Linux 上的 SQL Server 的系統需求](sql-server-linux-setup.md#system)。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="install"></a>安裝 SQL Server

若要設定 SQL Server 在 Ubuntu 上，執行下列命令來安裝終端機中**mssql server**封裝。

1. 匯入公用存放庫 GPG 金鑰：

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 註冊 Microsoft SQL Server Ubuntu 存放庫：

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!TIP]
   > 如果您想要試用 SQL Server 2019，則改為必須登錄**預覽 (2019)** 存放庫。 SQL Server 2019 安裝中使用下列命令：
   >
   > ```bash
   > sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
   > ```

3. 執行下列命令來安裝 SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. 在 執行套件安裝完成後**mssql conf 安裝**並遵循提示來設定 SA 密碼，然後選擇您的版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 下列的 SQL Server 2017 版本免費授權：Evaluation、 Developer 和 Express。

   > [!NOTE]
   > 請務必指定 SA 帳戶 （最小長度為 8 個字元，包括大寫和小寫字母、 10 進位數字和/或非英數符號） 的強式密碼。

5. 完成設定之後，請確認服務正在執行：

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. 如果您打算從遠端連線，您可能也需要開啟防火牆上的 SQL Server TCP 連接埠 （預設值 1433年）。

此時，SQL Server Ubuntu 電腦上執行，並可供使用 ！

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="install"></a>安裝 SQL Server

若要設定 SQL Server 在 Ubuntu 上，執行下列命令來安裝終端機中**mssql server**封裝。

1. 匯入公用存放庫 GPG 金鑰：

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 註冊 SQL Server 2019 preview 的 Microsoft SQL Server Ubuntu 存放庫：

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
   ```

3. 執行下列命令來安裝 SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

4. 在 執行套件安裝完成後**mssql conf 安裝**並遵循提示來設定 SA 密碼，然後選擇您的版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > 請務必指定 SA 帳戶 （最小長度為 8 個字元，包括大寫和小寫字母、 10 進位數字和/或非英數符號） 的強式密碼。

5. 完成設定之後，請確認服務正在執行：

   ```bash
   systemctl status mssql-server --no-pager
   ```

6. 如果您打算從遠端連線，您可能也需要開啟防火牆上的 SQL Server TCP 連接埠 （預設值 1433年）。

此時，SQL Server 2019 預覽 Ubuntu 電腦上執行，並可供使用 ！

::: moniker-end

## <a id="tools"></a>安裝 SQL Server 命令列工具

若要建立資料庫，您需要連線工具，可以在 SQL Server 上執行 TRANSACT-SQL 陳述式。 下列步驟會安裝 SQL Server 命令列工具： [sqlcmd](../tools/sqlcmd-utility.md)並[bcp](../tools/bcp-utility.md)。

使用下列步驟來安裝**mssql 工具**在 Ubuntu 上。 

1. 匯入公用存放庫 GPG 金鑰。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 註冊 Microsoft Ubuntu 存放庫。

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. 更新 [來源] 清單並執行安裝命令與 unixODBC 開發人員套件。

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > 若要更新至最新版本**mssql 工具**執行下列命令：
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **選擇性**:新增`/opt/mssql-tools/bin/`至您**路徑**bash 殼層中的環境變數。

   若要讓**sqlcmd/bcp**存取從 bash 殼層中的登入工作階段中，修改您**路徑**中 **~/.bash_profile**檔案使用下列命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   若要讓**sqlcmd/bcp**從 bash 殼層中互動式/非登入工作階段，可存取修改**路徑**中 **~/.bashrc**檔案使用下列命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
