---
title: 建立及設定可用性群組的 SQL Server on Linux |Microsoft 文件
description: 本教學課程會示範如何建立及設定可用性群組的 SQL Server on Linux。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/11/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: f02ec690caec1c33b4a316707c0011c8be032580
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>建立及設定可用性群組的 SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教學課程涵蓋如何建立及設定可用性群組 (AG) 的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]on Linux。 不同於[!INCLUDE[sssql15-md](../includes/sssql15-md.md)]和稍早在 Windows 中，您可以啟用 Ag 具有或不需要先建立基礎 Pacemaker 叢集。 整合與叢集，必要時，才完成更新版本。

本教學課程包括下列工作：
 
> [!div class="checklist"]
> * 啟用可用性群組。
> * 建立可用性群組端點和憑證。
> * 使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)](SSMS) 或 TRANSACT-SQL 來建立可用性群組。
> * 建立[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]登入和 Pacemaker 權限。
> * 建立可用性群組資源在 Pacemaker 叢集中 （只有外部型別）。

## <a name="prerequisite"></a>必要條件
- 中所述部署 Pacemaker 高可用性叢集[Pacemaker 叢集部署的 SQL Server on Linux](sql-server-linux-deploy-pacemaker-cluster.md)。


## <a name="enable-the-availability-groups-feature"></a>啟用可用性群組功能

不同於在 Windows 中，您無法使用 PowerShell 或[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]組態管理員來啟用可用性群組 (AG) 的功能。 在 Linux，您必須使用`mssql-conf`以啟用功能。 若要啟用的可用性群組功能的兩種方式： 使用`mssql-conf`公用程式或編輯`mssql.conf`手動檔案。

> [!IMPORTANT]
> 即使在只設定複本，必須啟用 AG 功能[!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]。

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
啟用可用性群組，因為在 Windows 中，您必須重新啟動之後[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 可如下：

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>建立可用性群組端點和憑證

可用性群組使用的 TCP 端點進行通訊。 在 Linux，AG 的端點才會受到支援憑證用來驗證。 這表示一個執行個體中的憑證必須先還原所有其他執行個體將會參與相同的 AG 的複本上。 即使只設定複本需要憑證的程序。 

建立端點及還原憑證才可透過 TRANSACT-SQL。 您可以使用非[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-產生以及憑證。 您也需要處理程序管理，並取代任何過期的憑證。

> [!IMPORTANT]
> 如果您打算使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]精靈來建立 AG，您仍需要建立及還原使用 TRANSACT-SQL 在 Linux 上的憑證。

選項可供各種不同的命令 （例如額外的安全性） 的完整語法，請參閱：

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [建立憑證](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> 雖然您會建立可用性群組，端點的型別會使用*FOR DATABASE_MIRRORING*，因為某些基礎層面，一次該現在已被取代的功能與共用。

這個範例會建立三個節點組態的憑證。 執行個體名稱是 LinAGN1、 LinAGN2 和 LinAGN3。

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
    
2.  執行 LinAGN2 相同的動作：
    
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
    
3.  最後，LinAGN3 上執行的相同順序：
    
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
    
    例如：
    
    - 將複製 LinAGN2 和 LinAGN3 LinAGN1_Cert.cer
    - 將複製 LinAGN2_Cert.cer LinAGN1 和 LinAGN3。
    - 將複製 LinAGN3_Cert.cer LinAGN1 和 LinAGN2。
    
5.  變更擁有權和複製的憑證檔案相關聯的群組`mssql`。
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  建立執行個體層級登入和使用者 LinAGN2 和 LinAGN3 LinAGN1 上的相關聯。
    
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
    
9.  建立執行個體層級登入和使用者 LinAGN1 和 LinAGN3 LinAGN2 上的相關聯。
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10.  還原 LinAGN1_Cert 和 LinAGN3_Cert LinAGN2 上。 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
11.  Grant the logins associated with LinAG1 and LinAGN3 permission to connect to the endpoint on LinAGN2.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12.  建立執行個體層級登入和使用者 LinAGN1 和 LinAGN2 LinAGN3 上的相關聯。
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13.  還原 LinAGN1_Cert 和 LinAGN2_Cert LinAGN3 上。 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
14.  Grant the logins associated with LinAG1 and LinAGN2 permission to connect to the endpoint on LinAGN3.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>建立可用性群組

本章節將說明如何使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)](SSMS) 或 TRANSACT-SQL 來建立可用性群組的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。

### <a name="use-includessmanstudiofull-mdincludesssmanstudiofull-mdmd"></a>使用 [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]

本節說明如何建立外部的叢集類型 AG SSMS 使用新增可用性群組精靈。

1.  在 SSMS 中，展開  **Alwayson 高可用性**，以滑鼠右鍵按一下**可用性群組**，然後選取**新增可用性群組精靈**。

2.  在 簡介 對話方塊中，按一下 **下一步**。

3.  在 [指定可用性群組選項] 對話方塊中，輸入可用性群組的名稱，然後選取叢集類型外部或無下拉式清單中。 將部署 Pacemaker 時，應該使用外部。 「 無 」 的特殊案例，例如讀取向外延展。選取資料庫層級的健全狀況偵測的選項是選擇性的。 如需有關這個選項的詳細資訊，請參閱[可用性群組資料庫層級的健全狀況偵測容錯移轉選項](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md)。 按一下 **[下一步]**。

    ![](./media/sql-server-linux-create-availability-group/image3.png)

4.  在 [選取資料庫] 對話方塊中，選取要參與 AG 的資料庫。 每個資料庫必須具備完整備份，才能將它新增到 AG。 按一下 **[下一步]**。

5.  在 指定複本 對話方塊中，按一下 **將複本加入**。

6.  在 [連線到伺服器] 對話方塊中，輸入 Linux 執行個體名稱[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，將次要複本，以及要連接的認證。 按一下 **[連接]**。

7.  重複前兩個步驟將會包含只設定複本或另一個次要複本之執行個體。

8.  所有的三個執行個體現在應該會顯示在 [指定複本] 對話方塊。 如果使用叢集類型的外部，次要複本將成為次要資料庫，則為 true，請確定可用性模式與相符的主要複本，而且容錯移轉模式已設為外部。 對於只設定複本，選取組態的僅限可用性模式。

    下列範例會示範兩個複本、 叢集類型的外部，以及設定專用的複本與 AG。

    ![](./media/sql-server-linux-create-availability-group/image4.png)

    下列範例顯示包含兩個複本 AG、 None、 以及設定唯讀複本的叢集類型。

    ![](./media/sql-server-linux-create-availability-group/image5.png)

9.  如果您想要變更的備份喜好設定，請按一下 [備份喜好設定] 索引標籤上。如需有關備份喜好設定與 Ag 的詳細資訊，請參閱[可用性複本上的設定備份](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)。

10. 如果使用可讀取的次要資料庫，或在叢集中建立 AG 輸入的無向外延展讀取，您可以藉由選取 [接聽程式] 索引標籤建立接聽程式。也可以稍後加入接聽程式。 若要建立接聽程式，請選擇選項**建立可用性群組接聽程式**並輸入名稱、 TCP/IP 通訊埠，以及是否要使用靜態或自動指派的 DHCP IP 位址。 請記住，ag 叢集類型為 None，IP 應該是靜態的並設定為主要伺服器的 IP 位址。

    ![](./media/sql-server-linux-create-availability-group/image6.png)

11. 如果可讀取的情況下建立接聽程式時，SSMS 17.3 或更新版本可讓唯讀路由精靈中的建立。 它也可以加入稍後透過 SSMS 或 TRANSACT-SQL。 若要新增唯讀路由現在：

    a.  選取唯讀路由索引標籤。

    b.  輸入 Url，唯讀複本。 這些 Url 如下的端點，不過它們會使用執行個體，而不是端點的連接埠。

    c.  選取每個 URL，然後從底部，選取 可讀取的複本。 多重選取，請按住 shift 鍵或按一下拖曳。

12. 按一下 **[下一步]**。

13. 選擇如何將初始化次要複本。 預設值是使用[自動植入](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md)，這需要參與 AG 的所有伺服器上的相同路徑。 您也可以讓精靈進行備份、 複製和還原 （第二個選項;）將它加入，如果您有手動備份、 複製，並在複本上的資料庫的還原 （第三個選項;）或更新版本加入資料庫 （最後一個選項）。 如同憑證，如果您是以手動方式進行備份，並將其複製，必須設定其他複本上的備份檔案的權限。 按一下 **[下一步]**。

14. 在 [驗證] 對話方塊中，如果所有項目不會傳回成功的顯示，調查。 某些警告是在可接受並不嚴重，例如，如果您未建立接聽程式。 按一下 **[下一步]**。

15. 在 摘要 對話方塊中，按一下 **完成**。 建立 AG 的程序將立即開始。

16. AG 建立完成後，按一下**關閉**的結果。 您現在可以看到 AG 複本中的動態管理檢視，以及在 SSMS 中的 [Alwayson 高可用性] 資料夾底下。

### <a name="use-transact-sql"></a>使用 TRANSACT-SQL

此區段顯示建立使用 TRANSACT-SQL AG 的範例。 AG 建立之後，可以設定接聽程式和唯讀路由。 AG 本身可以利用修改`ALTER AVAILABILITY GROUP`，但變更叢集類型中無法完成[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 如果您不打算 AG 建立與外部叢集類型，您必須將它刪除，並重新建立叢集類型為 None。 詳細資訊和其他選項，請參閱下列連結：

-   [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)
-   [ALTER AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [設定唯讀路由的可用性群組 (SQL Server)](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [建立或設定可用性群組接聽程式 (SQL Server)](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one--two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>範例 1 – 2 個複本設定唯讀複本 （外部叢集類型）

這個範例示範如何建立兩個複本 AG 使用僅限設定的複本。

1.  將會包含完整讀取/寫入複本資料庫的主要複本的節點上執行。 這個範例會使用自動植入。

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
    
2.  在查詢視窗中連接到其他複本，執行下列命令以將複本加入 AG 並起始從主要至次要複本植入程序。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  在查詢視窗中連接到組態的唯一複本，請將它加入 AG 中。
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
   ```

#### <a name="example-two--three-replicas-with-read-only-routing-external-cluster-type"></a>範例二 – 三個複本的唯讀路由 （外部叢集類型）

這個範例示範三個完整的初始 AG 建立的一部分，則可以設定複本和如何唯讀路由。

1.  將會包含完整讀取/寫入複本資料庫的主要複本的節點上執行。 這個範例會使用自動植入。

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
    
    請注意此組態相關的幾件事：
    
    - *AGName*是可用性群組的名稱。
    - *DBName*是將可用性群組搭配使用的資料庫名稱。 它也可以是一份以逗號分隔的名稱。
    - *ListenerName*是與基礎伺服器/節點的任何不同的名稱。 它將會登錄在 DNS 連同*IPAddress*。
    - *IPAddress*是相關聯的 IP 位址*ListenerName*。 它也是唯一和不完全相同的伺服器/節點。 應用程式和終端使用者將會使用*ListenerName*或*IPAddress*連接到 AG。
    - *子網路遮罩*是子網路遮罩*IPAddress*; 例如，255.255.255.0。

2.  在查詢視窗中連接到其他複本，執行下列命令以將複本加入 AG 並起始從主要至次要複本植入程序。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  重複步驟 2 的第三個複本。

#### <a name="example-three--two-replicas-with-read-only-routing-none-cluster-type"></a>範例 3 – 兩個複本的唯讀路由 （無叢集類型）

此範例顯示使用無叢集類型的兩個複本組態的建立。 它用於讀取的標尺案例預期容錯移轉的位置。 這會建立的接聽程式實際的主要複本，以及唯讀路由，使用的循環配置資源的功能。

1.  將會包含完整讀取/寫入複本資料庫的主要複本的節點上執行。 這個範例會使用自動植入。

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
    - *PortOfEndpoint*所建立的端點使用通訊埠編號。
    - *PortOfInstance*的執行個體所使用的通訊埠編號[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。
    - *ListenerName*是不同的任何基礎的複本，但不是實際上會使用的名稱。
    - *PrimaryReplicaIPAddress*是主要複本的 IP 位址。
    - *子網路遮罩*是子網路遮罩*IPAddress*。 例如，255.255.255.0。
    
2.  將次要複本聯結至 AG，起始自動植入。
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-includessnoversion-mdincludesssnoversion-mdmd-login-and-permissions-for-pacemaker"></a>建立[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]登入和權限 Pacemaker

Pacemaker 高可用性叢集基礎[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]on Linux 需要存取[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]執行個體，以及本身的可用性群組的權限。 下列步驟會建立登入和相關聯的權限，以及說明如何登入的 Pacemaker 檔案[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。

1.  在查詢視窗中連接到第一個複本，執行下列作業：

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD '<StrongPassword>';
    
    GO
    
    GRANT VIEW SERVER STATE TO PMLogin;
    
    GO
    
    GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::<AGThatWasCreated> TO PMLogin;
    
    GO
    ```
    
2.  在節點 1 上輸入的命令 
    ```bash
    sudo emacs /var/opt/mssql/secrets/passwd
    ```
    
    這會開啟 Emacs 編輯器。
    
3.  在編輯器中輸入下列兩行：

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  按住 CTRL 鍵，然後按 X，然後 C 以結束並儲存檔案。

5.  Execute 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    若要鎖定的檔案。

6.  重複步驟 1-5 將做為複本的伺服器上。

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>（只有外部） Pacemaker 叢集中建立可用性群組資源

之後可用性中建立群組[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，指定外部的叢集類型時，必須在 Pacemaker，建立對應的資源。 有兩個資源相關聯的 AG: AG 本身和 IP 位址。 設定 IP 位址資源為選擇性，如果您未使用接聽程式的功能，但建議使用。

建立 AG 資源是資源的一種特殊的稱為複製。 AG 資源基本上都有複本上每個節點，而且有一個稱為主要的控制資源。 與裝載主要複本的伺服器，主要是相關聯。 次要複本 （規則或僅限 configuration） 會被視為從屬與可提升為主要在容錯移轉。

1.  使用下列語法建立 AG 資源：

    **Red Hat Enterprise Linux (RHEL) 和 Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> --master meta notify=true
    ```

    >[!NOTE]
    >RHEL 7.4 上，您可能會使用-主要的警告。 若要避免這個問題，請使用 `sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> master notify=true`
   
    **SUSE Linux Enterprise Server (SLES)**
    
    ```bash
    primitive <NameForAGResource> \
    ocf:mssql:ag \
    params ag_name="<AGName>" \
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
    
    其中*NameForAGResource*是 ag，指定到這個叢集資源的唯一名稱和*AGName* AG 所建立的名稱。
 
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
    
    其中*NameForIPResource*是 IP 資源的唯一名稱和*IPAddress*是指派給資源的靜態 IP 位址。 在 SLES，您也需要提供網路遮罩。 例如，255.255.255.0 會有值為 24 的*網路遮罩。*
    
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
    
    其中*NameForIPResource* IP 資源的名稱*NameForAGResource*名稱 AG 資源，如和 SLES， *NameForConstraint*的名稱條件約束。

4.  建立排序條件約束，以確保 AG 資源已啟動且在執行之前的 IP 位址。 共置條件約束所指的是排序的條件約束，而這會強制執行它。

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
    
    其中*NameForIPResource* IP 資源的名稱*NameForAGResource*名稱 AG 資源，如和 SLES， *NameForConstraint*的名稱條件約束。

## <a name="next-steps"></a>後續的步驟

在本教學課程中，您學到如何建立及設定可用性群組的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]on Linux。 您已了解如何以：
> [!div class="checklist"]
> * 啟用可用性群組。
> * 建立 AG 端點和憑證。
> * 使用[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)](SSMS) 或 TRANSACT-SQL 來建立 AG。
> * 建立[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]登入和 Pacemaker 權限。
> * 建立 AG Pacemaker 叢集中的資源。

大部分 AG 系統管理工作，包括升級和容錯移轉，請參閱：

> [!div class="nextstepaction"]
> [SQL Server on Linux 會操作 HA 可用性群組](sql-server-linux-availability-group-failover-ha.md)

