---
title: 在 Linux 上設定 SQL Server 設定 |Microsoft Docs
description: 本文說明如何在 Linux 上設定 SQL Server 2017 時，用以 mssql-conf 工具。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 06/22/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.openlocfilehash: 3a919f19b0b1aaef4702ac9d6e456cb9c5cf1357
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982470"
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>使用 mssql-conf 工具，設定在 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

**mssql conf**是 Red Hat Enterprise Linux、 SUSE Linux Enterprise Server 和 Ubuntu 安裝 SQL Server 2017 的組態指令碼。 您可以使用此公用程式來設定下列參數：

|||
|---|---|
| [代理程式](#agent) | 啟用 SQL Server Agent |
| [定序](#collation) | 在 Linux 上 SQL Server 設定新的定序。 |
| [客戶的意見反應](#customerfeedback) | 選擇 SQL Server 傳送意見反應給 Microsoft。 |
| [Database Mail 設定檔](#dbmail) | 在 Linux 上設定 SQL Server 的預設 database mail 設定檔 |
| [預設資料目錄](#datadir) | 變更新的 SQL Server 資料庫資料檔案 (.mdf) 的預設目錄。 |
| [預設記錄檔目錄](#datadir) | 預設會將目錄變更為新的 SQL Server 資料庫記錄檔 (.ldf) 檔案。 |
| [預設 master 資料庫檔案目錄](#masterdatabasedir) | 變更現有的 SQL 安裝上的 master 資料庫檔案的預設目錄。|
| [預設 master 資料庫檔案名稱](#masterdatabasename) | 變更 master 資料庫檔案的名稱。 |
| [預設傾印目錄](#dumpdir) | 變更新的記憶體傾印和其他疑難排解檔案的預設目錄。 |
| [預設錯誤記錄檔目錄](#errorlogdir) | 預設會將目錄變更為新的 SQL Server 錯誤記錄檔，預設的 Profiler 追蹤、 系統健全狀況工作階段 XE，Hekaton 工作階段 XE 檔案。 |
| [預設備份目錄](#backupdir) | 變更新的備份檔案的預設目錄。 |
| [傾印類型](#coredump) | 選擇要收集傾印記憶體傾印檔案類型。 |
| [高可用性](#hadr) | 啟用可用性群組。 |
| [本機稽核目錄](#localaudit) | 設定要加入本機稽核檔案的目錄。 |
| [地區設定](#lcid) | 設定 SQL Server 使用的地區設定。 |
| [記憶體限制](#memorylimit) | 設定 SQL Server 的記憶體限制。 |
| [TCP 連接埠](#tcpport) | 變更 SQL Server 接聽的連接埠。 |
| [TLS](#tls) | 設定傳輸層級安全性。 |
| [追蹤旗標](#traceflags) | 設定服務將使用追蹤旗標。 |

> [!TIP]
> 其中某些設定也可以使用環境變數設定。 如需詳細資訊，請參閱 <<c0> [ 環境變數設定 SQL Server 設定](sql-server-linux-configure-environment-variables.md)。

## <a name="usage-tips"></a>使用方式的秘訣

* Always On 可用性群組和共用的磁碟叢集，一律在每個節點上進行相同的組態變更。

* 共用的磁碟叢集案例中，請勿嘗試重新啟動**mssql server**服務以套用變更。 SQL Server 正在執行之應用程式。 相反地，使資源離線，然後再重新連線。

* 這些範例中執行 mssql-conf 所指定的完整路徑： **/opt/mssql/bin/mssql-conf**。 如果您選擇改為瀏覽至該路徑，則在目前目錄的內容中執行 mssql conf: **。 / mssql conf**。

## <a id="agent"></a> 啟用 SQL Server Agent

**Sqlagent.enabled**設定可讓[SQL Server Agent](sql-server-linux-run-sql-server-agent-job.md)。 根據預設，SQL Server 代理程式已停用。 如果**sqlagent.enabled**不存在於 mssql.conf 設定檔中，則 SQL Server 在內部會假設 SQL Server 代理程式已停用。

若要變更此設定，請使用下列步驟：

1. 啟用 SQL Server 代理程式：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="collation"></a> 變更 SQL Server 定序

**組定序**選項會變更定序值到任何支援的定序。

1. 第一個[備份任何使用者資料庫](sql-server-linux-backup-and-restore-database.md)您伺服器上。

1. 然後使用[sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)預存程序來卸離的使用者資料庫。

1. 執行**組定序**選項，然後遵循提示：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. Mssql conf 公用程式會嘗試將變更為指定的定序值並重新啟動服務。 如果有任何錯誤，它會回復定序為先前的值。

1. 還原使用者資料庫備份。

如需支援的定序的清單，執行[sys.fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)函式： `SELECT Name from sys.fn_helpcollations()`。

## <a id="customerfeedback"></a> 設定客戶的意見反應

**Telemetry.customerfeedback**是否 SQL Server 會傳送給 Microsoft 的意見反應或未設定變更。 根據預設，這個值會設為 **，則為 true**適用於所有版本。 若要變更的值，執行下列命令：

> [!IMPORTANT]
> 您可以將關閉的客戶意見反應免費的 SQL Server、 Express 和 Developer 版本。

1. 以 root 身分執行 mssql conf 指令碼**設定**命令**telemetry.customerfeedback**。 下列範例指定關閉的客戶意見反應**false**。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

如需詳細資訊，請參閱 <<c0> [ 在 Linux 上的 SQL Server 的客戶意見反應](sql-server-linux-customer-feedback.md)並[SQL Server 隱私權聲明](http://go.microsoft.com/fwlink/?LinkID=868444)。

## <a id="datadir"></a> 變更預設的資料或記錄檔目錄位置

**Filelocation.defaultdatadir**並**filelocation.defaultlogdir**設定變更會建立新的資料庫和記錄檔的位置。 根據預設，此位置會是 /var/opt/mssql/data。 若要變更這些設定，請使用下列步驟：

1. 建立新資料庫的目標目錄資料和記錄檔。 下列範例會建立新 **/tmp/資料**目錄：

   ```bash
   sudo mkdir /tmp/data
   ```

1. 變更擁有者和群組的目錄**mssql**使用者：

   ```bash
   sudo chown mssql /tmp/data
   sudo chgrp mssql /tmp/data
   ```

1. 若要變更預設資料目錄，以使用 mssql conf**設定**命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdatadir /tmp/data
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

1. 現在建立的新資料庫的所有資料庫檔案會都儲存在這個新的位置。 如果您想要變更新資料庫的記錄 (.ldf) 檔案的位置，您可以使用下列的 「 集 」 命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. 此命令也會假設，/tmp/記錄檔目錄就會存在，而且它是在使用者與群組下**mssql**。


## <a id="masterdatabasedir"></a> 變更預設 master 資料庫檔案目錄位置

**Filelocation.masterdatafile**並**filelocation.masterlogfile**設定變更 SQL Server 引擎從中尋找 master 資料庫檔案的位置。 根據預設，此位置會是 /var/opt/mssql/data。 

若要變更這些設定，請使用下列步驟：

1. 建立新的錯誤記錄檔的目標目錄。 下列範例會建立新 **/tmp/masterdatabasedir**目錄：

   ```bash
   sudo mkdir /tmp/masterdatabasedir
   ```

1. 變更擁有者和群組的目錄**mssql**使用者：

   ```bash
   sudo chown mssql /tmp/masterdatabasedir
   sudo chgrp mssql /tmp/masterdatabasedir
   ```

1. 若要變更與 master 的資料和記錄檔的預設 master 資料庫目錄使用 mssql conf**設定**命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /tmp/masterdatabasedir/master.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterlogfile /tmp/masterdatabasedir/mastlog.ldf
   ```

1. 停止 SQL Server 服務：

   ```bash
   sudo systemctl stop mssql-server
   ```

1. 將 master.mdf 和 masterlog.ldf 移： 

   ```bash
   sudo mv /var/opt/mssql/data/master.mdf /tmp/masterdatabasedir/master.mdf 
   sudo mv /var/opt/mssql/data/mastlog.ldf /tmp/masterdatabasedir/mastlog.ldf
   ```

1. 啟動 SQL Server 服務：

   ```bash
   sudo systemctl start mssql-server
   ```
   
> [!NOTE]
> 如果 SQL Server 指定的目錄中找不到 master.mdf 和 mastlog.ldf 檔、 樣板化系統資料庫的複本將會自動建立在指定的目錄中，而且 SQL Server 將成功啟動。 不過，中繼資料，例如使用者資料庫、 伺服器登入、 伺服器憑證、 加密金鑰、 SQL agent 作業或舊的 SA 登入密碼不會更新新的 master 資料庫中。 您必須停止 SQL Server 並將您的舊 master.mdf 和 mastlog.ldf 移至新的指定位置並啟動 SQL Server 以繼續使用現有的中繼資料。 


## <a id="masterdatabasename"></a> 變更主要資料庫檔案的名稱。

**Filelocation.masterdatafile**並**filelocation.masterlogfile**設定變更 SQL Server 引擎從中尋找 master 資料庫檔案的位置。 根據預設，此位置會是 /var/opt/mssql/data。 若要變更這些設定，請使用下列步驟：

1. 停止 SQL Server 服務：

   ```bash
   sudo systemctl stop mssql-server
   ```

1. 若要變更預期的 master 資料庫的名稱與主要資料和記錄檔使用 mssql conf**設定**命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.masterdatafile /var/opt/mssql/data/masternew.mdf
   sudo /opt/mssql/bin/mssql-conf set filelocation.mastlogfile /var/opt/mssql/data /mastlognew.ldf
   ```

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

**Filelocation.defaultdumpdir**設定變更其中的記憶體和 SQL 傾印會產生損毀時的預設位置。 根據預設，這些檔案產生 /var/opt/mssql/log 中。

若要設定這個新的位置，使用下列命令：

1. 建立新的傾印檔案的目標目錄。 下列範例會建立新 **/tmp/傾印**目錄：

   ```bash
   sudo mkdir /tmp/dump
   ```

1. 變更擁有者和群組的目錄**mssql**使用者：

   ```bash
   sudo chown mssql /tmp/dump
   sudo chgrp mssql /tmp/dump
   ```

1. 若要變更預設資料目錄，以使用 mssql conf**設定**命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultdumpdir /tmp/dump
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="errorlogdir"></a> 變更預設錯誤記錄檔目錄位置

**Filelocation.errorlogfile**設定變更建立新的錯誤記錄檔、 預設的分析工具追蹤、 系統健康工作階段 XE 和 Hekaton XE 的工作階段檔案的位置。 根據預設，此位置會是 /var/opt/mssql/log。 其中設定 SQL 錯誤記錄檔的目錄會成為其他記錄檔的預設記錄目錄。

若要變更這些設定：

1. 建立新的錯誤記錄檔的目標目錄。 下列範例會建立新 **/tmp/logs**目錄：

   ```bash
   sudo mkdir /tmp/logs
   ```

1. 變更擁有者和群組的目錄**mssql**使用者：

   ```bash
   sudo chown mssql /tmp/logs
   sudo chgrp mssql /tmp/logs
   ```

1. 若要變更預設的錯誤記錄檔檔案名稱，與使用 mssql conf**設定**命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.errorlogfile /tmp/logs/errorlog
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```


## <a id="backupdir"></a> 變更預設備份目錄位置

**Filelocation.defaultbackupdir**設定變更備份檔案產生位置的預設位置。 根據預設，這些檔案產生 /var/opt/mssql/data 中。

若要設定這個新的位置，使用下列命令：

1. 建立新的備份檔案的目標目錄。 下列範例會建立新 **/tmp/備份**目錄：

   ```bash
   sudo mkdir /tmp/backup
   ```

1. 變更擁有者和群組的目錄**mssql**使用者：

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. 使用 mssql conf 變更使用 「 設定 」 命令的預設備份目錄：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="coredump"></a> 指定核心傾印設定

如果其中一個 SQL Server 處理序中發生例外狀況，SQL Server 就會建立記憶體傾印。

有兩個選項供控制類型的記憶體傾印，會收集 SQL Server: **coredump.coredumptype**並**coredump.captureminiandfull**。 這些與相關的兩個階段的核心傾印擷取。 

第一個階段擷取受到**coredump.coredumptype** ，地區設定會決定產生期間發生例外狀況的傾印檔案的類型。 當啟用第二個階段**coredump.captureminiandfull**設定。 如果**coredump.captureminiandfull**已設為 true，傾印所指定的檔案**coredump.coredumptype**產生，而且也會產生第二個的小型傾印。 設定**coredump.captureminiandfull**為 false 會停用第二個擷取的嘗試。

1. 決定是否要擷取與迷你與完整傾印**coredump.captureminiandfull**設定。

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    預設值： **false**

1. 指定的傾印檔案類型**coredump.coredumptype**設定。

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    預設值： **miniplus**

    下表列出可能**coredump.coredumptype**值。

    | 類型 | 描述 |
    |-----|-----|
    | **迷你** | 迷你是最小的傾印檔案類型。 它會使用 Linux 系統資訊來判斷執行緒和處理序中的模組。 傾印包含只有主機環境執行緒堆疊和模組。 它不包含間接記憶體參考或全域變數。 |
    | **迷你加強** | Mini、 miniPlus 大致，但包含額外的記憶體。 它了解 SQLPAL 和主機環境中，加入傾印中的下列記憶體區域的內部項目：</br></br> -各種全域變數</br> -所有的記憶體，大於 64 TB</br> -所有名為區域中找到 **/proc/$ pid/對應**</br> -間接與執行緒堆疊的記憶體</br> 執行緒的資訊</br> -關聯 Teb 的和 Peb 的</br> 模組資訊</br> VMM 和 VAD 樹狀結構 |
    | **filtered** | 減法為基礎的篩選會使用設計程序中的所有記憶體其中都包含除非特別排除。 設計了解 SQLPAL 和主機環境中，從傾印中排除特定區域的內部資訊。
    | **full** | 完整包含所有區域的完整程序傾印位於 **/proc/$ pid/對應**。 這不會受到**coredump.captureminiandfull**設定。 |

## <a id="dbmail"></a> 在 Linux 上設定 SQL Server 的預設 database mail 設定檔

**Sqlpagent.databasemailprofile**可讓您設定電子郵件警示的預設資料庫郵件設定檔。

```bash
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a> 高可用性

**Hadr.hadrenabled**選項可讓您的 SQL Server 執行個體上的可用性群組。 下列命令會啟用可用性群組，藉由設定**hadr.hadrenabled**為 1。 您必須重新啟動 SQL Server 設定才會生效。

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

這搭配可用性群組的資訊，請參閱下列兩個主題。

- [設定 Always On 可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)
- [Linux 上的 SQL Server 設定讀取級別可用性群組](sql-server-linux-availability-group-configure-rs.md)

## <a id="localaudit"></a> 設定本機稽核目錄

**Telemetry.userrequestedlocalauditdirectory**設定會啟用本機稽核，並建立可讓您設定本機稽核記錄檔的所在目錄。

1. 建立新的本機稽核記錄檔的目標目錄。 下列範例會建立新 **/tmp/稽核**目錄：

   ```bash
   sudo mkdir /tmp/audit
   ```

1. 變更擁有者和群組的目錄**mssql**使用者：

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. 以 root 身分執行 mssql conf 指令碼**設定**命令**telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

如需詳細資訊，請參閱 <<c0> [ 在 Linux 上的 SQL Server 的客戶意見反應](sql-server-linux-customer-feedback.md)。

## <a id="lcid"></a> 變更 SQL Server 的地區設定

**Language.lcid**將變更的 SQL Server 的地區設定設定為任何支援的語言識別碼 (LCID)。 

1. 下列範例會變更為法文的地區設定 (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. 重新啟動 SQL Server 服務，才能套用所做的變更：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a> 設定記憶體限制

**Memory.memorylimitmb**到 SQL Server 設定控制實體可用的記憶體數量 （以 mb 為單位）。 預設為實體記憶體的 80%。

1. 以 root 身分執行 mssql conf 指令碼**設定**命令**memory.memorylimitmb**。 下列範例會變成 3.25 gb (3328 MB) 的 SQL Server 中可用的記憶體。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. 重新啟動 SQL Server 服務，才能套用所做的變更：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="tcpport"></a> 變更 TCP 連接埠

**Network.tcpport**設定變更 SQL Server 接聽的連接的 TCP 連接埠。 根據預設，此連接埠是設定為 1433年。 若要變更連接埠，請執行下列命令：

1. 以"network.tcpport 」 的 「 設定 」 命令以 root 身分執行 mssql conf 指令碼：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

1. 時立即連線到 SQL Server，您必須指定以逗號 （，） 的自訂連接埠之後的主機名稱或 IP 位址。 例如，若要使用 SQLCMD 連接，您會使用下列命令：

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a> 指定 TLS 設定

下列選項會設定 TLS 在 Linux 上執行的 SQL Server 執行個體。

|選項 |描述 |
|--- |--- |
|**network.forceencryption** |如果是 1，然後[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]強制加密的所有連線。 根據預設，此選項會是 0。 |
|**network.tlscert** |憑證的絕對路徑檔案[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用於 TLS。 範例：`/etc/ssl/certs/mssql.pem`憑證檔案必須可由 mssql 帳戶存取。 Microsoft 建議您限制對檔案使用存取`chown mssql:mssql <file>; chmod 400 <file>`。 |
|**network.tlskey** |檔案的私密金鑰絕對路徑[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用於 TLS。 範例：`/etc/ssl/private/mssql.key`憑證檔案必須可由 mssql 帳戶存取。 Microsoft 建議您限制對檔案使用存取`chown mssql:mssql <file>; chmod 400 <file>`。 |
|**network.tlsprotocols** |以逗號分隔的清單，哪一個 TLS 的 SQL Server 所允許的通訊協定。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 一律會嘗試交涉的最強的允許通訊協定。 如果用戶端不支援任何允許的通訊協定，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]會拒絕連線嘗試。  所有支援的通訊協定相容性，都被允許預設 （1.2、 1.1 和 1.0）。  如果您的用戶端支援 TLS 1.2，Microsoft 建議讓只 TLS 1.2。 |
|**network.tlsciphers** |指定所允許的加密[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]tls。 此字串必須格式化每[OpenSSL 的加密清單格式](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html)。 一般情況下，您應該不需要變更這個選項。 <br /> 根據預設，可使用下列編碼器： <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Kerberos keytab 檔案路徑 |

如需使用 TLS 設定的範例，請參閱 <<c0> [ 加密的 Linux 上的 SQL Server 連接](sql-server-linux-encrypted-connections.md)。

## <a id="traceflags"></a> 啟用/停用追蹤旗標

這**traceflag**選項啟用或停用追蹤旗標的 SQL Server 服務啟動。 啟用/停用追蹤旗標，請使用下列命令：

1. 啟用追蹤旗標，使用下列命令。 例如，針對追蹤旗標 1234:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. 您可以分別指定它們，以啟用多個追蹤旗標：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. 類似的方式，您可以停用一或多個已啟用的追蹤旗標指定它們，並新增**關閉**參數：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. 重新啟動 SQL Server 服務，才能套用所做的變更：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>移除設定

若要取消設定使用中變更任何設定`mssql-conf set`，呼叫**mssql conf**與`unset`選項和設定的名稱。 這會清除設定，有效地將它傳回為其預設值。

1. 下列範例會清除**network.tcpport**選項。

   ```bash
   sudo /opt/mssql/bin/mssql-conf unset network.tcpport
   ```

1. 重新啟動 SQL Server 服務。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="view-current-settings"></a>檢視目前的設定

若要檢視任何設定的設定，請執行下列命令，以輸出的內容**mssql.conf**檔案：

```bash
sudo cat /var/opt/mssql/mssql.conf
```

請注意，此檔案中未顯示任何設定會使用其預設值。 下一節中提供的範例**mssql.conf**檔案。

## <a name="mssqlconf-format"></a>mssql.conf format

下列 **/var/opt/mssql/mssql.conf**檔案提供每個設定的範例。 您可以使用這個格式來手動變更**mssql.conf**檔案所需。 如果您以手動方式變更的檔案，您必須重新啟動 SQL Server 所做的變更會套用。 若要使用**mssql.conf**檔案使用 Docker，您必須具有 Docker[保存您的資料](sql-server-linux-configure-docker.md)。 第一次新增 完整**mssql.conf**檔案到您的主應用程式目錄，然後執行容器。 在這個範例[客戶的意見反應](sql-server-linux-customer-feedback.md)。

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

## <a name="next-steps"></a>後續的步驟

若要改為使用環境變數來進行一些組態變更，請參閱[環境變數設定 SQL Server 設定](sql-server-linux-configure-environment-variables.md)。

如需其他管理工具和案例，請參閱[管理 Linux 上的 SQL Server](sql-server-linux-management-overview.md)。
