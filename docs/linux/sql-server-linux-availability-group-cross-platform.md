---
title: 設定 Windows 和 Linux 上的 SQL Server Always On 可用性群組
description: 使用 Windows 和 Linux 上的複本設定 SQL Server Always On 可用性群組。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 01/31/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: f6758760d8ea73d9ec0ac95a0e824a0fd46a6dbb
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68045193"
---
# <a name="configure-sql-server-always-on-availability-group-on-windows-and-linux-cross-platform"></a>設定 Windows 和 Linux 上的 SQL Server Always On 可用性群組 (跨平台)

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

本文說明使用 Windows 伺服器上某個複本和 Linux 伺服器上另一個複本建立 Always On 可用性群組 (AG) 的步驟。 由於複本位於不同的作業系統上，因此這是一種跨平台設定。 您可將此設定用於從某個平台移轉至其他平台或災害復原 (DR)。 此設定不支援高可用性，因為沒有可管理跨平台設定的叢集解決方案。 

![混合式 NONE](./media/sql-server-linux-availability-group-overview/image1.png)

在繼續之前，您應該先熟悉 Windows 和 Linux 上的 SQL Server 執行個體安裝和設定。 

## <a name="scenario"></a>狀況

在此案例中，兩部伺服器位於不同的作業系統。 主要複本裝載在名為 `WinSQLInstance` 的 Windows Server 2016。 次要複本裝載在名為 `LinuxSQLInstance` 的 Linux 伺服器。

## <a name="configure-the-ag"></a>設定 AG 

建立 AG 的步驟與建立用於讀取級別工作負載 AG 步驟相同。 AG 叢集類型為 NONE，因為沒有叢集管理員。 

   >[!NOTE]
   >本文中指令碼會使用角括弧 `<` 和 `>` 來識別您要依據環境取代的值。 指令碼本身不需要角括弧。 

1. 在 Windows Server 2016 上安裝 SQL Server 2017、從 SQL Server 設定管理員啟用 Always On 可用性群組，以及設定混合模式驗證。 

   >[!TIP]
   >如果您要在 Azure 中驗證此解決方案，請將這兩部伺服器放在相同的可用性設定組中，確保它們會在資料中心內區隔開來。 

   **啟用可用性群組**

   如需指示，請參閱[啟用和停用 Always On 可用性群組 (SQL Server)](../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)。

   ![啟用可用性群組](./media/sql-server-linux-availability-group-cross-platform/1-sqlserver-configuration-manager.png)

   SQL Server 設定管理員會注意到電腦不是容錯移轉叢集中的節點。 

   啟用可用性群組之後，請重新啟動 SQL Server。

   **設定混合模式驗證**

   如需指示，請參閱[變更伺服器驗證模式](../database-engine/configure-windows/change-server-authentication-mode.md#SSMSProcedure)。

1. 在 Linux 上安裝 SQL Server 2017。 如需指示，請參閱[在 Linux 上安裝 SQL Server](sql-server-linux-setup.md)。 透過 mssql-conf 啟用 `hadr`。

   若要從殼層提示透過 mssql-conf 啟用 `hadr`，請發出下列命令：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
   ```

   啟用 `hadr` 之後，請重新啟動 SQL Server 執行個體。  

   下圖顯示此完整步驟。

   ![啟用可用性群組 Linux](./media/sql-server-linux-availability-group-cross-platform/2-sqlserver-linux-set-hadr.png)

1. 在兩部伺服器上設定 hosts 檔案，或向 DNS 註冊伺服器名稱。

1. 在 Windows 和 Linux 上開啟 TPC 1433 和 5022 的防火牆連接埠。

1. 在主要複本上，建立資料庫登入和密碼。

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   ```

1. 在主要複本上，建立主要金鑰和憑證，然後使用私密金鑰來備份憑證。

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

1. 將憑證和私密金鑰複製到 Linux 伺服器 (次要複本) 的 `/var/opt/mssql/data` 位置。 您可以使用 `pscp`，將檔案複製到 Linux 伺服器。 

1. 將私密金鑰與憑證的群組和擁有權設定為 `mssql:mssql`。

   下列指令碼會設定這些檔案的群組和擁有權。 

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.pvk
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.cer
   ```

   下圖已正確設定憑證與金鑰的擁有權和群組。

   ![啟用可用性群組 Linux](./media/sql-server-linux-availability-group-cross-platform/3-cert-key-owner-group.png)


1. 在次要複本上，建立資料庫登入和密碼，然後建立主要金鑰。

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<M@st3rKeyP@55w0rD!>'
   GO
   ```

1. 在次要複本上，還原您複製到 `/var/opt/mssql/data` 的憑證。 

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

1. 在主要複本上，建立端點。

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
   >您必須為接聽程式 TCP 通訊埠開啟防火牆。 在前一段指令碼中，連接埠為 5022。 使用任何可用的 TCP 通訊埠。 

1. 在次要複本上，建立端點。 在次要複本上重複前一段指令碼，以建立端點。 

1. 在主要複本上，建立 `CLUSTER_TYPE = NONE` 的 AG。 範例指令碼會使用 `SEEDING_MODE = AUTOMATIC` 來建立 AG。 

   >[!NOTE]
   >當 SQL Server 的 Windows 執行個體使用不同資料和記錄檔路徑時，自動植入 SQL Server 的 Linux 執行個體會失敗，因為這些路徑不存在於次要複本上。 若要針對跨平台 AG 使用下列指令碼，資料庫必須具備 Windows 伺服器上資料和記錄檔的相同路徑。 或者，您可以更新指令碼以設定 `SEEDING_MODE = MANUAL`，然後使用 `NORECOVERY` 來備份和還原資料庫，以植入資料庫。 
   >
   >上述行為適用於 Azure Marketplace 映像。 
   >
   >如需自動植入的詳細資訊，請參閱[自動植入 - 磁碟配置](../database-engine/availability-groups/windows/automatic-seeding-secondary-replicas.md#disklayout)。 

   執行指令碼之前，請先更新 AG 的值。

      * 將 `<WinSQLInstance>` 取代為主要複本 SQL Server 執行個體的伺服器名稱。

      * 將 `<LinuxSQLInstance>` 取代為次要複本 SQL Server 執行個體的伺服器名稱。 

   若要建立 AG，請更新值，並在主要複本上執行指令碼。  

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
   
   如需詳細資訊，請參閱 [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)。

1. 在次要複本上，加入 AG。

   ```sql
   ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE)
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE
   GO
   ```

1. 建立 AG 的資料庫。 範例步驟會使用名為 `<TestDB>` 的資料庫。 如果您使用自動植入，請為資料和記錄檔設定相同的路徑。 

   執行指令碼之前，請先更新資料庫的值。

      * 將 `<TestDB>` 取代為您的資料庫名稱。

      * 將 `<F:\Path>` 取代為您的資料庫和記錄檔路徑。 針對資料庫和記錄檔使用相同的路徑。 

      您也可以使用預設路徑。 

    若要建立您的資料庫，請執行指令碼。 

   ```sql
   CREATE DATABASE [<TestDB>]
      CONTAINMENT = NONE
     ON  PRIMARY ( NAME = N'<TestDB>', FILENAME = N'<F:\Path>\<TestDB>.mdf')
     LOG ON ( NAME = N'<TestDB>_log', FILENAME = N'<F:\Path>\<TestDB>_log.ldf')
   GO
   ```

1. 完整備份資料庫。 

1. 如果您不是使用自動植入，請在次要複本 (Linux) 伺服器上還原資料庫。 [使用備份與還原將 SQL Server 資料庫從 Windows 移轉至 Linux](sql-server-linux-migrate-restore-database.md)。 在次要複本上還原資料庫 `WITH NORECOVERY`。 

1. 將資料庫新增至 AG。 更新範例指令碼。 將 `<TestDB>` 取代為您的資料庫名稱。 在主要複本上，執行 SQL 查詢以將資料庫新增至 AG。

   ```sql
   ALTER AG [ag1] ADD DATABASE <TestDB>
   GO
   ```

1. 驗證資料庫是否開始填入次要複本。 

## <a name="fail-over-the-primary-replica"></a>容錯移轉主要複本

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

本文複習建立跨平台 AG 以支援移轉或讀取級別工作負載的步驟。 本文可用於手動災害復原， 同時說明如何容錯移轉 AG。 跨平台 AG 會使用 `NONE` 叢集類型，且不支援高可用性，因為跨平台沒有叢集工具。 

## <a name="next-steps"></a>後續步驟

[Always On 可用性群組概觀](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

[適用於 Linux 部署的 SQL Server 可用性基本概念](sql-server-linux-ha-basics.md)
