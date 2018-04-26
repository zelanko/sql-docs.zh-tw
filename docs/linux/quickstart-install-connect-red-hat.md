---
title: 開始使用 Red Hat Enterprise Linux 上的 SQL Server 2017 |Microsoft 文件
description: 本快速入門示範如何在 Red Hat Enterprise Linux 上安裝 SQL Server 2017 然後建立並查詢資料庫，以使用 sqlcmd。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/22/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.workload: Active
ms.openlocfilehash: 145f829b3baf5392ed3d6ed93db43b01603b9b8f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>快速入門： 安裝 SQL Server 和 Red Hat 上建立資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本快速入門中，您先安裝 SQL Server 2017 上 Red Hat Enterprise Linux (RHEL) 7.3 +。 然後與 **sqlcmd**連線來建立您的第一個資料庫並執行查詢。

> [!TIP]
> 本教學課程需要使用者輸入和網際網路連線。 如果您有興趣[自動](sql-server-linux-setup.md#unattended)或[離線](sql-server-linux-setup.md#offline)安裝程序，請參閱[SQL Server on Linux 的安裝指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>필수 구성 요소

您必須擁有 RHEL 7.3 或 7.4 機器**至少 2 GB**的記憶體。

若要在自己電腦上安裝 Red Hat Enterprise Linux，請移至[ http://access.redhat.com/products/red-hat-enterprise-linux/evaluation ](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)。 您也可以在 Azure 中建立 RHEL 虛擬機器。 請參閱[建立和管理 Linux Vm 與 Azure CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)，並使用`--image RHEL`呼叫`az vm create`。

其他系統需求，請參閱[系統需求的 SQL Server on Linux](sql-server-linux-setup.md#system)。

## <a id="install"></a>安裝 SQL Server

若要設定 SQL Server RHEL 上，執行下列命令中安裝終端機**mssql 伺服器**封裝：

> [!IMPORTANT]
> 如果您先前曾安裝 CTP 或 RC 版本的 SQL Server 2017，您必須先移除舊的存放庫，再註冊 GA 儲存機制的其中一個。 如需詳細資訊，請參閱[從預覽儲存機制的儲存機制變更至 GA 儲存機制](sql-server-linux-change-repo.md)。

1. 下載 Microsoft SQL Server Red Hat 儲存機制設定檔：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

   > [!NOTE]
   > 這是累計更新 (CU) 儲存機制。 如需有關您的儲存機制選項以及其差異的詳細資訊，請參閱[儲存機制設定 SQL Server on Linux](sql-server-linux-change-repo.md)。

1. 執行下列命令來安裝 SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

1. 在套件安裝完成執行之後**mssql conf 安裝**並遵循提示設定 SA 密碼並選擇您的版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```
   > [!TIP]
   > 如果您嘗試在此教學課程中的 SQL Server 2017，自由地滹砅下列版本： Evaluation、 Developer 和 Express。

   > [!NOTE]
   > 請務必指定 SA 帳戶 （最小長度為 8 個字元，包括大寫和小寫字母、 10 進位數字及/或非英數符號） 的強式密碼。

1. 一旦完成設定，請確認服務正在執行：

   ```bash
   systemctl status mssql-server
   ```
   
1. 若要允許遠端連接，請開啟 RHEL 上的防火牆上的 SQL Server 連接埠。 預設 SQL Server 連接埠為 TCP 1433。 如果您使用**FirewallD**防火牆，您可以使用下列命令：

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

此時，SQL Server RHEL 機器上執行，並可供使用 ！

## <a id="tools"></a>安裝 SQL Server 命令列工具

若要建立資料庫，您需要連接與一種工具，可以在 SQL Server 上執行 TRANSACT-SQL 陳述式。 下列步驟安裝的 SQL Server 命令列工具： [sqlcmd](../tools/sqlcmd-utility.md)和[bcp](../tools/bcp-utility.md)。

1. 下載 Microsoft Red Hat 儲存機制設定檔。

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/7/prod.repo
   ```

1. 如果您在舊版的**mssql 工具**安裝，請移除任何舊版 unixODBC 封裝。

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 執行下列命令安裝**mssql 工具**unixODBC 開發人員套件。

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. 為了方便起見，新增`/opt/mssql-tools/bin/`到您**路徑**環境變數。 這可讓您執行這些工具，而不指定完整路徑。 執行下列命令，以修改**路徑**登入工作階段和互動式/非-登入工作階段：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd**是一個工具連接到 SQL Server 來執行查詢，並執行管理和開發工作。 其他工具包括：
>
> * [SQL Server Operations Studio (預覽)](../sql-operations-studio/what-is.md)
> * [SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)
> * [Visual Studio 程式碼](sql-server-linux-develop-use-vscode.md)。
> * [mssql-cli (預覽)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
