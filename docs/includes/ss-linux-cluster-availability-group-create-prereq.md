## <a name="prerequisites"></a>必要條件

建立可用性群組之前，您需要：

- 設定您的環境，以便將要裝載可用性複本的所有伺服器可以都通訊。
- 安裝 SQL Server。

>[!NOTE]
>On Linux，您必須建立可用性群組之前將它新增為叢集資源，以管理叢集。 本文件提供建立可用性群組的範例。 若要建立叢集，並新增為叢集資源的可用性群組的發佈特定指示，請參閱 < 後續步驟。 > 下的連結

1. 更新每一部主機的電腦名稱。

   每個 SQL Server 名稱必須是：
   
   - 15 個字元或更少。
   - 在 網路內是唯一的。
   
   若要設定電腦名稱，請編輯 `/etc/hostname`。 下列指令碼可讓您編輯`/etc/hostname`與`vi`:

   ```bash
   sudo vi /etc/hostname
   ```

2. 設定主機檔案。

    >[!NOTE]
    >如果主機名稱會登錄在 DNS 伺服器及其 IP，您不需要執行下列步驟。 驗證所有節點要成為可用性群組組態的一部分，可與對方進行通訊。 （主機名稱 ping 應該回覆與對應的 IP 位址）。此外，請確定 /etc/hosts 檔案不包含 localhost IP 位址 127.0.0.1 與節點的主機名稱，對應的記錄。
    >

   每一部伺服器上的 hosts 檔案包含將參與可用性群組之所有伺服器的 IP 位址和名稱。 

   下列命令會傳回目前伺服器的 IP 位址：

   ```bash
   sudo ip addr show
   ```

   更新 `/etc/hosts`。 下列指令碼可讓您編輯`/etc/hosts`與`vi`:

   ```bash
   sudo vi /etc/hosts
   ```

   下列範例顯示 **node1** 上的 `/etc/hosts`，以及 **node1**、**node2** 和 **node3** 上的新增項目。 本文件**node1**是指裝載主要複本的伺服器。 和**node2**和**node3**到裝載次要複本的伺服器，請參閱。

    ```
    127.0.0.1   localhost localhost4 localhost4.localdomain4
    ::1       localhost localhost6 localhost6.localdomain6
    10.128.18.12 node1
    10.128.16.77 node2
    10.128.15.33 node3
    ```

### <a name="install-sql-server"></a>安裝 SQL Server

安裝 SQL Server。 下列連結指向各種分佈的 SQL Server 安裝指示： 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)
- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-alwayson-availability-groups-and-restart-mssql-server"></a>啟用 AlwaysOn 可用性群組，然後重新啟動 mssql 伺服器

啟用 AlwaysOn 可用性群組，每個節點裝載 SQL Server 執行個體上。 然後重新啟動`mssql-server`。 請執行下列指令碼：

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-an-alwaysonhealth-event-session"></a>啟用 AlwaysOn_health 事件工作階段 

您可以選擇性地啟用 AlwaysOn 可用性群組擴充的事件，以協助診斷根本原因，當您疑難排解可用性群組。 每個 SQL Server 執行個體上執行下列命令： 

```SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

如需此 XE 工作階段的詳細資訊，請參閱[擴充事件的 AlwaysOn](http://msdn.microsoft.com/library/dn135324.aspx)。

## <a name="create-a-database-mirroring-endpoint-user"></a>建立資料庫鏡像端點的使用者

下列的 TRANSACT-SQL 指令碼會建立名為登入`dbm_login`和名為使用者`dbm_user`。 請以強式密碼更新指令碼。 若要建立資料庫鏡像端點的使用者，請在所有 SQL Server 執行個體上執行下列命令：

```SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>建立憑證

Linux 上的 SQL Server 服務使用憑證來驗證鏡像端點之間的通訊。 

下列的 TRANSACT-SQL 指令碼會建立主要金鑰和憑證。 它接著備份憑證，並具有私密金鑰的金鑰保護的檔案。 請以強式密碼更新指令碼。 連接到主要 SQL Server 執行個體。 若要建立憑證，請執行下列 TRANSACT-SQL 指令碼：

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

此時，主要的 SQL Server 複本已位於憑證`/var/opt/mssql/data/dbm_certificate.cer`和私用的索引鍵在`var/opt/mssql/data/dbm_certificate.pvk`。 將這兩個檔案複製到將裝載可用性複本的所有伺服器上的相同位置。 使用 mssql 使用者，或授與權限給 mssql 使用者存取這些檔案。 

例如，在來源伺服器上，下列命令將檔案複製到目標電腦。 取代`**<node2>**`將裝載複本的 SQL Server 執行個體名稱的值。 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

在每個目標伺服器上，授與給 mssql 使用者存取此憑證的權限。

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>在次要伺服器上建立憑證

下列的 TRANSACT-SQL 指令碼會從您建立 SQL Server 的主要複本的備份來建立主要金鑰和憑證。 此命令也會授權使用者存取憑證。 請以強式密碼更新指令碼。 解密密碼與您在上一個步驟中用來建立 .pvk 檔案的密碼相同。 若要建立憑證，請在所有次要伺服器上執行下列程式碼：

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

資料庫鏡像端點使用傳輸控制通訊協定 (TCP) 來傳送和接收參與資料庫鏡像工作階段或裝載可用性複本之伺服器執行個體之間的訊息。 資料庫鏡像端點會在唯一的 TCP 通訊埠編號上接聽。 TCP 接聽程式需要一個接聽程式 IP 位址。 接聽程式 IP 位址必須是 IPv4 位址。 您也可以使用`0.0.0.0`。 

下列的 TRANSACT-SQL 指令碼會建立名為接聽端點`Hadr_endpoint`可用性群組。 它會啟動端點，並可讓您建立的使用者連接權限。 執行指令碼之前，請取代 `**< ... >**` 之間的值。

更新您的環境，所有 SQL Server 執行個體上的下列 TRANSACT-SQL 指令碼： 

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
>如果您使用 SQL Server Express Edition 其中一個節點上裝載設定唯讀複本，唯一的有效值`ROLE`是`WITNESS`。 SQL Server Express Edition 上執行下列指令碼：

```SQL
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

在防火牆上的 TCP 連接埠必須開啟接聽程式連接埠。



>[!IMPORTANT]
>SQL Server 2017 版本中，資料庫鏡像端點支援的唯一的驗證方法是`CERTIFICATE`。 `WINDOWS`選項將會在未來的版本中啟用。

如需詳細資訊，請參閱[資料庫鏡像端點 (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx)。


