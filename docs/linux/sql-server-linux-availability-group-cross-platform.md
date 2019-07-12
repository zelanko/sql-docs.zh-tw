---
title: 設定 SQL Server Always On 可用性群組，在 Windows 和 Linux 上
description: 設定 SQL Server 可用性群組與在 Windows 和 Linux 上的複本。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 01/31/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 08e30f19c210b0edeb8183603b4107a83393aae7
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834266"
---
# <a name="configure-sql-server-always-on-availability-group-on-windows-and-linux-cross-platform"></a>設定 SQL Server Always On 可用性群組上 Windows 和 Linux （跨平台）

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

這篇文章說明建立 Windows 伺服器上的一個複本和 Linux 伺服器上的其他複本的 Alwayson 可用性群組 (AG) 的步驟。 由於複本位於不同的作業系統，此設定會是跨平台。 使用此組態移轉到另一個平台或災害復原 (DR)。 此組態不支援高可用性，因為沒有任何叢集方案，以便管理跨平台設定。 

![混合式無](./media/sql-server-linux-availability-group-overview/image1.png)

在繼續之前，您應該熟悉在 Windows 和 Linux 上的 SQL Server 執行個體的安裝和設定。 

## <a name="scenario"></a>狀況

在此案例中，兩部伺服器位於不同的作業系統。 名為 Windows Server 2016`WinSQLInstance`裝載主要複本。 在 Linux 伺服器名為`LinuxSQLInstance`裝載次要複本。

## <a name="configure-the-ag"></a>設定 AG 

建立 AG 的步驟是建立讀取規模的工作負載的 AG 的步驟相同。 AG 叢集類型是 NONE，因為沒有叢集管理員。 

   >[!NOTE]
   >這篇文章中的指令碼，為角括號`<`和`>`識別您需要將您的環境的值。 角括號本身並不需要指令碼。 

1. Windows Server 2016 上安裝 SQL Server 2017 中，啟用 Always On 可用性群組從 「 SQL Server 組態管理員 」 中，並設定混合的模式驗證。 

   >[!TIP]
   >如果您要驗證此解決方案在 Azure 中的，置於同一個可用性設定，以確保會在資料中心分隔這兩部伺服器。 

   **啟用可用性群組**

   如需相關指示，請參閱 <<c0> [ 啟用和停用 Alwayson 可用性群組 (SQL Server)](../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)。

   ![啟用可用性群組](./media/sql-server-linux-availability-group-cross-platform/1-sqlserver-configuration-manager.png)

   SQL Server 組態管理員會註明的電腦不是容錯移轉叢集中的節點。 

   啟用可用性群組之後，重新啟動 SQL Server。

   **設定混合的模式驗證**

   如需相關指示，請參閱 <<c0> [ 變更伺服器驗證模式](../database-engine/configure-windows/change-server-authentication-mode.md#SSMSProcedure)。

1. 在 Linux 上安裝 SQL Server 2017。 如需相關指示，請參閱 <<c0> [ 安裝 SQL Server](sql-server-linux-setup.md)。 啟用`hadr`透過 mssql 設定

   若要啟用`hadr`mssql conf 殼層提示字元中，透過發出下列命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
   ```

   啟用後`hadr`，重新啟動 SQL Server 執行個體。  

   下圖顯示這個完成的步驟。

   ![啟用可用性群組的 Linux](./media/sql-server-linux-availability-group-cross-platform/2-sqlserver-linux-set-hadr.png)

1. 設定兩部伺服器上的 hosts 檔案，或使用 DNS 登錄的伺服器名稱。

1. 開啟防火牆連接埠 TPC 1433 和 5022 上 Windows 和 Linux。

1. 在主要複本上建立資料庫登入和密碼。

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   ```

1. 在主要複本，建立主要金鑰和憑證，然後使用私密金鑰備份憑證。

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
   BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
       );
   GO
   ```

1. 在中將憑證和私密金鑰複製到 Linux 伺服器 （次要複本） `/var/opt/mssql/data`。 您可以使用`pscp`將檔案複製到 Linux 伺服器。 

1. 將群組和擁有權的私用金鑰和憑證，以設定`mssql:mssql`。

   下列指令碼設定的群組和檔案的擁有權。 

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.pvk
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.cer
   ```

   在下列圖表中，擁有權和群組已為正確的憑證和金鑰。

   ![啟用可用性群組的 Linux](./media/sql-server-linux-availability-group-cross-platform/3-cert-key-owner-group.png)


1. 在次要複本上建立資料庫登入和密碼，並建立主要金鑰。

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<M@st3rKeyP@55w0rD!>'
   GO
   ```

1. 在次要複本上還原的憑證複製到`/var/opt/mssql/data`。 

   ```sql
   CREATE CERTIFICATE dbm_certificate   
       AUTHORIZATION dbm_user
       FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
       WITH PRIVATE KEY (
       FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
       DECRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
   )
   GO
   ```

1. 在主要複本上建立端點。

   ```sql
   CREATE ENDPOINT [Hadr_endpoint]
       AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = 5022)
       FOR DATA_MIRRORING (
           ROLE = ALL,
           AUTHENTICATION = CERTIFICATE dbm_certificate,
           ENCRYPTION = REQUIRED ALGORITHM AES
           );
   ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
   GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login]
   GO
   ```

   >[!IMPORTANT]
   >防火牆必須開啟 TCP 通訊埠接聽程式。 在上述指令碼中，連接埠為 5022。 使用任何可用的 TCP 連接埠。 

1. 在次要複本上建立的端點。 重複上述的指令碼，以建立端點在次要複本上。 

1. 在主要複本上建立與 AG `CLUSTER_TYPE = NONE`。 範例指令碼會使用`SEEDING_MODE = AUTOMATIC`建立 AG。 

   >[!NOTE]
   >當 SQL Server 的 Windows 執行個體資料和記錄檔，自動植入到 SQL Server 的 Linux 執行個體的失敗，因為這些路徑不存在的次要複本上，使用不同的路徑。 若要使用下列指令碼的跨平台 AG，資料庫會要求相同的路徑，為 Windows 伺服器上的資料和記錄檔。 或者，您也可以更新指令碼來設定`SEEDING_MODE = MANUAL`，然後備份並還原資料庫與`NORECOVERY`植入資料庫。 
   >
   >此行為適用於 Azure Marketplace 映像。 
   >
   >如需有關自動植入的詳細資訊，請參閱 <<c0> [ 自動植入的磁碟配置](../database-engine/availability-groups/windows/automatic-seeding-secondary-replicas.md#disklayout)。 

   執行指令碼之前，請 ag 中更新這些值。

      * 取代`<WinSQLInstance>`與主要複本的 SQL Server 執行個體的伺服器名稱。

      * 取代`<LinuxSQLInstance>`次要複本的 SQL Server 執行個體的伺服器名稱。 

   若要建立 AG，更新的值，並在主要複本上執行指令碼。  

   ```sql
   CREATE AVAILABILITY GROUP [ag1]
       WITH (CLUSTER_TYPE = NONE)
       FOR REPLICA ON
           N'<WinSQLInstance>' 
        WITH (
           ENDPOINT_URL = N'tcp://<WinSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            SEEDING_MODE = AUTOMATIC,
            FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
           N'<LinuxSQLInstance>' 
       WITH (
            ENDPOINT_URL = N'tcp://<LinuxSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
           SEEDING_MODE = AUTOMATIC,
           FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
           )
   GO
   ```
   
   如需詳細資訊，請參閱 < [CREATE AVAILABILITY GROUP & Amp;#40;transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md)。

1. 在次要複本加入 AG。

   ```sql
   ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE)
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE
   GO
   ```

1. 建立資料庫的 ag。 範例步驟會使用名為資料庫`<TestDB>`。 如果您使用自動植入，請設定資料和記錄檔的相同路徑。 

   執行指令碼之前，請更新您的資料庫的值。

      * 取代`<TestDB>`與您的資料庫名稱。

      * 取代`<F:\Path>`您資料庫和記錄檔的路徑。 使用資料庫和記錄檔相同的路徑。 

      您也可以使用的預設路徑。 

    若要建立您的資料庫，執行指令碼。 

   ```sql
   CREATE DATABASE [<TestDB>]
      CONTAINMENT = NONE
     ON  PRIMARY ( NAME = N'<TestDB>', FILENAME = N'<F:\Path>\<TestDB>.mdf')
     LOG ON ( NAME = N'<TestDB>_log', FILENAME = N'<F:\Path>\<TestDB>_log.ldf')
   GO
   ```

1. 進行完整備份的資料庫。 

1. 如果您不使用自動植入，請還原次要複本 (Linux) 伺服器上的資料庫。 [從 Windows 的 SQL Server 資料庫移轉至 Linux 使用 backup 和 restore](sql-server-linux-migrate-restore-database.md)。 將資料庫還原`WITH NORECOVERY`次要複本上。 

1. 將資料庫加入至 AG。 更新的範例指令碼。 取代`<TestDB>`與您的資料庫名稱。 在主要複本上，執行 SQL 查詢，以將資料庫加入至 AG。

   ```sql
   ALTER AG [ag1] ADD DATABASE <TestDB>
   GO
   ```

1. 確認次要複本上，會開始填入資料庫。 

## <a name="fail-over-the-primary-replica"></a>容錯移轉的主要複本

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

這篇文章會檢閱建立以支援移轉或讀取級別的工作負載的跨平台 AG 的步驟。 它可以用手動的災害復原。 它也會說明如何將 AG 容錯移轉。 跨平台 AG 會使用叢集類型`NONE`，而且不支援高可用性，因為沒有任何叢集工具跨平台。 

## <a name="next-steps"></a>後續步驟

[Alwayson 可用性群組概觀](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

[Linux 部署的 SQL Server 可用性基本概念](sql-server-linux-ha-basics.md)
