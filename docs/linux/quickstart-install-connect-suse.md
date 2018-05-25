---
title: 開始使用 SUSE Linux Enterprise Server 上的 SQL Server 2017 |Microsoft 文件
description: 本快速入門示範如何在 SUSE Linux Enterprise Server 上安裝 SQL Server 2017 然後建立並查詢資料庫，以使用 sqlcmd。
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
ms.assetid: 31ddfb80-f75c-4f51-8540-de6213cb68b8
ms.openlocfilehash: 77dd13139eba88a40cbf20094b880c5046ebfb05
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-suse-linux-enterprise-server"></a>快速入門： 安裝 SQL Server 和 SUSE Linux Enterprise Server 上建立資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本快速入門中，您先安裝 SQL Server 2017 SUSE Linux Enterprise Server (SLES) v12 SP2 上。 然後與 **sqlcmd**連線來建立您的第一個資料庫並執行查詢。

> [!TIP]
> 本教學課程需要使用者輸入和網際網路連線。 如果您有興趣[自動](sql-server-linux-setup.md#unattended)或[離線](sql-server-linux-setup.md#offline)安裝程序，請參閱[SQL Server on Linux 的安裝指南](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>필수 구성 요소

您必須具有的 SLES v12 SP2 機器**至少 2 GB**的記憶體。 檔案系統必須是**XFS**或**EXT4**。 其他檔案系統，例如**BTRFS**，不受支援。

若要安裝 SUSE Linux Enterprise Server 的電腦上，請移至[ https://www.suse.com/products/server ](https://www.suse.com/products/server)。 您也可以在 Azure 中建立 SLES 虛擬機器。 請參閱[建立和管理 Linux Vm 與 Azure CLI](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm)，並使用`--image SLES`呼叫`az vm create`。

> [!NOTE]
> 此時，[適用於 Linux 的 Windows 子系統](https://msdn.microsoft.com/commandline/wsl/about)做為安裝目標不支援 Windows 10。

其他系統需求，請參閱[系統需求的 SQL Server on Linux](sql-server-linux-setup.md#system)。

## <a id="install"></a>安裝 SQL Server

若要設定 SQL Server SLES 上，執行下列命令中安裝終端機**mssql 伺服器**封裝：

> [!IMPORTANT]
> 如果您先前曾安裝 CTP 或 RC 版本的 SQL Server 2017，您必須先移除舊的存放庫，再註冊 GA 儲存機制的其中一個。 如需詳細資訊，請參閱[從預覽儲存機制的儲存機制變更至 GA 儲存機制](sql-server-linux-change-repo.md)。

1. 下載 Microsoft SQL Server SLES 儲存機制設定檔：

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
   ```

   > [!NOTE]
   > 這是累計更新 (CU) 儲存機制。 如需有關您的儲存機制選項以及其差異的詳細資訊，請參閱[儲存機制設定 SQL Server on Linux](sql-server-linux-change-repo.md)。

1. 重新整理您的儲存機制。

   ```bash
   sudo zypper --gpg-auto-import-keys refresh 
   ```
   
1. 執行下列命令來安裝 SQL Server:

   ```bash
   sudo zypper install -y mssql-server
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

1. 如果您打算從遠端連線，您可能也需要開啟防火牆上的 SQL Server TCP 連接埠 （預設值 1433年）。 如果您使用 SuSE 防火牆，您需要編輯 **/etc/sysconfig/SuSEfirewall2**組態檔。 修改**FW_SERVICES_EXT_TCP**包含 SQL Server 連接埠號碼的項目。

   ```
   FW_SERVICES_EXT_TCP="1433"
   ```

此時，SQL Server SLES 機器上執行，並可供使用 ！

## <a id="tools"></a>安裝 SQL Server 命令列工具

若要建立資料庫，您需要連接與一種工具，可以在 SQL Server 上執行 TRANSACT-SQL 陳述式。 下列步驟安裝的 SQL Server 命令列工具： [sqlcmd](../tools/sqlcmd-utility.md)和[bcp](../tools/bcp-utility.md)。

1. 加入 Zypper Microsoft SQL Server 儲存機制。

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. 安裝**mssql 工具**unixODBC 開發人員套件。

   ```bash
   sudo zypper install -y mssql-tools unixODBC-devel
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
> * [SQL Server Management Studio](sql-server-linux-manage-ssms.md)
> * [Visual Studio 程式碼](sql-server-linux-develop-use-vscode.md)。
> * [mssql-cli (預覽)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
