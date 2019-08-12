---
title: 在 Linux 上設定 SQL Server 設定
description: 此文章說明如何使用 mssql-conf 工具，在 Linux 上設定 SQL Server 設定。
author: VanMSFT
ms.author: vanto
ms.date: 07/30/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.openlocfilehash: aaddcbfb9520f2619df82ddbf3695604c2cbee40
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661379"
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>使用 mssql-conf 工具在 Linux 上設定 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

**mssql-conf** 是一個設定指令碼，會使用適用於 Red Hat Enterprise Linux、SUSE Linux Enterprise Server 和 Ubuntu 的 SQL Server 2017 進行安裝。 您可以使用此公用程式來設定下列參數：

|||
|---|---|
| [代理程式](#agent) | 啟用 SQL Server Agent。 |
| [定序](#collation) | 為 Linux 上的 SQL Server 設定新的定序。 |
| [客戶意見反應](#customerfeedback) | 選擇 SQL Server 是否要將意見反應傳送給 Microsoft。 |
| [Database Mail 設定檔](#dbmail) | 為 Linux 上的 SQL Server 設定預設 Database Mail 設定檔。 |
| [預設資料目錄](#datadir) | 變更新 SQL Server 資料庫資料檔案 (.mdf) 的預設目錄。 |
| [預設記錄目錄](#datadir) | 變更新 SQL Server 資料庫記錄 (.ldf) 檔案的預設目錄。 |
| [預設 master 資料庫目錄](#masterdatabasedir) | 變更 master 資料庫和記錄檔的預設目錄。|
| [預設 master 資料庫檔案名稱](#masterdatabasename) | 變更 master 資料庫檔案的名稱。 |
| [預設傾印目錄](#dumpdir) | 變更新記憶體傾印和其他疑難排解檔案的預設目錄。 |
| [預設錯誤記錄檔目錄](#errorlogdir) | 變更新 SQL Server 錯誤記錄檔、預設分析工具追蹤、系統健康情況工作階段 XE，以及 Hekaton 工作階段 XE 檔案的預設目錄。 |
| [預設備份目錄](#backupdir) | 變更新備份檔案的預設目錄。 |
| [傾印類型](#coredump) | 選擇要收集的傾印記憶體傾印檔案類型。 |
| [高可用性](#hadr) | 啟用可用性群組。 |
| [本機稽核目錄](#localaudit) | 設定目錄來新增本機稽核檔案。 |
| [地區設定](#lcid) | 設定要針對 SQL Server 使用的地區設定。 |
| [記憶體限制](#memorylimit) | 設定 SQL Server 的記憶體限制。 |
| [TCP 連接埠](#tcpport) | 變更 SQL Server 接聽連線所在的連接埠。 |
| [TLS](#tls) | 設定傳輸層級安全性。 |
| [追蹤旗標](#traceflags) | 設定服務即將使用的追蹤旗標。 |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

**mssql-conf** 是一個設定指令碼，會使用適用於 Red Hat Enterprise Linux、SUSE Linux Enterprise Server 和 Ubuntu 的 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 進行安裝。 您可以使用此公用程式來設定下列參數：

|||
|---|---|
| [代理程式](#agent) | 啟用 SQL Server Agent |
| [定序](#collation) | 為 Linux 上的 SQL Server 設定新的定序。 |
| [客戶意見反應](#customerfeedback) | 選擇 SQL Server 是否要將意見反應傳送給 Microsoft。 |
| [Database Mail 設定檔](#dbmail) | 為 Linux 上的 SQL Server 設定預設 Database Mail 設定檔。 |
| [預設資料目錄](#datadir) | 變更新 SQL Server 資料庫資料檔案 (.mdf) 的預設目錄。 |
| [預設記錄目錄](#datadir) | 變更新 SQL Server 資料庫記錄 (.ldf) 檔案的預設目錄。 |
| [預設 master 資料庫檔案目錄](#masterdatabasedir) | 在現有 SQL 安裝上變更 master 資料庫檔案的預設目錄。|
| [預設 master 資料庫檔案名稱](#masterdatabasename) | 變更 master 資料庫檔案的名稱。 |
| [預設傾印目錄](#dumpdir) | 變更新記憶體傾印和其他疑難排解檔案的預設目錄。 |
| [預設錯誤記錄檔目錄](#errorlogdir) | 變更新 SQL Server 錯誤記錄檔、預設分析工具追蹤、系統健康情況工作階段 XE，以及 Hekaton 工作階段 XE 檔案的預設目錄。 |
| [預設備份目錄](#backupdir) | 變更新備份檔案的預設目錄。 |
| [傾印類型](#coredump) | 選擇要收集的傾印記憶體傾印檔案類型。 |
| [高可用性](#hadr) | 啟用可用性群組。 |
| [本機稽核目錄](#localaudit) | 設定目錄來新增本機稽核檔案。 |
| [地區設定](#lcid) | 設定要針對 SQL Server 使用的地區設定。 |
| [記憶體限制](#memorylimit) | 設定 SQL Server 的記憶體限制。 |
| [Microsoft 分散式交易協調器](#msdtc) | 設定和疑難排解 Linux 上的 MSDTC。 |
| [MLServices EULA](#mlservices-eula) | 接受適用於 mlservices 套件的 R 和 Python EULA。 只適用於 SQL Server 2019。|
| [outboundnetworkaccess](#mlservices-outbound-access) |針對 [mlservices](sql-server-linux-setup-machine-learning.md) R、Python 及 Java 延伸模組啟用輸出網路存取。|
| [TCP 連接埠](#tcpport) | 變更 SQL Server 接聽連線所在的連接埠。 |
| [TLS](#tls) | 設定傳輸層級安全性。 |
| [追蹤旗標](#traceflags) | 設定服務即將使用的追蹤旗標。 |

::: moniker-end

> [!TIP]
> 這其中一些設定也可以使用環境變數來設定。 如需詳細資訊，請參閱[使用環境變數設定 SQL Server 設定](sql-server-linux-configure-environment-variables.md)。

## <a name="usage-tips"></a>使用提示

* 對於 Always On 可用性群組和共用磁碟叢集，一律會在每個節點上進行相同的設定變更。

* 針對共用磁碟叢集案例，請勿嘗試重新開啟 **mssql-server** 服務來套用變更。 SQL Server 正以應用程式形式執行中。 相反地，讓資源離線，然後重新上線。

* 這些範例會藉由指定完整路徑來執行 mssql-conf： **/opt/mssql/bin/mssql-conf**。 如果您選擇改為巡覽至該路徑，請在目前目錄的內容中執行 mssql-conf： **./mssql-conf**。

## <a id="agent"></a> 啟用 SQL Server Agent

**sqlagent.enabled** 設定會啟用 [SQL Server Agent](sql-server-linux-run-sql-server-agent-job.md)。 預設會停用 SQL Server Agent。 如果 **sqlagent.enabled** 未出現在 mssql.conf 設定檔中，則 SQL Server 會在內部假設 SQL Server Agent 已停用。

若要變更此設定，請執行下列步驟：

1. 啟用 SQL Server Agent：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   ```

2. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="collation"></a> 變更 SQL Server 定序

**set-collation** 選項會將定序值變更為任何支援的定序。

1. 先在您的伺服器上[備份所有使用者資料庫](sql-server-linux-backup-and-restore-database.md)。

1. 接著，使用 [ sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) 預存程序來中斷連結使用者資料庫。

1. 執行 **set-collation** 選項並遵循提示：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. mssql-conf 公用程式將嘗試變更為指定的定序值，並重新啟動服務。 如果發生任何錯誤，則會將定序復原為先前的值。

1. 還原您的使用者資料庫備份。

如需支援的定序清單，請執行 [fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) 函數：`SELECT Name from sys.fn_helpcollations()`。

## <a id="customerfeedback"></a> 設定客戶意見反應

**telemetry.customerfeedback** 設定會變更 SQL Server 是否要將意見反應傳送給 Microsoft。 預設會針對所有版本將此值設為 **true**。 若要變更此值，請執行下列命令：

> [!IMPORTANT]
> 您不能針對免費的 SQL Server 版本 (Express 和 Developer) 關閉客戶意見反應。

1. 使用 **telemetry.customerfeedback** 的 **set** 命令，以 root 身分執行 mssql-conf 指令碼。 下列範例藉由指定 **false** 來關閉客戶意見反應。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

如需詳細資訊，請參閱[對於 Linux 上 SQL Server 的客戶意見反應](sql-server-linux-customer-feedback.md)和 [SQL Server 隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=868444)。

## <a id="datadir"></a> 變更預設資料或記錄目錄位置

**filelocation.defaultdatadir** 和 **filelocation.defaultlogdir** 設定會變更建立新資料庫和記錄檔的位置。 根據預設，此位置為 /var/opt/mssql/data。 若要變更這些設定，請使用下列步驟：

1. 為新的資料庫資料和記錄檔建立目標目錄。 下列範例會建立新的 **/tmp/data** 目錄：

   ```bash
   sudo mkdir /tmp/data
   ```

1. 將目錄的擁有者和群組變更為 **mssql** 使用者：

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. 使用 mssql-conf 搭配 **set** 命令來變更預設資料目錄：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

1. 現在，新建資料庫的所有資料庫檔案都將儲存於這個新位置。 如果您想要變更新資料庫的記錄 (.ldf) 檔案位置，您可以使用下列 "set" 命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. 此命令也會假設 /tmp/log 目錄存在，而且它位於使用者和群組 **mssql** 之下。


## <a id="masterdatabasedir"></a> 變更預設 master 資料庫檔案目錄位置

**filelocation.masterdatafile** 和 **filelocation.masterlogfile** 設定會變更 SQL Server 引擎尋找 master 資料庫檔案的位置。 根據預設，此位置為 /var/opt/mssql/data。

若要變更這些設定，請使用下列步驟：

1. 為新的錯誤記錄檔建立目標目錄。 下列範例會建立新的 **/tmp/masterdatabasedir** 目錄：

   ```bash
   sudo mkdir /tmp/masterdatabasedir
   ```

1. 將目錄的擁有者和群組變更為 **mssql** 使用者：

   ```bash
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
   ```

1. 使用 mssql-conf 搭配 **set** 命令，來變更主要資料和記錄檔的預設 master 資料庫目錄：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
   ```

   > [!NOTE]
   > 除了移動主要資料和記錄檔，這也會移動所有其他系統資料庫的預設位置。

1. 停止 SQL Server 服務：

   ```bash
   sudo systemctl stop mssql-server
   ```

1. 移動 master.mdf 和 masterlog.ldf：

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf 
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
   ```

1. 啟動 SQL Server 服務：

   ```bash
   sudo systemctl start mssql-server
   ```

   > [!NOTE]
   > 如果 SQL Server 在指定目錄中找不到 master.mdf 和 mastlog.ldf 檔案，將在指定目錄中自動建立系統資料庫的樣板化複本，而 SQL Server 將會成功啟動。 不過，中繼資料 (例如，使用者資料庫、伺服器登入、伺服器憑證、加密金鑰、SQL Agent 作業或舊的 SA 登入密碼) 將不會在新的 master 資料庫中更新。 您將必須停止 SQL Server，並將舊的 master.mdf 和 mastlog.ldf 移到新的指定位置，然後啟動 SQL Server 以繼續使用現有的中繼資料。
 
## <a id="masterdatabasename"></a> 變更 master 資料庫檔案的名稱

**filelocation.masterdatafile** 和 **filelocation.masterlogfile** 設定會變更 SQL Server 引擎尋找 master 資料庫檔案的位置。 您也可以使用此動作來變更 master 資料庫和記錄檔的名稱。 

若要變更這些設定，請使用下列步驟：

1. 停止 SQL Server 服務：

   ```bash
   sudo systemctl stop mssql-server
   ```

1. 使用 mssql-conf 搭配 **set** 命令，來變更主要資料和記錄檔的預期 master 資料庫名稱：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data/mastlognew.ldf
   ```

   > [!IMPORTANT]
   > 當 SQL Server 成功啟動之後，您就只能變更 master 資料庫和記錄檔的名稱。 初始執行之前，SQL Server 預期會將檔案命名為 master.mdf 和 mastlog.ldf。

1. 變更 master 資料庫資料和記錄檔的名稱 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /var/opt/mssql/data/masternew.mdf
   sudo mv /var/opt/mssql/data/mastlog.ldf /var/opt/mssql/data/mastlognew.ldf
   ```

1. 啟動 SQL Server 服務：

   ```bash
   sudo systemctl start mssql-server
   ```

## <a id="dumpdir"></a> 變更預設傾印目錄位置

**filelocation.defaultdumpdir** 設定會變更在發生損毀時產生記憶體和 SQL 傾印的預設位置。 根據預設，這些檔案會產生於 /var/opt/mssql/log 中。

若要設定這個新位置，請使用下列命令：

1. 為新的傾印檔案建立目標目錄。 下列範例會建立新的 **/tmp/dump** 目錄：

   ```bash
   sudo mkdir /tmp/dump
   ```

1. 將目錄的擁有者和群組變更為 **mssql** 使用者：

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. 使用 mssql-conf 搭配 **set** 命令來變更預設資料目錄：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="errorlogdir"></a> 變更預設錯誤記錄檔目錄位置

**filelocation.errorlogfile** 設定會變更建立新錯誤記錄檔、預設分析工具追蹤、系統健康情況工作階段 XE，以及 Hekaton 工作階段 XE 檔案的位置。 根據預設，此位置為 /var/opt/mssql/log。 設定 SQL 錯誤記錄檔的目錄會成為其他記錄的預設記錄目錄。

變更這些設定：

1. 為新的錯誤記錄檔建立目標目錄。 下列範例會建立新的 **/tmp/logs** 目錄：

   ```bash
   sudo mkdir /tmp/logs
   ```

1. 將目錄的擁有者和群組變更為 **mssql** 使用者：

   ```bash
   sudo chown mssql /tmp/logs
   sudo chgrp mssql /tmp/logs
   ```

1. 使用 mssql-conf 搭配 **set** 命令來變更預設錯誤記錄檔的檔案名稱：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```


## <a id="backupdir"></a> 變更預設備份目錄位置

**filelocation.defaultbackupdir** 設定會變更產生備份檔案的預設位置。 根據預設，這些檔案會產生於 /var/opt/mssql/data 中。

若要設定這個新位置，請使用下列命令：

1. 為新的備份檔案建立目標目錄。 下列範例會建立新的 **/tmp/backup** 目錄：

   ```bash
   sudo mkdir /tmp/backup
   ```

1. 將目錄的擁有者和群組變更為 **mssql** 使用者：

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. 使用 mssql-conf 搭配 "set" 命令來變更預設備份目錄：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="coredump"></a> 指定核心傾印設定

如果其中一個 SQL Server 程序中發生例外狀況，SQL Server 就會建立記憶體傾印。

有兩個選項可控制 SQL Server 所收集的記憶體傾印類型：**coredump.coredumptype** 和 **coredump.captureminiandfull**。 這些都與核心傾印擷取的兩個階段有關。 

第一個階段的擷取是由 **coredump.coredumptype** 設定所控制，它會決定例外狀況期間所產生的傾印檔案類型。 第二個階段會在 **coredump.captureminiandfull** 設定時啟用。 如果將 **coredump.captureminiandfull** 設定為 true，則會產生 **coredump.coredumptype** 所指定的傾印檔案，同時也會產生第二個迷你傾印。 將 **coredump.captureminiandfull** 設定為 false，會停用第二次擷取嘗試。

1. 決定是否要使用 **coredump.captureminiandfull** 設定來擷取迷你和完整傾印。

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    預設值：**false**

1. 使用 **coredump.coredumptype** 設定來指定傾印檔案的類型。

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    預設值：**miniplus**

    下表列出可能的 **coredump.coredumptype** 值。

    | 類型 | Description |
    |-----|-----|
    | **mini** | Mini 是最小的傾印檔案類型。 它會使用 Linux 系統資訊來判斷程序中的執行緒和模組。 傾印僅包含主機環境執行緒堆疊和模組。 它不包含間接記憶體參考或 Globals。 |
    | **miniplus** | MiniPlus 類似於 mini，但它包含額外的記憶體。 它瞭解 SQLPAL 和主機環境的內部，並將下列記憶體區域新增至傾印：</br></br> - 各種 Globals</br> - 所有高於 64TB 的記憶體</br> - 在 **/proc/$pid/maps** 中找到的所有具名區域</br> - 來自執行緒和堆疊的間接記憶體</br> - 執行緒資訊</br> - 相關聯的 Teb 和 Peb</br> - 模組資訊</br> - VMM 和 VAD 樹狀 |
    | **filtered** | Filtered 會使用以減法為基礎的設計，除非特別排除，否則會包含程序中的所有記憶體。 此設計瞭解 SQLPAL 和主機環境的內部，但不包括來自傾印的特定區域。
    | **full** | Full 是完整處理的傾印，其中包含位於 **/proc/$pid/maps** 的所有區域。 這不是由 **coredump.captureminiandfull** 設定所控制的。 |

## <a id="dbmail"></a> 為 Linux 上的 SQL Server 設定預設 Database Mail 設定檔

**sqlpagent.databasemailprofile** 可讓您針對電子郵件警示設定預設的 DB Mail 設定檔。

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a> 高可用性

**hadr.hadrenabled** 選項會在您的 SQL Server 執行個體上啟用可用性群組。 下列命令藉由將 **hadr.hadrenabled** 設定為 1 來啟用可用性群組。 您必須重新啟動 SQL Server，才能使設定生效。

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

如需如何搭配可用性群組使用此操作的詳細資訊，請參閱下列兩個主題。

- [在 Linux 上設定 SQL Server 的 Always On 可用性群組](sql-server-linux-availability-group-configure-ha.md)
- [在 Linux 上設定 SQL Server 的讀取級別可用性群組](sql-server-linux-availability-group-configure-rs.md)


## <a id="localaudit"></a> 設定本機稽核目錄

**telemetry.userrequestedlocalauditdirectory** 設定會啟用本機稽核，並讓您能夠設定建立本機稽核記錄的目錄。

1. 為新的本機稽核記錄建立目標目錄。 下列範例會建立新的 **/tmp/audit** 目錄：

   ```bash
   sudo mkdir /tmp/audit
   ```

1. 將目錄的擁有者和群組變更為 **mssql** 使用者：

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. 使用 **telemetry.userrequestedlocalauditdirectory** 的 **set** 命令，以 root 身分執行 mssql-conf 指令碼：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

如需詳細資訊，請參閱[對於 Linux 上 SQL Server 的客戶意見反應](sql-server-linux-customer-feedback.md)。

## <a id="lcid"></a> 變更 SQL Server 地區設定

**language.lcid** 設定會將 SQL Server 地區設定變更為任何支援的語言識別碼 (LCID)。 

1. 下列範例會將地區設定變更為 [法文 (1036)]：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. 重新啟動 SQL Server 服務以套用變更：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a> 設定記憶體限制

**memory.memorylimitmb** 設定會控制 SQL Server 可用的實體記憶體數量 (以 MB 為單位)。 預設值為 80% 的實體記憶體。

1. 使用 **memory.memorylimitmb** 的 **set** 命令，以 root 身分執行 mssql-conf 指令碼。 下列範例會將 SQL Server 可用的記憶體變更為 3.25 GB (3328 MB)。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. 重新啟動 SQL Server 服務以套用變更：

   ```bash
   sudo systemctl restart mssql-server
   ```

::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="msdtc"></a> 設定 MSDTC

**network.rpcport** 和 **distributedtransaction.servertcpport** 設定會用來設定 Microsoft 分散式交易協調器 (MSDTC)。 若要變更這些設定，請執行下列命令：

1. 使用 "network.rpcport" 的 **set** 命令，以 root 身分執行 mssql-conf 指令碼：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport <rcp_port>
   ```

2. 接著，設定 "distributedtransaction.servertcpport" 設定：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport <servertcpport_port>
   ```

除了設定這些值，您還必須為連接埠 135 設定路由及更新防火牆。 如需如何執行此動作的詳細資訊，請參閱[如何在 Linux 上設定 MSDTC](sql-server-linux-configure-msdtc.md)。

您可以使用其他數個適用於 mssql-conf 的設定來監視和疑難排解 MSDTC。 下表簡短描述這些設定。 如需其使用方式的詳細資訊，請參閱 Windows 支援文章中的詳細資料：[如何針對 MS DTC 啟用診斷追蹤](https://support.microsoft.com/help/926099/how-to-enable-diagnostic-tracing-for-ms-dtc-on-a-windows-based-compute) \(機器翻譯\)。

| mssql-conf 設定 | Description |
|---|---|
| distributedtransaction.allowonlysecurerpccalls | 針對分散式交易設定僅安全的 RPC 呼叫 |
| distributedtransaction.fallbacktounsecurerpcifnecessary | 設定僅安全的 RPC 呼叫以用於分散式 |交易
| distributedtransaction.maxlogsize | DTC 交易記錄檔大小 (以 MB 為單位)。 預設值是 64MB |
| distributedtransaction.memorybuffersize | 儲存追蹤的循環緩衝區大小。 此大小會以 MB 為單位，預設值為 10MB |
| distributedtransaction.servertcpport | MSDTC rpc 伺服器連接埠 |
| distributedtransaction.trace_cm | 連線管理員中的追蹤 |
| distributedtransaction.trace_contact | 追蹤連絡人集區和連絡人 |
| distributedtransaction.trace_gateway | 追蹤閘道來源 |
| distributedtransaction.trace_log | 記錄追蹤 |
| distributedtransaction.trace_misc | 無法分類到其他類別的追蹤 |
| distributedtransaction.trace_proxy | MSDTC Proxy 中所產生的追蹤 |
| distributedtransaction.trace_svc | 追蹤服務和 .exe 檔案啟動 |
| distributedtransaction.trace_trace | 追蹤基礎結構本身 |
| distributedtransaction.trace_util | 追蹤從多個位置呼叫的公用程式常式 |
| distributedtransaction.trace_xa | XA 交易管理員 (XATM) 追蹤來源 |
| distributedtransaction.tracefilepath | 應在其中儲存追蹤檔案的資料夾 |
| distributedtransaction.turnoffrpcsecurity | 啟用或停用分散式交易的 RPC 安全性 |

::: moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-eula"></a> 接受 MLServices EULA

將[機器學習 R 或 Python 套件](sql-server-linux-setup-machine-learning.md)新增至資料庫引擎，要求您接受適用於 R 和 Python 開放原始碼發行版本的授權條款。 下表列舉與 mlservices EULA 相關的所有可用命令或選項。 根據您安裝的內容而定，會針對 R 和 Python 使用相同的 EULA 參數。

```bash
# For all packages: database engine and mlservices
# Setup prompts for mlservices EULAs, which you need to accept
sudo /opt/mssql/bin/mssql-conf setup

# Add R or Python to an existing installation
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml

# Alternative valid syntax
# Adds the EULA section to the INI and sets acceptulam to yes
sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y

# Rescind EULA acceptance and removes the setting
sudo /opt/mssql/bin/mssql-conf unset EULA accepteulaml
```

您也可以將接受 EULA 直接新增至 [mssql.conf 檔案](#mssql-conf-format)：

```ini
[EULA]
accepteula = Y
accepteulaml = Y
```
:::moniker-end
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="mlservices-outbound-access"></a> 啟用輸出網路存取

預設會在 [SQL Server 機器學習服務](sql-server-linux-setup-machine-learning.md)功能中，停用 R、Python 和 JAVA 延伸模組的輸出網路存取。 若要啟用輸出要求，請使用 mssql-conf 來設定 "outboundnetworkaccess" 布林值屬性。

設定屬性之後，重新啟動 SQL Server Launchpad 服務，以從 INI 檔案讀取更新後的值。 每當修改擴充性相關設定時，系統就會顯示重新啟動訊息來提醒您。

```bash
# Adds the extensibility section and property.
# Sets "outboundnetworkaccess" to true.
# This setting is required if you want to access data or operations off the server.
sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1

# Turns off network access but preserves the setting
/opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 0

# Removes the setting and rescinds network access
sudo /opt/mssql/bin/mssql-conf unset extensibility.outboundnetworkaccess
```

您也可以將 "outboundnetworkaccess" 直接新增至 [mssql.conf 檔案](#mssql-conf-format)：

```ini
[extensibility]
outboundnetworkaccess = 1
```
:::moniker-end

## <a id="tcpport"></a> 變更 TCP 通訊埠

**network.tcpport** 設定會變更 SQL Server 用來接聽連線的 TCP 連接埠。 此連接埠預設為 1433。 若要變更此連接埠，請執行下列命令：

1. 使用 "network.rpcport" 的 "set" 命令，以 root 身分執行 mssql-conf 指令碼：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

2. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

3. 目前在連線到 SQL Server 時，您必須在主機名稱或 IP 位址之後，以逗號 (,) 指定自訂連接埠。 例如，若要使用 SQLCMD 連線，您可以使用下列命令：

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a> 指定 TLS 設定

下列選項會針對在 Linux 上執行的 SQL Server 執行個體設定 TLS。

|選項 |Description |
|--- |--- |
|**network.forceencryption** |如果是 1，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會強制加密所有連線。 根據預設，這個選項是 0。 |
|**network.tlscert** |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 針對 TLS 使用之憑證檔案的絕對路徑。 範例 `/etc/ssl/certs/mssql.pem` 憑證檔案必須可由 mssql 帳戶存取。 Microsoft 建議使用 `chown mssql:mssql <file>; chmod 400 <file>` 來限制檔案的存取。 |
|**network.tlskey** |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 針對 TLS 使用之私密金鑰檔案的絕對路徑。 範例`/etc/ssl/private/mssql.key` 憑證檔案必須可由 mssql 帳戶存取。 Microsoft 建議使用 `chown mssql:mssql <file>; chmod 400 <file>` 來限制檔案的存取。 |
|**network.tlsprotocols** |SQL Server 所允許的 TLS 通訊協定清單 (以逗號分隔)。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 一律會嘗試交涉最強的允許通訊協定。 如果用戶端不支援任何允許的通訊協定，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 就會拒絕連線嘗試。  若要取得相容性，預設允許所有支援的通訊協定 (1.2、1.1、1.0)。  如果您的用戶端支援 TLS 1.2，則 Microsoft 建議只允許 TLS 1.2。 |
|**network.tlsciphers** |針對 TLS 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 允許哪些 Cipher。 此字串必須根據每個 [OpenSSL 的 Cipher 清單格式](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html) \(英文\) 來格式化。 一般來說，您應該不需要變更此選項。 <br /> 預設允許下列 Cipher： <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Kerberos keytab 檔案的路徑 |

如需使用 TLS 設定的範例，請參閱[在 Linux 上加密 SQL Server 連線](sql-server-linux-encrypted-connections.md)。

## <a id="traceflags"></a> 啟用/停用追蹤旗標

這個**追蹤旗標**選項會啟用或停用啟動 SQL Server 服務的追蹤旗標。 若要啟用/停用追蹤旗標，請使用下列命令：

1. 使用下列命令來啟用追蹤旗標。 例如，針對追蹤旗標 1234：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. 您可以分別指定多個追蹤旗標來啟用它們：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. 同樣地，您可以藉由指定追蹤旗標並新增 **off** 參數來停用一或多個已啟用的追蹤旗標：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. 重新啟動 SQL Server 服務以套用變更：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>移除設定

若要取消設定 `mssql-conf set` 所做的任何設定，請使用 `unset` 選項和設定的名稱來呼叫 **mssql-conf**。 這會清除設定，有效地使其返回預設值。

1. 下列範例會清除 **network.tcpport** 選項。

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. 重新啟動 SQL Server 服務。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>檢視目前設定

若要檢視任何已設定的設定，請執行下列命令以輸出 **mssql.conf** 檔案的內容：

```bash
sudo cat /var/opt/mssql/mssql.conf
```

請注意，此檔案中未顯示的任何設定都會使用其預設值。 下一節提供範例 **mssql.conf** 檔案。


## <a id="mssql-conf-format"></a> mssql.conf 格式

下列 **/var/opt/mssql/mssql.conf** 檔案提供適用於每個設定的範例。 您可以視需要使用此格式，手動對 **mssql.conf** 檔案進行變更。 如果您手動變更檔案，則必須先重新啟動 SQL Server 之後才能套用變更。 若要搭配 Docker 使用 **mssql.conf** 檔案，您必須讓 Docker [保存您的資料](sql-server-linux-configure-docker.md)。 首先，將完整的 **mssql.conf** 檔案新增至您的主機目錄，然後執行該容器。 [客戶意見反應](sql-server-linux-customer-feedback.md)中有一個這類範例。

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```ini
[EULA]
accepteula = Y

[coredump]
captureminiandfull = true
coredumptype = full

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```ini
[EULA]
accepteula = Y
accepteulaml = Y

[coredump]
captureminiandfull = true
coredumptype = full

[distributedtransaction]
servertcpport = 51999

[filelocation]
defaultbackupdir = /var/opt/mssql/data/
defaultdatadir = /var/opt/mssql/data/
defaultdumpdir = /var/opt/mssql/data/
defaultlogdir = /var/opt/mssql/data/

[hadr]
hadrenabled = 0

[language]
lcid = 1033

[memory]
memorylimitmb = 4096

[network]
forceencryption = 0
ipaddress = 10.192.0.0
kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
rpcport = 13500
tcpport = 1401
tlscert = /etc/ssl/certs/mssql.pem
tlsciphers = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA
tlskey = /etc/ssl/private/mssql.key
tlsprotocols = 1.2,1.1,1.0

[sqlagent]
databasemailprofile = default
errorlogfile = /var/opt/mssql/log/sqlagentlog.log
errorlogginglevel = 7

[telemetry]
customerfeedback = true
userrequestedlocalauditdirectory = /tmp/audit

[traceflag]
traceflag0 = 1204
traceflag1 = 2345
traceflag = 3456
```

::: moniker-end

## <a name="next-steps"></a>後續步驟

若要改用環境變數進行這其中的一些設定變更，請參閱[使用環境變數設定 SQL Server 設定](sql-server-linux-configure-environment-variables.md)。

如需其他管理工具和案例，請參閱[管理 Linux 上的 SQL Server](sql-server-linux-management-overview.md)。
