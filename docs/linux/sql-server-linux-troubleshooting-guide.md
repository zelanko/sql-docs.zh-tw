---
title: "疑難排解 SQL Server on Linux |Microsoft 文件"
description: "提供在 Linux 上使用 SQL Server 2017 疑難排解秘訣。"
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 05/08/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: fdaa3435a26bc96a0dfbd3b1043e92f800ab9915
ms.contentlocale: zh-tw
ms.lasthandoff: 10/02/2017

---
# <a name="troubleshoot-sql-server-on-linux"></a>疑難排解 SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本文件說明如何疑難排解 Microsoft SQL Server on Linux 或 Docker 容器中執行。 疑難排解 SQL Server on Linux，請務必檢閱支援的功能與中的已知的限制[SQL Server on Linux 版本資訊](sql-server-linux-release-notes.md)。

## <a id="connection"></a>連接錯誤進行疑難排解
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

- 嘗試明確地設定通訊協定和連接埠號碼的伺服器名稱，如下所示： **tcp:servername，1433年**。

- 連接錯誤及逾時，也可能會導致網路連線問題。 確認您的連接資訊和網路連線能力後, 再次嘗試連線。

## <a name="manage-the-sql-server-service"></a>管理 SQL Server 服務

下列章節將示範如何啟動、 停止、 重新啟動，並檢查 SQL Server 服務的狀態。 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>管理在 Red Hat Enterprise Linux (RHEL) 和 Ubuntu mssql 伺服器服務 

檢查 SQL Server 服務使用這個命令的狀態，狀態：

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

您可以執行下列命令 （識別碼會是 「 容器識別碼 」 資料行底下），以取得最新版本建立 SQL Server Docker 容器的狀態和容器識別碼：

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

## <a name="common-issues"></a>常見的問題

1. 您無法連線到遠端的 SQL Server 執行個體。

   請參閱疑難排解一節的主題，[連接到 SQL Server on Linux](#connection)。

2. 錯誤： 主機名稱必須為 15 個字元或更少。

   這是電腦的每當嘗試安裝 SQL Server Debian 封裝名稱長度超過 15 個字元的已知問題。 目前沒有任何因應措施以外變更的電腦名稱。 為了達成此目的的一個方式是編輯主機檔案，重新啟動電腦。 下列[網站指南](http://www.cyberciti.biz/faq/ubuntu-change-hostname-command/)這將詳細說明。

3. 重設的系統管理 (SA) 密碼。

   如果您忘記系統管理員 (SA) 密碼，或需要重設某些其他原因，請遵循下列步驟。

   > [!NOTE]
   > 下列步驟將會停止 SQL Server 服務暫時。

   登入主機終端機中，執行下列命令，並遵循提示以重設的 SA 密碼：

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. 密碼中使用特殊字元。

   如果您在 SQL Server 登入密碼中使用某些字元您可能需要將其逸出 Linux 終端機中使用它們時。 您必須逸出 $ 隨時使用反斜線字元會使用終端機的命令/殼層指令碼中：

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

## <a name="support"></a>支援

支援是透過社群和受監視的工程團隊。 如有特定問題，使用下列資源：

- [DBA 堆疊 Exchange](https://dba.stackexchange.com/questions/tagged/sql-server)： 提問資料庫管理
- [堆疊溢位](http://stackoverflow.com/questions/tagged/sql-server)： 開發提問
- [MSDN 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)： 詢問技術問題
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)： 報告錯誤和要求的功能
- [Reddit](https://www.reddit.com/r/SQLServer/)： 討論 SQL Server
