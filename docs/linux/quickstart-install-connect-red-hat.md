---
title: "開始使用 Red Hat Enterprise Linux 上的 SQL Server 2017 |Microsoft 文件"
description: "本快速入門教學課程會示範如何在 Red Hat Enterprise Linux 上安裝 SQL Server 2017 然後建立並查詢資料庫，以使用 sqlcmd。"
author: sabotta
ms.author: carlasab
manager: craigg
ms.date: 07/24/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 53f3c2dbda293d6c3f9beb8bd16287b6aa0d9e26
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-and-create-a-database-on-red-hat"></a>安裝 SQL Server，並在 Red Hat 上建立資料庫

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

在本快速入門教學課程中，您先安裝 SQL Server 2017 RC2 上 Red Hat Enterprise Linux (RHEL) 7.3。 然後以連接**sqlcmd**來建立您的第一個資料庫和執行查詢。

> [!TIP]
> 本教學課程需要使用者輸入和網際網路連線。 如果您有興趣[自動](sql-server-linux-setup.md#unattended)或[離線](sql-server-linux-setup.md#offline)安裝程序，請參閱[SQL Server on Linux 的安裝指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>필수 구성 요소

您必須擁有的 RHEL 7.3 機器**至少 3.25 GB**的記憶體。

若要在自己電腦上安裝 Red Hat Enterprise Linux，請移至[http://access.redhat.com/products/red-hat-enterprise-linux/evaluation](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)。 您也可以在 Azure 中建立 RHEL 虛擬機器。 請參閱[建立和管理 Linux Vm 與 Azure CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)，並使用`--image RHEL`呼叫`az vm create`。

其他系統需求，請參閱[系統需求的 SQL Server on Linux](sql-server-linux-setup.md#system)。

## <a id="install"></a>安裝 SQL Server

若要設定 SQL Server RHEL 上，執行下列命令中安裝終端機**mssql 伺服器**封裝：

1. 下載 Microsoft SQL Server Red Hat 儲存機制設定檔：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server.repo
   ```

1. 執行下列命令來安裝 SQL Server:

   ```bash
   sudo yum update
   sudo yum install -y mssql-server
   ```

1. 在套件安裝完成執行之後**mssql conf 安裝**並遵循提示來設定 SA 密碼，並選擇版本。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```
   > [!TIP]
   > 請務必指定 SA 帳戶 （最小長度為 8 個字元，包括大寫和小寫字母、 10 進位數字及/或非英數符號） 的強式密碼。

   > [!TIP]
   > 當安裝 RC2，沒有購買的授權才能任何版本再試一次。 因為它是發行候選版本，不論您選取的版本為何會出現下列訊息：
   >
   > `This is an evaluation version.  There are [175] days left in the evaluation period.`
   >
   > 此訊息並不會反映您所選取的版本。 它在預覽期間與相關 rc2。

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
   sudo yum update
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 執行下列命令安裝**mssql 工具**unixODBC 開發人員套件。

   ```bash
   sudo yum update
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. 為了方便起見，新增`/opt/mssql-tools/bin/`到您**路徑**環境變數。 這可讓您執行這些工具，而不指定完整路徑。 執行下列命令，以修改**路徑**登入工作階段和互動式/非-登入工作階段：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> **Sqlcmd**是一個工具連接到 SQL Server 來執行查詢，並執行管理和開發工作。 其他工具包括[SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)和[Visual Studio Code](sql-server-linux-develop-use-vscode.md)。

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
