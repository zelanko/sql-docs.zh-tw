---
title: "開始使用 SQL Server 2017 Ubuntu 上 |Microsoft 文件"
description: "本快速入門教學課程會示範如何在 Ubuntu 上安裝 SQL Server 2017 然後建立並查詢資料庫，以使用 sqlcmd。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/24/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 052a2f0a7618c5e160d3c17a3a1efd7d7a4b3fd6
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-and-create-a-database-on-ubuntu"></a>安裝 SQL Server 和 Ubuntu 上建立資料庫

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

在本快速入門教學課程中，您先安裝 SQL Server 2017 RC2 Ubuntu 16.04 上。 然後以連接**sqlcmd**來建立您的第一個資料庫和執行查詢。

> [!TIP]
> 本教學課程需要使用者輸入和網際網路連線。 如果您有興趣[自動](sql-server-linux-setup.md#unattended)或[離線](sql-server-linux-setup.md#offline)安裝程序，請參閱[SQL Server on Linux 的安裝指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>필수 구성 요소

您必須擁有的 Ubuntu 機器**至少 3.25 GB**的記憶體。

若要安裝的電腦上的 Ubuntu，請移至[http://www.ubuntu.com/download/server](http://www.ubuntu.com/download/server)。 您也可以在 Azure 中建立 Ubuntu 虛擬機器。 請參閱[建立和管理 Linux Vm，使用 Azure CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)。

其他系統需求，請參閱[系統需求的 SQL Server on Linux](sql-server-linux-setup.md#system)。

## <a id="install"></a>安裝 SQL Server

若要設定 SQL Server 在 Ubuntu 上，執行下列命令中安裝終端機**mssql 伺服器**封裝。

1. 匯入公用儲存機制 GPG 機碼：

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 註冊 Microsoft SQL Server Ubuntu 儲存機制：

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server.list)"
   ```

1. 執行下列命令來安裝 SQL Server:

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server
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

1. 如果您打算從遠端連線，您可能也需要開啟防火牆上的 SQL Server TCP 連接埠 （預設值 1433年）。

此時，SQL Server Ubuntu 機器上執行，並可供使用 ！

## <a id="tools"></a>安裝 SQL Server 命令列工具

若要建立資料庫，您需要連接與一種工具，可以在 SQL Server 上執行 TRANSACT-SQL 陳述式。 下列步驟安裝的 SQL Server 命令列工具： [sqlcmd](../tools/sqlcmd-utility.md)和[bcp](../tools/bcp-utility.md)。

1. 匯入公用儲存機制 GPG 機碼：

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 註冊 Microsoft Ubuntu 儲存機制：

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
   ```

1. 更新 [來源] 清單並執行的安裝命令與 unixODBC 開發人員套件：

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-tools unixodbc-dev
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
