## <a name="prerequisites"></a>必要條件

建立可用性群組之前，您需要：

- 設定您的環境，讓所有將要裝載可用性複本的伺服器能夠通訊
- 安裝 SQL Server

>[!NOTE]
>在 Linux 上，您必須先建立可用性群組，再將其新增為叢集資源，以供叢集管理。 本文件提供建立可用性群組的範例。 如需建立叢集並將可用性群組新增為叢集資源的發行套件特定指示，請參閱[後續步驟](#next-steps)底下的連結。

1. **更新每一部主機的電腦名稱**

   每個 SQL Server 名稱必須是：
   
   - 15 個字元以下
   - 在網路內是唯一的
   
   若要設定電腦名稱，請編輯 `/etc/hostname`。 下列指令碼可讓您使用 `vi` 編輯 `/etc/hostname`。

   ```bash
   sudo vi /etc/hostname
   ```

1. **設定 hosts 檔案**

>[!NOTE]
>如果在 DNS 伺服器中註冊了主機名稱及其 IP，就無需執行下列步驟。 驗證將要成為可用性群組組態一部分的所有節點都可以彼此通訊 (Ping 主機名稱應該會回覆對應的 IP 位址)。 此外，請確定 /etc/hosts 檔案不包含對應 localhost IP 位址 127.0.0.1 與節點主機名稱的記錄。


   每一部伺服器上的 hosts 檔案包含將參與可用性群組之所有伺服器的 IP 位址和名稱。 

   下列命令會傳回目前伺服器的 IP 位址：

   ```bash
   sudo ip addr show
   ```

   更新 `/etc/hosts`。 下列指令碼可讓您使用 `vi` 編輯 `/etc/hosts`。

   ```bash
   sudo vi /etc/hosts
   ```

   下列範例顯示 **node1** 上的 `/etc/hosts`，以及 **node1**、**node2** 和 **node3** 上的新增項目。 在本文件中，**node1** 指的是裝載主要複本的伺服器。 **node2** 和 **node3** 指的是裝載次要複本的伺服器。


   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.12 node1
   10.128.16.77 node2
   10.128.15.33 node3
   ```

### <a name="install-sql-server"></a>安裝 SQL Server

安裝 SQL Server。 下列連結指向各種發行套件的 SQL Server 安裝指示。 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)

- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)

- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-always-on-availability-groups-and-restart-sqlserver"></a>啟用 Always On 可用性群組並重新啟動 sqlserver

在裝載 SQL Server 執行個體的每個節點上啟用 AlwaysOn 可用性群組，然後重新啟動 `mssql-server`。  請執行下列指令碼：

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-alwaysonhealth-event-session"></a>啟用 AlwaysOn_health 事件工作階段 

當您針對可用性群組進行疑難排解時，您可以選擇性地啟用 AlwaysOn 可用性群組擴充事件來協助診斷根本原因。 在每個 SQL Server 執行個體上執行下列命令。 

```SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

如需此 XE 工作階段的詳細資訊，請參閱 [Always On 擴充事件](http://msdn.microsoft.com/library/dn135324.aspx)。

## <a name="create-db-mirroring-endpoint-user"></a>建立資料庫鏡像端點使用者

下列 Transact-SQL 指令碼會建立名為 `dbm_login` 的登入，以及名為 `dbm_user` 的使用者。 請以強式密碼更新指令碼。 在所有 SQL Server 執行個體上執行下列命令，以建立資料庫鏡像端點使用者。

```SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>建立憑證

Linux 上的 SQL Server 服務使用憑證來驗證鏡像端點之間的通訊。 

下列 Transact-SQL 指令碼會建立主要金鑰和憑證。 然後它會備份憑證，並使用私密金鑰保護檔案。 請以強式密碼更新指令碼。 連線到主要 SQL Server 執行個體，然後執行下列 Transact-SQL 來建立憑證：

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

此時，您的 SQL Server 主要複本含有一個位於 `/var/opt/mssql/data/dbm_certificate.cer` 的憑證，以及一個位於 `var/opt/mssql/data/dbm_certificate.pvk` 的私密金鑰。 將這兩個檔案複製到將裝載可用性複本的所有伺服器上的相同位置。 使用 mssql 使用者，或授與 mssql 使用者存取這些檔案的權限。 

例如在來源伺服器上，下列命令會將檔案複製到目標電腦。 將 **<node2>** 值取代為要裝載複本的 SQL Server 執行個體的名稱。 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

在每部目標伺服器上，授與 mssql 使用者存取憑證的權限。

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>在次要伺服器上建立憑證

下列 Transact-SQL 指令碼會從您在 SQL Server 主要複本上建立的備份來建立主要金鑰和憑證。 此命令也會授權使用者存取憑證。 請以強式密碼更新指令碼。 解密密碼與您在上一個步驟中用來建立 .pvk 檔案的密碼相同。 請在所有次要伺服器上執行下列指令碼來建立憑證。

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate   
    AUTHORIZATION dbm_user
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>在所有複本上建立資料庫鏡像端點

資料庫鏡像端點使用「傳輸控制通訊協定」(TCP)，在參與資料庫鏡像工作階段或裝載可用性複本的伺服器執行個體之間傳送和接收訊息。 資料庫鏡像端點會在唯一的 TCP 通訊埠編號上接聽。 TCP 接聽程式需要一個接聽程式 IP 位址。 接聽程式 IP 位址必須是 IPv4 位址。 您也可以使用`0.0.0.0`。 

下列 Transact-SQL 會為可用性群組建立名為 `Hadr_endpoint` 的接聽端點。 它會啟動端點，並授與您建立的使用者連線權限。 執行指令碼之前，請取代 `**< ... >**` 之間的值。

更新下列 TRANSACT-SQL 為您所有的 SQL Server 執行個體上的環境： 

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login];
```

>[!NOTE]
>如果您使用 SQL Server Express Edition 其中一個節點上裝載組態的唯一複本，角色的唯一有效的值是`WITNESS`。 SQL Server Express Edition 上執行下列指令碼。
>```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login];
```

The TCP port on the firewall needs to be open for the listener port.



>[!IMPORTANT]
>For SQL Server 2017 release, the only authentication method supported for database mirroring endpoint is `CERTIFICATE`. `WINDOWS` option will be enabled in a future release.

For complete information, see [The Database Mirroring Endpoint (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx).
