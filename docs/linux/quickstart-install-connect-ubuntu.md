---
title: 開始使用在 Ubuntu 上的 SQL Server 2017 |Microsoft Docs
description: 本快速入門示範如何在 Ubuntu 上安裝 SQL Server 2017 然後建立並查詢資料庫，以使用 sqlcmd。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/22/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: ebe7da1e1024cefc14c52d0a02e0517b764c8d07
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38057316"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-ubuntu"></a>快速入門： 安裝 SQL Server，並在 Ubuntu 上建立資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在本快速入門中，您先安裝 SQL Server 2017 上 Ubuntu 16.04。 然後與 **sqlcmd**連線來建立您的第一個資料庫並執行查詢。

> [!TIP]
> 本教學課程需要使用者輸入和網際網路連線。 如果您有興趣[無人看管](sql-server-linux-setup.md#unattended)或是[離線](sql-server-linux-setup.md#offline)安裝程序，請參閱[的 Linux 上的 SQL Server 的安裝指引](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>先決條件

您必須有一個 Ubuntu 16.04 的機器**至少 2 GB**的記憶體。

若要在您自己的電腦上安裝 Ubuntu，請前往[ http://www.ubuntu.com/download/server ](http://www.ubuntu.com/download/server)。 您也可以在 Azure 中建立 Ubuntu 虛擬機器。 請參閱[建立和管理 Linux Vm 使用 Azure CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)。

> [!NOTE]
> 在此階段中，[適用於 Linux 的 Windows 子系統](https://msdn.microsoft.com/commandline/wsl/about)Windows 10 不支援做為安裝目標。

如需其他系統需求，請參閱[在 Linux 上的 SQL Server 的系統需求](sql-server-linux-setup.md#system)。

## <a id="install"></a>安裝 SQL Server

若要設定 SQL Server 在 Ubuntu 上，執行下列命令來安裝終端機中**mssql server**封裝。

> [!IMPORTANT]
> 如果您先前已安裝 CTP 或 RC 版本的 SQL Server 2017，您必須先移除舊的存放庫，再註冊 GA 存放庫的其中一個。 如需詳細資訊，請參閱 <<c0> [ 預覽儲存機制中的存放庫變更至 GA 存放庫](sql-server-linux-change-repo.md)。

1. 匯入公用存放庫 GPG 金鑰：

   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 註冊 Microsoft SQL Server Ubuntu 存放庫：

   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

   > [!NOTE]
   > 這是累積更新 (CU) 存放庫。 如需有關您的儲存機制選項以及其差異的詳細資訊，請參閱 <<c0> [ 在 Linux 上的 SQL server 設定存放庫](sql-server-linux-change-repo.md)。

1. 執行下列命令來安裝 SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
   ```

1. 在 執行套件安裝完成後**mssql conf 安裝**並遵循提示來設定 SA 密碼，然後選擇您的版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > 如果您嘗試在此教學課程中的 SQL Server 2017，免費授權下列版本： Evaluation、 Developer 和 Express。

   > [!NOTE]
   > 請務必指定 SA 帳戶 （最小長度為 8 個字元，包括大寫和小寫字母、 10 進位數字和/或非英數符號） 的強式密碼。

1. 完成設定之後，請確認服務正在執行：

   ```bash
   systemctl status mssql-server
   ```

1. 如果您打算從遠端連線，您可能也需要開啟防火牆上的 SQL Server TCP 連接埠 （預設值 1433年）。

此時，SQL Server Ubuntu 電腦上執行，並可供使用 ！

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

1. **選擇性**： 新增`/opt/mssql-tools/bin/`至您**路徑**bash 殼層中的環境變數。

   若要讓**sqlcmd/bcp**存取從 bash 殼層中的登入工作階段中，修改您**路徑**中 **~/.bash_profile**檔案使用下列命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   若要讓**sqlcmd/bcp**從 bash 殼層中互動式/非登入工作階段，可存取修改**路徑**中 **~/.bashrc**檔案使用下列命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd**是一個工具，可連接到 SQL Server 執行查詢，並執行管理和開發工作。 其他工具包括：
>
> * [SQL Server Operations Studio (預覽)](../sql-operations-studio/what-is.md)
> * [Transact-SQL](sql-server-linux-manage-ssms.md)
> * [Visual Studio Code](sql-server-linux-develop-use-vscode.md)。
> * [mssql-cli (預覽)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
