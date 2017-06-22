## <a name="prerequisites"></a>必要條件

建立可用性群組之前，您需要：

- 設定您的環境，讓所有將要裝載可用性複本的伺服器能夠通訊
- 安裝 SQL Server

>[!NOTE]
>On Linux，您必須建立可用性群組，再將其新增為叢集資源，以管理叢集。 本文件提供的範例會建立可用性群組。 發佈的特定指示來建立叢集和可用性群組新增為叢集資源，請參閱底下的連結[後續步驟](#next-steps)。

1. **更新每一部主機的電腦名稱**

   每個 SQL Server 名稱必須是：
   
   - 15 個字元或更少
   - 在 網路內唯一
   
   若要設定的電腦名稱，請編輯`/etc/hostname`。 下列指令碼可讓您編輯`/etc/hostname`與`vi`。

   ```bash
   sudo vi /etc/hostname
   ```

1. **設定主機檔案。**

>[!NOTE]
>如果主機名稱會登錄在 DNS 伺服器及其 IP，但沒有需要執行下列步驟。 驗證要將可用性群組組態的一部分的所有節點可以與 (ping 主機名稱應該回覆與對應的 IP 位址) 彼此都通訊。 此外，請確定 /etc/hosts 檔案不包含 localhost IP 位址 127.0.0.1 與節點的主機名稱，對應的記錄。


   每一部伺服器上的主機檔案包含 IP 位址和要參與可用性群組的所有伺服器的名稱。 

   下列命令會傳回目前伺服器的 IP 位址：

   ```bash
   sudo ip addr show
   ```

   更新`/etc/hosts`。 下列指令碼可讓您編輯`/etc/hosts`與`vi`。

   ```bash
   sudo vi /etc/hosts
   ```

   下列範例所示`/etc/hosts`上**node1**的新增項目與**node1**和**node2**。 本文件**node1**指的是 SQL Server 的主要複本。 **node2**指的是次要 SQL Server。;


   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 node1
   10.128.16.77 node2
   ```

### <a name="install-sql-server"></a>安裝 SQL Server

安裝 SQL Server。 下列連結指向各種分佈的 SQL Server 安裝指示。 

- [Red Hat Enterprise Linux](..\linux\sql-server-linux-setup-red-hat.md)

- [SUSE Linux Enterprise Server](..\linux\sql-server-linux-setup-suse-linux-enterprise-server.md)

- [Ubuntu](..\linux\sql-server-linux-setup-ubuntu.md)

## <a name="enable-always-on-availability-groups-and-restart-sqlserver"></a>啟用 Alwayson 可用性群組並重新啟動 sql server

啟用 Alwayson 可用性群組裝載 SQL Server 服務，每個節點上的，然後重新啟動`mssql-server`。  請執行下列指令碼：

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-alwaysonhealth-event-session"></a>啟用 AlwaysOn_health 事件工作階段 

您可以 optionaly 啟用 Alwayson 可用性群組特定擴充事件來協助診斷根本原因，當您疑難排解可用性群組。

```Transact-SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

如需此 XE 工作階段的詳細資訊，請參閱[一律在擴充事件](http://msdn.microsoft.com/library/dn135324.aspx)。

## <a name="create-db-mirroring-endpoint-user"></a>建立資料庫鏡像端點的使用者

下列的 TRANSACT-SQL 指令碼會建立名為登入`dbm_login`，和名為使用者`dbm_user`。 更新的指令碼以強式密碼。 若要建立資料庫鏡像端點使用者的所有 SQL Server 上執行下列命令。

```Transact-SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>建立憑證

在 Linux 上的 SQL Server 服務使用憑證來驗證的鏡像端點之間的通訊。 

下列的 TRANSACT-SQL 指令碼會建立主要金鑰和憑證。 然後會將憑證備份，並具有私密金鑰的金鑰保護的檔案。 更新的指令碼以強式密碼。 連接到主要 SQL Server，然後執行下列 TRANSACT-SQL 來建立憑證：

```Transact-SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

此時您 SQL Server 的主要複本已位於憑證`/var/opt/mssql/data/dbm_certificate.cer`和私用的索引鍵在`var/opt/mssql/data/dbm_certificate.pvk`。 將這兩個檔案複製到將要裝載可用性複本的所有伺服器上的相同位置。 使用 mssql 使用者或授與權限給 mssql 使用者存取這些檔案。 

例如在來源伺服器上，下列命令將檔案複製到目標電腦。 取代 **<node2>** 將裝載複本的 SQL Server 執行個體名稱的值。 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

在目標伺服器上，授與存取憑證 mssql 使用者的權限。

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>在次要伺服器上建立憑證

下列的 TRANSACT-SQL 指令碼會從您建立 SQL Server 的主要複本的備份來建立主要金鑰和憑證。 此命令也會授權使用者存取的憑證。 更新的指令碼以強式密碼。 您用來建立.pvk 檔案上一個步驟中的相同密碼的解密密碼。 若要建立憑證的所有次要伺服器上執行下列指令碼。

```Transact-SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate   
    AUTHORIZATION dbm_user
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>建立資料庫鏡像端點，在所有複本上，

資料庫鏡像端點使用「傳輸控制通訊協定」(TCP)，在參與資料庫鏡像工作階段或裝載可用性複本的伺服器執行個體之間傳送和接收訊息。 資料庫鏡像端點會在唯一的 TCP 通訊埠編號上接聽。 

下列 TRANSACT-SQL 會建立名為接聽端點`Hadr_endpoint`可用性群組。 啟動端點，並可讓您建立之使用者的連接權限。 執行指令碼之前，請將之間的值取代`**< ... >**`。


>[!NOTE]
>此版本中，請勿用於不同的 IP 位址的接聽程式 IP。 我們正在解決這個問題，但只可接受的值現在是 '0.0.0.0'。

更新下列 TRANSACT-SQL 為您所有的 SQL Server 執行個體上的環境： 

```Transact-SQL
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

>[!IMPORTANT]
>在防火牆上的 TCP 連接埠必須開啟接聽程式連接埠。

如需完整資訊，請參閱[資料庫鏡像端點 (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx)。
