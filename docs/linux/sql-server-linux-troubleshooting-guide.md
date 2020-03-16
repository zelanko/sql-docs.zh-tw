---
title: 針對 Linux 上的 SQL Server 進行疑難排解
description: 針對使用 Linux 上的 SQL Server 提供疑難排解秘訣。
author: VanMSFT
ms.author: vanto
ms.date: 05/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.openlocfilehash: a4103e22facbb717b6797b91d8b218cc6ce4b0b7
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79288112"
---
# <a name="troubleshoot-sql-server-on-linux"></a>針對 Linux 上的 SQL Server 進行疑難排解

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文件說明如何針對在 Linux 上或在 Docker 容器中執行的 Microsoft SQL Server 進行疑難排解。 針對 Linux 上的 SQL Server 進行疑難排解時，請記得檢閱 [Linux 上的 SQL Server 版本資訊](sql-server-linux-release-notes.md)中支援的功能和已知限制。

> [!TIP]
> 如需常見問題的解答，請參閱 [Linux 上的 SQL Server 常見問題集](sql-server-linux-faq.md)。

## <a id="connection"></a> 針對連線失敗進行疑難排解
如果您無法連線到 Linux SQL Server，有幾個事項需要檢查。

- 如果您無法使用 **localhost** 來連線到本機，請嘗試改用 IP 位址 127.0.0.1。 有可能是 **localhost** 未正確地對應到此位址。

- 確認可從您的用戶端機器連線到該伺服器名稱或 IP 位址。

   > [!TIP]
   > 若要尋找您 Ubuntu 機器的 IP 位址，您可以執行 ifconfig 命令，如以下範例所示：
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > 針對 Red Hat，您可以使用 ip addr，如以下範例所示：
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > 此技術的其中一個例外與 Azure VM 相關。 針對 Azure VM，請[在 Azure 入口網站中尋找 VM 的公用 IP](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect)。

- 如果適用，請確認您已在防火牆上開啟 SQL Server 連接埠 (預設值為 1433)。

- 針對 Azure VM，請確認您有[適用於預設 SQL Server 連接埠的網路安全性群組規則](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote)。

- 確認使用者名稱和密碼未包含任何錯字、額外空格或不正確的大小寫。

- 嘗試搭配伺服器名稱明確設定通訊協定和連接埠號碼，如以下範例所示：**tcp:servername,1433**。

- 網路連線問題也可能造成連線錯誤和逾時。 確認您的連線資訊和網路連線能力之後，請重新嘗試連線。

## <a name="manage-the-sql-server-service"></a>管理 SQL Server 服務

下列各節說明如何啟動、停止、重新啟動及檢查 SQL Server 服務的狀態。

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>管理 Red Hat Enterprise Linux (RHEL) 和 Ubuntu 中的 mssql-server 服務 

使用此命令來檢查 SQL Server 服務的狀態：

   ```bash
   sudo systemctl status mssql-server
   ```

您可以使用下列命令，視需要停止、啟動或重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>管理 mssql Docker 容器的執行

您可以執行下列命令來取得最新建立之 SQL Server Docker容器的狀態和容器識別碼 (識別碼位於 [容器識別碼]  資料行底下)：

   ```bash
   sudo docker ps -l
   ```
   
您可以使用下列命令來停止或重新啟動 SQL Server 服務：
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> 如需更多 Docker 疑難排解秘訣，請參閱[針對 SQL Server Docker 容器進行疑難排解](sql-server-linux-configure-docker.md#troubleshooting)。

## <a name="access-the-log-files"></a>存取記錄檔
   
SQL Server 引擎在 Linux 和 Docker 安裝中都會記錄至 /var/opt/mssql/log/errorlog 檔案。 您必須處於「超級使用者」模式，才能瀏覽此目錄。

安裝程式會記錄到這裡：/var/opt/mssql/setup-<代表安裝時間的時間戳記>。您可以使用任何 UTF-16 相容工具 (例如 'vim' 或 'cat') 來瀏覽錯誤記錄檔，就像這樣： 

   ```bash
   sudo cat errorlog
   ```

如果您想要的話，也可以將檔案轉換成 UTF-8，以使用下列命令來或「多」或「少」地讀取這些檔案：
   
   ```bash
   sudo iconv -f UTF-16LE -t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>擴充事件

透過 SQL 命令可以查詢擴充事件。  如需有關擴充事件的詳細資訊，可以在[這裡](https://technet.microsoft.com/library/bb630282.aspx)找到：

## <a name="crash-dumps"></a>損毀傾印 

在 Linux 的記錄檔目錄中尋找傾印。 檢查 /var/opt/mssql/log 目錄底下是否有 Linux 核心傾印 (.tar.gz2 副檔名) 或 SQL 小型傾印 (.mdmp 副檔名)

針對核心傾印 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

針對 SQL 傾印 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>以最小設定或單一使用者模式啟動 SQL Server

### <a name="start-sql-server-in-minimal-configuration-mode"></a>以最小設定模式啟動 SQL Server
如果組態值設定 (如過度調配記憶體) 造成伺服器無法啟動，這就很有用。
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>以單一使用者模式啟動 SQL Server
在某些情況下，您可能需要使用 startup option -m，以單一使用者模式啟動 SQL Server 的執行個體。 例如，您可能想要變更伺服器組態選項，或復原損毀的 master 資料庫或其他系統資料庫。 例如，您可能會想要變更伺服器組態選項，或是復原損毀的 master 資料庫或其他系統資料庫   

以單一使用者模式啟動 SQL Server
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

使用 SQLCMD 以單一使用者模式啟動 SQL Server
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  以 "mssql" 使用者身分啟動 Linux 上的 SQL Server，以免未來發生啟動問題。 例如，"sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]" 

如果您不小心以另一位使用者啟動了 SQL Server，就必須先將 SQL Server 資料庫檔案的擁有權變更回 'mssql' 使用者，再使用 systemd 來啟動 SQL Server。 例如，若要將 /var/opt/mssql 底下所有資料庫檔案的擁有權變更為 'mssql' 使用者，請執行下列命令

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="rebuild-system-databases"></a>重建系統資料庫
作為最後的手段，您可以選擇將 master 和模型資料庫重建回預設板板。

> [!WARNING]
> 這些步驟將會**刪除您已設定的所有 SQL Server 系統資料**！ 這包括與您使用者資料庫相關 (但非使用者資料庫本身) 的資訊。 它也會刪除其他儲存在系統資料庫中的資訊，包括下列資訊：主要金鑰資訊、在 master 中載入的任何憑證、SA 登入密碼、來自 msdb 的作業相關資訊、來自 msdb 的 DB 郵件資訊，以及 sp_configure 選項。 請只在您了解其含意時才使用！

1. 停止 SQL Server。

   ```bash
   sudo systemctl stop mssql-server
   ```

1. 執行 **sqlservr** 搭配 **force-setup** 參數。 

   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr --force-setup
   ```
   
   > [!WARNING]
   > 請參閱先前的警告！ 此外，如這裡所示，您必須以 **mssql** 使用者的身分執行此操作。

1. 看到「復原已完成」訊息之後，按 CTRL+C。 這會關閉 SQL Server

1. 重新設定 SA 密碼。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-sa-password
   ```
   
1. 啟動 SQL Server 並重新設定伺服器。 這包括還原或重新連結任何使用者資料庫。

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="improve-performance"></a>改善效能

有許多影響效能的因素，包括資料庫設計、硬體及工作負載需求。 如果您想要改善效能，請從檢閱 [Linux 上 SQL Server 的效能最佳做法和設定方針](sql-server-linux-performance-best-practices.md)一文中的最佳做法開始著手。 然後探索一些可用來針對效能問題進行疑難排解的工具。

- [查詢存放區](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [系統動態管理檢視 (DMV)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [SQL Server Management Studio 中的效能儀表板](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)

## <a name="common-issues"></a>常見問題

1. 您無法連線到遠端 SQL Server 執行個體。

   請參閱[連線到 Linux 上的 SQL Server](#connection)一文的疑難排解小節。

2. 錯誤：主機名稱長度必須等於或少於 15 個字元。

   這是一個已知問題，每當嘗試安裝 SQL Server Debian 套件的機器名稱長度超過 15 個字元時就會發生。 目前除了變更機器名稱之外，沒有任何因應措施。 其中一個達到此目的的方法就是編輯主機名稱檔案，然後重新啟動機器。 下列[網站指南](https://www.cyberciti.biz/faq/ubuntu-change-hostname-command/)會詳細說明這一點。

3. 重設系統管理員 (SA) 密碼。

   如果您已忘記系統管理員 (SA) 密碼，或因其他原因而必須重設此密碼，請依照下列步驟進行操作。

   > [!NOTE]
   > 下列步驟會暫時停止 SQL Server 服務。

   登入主機終端機，執行下列命令，然後依照提示來重設 SA 密碼：

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. 在密碼中使用特殊字元。

   如果您在 SQL Server 登入密碼中使用某些字元，則在終端機的 Linux 命令中使用這些字元時，可能需要以反斜線將其逸出。 例如，每當您在終端機命令/殼層指令碼中使用貨幣符號 ($) 時，都必須將其逸出：

   無效：

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   有效：

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   資源：[特殊字元](https://tldp.org/LDP/abs/html/special-chars.html)
   [逸出](https://tldp.org/LDP/abs/html/escapingsection.html)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
