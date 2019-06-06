---
title: 建立和設定 Linux 上的 SQL Server 可用性群組 |Microsoft Docs
description: 本教學課程會示範如何建立和設定 Linux 上的 SQL Server 可用性群組。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 06/28/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 1841b7e38e47ffa1192b19564e1c6596ea9804a3
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719384"
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>建立和設定 Linux 上的 SQL Server 可用性群組

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教學課程涵蓋如何建立及設定可用性群組 (AG) 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上。 不同於[!INCLUDE[sssql15-md](../includes/sssql15-md.md)]和稍早在 Windows 中，您可以啟用 Ag 不論是否先建立基礎的 Pacemaker 叢集。 整合與叢集，如有需要不是稍後才。

本教學課程包含下列工作：
 
> [!div class="checklist"]
> * 啟用可用性群組。
> * 建立可用性群組端點和憑證。
> * 使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)](SSMS) 或 TRANSACT-SQL 來建立可用性群組。
> * 建立[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]登入和 Pacemaker 的權限。
> * 在 Pacemaker 叢集 （僅外部型別） 中建立可用性群組資源。

## <a name="prerequisite"></a>必要條件
- 部署 Pacemaker 高可用性叢集，如中所述[部署在 Linux 上的 SQL server 的 Pacemaker 叢集](sql-server-linux-deploy-pacemaker-cluster.md)。


## <a name="enable-the-availability-groups-feature"></a>啟用可用性群組功能

不同於 Windows，您無法使用 PowerShell 或[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]組態管理員來啟用可用性群組 (AG) 功能。 在 Linux，您必須使用`mssql-conf`啟用功能。 若要啟用可用性群組功能的兩種方式： 使用`mssql-conf`公用程式或編輯`mssql.conf`手動檔案。

> [!IMPORTANT]
> 即使僅設定的複本，必須啟用 AG 功能[!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]。

### <a name="use-the-mssql-conf-utility"></a>使用 mssql conf 公用程式

在提示字元中發出下列項目：

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>編輯 mssql.conf 檔案

您也可以修改`mssql.conf`檔案，位於`/var/opt/mssql`資料夾中，加入下列幾行：

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-includessnoversion-mdincludesssnoversion-mdmd"></a>重新啟動 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
啟用可用性群組，因為在 Windows 中，您必須重新啟動之後[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 可藉由下列：

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>建立可用性群組端點和憑證

可用性群組會使用 TCP 端點進行通訊。 下，如果憑證用來驗證，只會支援 AG 的端點。 這表示一個執行個體中的憑證必須先還原所有其他將會參與相同的 AG 的複本的執行個體上。 即使僅設定的複本需要憑證的程序。 

建立端點及還原憑證只能透過 Transact SQL。 您可以使用非[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-所產生的憑證以及。 您也必須管理，並取代過期的任何憑證的程序。

> [!IMPORTANT]
> 如果您打算使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]精靈來建立 AG，您仍然必須建立並在 Linux 上使用 TRANSACT-SQL 還原憑證。

如需適用於各種不同的命令 （例如額外的安全性） 之選項的完整語法，請參閱：

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [建立憑證](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> 雖然您會建立可用性群組，所使用的端點類型*FOR DATABASE_MIRRORING*，因為某些基礎層面一次該現在已被取代的功能與共用。

此範例會建立三個節點組態的憑證。 執行個體名稱是 LinAGN1、 LinAGN2 和 LinAGN3。

1.  執行下列命令 LinAGN1 建立主要金鑰、 憑證和端點，以及備份憑證。 例如，一般的 TCP 通訊埠 5022 的用於端點。
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN1_Cert
    WITH SUBJECT = 'LinAGN1 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN1_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN1_Cert,
        ROLE = ALL);
    
    GO
    ```
    
2.  執行 LinAGN2 上相同的動作：
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    WITH SUBJECT = 'LinAGN2 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN2_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN2_Cert,
        ROLE = ALL);
    
    GO
    ```
    
3.  最後，在 LinAGN3 上執行的相同順序：
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    WITH SUBJECT = 'LinAGN3 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN3_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN3_Cert,
        ROLE = ALL);
    
    GO
    ```
    
4.  使用`scp`或其他公用程式，將憑證的備份複製到將成為 AG 一部分的每個節點。
    
    此範例中：
    
    - 複製 LinAGN1_Cert.cer LinAGN2 和 LinAGN3
    - 複製 LinAGN2_Cert.cer LinAGN1 和 LinAGN3。
    - 複製 LinAGN3_Cert.cer LinAGN1 和 LinAGN2。
    
5.  變更擁有權和複製的憑證檔案，以與相關聯的群組`mssql`。
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  建立執行個體層級登入和 LinAGN2 和 LinAGN3 LinAGN1 上的相關聯的使用者。
    
    ```SQL
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
7.  還原 LinAGN2_Cert 和 LinAGN3_Cert LinAGN1 上。 其他複本的憑證是 AG 通訊和安全性的重要層面。
    
    ```SQL
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
8.  Grant the logins associated with LinAG2 and LinAGN3 permission to connect to the endpoint on LinAGN1.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
9.  建立執行個體層級登入和 LinAGN1 和 LinAGN3 LinAGN2 上的相關聯的使用者。
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10. 還原 LinAGN1_Cert 和 LinAGN3_Cert LinAGN2 上。
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    ```
    
11. 授與連接到 LinAGN2 上的端點的 LinAG1 和 LinAGN3 權限相關聯的登入。
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12. 建立執行個體層級登入和 LinAGN1 和 LinAGN2 LinAGN3 上的相關聯的使用者。
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13. 還原 LinAGN1_Cert 和 LinAGN2_Cert LinAGN3 上。 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    ```
    
14. 授與連接到 LinAGN3 上的端點的 LinAG1 和 LinAGN2 權限相關聯的登入。
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>建立可用性群組

本節說明如何使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)](SSMS) 或 TRANSACT-SQL 來建立可用性群組[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。

### <a name="use-includessmanstudiofull-mdincludesssmanstudiofull-mdmd"></a>使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]

本節說明如何建立外部叢集類型 AG 使用 SSMS 搭配新的可用性群組精靈。

1.  在 SSMS 中，依序展開**Always On 高可用性**，以滑鼠右鍵按一下**可用性群組**，然後選取**新增可用性群組精靈**。

2.  在 [簡介] 對話方塊中，按一下 [**下一步]** 。

3.  在 [指定可用性群組選項] 對話方塊中，輸入可用性群組的名稱，然後選取叢集類型 EXTERNAL 或 NONE 的下拉式清單中。 將部署 Pacemaker 時，應該使用外部。 都不是特殊的情況下，例如讀取向外延展。選取的資料庫層級的健全狀況偵測選項是選擇性的。 如需有關這個選項的詳細資訊，請參閱 <<c0> [ 可用性群組資料庫層級健全狀況偵測容錯移轉選項](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md)。 按一下 [下一步]  。

    ![](./media/sql-server-linux-create-availability-group/image3.png)

4.  在 選取資料庫 對話方塊中，選取 將參與 AG 中的資料庫。 每個資料庫必須有完整備份，才能將它加入至 AG。 按一下 [下一步]  。

5.  在 [指定複本] 對話方塊中，按一下**將複本加入**。

6.  在 [連線到伺服器] 對話方塊中，輸入 Linux 執行個體名稱[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，就會在次要複本，以及要連接的認證。 按一下 **[連接]** 。

7.  重複前兩個步驟將包含僅設定的複本或另一個次要複本之執行個體。

8.  現在應該在 [指定複本] 對話方塊會列出所有的三個執行個體。 如果次要複本將成為，則為 true 的次要資料庫，請使用外部叢集類型，請確定可用性模式比對的主要複本，並容錯移轉模式設定為外部。 僅設定的複本，選取 設定的僅限可用性模式。

    下列範例顯示兩個複本、 外部叢集類型，與僅設定的複本 AG。

    ![](./media/sql-server-linux-create-availability-group/image4.png)

    下列範例示範具有兩個複本 AG，叢集類型為 None、 和僅設定的複本。

    ![](./media/sql-server-linux-create-availability-group/image5.png)

9.  如果您想要改變的備份喜好設定，按一下 [備份喜好設定] 索引標籤。如需有關使用 Ag 的備份喜好設定的詳細資訊，請參閱[可用性複本上的設定備份](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)。

10. 如果使用可讀取次要複本，或與叢集建立 AG 輸入的無讀取規模，您可以選取 [接聽程式] 索引標籤來建立接聽程式。也可以稍後新增接聽程式。 若要建立接聽程式，選擇**建立可用性群組接聽程式**並輸入名稱、 TCP/IP 通訊埠，以及是否要使用靜態或自動指派的 DHCP IP 位址。 請記住，none 叢集類型 ag，IP 應該是靜態的並設定為主要伺服器的 IP 位址。

    ![](./media/sql-server-linux-create-availability-group/image6.png)

11. 如果可讀取的情況下建立接聽程式時，SSMS 17.3 或更新版本可讓唯讀路由在精靈中建立。 它也可以新增稍後透過 SSMS 或 TRANSACT-SQL。 若要新增唯讀路由現在：

    a.  選取 [唯讀路由] 索引標籤。

    b.  輸入 Url，唯讀複本。 這些 Url 可端點，類似，但它們要使用的執行個體，而不需將端點的連接埠。

    c.  選取每個 URL，然後從底部，選取 可讀取的複本。 多重選取時，請按住 shift 鍵或按一下拖曳。

12. 按一下 [下一步]  。

13. 選擇將初始化次要複本的方式。 若要使用的預設值是[自動植入](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md)，這需要參與 AG 中的所有伺服器上相同的路徑。 您也可以讓精靈進行備份、 複製和還原 （第二個選項）;如果您有手動備份、 複製和還原項目上的資料庫加入它 （第三個選項）;或更新版本加入資料庫 （最後一個選項）。 使用憑證，如果您是以手動方式進行備份，並將它們複製，因為備份檔案的權限必須設定其他項目上。 按一下 [下一步]  。

14. 在 [驗證] 對話方塊中，如果所有項目不會不回來為成功，調查。 某些警告是可接受和不嚴重，例如，如果您未建立接聽程式。 按一下 [下一步]  。

15. 在 摘要 對話方塊中，按一下 **完成**。 建立 AG 的程序將立即開始。

16. AG 建立完畢後，按一下**關閉**結果。 您現在可以看到 AG 複本中的動態管理檢視，以及在 SSMS 中的 [Alwayson 高可用性] 資料夾底下。

### <a name="use-transact-sql"></a>使用 Transact-SQL

本節說明建立使用 Transact SQL AG 的範例。 建立 AG 之後，可以設定接聽程式和唯讀路由。 可以使用修改 AG 本身`ALTER AVAILABILITY GROUP`，但無法進行變更的叢集類型[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 如果您不打算建立的外部叢集類型 AG，您必須刪除它，並重新建立它的叢集類型為 None。 詳細資訊和其他選項可在下列連結：

-   [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)
-   [ALTER AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [設定唯讀路由，可用性群組 (SQL Server)](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [建立或設定可用性群組接聽程式 (SQL Server)](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one---two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>範例 1-2 個複本，與僅設定的複本 （外部叢集類型）

此範例示範如何建立會使用僅限設定複本的兩個複本 AG。

1.  將會包含完整讀取/寫入複本資料庫的主要複本的節點上執行。 此範例會使用自動植入。

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1' WITH (
       ENDPOINT_URL = N' TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       SEEDING_MODE = AUTOMATIC),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       AVAILABILITY_MODE = CONFIGURATION_ONLY);
       
    GO
    ```
    
2.  在查詢視窗中連接到其他複本，執行下列命令來將複本加入至 AG，並起始從主要到次要複本植入程序。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3. 在查詢視窗中連線到僅限設定的複本，請將它加入 AG 中。
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
   ```

#### <a name="example-two---three-replicas-with-read-only-routing-external-cluster-type"></a>使用唯讀路由 （外部叢集類型） 的範例中兩個三個複本

此範例示範三個完整初始的 AG 建立過程，則可以設定複本和如何唯讀路由。

1.  將會包含完整讀取/寫入複本資料庫的主要複本的節點上執行。 此範例會使用自動植入。

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN2.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:1433')),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN2.FullyQualified.Name:1433')),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN3.FullyQualified.Name:1433'))
    LISTENER '<ListenerName>' (WITH IP = ('<IPAddress>', '<SubnetMask>'), Port = 1433);
    
    GO
    ```
    
    關於這項設定，請注意幾件事：
    
    - *AGName*是可用性群組的名稱。
    - *DBName*是將可用性群組搭配使用的資料庫名稱。 它也可以是一份以逗號分隔的名稱。
    - *ListenerName*是不同於任何基礎的伺服器/節點的名稱。 它會登錄在 DNS 中連同*IPAddress*。
    - *IPAddress*是相關聯的 IP 位址*ListenerName*。 它也是唯一並不完全相同的任何伺服器/節點。 應用程式和終端使用者將會使用*ListenerName*或是*IPAddress*來連接到 AG。
    - *指定子網路遮罩*是子網路遮罩*IPAddress*; 例如，255.255.255.0。

2.  在查詢視窗中連接到其他複本，執行下列命令來將複本加入至 AG，並起始從主要到次要複本植入程序。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  重複步驟 2 的第三個複本。

#### <a name="example-three---two-replicas-with-read-only-routing-none-cluster-type"></a>範例三兩個複本的唯讀路由 （None 叢集類型）

此範例顯示使用 None 叢集類型的兩個複本組態的建立。 它用於讀取的級別案例沒有容錯移轉所預期的位置。 這會建立的接聽程式實際的主要複本，以及唯讀路由，使用循環配置資源功能。

1.  將會包含完整讀取/寫入複本資料庫的主要複本的節點上執行。 此範例會使用自動植入。

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = NONE)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name: <PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name'.'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:<PortOfInstance>'));
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:<PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL =N'TCP://LinAGN2.FullyQualified.Name:<PortOfInstance>'));
    LISTENER '<ListenerName>' (WITH IP = ('<PrimaryReplicaIPAddress>', '<SubnetMask>'), Port = <PortOfListener>);
    
    GO
    ```
    
    位置
    - *AGName*是可用性群組的名稱。
    - *DBName*是將可用性群組搭配使用的資料庫名稱。 它也可以是一份以逗號分隔的名稱。
    - *PortOfEndpoint*所建立的端點使用的通訊埠編號。
    - *PortOfInstance*的執行個體所使用的通訊埠編號[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。
    - *ListenerName*是不同於任何基礎的複本，但不是實際上會使用的名稱。
    - *PrimaryReplicaIPAddress*是主要複本的 IP 位址。
    - *指定子網路遮罩*是子網路遮罩*IPAddress*。 例如，255.255.255.0。
    
2.  將次要複本聯結至 AG，起始自動植入。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-includessnoversion-mdincludesssnoversion-mdmd-login-and-permissions-for-pacemaker"></a>建立[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]登入和 Pacemaker 的權限

Pacemaker 高可用性叢集基礎[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]需要在 Linux 上的 存取[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]執行個體，以及本身的可用性群組的權限。 這些步驟會建立登入和相關聯的權限，以及告知 Pacemaker 如何登入的檔案[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。

1.  在查詢視窗中連接到第一個複本，執行下列作業︰

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD ='<StrongPassword>';
    
    GO
    
    GRANT VIEW SERVER STATE TO PMLogin;
    
    GO
    
    GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::<AGThatWasCreated> TO PMLogin;
    
    GO
    ```
    
2.  在節點 1 中，輸入命令 
    ```bash
    sudo emacs /var/opt/mssql/secrets/passwd
    ```
    
    這會開啟在 Emacs 編輯器。
    
3.  在編輯器中輸入下列兩行：

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  按住 CTRL 鍵，然後按 X，然後 C，以結束並儲存檔案。

5.  Execute 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    若要鎖定的檔案。

6.  重複步驟 1-5，將做為複本的伺服器上。

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>在 Pacemaker 叢集 （僅外部） 中建立可用性群組資源

之後的可用性群組會在[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，指定外部叢集類型時，必須在 Pacemaker，建立對應的資源。 有兩個 AG 相關聯的資源： AG 本身和 IP 位址。 設定 IP 位址資源是選擇性的如果您未使用接聽程式的功能，但建議使用。

建立的 AG 資源是資源的一種特殊，名叫複製品。 AG 資源基本上有複本，每個節點，而且有一個稱為主要的控制資源。 與裝載主要複本的伺服器，主要是為相關聯。 次要複本 （一般或僅設定的） 會被視為從屬節點，並可提升為主要在容錯移轉。

1.  使用下列語法建立 AG 資源：

    **Red Hat Enterprise Linux (RHEL) 和 Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failure-timeout=30s --master meta notify=true
    ```

    >[!NOTE]
    >在 RHEL 7.4 中，您可能會遇到與使用，主要的警告。 若要避免這個問題，請使用 `sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failover-timeout=30s master notify=true`
   
    **SUSE Linux Enterprise Server (SLES)**
    
    ```bash
    primitive <NameForAGResource> \
    ocf:mssql:ag \
    params ag_name="<AGName>" \
    meta failure-timeout=60s \
    op start timeout=60s \
    op stop timeout=60s \
    op promote timeout=60s \
    op demote timeout=10s \
    op monitor timeout=60s interval=10s \
    op monitor timeout=60s interval=11s role="Master" \
    op monitor timeout=60s interval=12s role="Slave" \
    op notify timeout=60s
    ms ms-ag_cluster <NameForAGResource> \
    meta master-max="1" master-node-max="1" clone-max="3" \
    clone-node-max="1" notify="true" \
    commit
    ```
    
    何處*NameForAGResource*是 ag 中，指定到這個叢集資源的唯一名稱和*AGName* AG 所建立的名稱。
 
2.  建立 ag 接聽程式功能相關聯的 IP 位址資源。

    **RHEL 和 Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForIPResource> ocf:heartbeat:IPaddr2 ip=<IPAddress> cidr_netmask=<Netmask>
    ```

    **SLES**
    
    ```bash
    crm configure \
    primitive <NameForIPResource> \
       ocf:heartbeat:IPaddr2 \
       params ip=<IPAddress> \
          cidr_netmask=<Netmask>
    ```
    
    何處*NameForIPResource*是 IP 資源的唯一名稱並*IPAddress*是靜態的 IP 位址指派給資源。 在 SLES，您也必須提供網路遮罩。 例如，255.255.255.0 會有 24 個做為值*網路遮罩。*
    
3.  若要確保 IP 位址和 AG 資源相同的節點上執行，就必須設定共置條件約束。

    **RHEL 和 Ubuntu**
    
    ```bash
    sudo pcs constraint colocation add <NameForIPResource> <NameForAGResource>-master INFINITY with-rsc-role=Master
    ```

    **SLES**
    
    ```bash
    crm configure <NameForConstraint> inf: \
    <NameForIPResource> <NameForAGResource>:Master 
    commit
    ```
    
    何處*NameForIPResource* IP 資源，名稱*NameForAGResource*是針對 AG 資源，而且 SLES，名稱*NameForConstraint*的名稱條件約束。

4.  建立順序條件約束，以確定 AG 資源已啟動並執行前的 IP 位址。 共置條件約束所指的排序條件約束，而這會強制執行它。

    **RHEL 和 Ubuntu**
    
    ```bash
    sudo pcs constraint order promote <NameForAGResource>-master then start <NameForIPResource>
    ```
    
    **SLES**
    
    ```bash
    crm configure \
    order <NameForConstraint> inf: <NameForAGResource>:promote <NameForIPResource>:start
    commit
    ```
    
    何處*NameForIPResource* IP 資源，名稱*NameForAGResource*是針對 AG 資源，而且 SLES，名稱*NameForConstraint*的名稱條件約束。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何建立及設定可用性群組的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上。 您已學到如何以：
> [!div class="checklist"]
> * 啟用可用性群組。
> * 建立 AG 端點和憑證。
> * 使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)](SSMS) 或 TRANSACT-SQL 來建立 AG。
> * 建立[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]登入和 Pacemaker 的權限。
> * 在 Pacemaker 叢集中建立 AG 資源。

大部分 AG 系統管理工作，包括升級和容錯移轉，請參閱：

> [!div class="nextstepaction"]
> [Linux 上的 SQL Server 運作 HA 可用性群組](sql-server-linux-availability-group-failover-ha.md)

