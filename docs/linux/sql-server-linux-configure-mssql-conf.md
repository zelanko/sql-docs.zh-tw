---
title: 在 Linux 上的 SQL Server 設定 |Microsoft 文件
description: 本文說明如何在 Linux 上設定 SQL Server 2017 設定使用 mssql conf 工具。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 06798dff-65c7-43e0-9ab3-ffb23374b322
ms.workload: On Demand
ms.openlocfilehash: 7ff775907a9f34d635c7ecf23965ce2ef96179f6
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="configure-sql-server-on-linux-with-the-mssql-conf-tool"></a>設定 SQL Server on Linux mssql conf 工具

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

**mssql conf**是隨 SQL Server 2017 Red Hat Enterprise Linux、 SUSE Linux Enterprise Server 和 Ubuntu 的組態指令碼。 您可以使用此公用程式來設定下列參數：

|||
|---|---|
| [代理程式](#agent) | 啟用 SQL Server 代理程式 |
| [定序](#collation) | 在 Linux 中設定 SQL Server 的新定序。 |
| [客戶的意見反應](#customerfeedback) | 選擇 SQL Server 傳送意見給 Microsoft。 |
| [Database Mail 設定檔](#dbmail) | 設定 SQL Server 的預設資料庫郵件設定檔，在 Linux 上 |
| [預設資料目錄](#datadir) | 變更新的 SQL Server 資料庫資料檔案 (.mdf) 的預設目錄。 |
| [預設記錄檔目錄](#datadir) | 變更新的 SQL Server 資料庫記錄檔 (.ldf) 檔案的預設目錄。 |
| [預設 master 資料庫檔案目錄](#masterdatabasedir) | 變更現有的 SQL 安裝上的主要資料庫檔案的預設目錄。|
| [預設 master 資料庫檔案名稱](#masterdatabasename) | 變更 master 資料庫檔案名稱。 |
| [預設傾印目錄](#dumpdir) | 變更新的記憶體傾印和疑難排解的其他檔案的預設目錄。 |
| [預設記錄檔目錄時發生錯誤](#errorlogdir) | 變更新的 SQL Server 錯誤記錄檔、 預設的程式碼剖析工具追蹤、 系統健康工作階段 XE 和 Hekaton 工作階段 XE 檔的預設目錄。 |
| [預設備份目錄](#backupdir) | 變更新的備份檔案的預設目錄。 |
| [傾印類型](#coredump) | 選擇要收集傾印記憶體傾印檔案類型。 |
| [高可用性](#hadr) | 啟用可用性群組。 |
| [稽核的本機目錄](#localaudit) | 設定要加入本機的稽核檔案的目錄。 |
| [地區設定](#lcid) | 設定 SQL Server 使用的地區設定。 |
| [記憶體限制](#memorylimit) | 設定 SQL Server 的記憶體限制。 |
| [TCP 連接埠](#tcpport) | 變更 SQL Server 接聽的連接的連接埠。 |
| [TLS](#tls) | 設定傳輸層級安全性。 |
| [Traceflag](#traceflags) | 設定服務所要使用的 traceflag。 |

> [!TIP]
> 其中某些設定也可以使用環境變數設定。 如需詳細資訊，請參閱[與環境變數設定 SQL Server 設定](sql-server-linux-configure-environment-variables.md)。

## <a name="usage-tips"></a>使用提示

* Alwayson 可用性群組和共用的磁碟叢集，請務必相同的組態變更每個節點上。

* 共用的磁碟叢集案例中，請勿嘗試重新啟動**mssql 伺服器**服務以套用變更。 SQL Server 正在執行做為應用程式。 相反地，使資源離線再恢復上線。

* 這些範例執行 mssql-conf 所指定的完整路徑： **/opt/mssql/bin/mssql-conf**。 如果您選擇改為瀏覽至該路徑，則在目前目錄的內容中執行 mssql conf: **。 / mssql conf**。

## <a id="agent"></a> 啟用 SQL Server 代理程式

**Sqlagent.enabled**設定可讓[SQL Server Agent](sql-server-linux-run-sql-server-agent-job.md)。 根據預設，SQL Server 代理程式已停用。 如果**sqlagent.enabled**不存在於 mssql.conf 設定檔，則 SQL Server 在內部會假設已啟用 SQL Server 代理程式。

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

**組定序**選項變更為任何支援的定序的定序值。

1. 第一個[備份任何使用者資料庫](sql-server-linux-backup-and-restore-database.md)您伺服器上。

1. 然後使用[sp_detach_db](../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)預存程序來卸離的使用者資料庫。

1. 執行**組定序**選項，然後遵循提示：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-collation
   ```

1. Mssql conf 公用程式會嘗試將指定的定序值變更，然後重新啟動服務。 如果有任何錯誤，便會復原定序為先前的值。

1. 還原使用者資料庫備份。

如需支援的定序的清單，請執行[sys.fn_helpcollations](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)函式： `SELECT Name from sys.fn_helpcollations()`。

## <a id="customerfeedback"></a> 設定客戶意見反應

**Telemetry.customerfeedback**是否 SQL Server 會傳送給 Microsoft 的意見反應或未設定變更。 根據預設，這個值設為**true**。 若要變更的值，執行下列命令：

1. 以具有 root 身分執行 mssql conf 指令碼**設定**命令**telemetry.customerfeedback**。 下列範例藉由指定關閉客戶的意見反應**false**。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

如需詳細資訊，請參閱[客戶的意見反應的 SQL Server on Linux](sql-server-linux-customer-feedback.md)。

## <a id="datadir"></a> 變更預設資料或記錄檔的目錄位置

**Filelocation.defaultdatadir**和**filelocation.defaultlogdir**設定變更會建立新的資料庫和記錄檔的位置。 根據預設，這個位置是 /var/opt/mssql/data。 若要變更這些設定，請使用下列步驟：

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

1. 現在建立的新資料庫的所有資料庫檔案會都儲存在這個新的位置。 如果您想要變更新資料庫的記錄 (.ldf) 檔案的位置，您可以使用下列 「 組 」 命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultlogdir /tmp/log
   ```

1. 此命令也會假設確認/tmp/記錄檔目錄就會存在，且其位於下的使用者和群組**mssql**。


## <a id="masterdatabasedir"></a> 變更預設的 master 資料庫檔案目錄位置

**Filelocation.masterdatafile**和**filelocation.masterlogfile**設定變更 SQL Server 引擎從中尋找 master 資料庫檔案的位置。 根據預設，這個位置是 /var/opt/mssql/data。 

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

1. 若要變更與主要資料和記錄檔的預設 master 資料庫目錄使用 mssql conf**設定**命令：

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
> 如果 SQL Server 指定的目錄中找不到 master.mdf 和 mastlog.ldf 檔、 樣板化的系統資料庫的複本將會自動建立在指定的目錄中，而且 SQL Server 就已成功啟動。 不過，中繼資料，例如使用者資料庫、 伺服器登入、 伺服器憑證、 加密金鑰、 SQL agent 作業或舊的 SA 登入密碼不會更新新的 master 資料庫中。 您必須停止 SQL Server 並將您的舊 master.mdf 和 mastlog.ldf 移至新指定的位置，啟動 SQL Server 以繼續使用現有的中繼資料。 


## <a id="masterdatabasename"></a> 變更 master 資料庫檔案的名稱。

**Filelocation.masterdatafile**和**filelocation.masterlogfile**設定變更 SQL Server 引擎從中尋找 master 資料庫檔案的位置。 根據預設，這個位置是 /var/opt/mssql/data。 若要變更這些設定，請使用下列步驟：

1. 停止 SQL Server 服務：

   ```bash
   sudo systemctl stop mssql-server
   ```

1. 將 master 資料與記錄檔與預期的主要資料庫名稱變更為使用 mssql conf**設定**命令：

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

**Filelocation.defaultdumpdir**設定變更其中的記憶體和 SQL 傾印會產生損毀時的預設位置。 根據預設，這些檔案會產生 /var/opt/mssql/log。

若要設定這個新的位置，請使用下列命令：

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

## <a id="errorlogdir"></a> 變更預設錯誤記錄檔檔案目錄位置

**Filelocation.errorlogfile**設定變更建立新的錯誤記錄檔、 預設的程式碼剖析工具追蹤，系統健康工作階段 」 XE 和 Hekaton XE 工作階段檔案的位置。 根據預設，這個位置是 /var/opt/mssql/log。 設定 SQL 錯誤記錄檔所在的目錄會成為其他記錄檔的預設記錄目錄。

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

**Filelocation.defaultbackupdir**設定變更備份檔案產生位置的預設位置。 根據預設，這些檔案會產生 /var/opt/mssql/data。

若要設定這個新的位置，請使用下列命令：

1. 建立新的備份檔案的目標目錄。 下列範例會建立新 **/tmp/備份**目錄：

   ```bash
   sudo mkdir /tmp/backup
   ```

1. 變更擁有者和群組的目錄**mssql**使用者：

   ```bash
   sudo chown mssql /tmp/backup
   sudo chgrp mssql /tmp/backup
   ```

1. 若要變更與"set"命令的預設備份目錄使用 mssql conf:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set filelocation.defaultbackupdir /tmp/backup
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="coredump"></a> 指定核心傾印設定

其中一個 SQL Server 處理序中發生的例外狀況，SQL Server 建立的記憶體傾印。

有兩個選項的控制類型的記憶體傾印，會收集 SQL Server: **coredump.coredumptype**和**coredump.captureminiandfull**。 這些與核心傾印擷取的兩個階段。 

第一個階段擷取由**coredump.coredumptype**設定，可判斷例外狀況期間所產生的傾印檔案的類型。 當啟用第二個階段**coredump.captureminiandfull**設定。 如果**coredump.captureminiandfull**設為 true，傾印檔案所指定**coredump.coredumptype**產生，也會產生第二個小型傾印。 設定**coredump.captureminiandfull**設為 false 會停用第二個擷取的嘗試。

1. 決定是否要擷取與迷你和完整傾印**coredump.captureminiandfull**設定。

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.captureminiandfull <true or false>
    ```

    預設值： **false**

1. 指定的傾印檔案使用類型**coredump.coredumptype**設定。

    ```bash
    sudo /opt/mssql/bin/mssql-conf set coredump.coredumptype <dump_type>
    ```

    預設值： **miniplus**

    下表列出可能**coredump.coredumptype**值。

    | 型別 | Description |
    |-----|-----|
    | **迷你** | 迷你是最小的傾印檔案類型。 它使用 Linux 系統資訊來決定執行緒和處理序中的模組。 傾印包含只有主機環境執行緒堆疊和模組。 它不包含間接記憶體參考或全域變數。 |
    | **miniplus** | MiniPlus 迷你，類似，但它包含額外的記憶體。 其了解 SQLPAL 和主機環境中，傾印中加入下列的記憶體區域的內部資訊：</br></br> -各種全域變數</br> -所有以上 64 TB 的記憶體</br> -All 名為區域中找到 **/proc/$ pid/對應**</br> 間接記憶體與執行緒堆疊</br> 執行緒的資訊</br> 關聯 Teb 的和 Peb 的</br> 模組資訊</br> VMM 和 VAD 樹狀結構 |
    | **filtered** | 減法為基礎的篩選會使用設計程序中的所有記憶體其中都包含除非明確地排除。 設計了解 SQLPAL 和主機環境中，從傾印中排除特定區域的內部資訊。
    | **full** | 完整的完整程序傾印包含所有區域位於 **/proc/$ pid/對應**。 這不由控制**coredump.captureminiandfull**設定。 |

## <a id="dbmail"></a> 設定 SQL Server 的預設資料庫郵件設定檔，在 Linux 上

**Sqlpagent.databasemailprofile**可讓您設定電子郵件警示的預設 DB 郵件設定檔。

```bash
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile <profile_name>
```
## <a id="hadr"></a> 高可用性

**Hadr.hadrenabled**選項可讓您的 SQL Server 執行個體的可用性群組。 下列命令會啟用可用性群組設定**hadr.hadrenabled**設為 1。 您必須重新啟動 SQL Server 的設定才會生效。

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

這與可用性群組的使用方式的資訊，請參閱下列兩個主題。

- [設定 Alwayson 可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)
- [設定向外延展讀取可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-rs.md)

## <a id="localaudit"></a> 設定本機稽核的目錄

**Telemetry.userrequestedlocalauditdirectory**設定可讓本機稽核，並建立可讓您設定本機的稽核記錄，其中的目錄。

1. 建立新的本機稽核記錄檔的目標目錄。 下列範例會建立新 **/tmp/稽核**目錄：

   ```bash
   sudo mkdir /tmp/audit
   ```

1. 變更擁有者和群組的目錄**mssql**使用者：

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. 以具有 root 身分執行 mssql conf 指令碼**設定**命令**telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

如需詳細資訊，請參閱[客戶的意見反應的 SQL Server on Linux](sql-server-linux-customer-feedback.md)。

## <a id="lcid"></a> 變更 SQL Server 的地區設定

**Language.lcid**設定變更為任何支援的語言識別碼 (LCID) 的 SQL 伺服器地區設定。 

1. 下列範例會變更為法文的地區設定 (1036):

   ```bash
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
   ```

1. 重新啟動才能套用變更的 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="memorylimit"></a> 設定記憶體限制

**Memory.memorylimitmb**到 SQL Server 設定控制實體可用的記憶體數量 （以 mb 為單位）。 預設為 80%的實體記憶體。

1. 以具有 root 身分執行 mssql conf 指令碼**設定**命令**memory.memorylimitmb**。 下列範例會變成 3.25 gb (3328 MB) 的 SQL Server 中可用的記憶體。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
   ```

1. 重新啟動才能套用變更的 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a id="tcpport"></a> 變更 TCP 連接埠

**Network.tcpport**設定變更 SQL Server 接聽的連接的 TCP 連接埠。 根據預設，此連接埠設定為 1433年。 若要變更連接埠，請執行下列命令：

1. 以"network.tcpport 」 的 「 設定 」 命令以 root 身分執行 mssql conf 指令碼：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.tcpport <new_tcp_port>
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

1. 當連接到 SQL Server 現在，您必須指定以逗號 （，） 自訂連接埠後的主機名稱或 IP 位址。 例如，若要使用 SQLCMD 連接，您會使用下列命令：

   ```bash
   sqlcmd -S localhost,<new_tcp_port> -U test -P test
   ```

## <a id="tls"></a> 指定 TLS 設定

下列選項會設定 TLS 在 Linux 上執行的 SQL Server 執行個體。

|選項 |Description |
|--- |--- |
|**network.forceencryption** |如果是 1，然後[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]會強制所有連線必須加密。 根據預設，此選項為 0。 |
|**network.tlscert** |憑證的絕對路徑檔[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用於 TLS。 範例：`/etc/ssl/certs/mssql.pem`憑證檔案必須是可由 mssql 帳戶存取。 Microsoft 建議限制對檔案使用存取`chown mssql:mssql <file>; chmod 400 <file>`。 |
|**network.tlskey** |私用金鑰的絕對路徑檔[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用於 TLS。 範例：`/etc/ssl/private/mssql.key`憑證檔案必須是可由 mssql 帳戶存取。 Microsoft 建議限制對檔案使用存取`chown mssql:mssql <file>; chmod 400 <file>`。 |
|**network.tlsprotocols** |以逗號分隔清單的哪一個 TLS 通訊協定所允許 SQL Server。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 一律會嘗試交涉的最強的允許通訊協定。 如果用戶端不支援任何允許的通訊協定，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]會拒絕連線嘗試。  為了相容性，允許進行所有支援的通訊協定的預設 （1.2、 1.1、 1.0）。  如果您的用戶端支援 TLS 1.2，Microsoft 建議允許只 TLS 1.2。 |
|**network.tlsciphers** |指定所允許的密碼[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]tls。 這個字串必須格式化每個[OpenSSL 的加密清單格式](https://www.openssl.org/docs/man1.0.2/apps/ciphers.html)。 一般情況下，您應該不需要變更這個選項。 <br /> 根據預設，可使用下列密碼： <br /> `ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA:ECDHE-RSA-AES128-SHA:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA` |
| **network.kerberoskeytabfile** |Kerberos keytab 檔案路徑 |

如需使用 TLS 設定的範例，請參閱[加密的 SQL Server on Linux 連接](sql-server-linux-encrypted-connections.md)。

## <a id="traceflags"></a> 啟用/停用 traceflag

這**traceflag**選項啟用或停用 traceflag 針對 SQL Server 服務啟動。 啟用/停用 traceflag 會使用下列命令：

1. 啟用 traceflag，使用下列命令。 例如，針對指定了 Traceflag 1234:

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 on
   ```

1. 您可以啟用多個 traceflag 它們分別指定：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 2345 3456 on
   ```

1. 類似的方式，您可以停用一或多個已啟用的 traceflag 指定它們，並加入**關閉**參數：

   ```bash
   sudo /opt/mssql/bin/mssql-conf traceflag 1234 2345 3456 off
   ```

1. 重新啟動才能套用變更的 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="remove-a-setting"></a>移除設定

未設定任何設定進行與`mssql-conf set`，呼叫**mssql conf**與`unset`選項和設定的名稱。 這會清除的設定值，有效地將它傳回為其預設值。

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

請注意，此檔案中未顯示任何設定都使用其預設值。 下節將提供範例**mssql.conf**檔案。

## <a name="mssqlconf-format"></a>mssql.conf format

下列 **/var/opt/mssql/mssql.conf**每個設定檔提供的範例。 您可以使用此格式，以手動方式進行變更以**mssql.conf**檔案所需。 如果您不要手動變更的檔案，必須套用變更之前，先重新啟動 SQL Server。 若要使用**mssql.conf**檔案使用 Docker 時，您必須擁有 Docker[保存您的資料](sql-server-linux-configure-docker.md)。 第一次加入完整**mssql.conf**檔至主應用程式目錄，然後再執行容器。 沒有在這個範例[客戶的意見反應](sql-server-linux-customer-feedback.md)。

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

若要改為使用環境變數來進行一些組態變更，請參閱[與環境變數設定 SQL Server 設定](sql-server-linux-configure-environment-variables.md)。

其他管理工具和案例，請參閱[管理 SQL Server on Linux](sql-server-linux-management-overview.md)。
