## <a name="prerequisites"></a>Prerequisites

建立可用性群組之前，您需要：

- 設定您的環境，讓所有將要裝載可用性複本的伺服器能夠通訊。
- 安裝 SQL Server。 如需詳細資訊，請參閱[安裝 SQL Server](../database-engine/install-windows/install-sql-server.md)。

## <a name="enable-always-on-availability-groups-and-restart-mssql-server"></a>啟用 AlwaysOn 可用性群組並重新啟動 mssql-server

>[!NOTE]
>下列命令會利用發佈於 PowerShell 資源庫之 sqlserver 模組中的 Cmdlet。 您可以使用 Install-Module 命令安裝此模組。

在每個裝載 SQL Server 執行個體的複本上啟用 AlwaysOn 可用性群組。 然後重新啟動 SQL Server 服務。 執行下列命令以啟用並重新啟動 SQL Server 服務：

```powershell
Enable-SqlAlwaysOn -ServerInstance <server\instance> -Force
```

## <a name="enable-an-alwayson_health-event-session"></a>啟用 AlwaysOn_health 事件工作階段

 當您針對可用性群組進行疑難排解時，若要協助診斷根本原因，您可以選擇性地啟用 AlwaysOn 可用性群組擴充事件(XEvents) 工作階段。 若要這樣做，請在每個 SQL Server 執行個體上執行下列命令：

```sql
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

如需此 XEvents 工作階段的詳細資訊，請參閱 [AlwaysOn 可用性群組擴充事件](../database-engine/availability-groups/windows/always-on-extended-events.md)。

## <a name="database-mirroring-endpoint-authentication"></a>資料庫鏡像端點驗證

為了讓同步處理正常運作，參與讀取縮放可用性群組的複本必須透過端點進行驗證。 以下幾節將說明可用於這類驗證的兩個主要案例。

### <a name="service-account"></a>服務帳戶

在所有次要複本都會加入相同網域的 Active Directory 環境中，SQL Server 可以利用服務帳戶進行驗證。 您必須在每個 SQL Server 執行個體上，為服務帳戶明確建立登入：

```sql
CREATE LOGIN [<domain>\service account] FROM WINDOWS;
```

### <a name="sql-login-authentication"></a>SQL 登入驗證

在次要複本可能不會加入 Active Directory 網域的環境中，您必須利用 SQL 驗證。 下列 Transact-SQL 指令碼會建立名為 `dbm_login` 的登入，以及名為 `dbm_user` 的使用者。 請以強式密碼更新指令碼。 若要建立資料庫鏡像端點使用者，請在所有 SQL Server 執行個體上執行下列命令：

```sql
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

#### <a name="certificate-authentication"></a>憑證驗證

如果您利用需要使用 SQL 驗證進行驗證的次要複本，請使用憑證在鏡像端點之間進行驗證。

下列 Transact-SQL 指令碼會建立主要金鑰和憑證。 然後它會備份憑證，並使用私密金鑰保護檔案。 請以強式密碼更新指令碼。 在主要 SQL Server 執行個體上執行指令碼來建立憑證：

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

此時，您的 SQL Server 主要複本含有一個位於 `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer` 的憑證，以及一個位於 `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk` 的私密金鑰。 將這兩個檔案複製到將裝載可用性複本的所有伺服器上的相同位置。

在每個次要複本上，請確定 SQL Server 執行個體的服務帳戶都有存取憑證的權限。

#### <a name="create-the-certificate-on-secondary-servers"></a>在次要伺服器上建立憑證

下列 Transact-SQL 指令碼會從您在 SQL Server 主要複本上建立的備份來建立主要金鑰和憑證。 此命令也會授權使用者存取憑證。 請以強式密碼更新指令碼。 解密密碼與您在上一個步驟中用來建立 *.pvk* 檔案的密碼相同。 若要建立憑證，請在所有次要複本上執行下列指令碼：

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate
    AUTHORIZATION dbm_user
    FROM FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-database-mirroring-endpoints-on-all-replicas"></a>在所有複本上建立資料庫鏡像端點

資料庫鏡像端點使用「傳輸控制通訊協定」(TCP)，在參與資料庫鏡像工作階段或裝載可用性複本的伺服器執行個體之間傳送和接收訊息。 資料庫鏡像端點會在唯一的 TCP 通訊埠編號上接聽。

下列 Transact-SQL 指令碼會為可用性群組建立名為 `Hadr_endpoint` 的接聽端點。 它會啟動端點，並為服務帳戶或您在上一個步驟中建立的 SQL 登入提供連線權限。 執行指令碼之前，請取代 `**< ... >**` 之間的值。 您可以選擇性地包含 IP 位址 `LISTENER_IP = (0.0.0.0)`。 接聽程式 IP 位址必須是 IPv4 位址。 您也可以使用 `0.0.0.0`。

請在所有 SQL Server 執行個體上更新您環境的下列 Transact-SQL 指令碼：

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [<service account or user>];
```

防火牆上的 TCP 連接埠必須開啟以作為接聽程式連接埠。

如需詳細資訊，請參閱[資料庫鏡像端點 (SQL Server)](../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md?view=sql-server-2017)。