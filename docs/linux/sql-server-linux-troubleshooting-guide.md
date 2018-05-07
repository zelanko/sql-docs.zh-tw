---
title: 疑難排解 SQL Server on Linux |Microsoft 文件
description: 提供在 Linux 上使用 SQL Server 2017 疑難排解秘訣。
author: annashres
ms.author: anshrest
manager: craigg
ms.date: 04/30/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.openlocfilehash: ec2fac2c39097fa4091c9cddfe78ae949cd25953
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="troubleshoot-sql-server-on-linux"></a>疑難排解 SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文件說明如何疑難排解 Microsoft SQL Server on Linux 或 Docker 容器中執行。 當疑難排解 SQL Server on Linux，請記得要檢閱的已知的限制的支援的功能[SQL Server on Linux 版本資訊](sql-server-linux-release-notes.md)。

> [!TIP]
> 常見問題的解答，請參閱[Linux 常見問題集 > 的 SQL Server](sql-server-linux-faq.md)。

## <a id="connection"></a> 連接錯誤進行疑難排解
如果您無法連線到您的 Linux SQL Server，有幾件事檢查。 

- 請確認伺服器名稱或 IP 位址是從用戶端電腦。

   > [!TIP]
   > 若要尋找 Ubuntu 機器的 IP 位址，您可以執行 ifconfig 命令，如下列範例所示：
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > Red Hat，您可以使用 ip 位址，如下列範例所示：
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > Azure Vm 與這項技術的例外狀況。 對於 Azure Vm， [Azure 入口網站中，找到的 VM 的公用 IP](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect)。

- 如果適用的話，請檢查您已開啟防火牆上的 SQL Server 連接埠 （預設值 1433年）。

- 對於 Azure Vm，請確認您已[網路安全性群組規則的預設 SQL Server 連接埠](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote)。

- 請確認的使用者名稱和密碼不包含任何拼字錯誤或額外的空格或不正確的大小寫。

- 嘗試明確地設定通訊協定和連接埠號碼的伺服器名稱，如下列範例： **tcp:servername，1433年**。

- 連接錯誤及逾時，也可能會導致網路連線問題。 確認您的連接資訊和網路連線能力後, 再次嘗試連線。

## <a name="manage-the-sql-server-service"></a>管理 SQL Server 服務

下列章節將示範如何啟動、 停止、 重新啟動，並檢查 SQL Server 服務的狀態。 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>管理在 Red Hat Enterprise Linux (RHEL) 和 Ubuntu mssql 伺服器服務 

檢查 SQL Server 服務使用這個命令的狀態：

   ```bash
   sudo systemctl status mssql-server
   ```

您可以停止、 啟動或重新啟動 SQL Server 服務，視需要使用下列命令：

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>管理 mssql Docker 容器的執行

您可以執行下列命令，以取得最新版本建立 SQL Server Docker 容器的狀態和容器識別碼 (ID 低於**容器識別碼**資料行):

   ```bash
   sudo docker ps -l
   ```
   
您可以停止或重新啟動 SQL Server 服務，視需要使用下列命令：
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> 如需疑難排解秘訣，對 Docker，請參閱[疑難排解 SQL Server Docker 容器](sql-server-linux-configure-docker.md#troubleshooting)。

## <a name="access-the-log-files"></a>存取記錄檔
   
/Var/opt/mssql/log/errorlog 檔案在 Linux 和 Docker 安裝 SQL Server 引擎記錄檔。 您必須是 'superuser' 模式瀏覽此目錄中。

安裝程式會記錄以下: / var/選擇/mssql/安裝-< 表示安裝的時間的時間戳記 > 您可以瀏覽錯誤記錄檔檔案，使用任何 utf-16 相容工具，例如 'vim' 或 '數據機' 如下所示： 

   ```bash
   sudo cat errorlog
   ```

如果您想要的話，您也可以將轉換檔案讀取以 utf-8 '' 或多或少 '' 使用下列命令：
   
   ```bash
   sudo iconv –f UTF-16LE –t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>擴充事件

透過 SQL 命令，您可以查詢擴充的事件。  可以找到有關擴充事件的詳細資訊[這裡](https://technet.microsoft.com/en-us/library/bb630282.aspx):

## <a name="crash-dumps"></a>損毀傾印 

尋找在 Linux 中的記錄檔目錄中的傾印。 檢查 /var/opt/mssql/log 目錄下 Linux 核心傾印 (。 tar.gz2 擴充功能) 或 SQL 小型傾印 （.mdmp 擴充功能）

核心傾印 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

SQL 傾印 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>最基本的組態，或在單一使用者模式啟動 SQL Server

### <a name="start-sql-server-in-minimal-configuration-mode"></a>以最低組態模式啟動 SQL Server
如果組態值設定 (如過度調配記憶體) 造成伺服器無法啟動，這就很有用。
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>以單一使用者模式啟動 SQL Server
在某些情況下，您可能要以單一使用者模式啟動 SQL Server 執行個體使用啟動選項-m。 例如，您可能想要變更伺服器組態選項，或復原損毀的 master 資料庫或其他系統資料庫。 例如，您可能想要變更伺服器組態選項或復原損毀的 master 資料庫或其他系統資料庫   

以單一使用者模式啟動 SQL Server
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

使用 SQLCMD 的單一使用者模式啟動 SQL Server
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  以 "mssql" 使用者身分啟動 Linux 上的 SQL Server，以免未來發生啟動問題。 例如，"sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]" 

如果您不小心與其他使用者啟動 SQL Server，您必須回到之前啟動 SQL Server 與 systemd 'mssql' 使用者變更 SQL Server 資料庫檔案的擁有權。 例如，若要變更 'mssql' 使用者 /var/opt/mssql 底下的所有資料庫檔案的擁有權，執行下列命令

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="rebuild-system-databases"></a>重建系統資料庫
作為最後的方法，您可以選擇重建 master 和模型資料庫會回到預設版本。

> [!WARNING]
> 這些步驟將**刪除所有的 SQL Server 系統資料**您設定 ！ 這包括使用者資料庫 （但不是在使用者資料庫本身） 的相關資訊。 它也會刪除儲存在系統資料庫，包括下列其他資訊： 主要金鑰資訊，請在 master、 SA 登入密碼，與工作相關的資訊，從 msdb、 msdb 和 sp_configure 選項從 DB 郵件資訊載入任何憑證。 只有當您了解影響使用 ！

1. 停止 SQL Server。

   ```bash
   sudo systemctl stop mssql-server
   ```

1. 執行**sqlservr**與**強制安裝**參數。 

   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr --force-setup
   ```
   
   > [!WARNING]
   > 請參閱先前的警告 ！ 此外，您必須執行此方法做**mssql**如下所示的使用者。

1. 您會看到訊息 「 復原 」 完成之後，請按 CTRL + C。 這將會關閉 SQL Server

1. 重新設定 SA 的密碼。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-sa-password
   ```
   
1. 啟動 SQL Server，然後重新設定伺服器。 這包括還原或重新附加任何使用者資料庫。

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="common-issues"></a>常見的問題

1. 您無法連接到遠端的 SQL Server 執行個體。

   請參閱疑難排解一節的發行項[連接到 SQL Server on Linux](#connection)。

2. 錯誤： 主機名稱必須為 15 個字元或更少。

   這是電腦的每當嘗試安裝 SQL Server Debian 封裝名稱長度超過 15 個字元的已知問題。 目前沒有任何因應措施以外變更的電腦名稱。 為了達成此目的的一個方式是編輯主機檔案，重新啟動電腦。 下列[網站指南](http://www.cyberciti.biz/faq/ubuntu-change-hostname-command/)這將詳細說明。

3. 重設的系統管理 (SA) 密碼。

   如果您忘記系統管理員 (SA) 密碼，或需要重設它因其他原因，請遵循下列步驟。

   > [!NOTE]
   > 下列步驟會暫時停止 SQL Server 服務。

   登入主機終端機中，執行下列命令，並遵循提示以重設的 SA 密碼：

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. 密碼中使用特殊字元。

   如果您使用某些字元在 SQL Server 登入密碼時，您可能需要使用 Linux 命令，在終端機中時以反斜線逸出。 比方說，您必須逸出錢幣符號 （$） 每當您使用它在終端機的命令/殼層指令碼：

   無法:

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   適用於：

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   資源：[特殊字元](http://tldp.org/LDP/abs/html/special-chars.html)
   [Escaping](http://tldp.org/LDP/abs/html/escapingsection.html)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
