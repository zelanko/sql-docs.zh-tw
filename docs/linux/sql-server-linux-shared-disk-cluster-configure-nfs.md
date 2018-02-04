---
title: "設定容錯移轉叢集執行個體存放區 NFS-SQL Server on Linux |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 25bcc2fb0ddb60198208d88ce9c19be139d6ec2f
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2018
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>設定容錯移轉叢集執行個體-NFS-SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文說明如何在 Linux 上設定容錯移轉叢集執行個體 (FCI) 的 NFS 存放裝置。 

NFS 或網路檔案系統中，為共用磁碟 Linux 世界，但不是一的 Windows 中的常用方法。 類似於 iSCSI，NFS 可以設定或某種應用裝置或儲存體單位的伺服器上，只要符合 SQL Server 的存放裝置需求。

## <a name="important-nfs-server-information"></a>NFS 伺服器的重要資訊

裝載 NFS （在 Linux 伺服器或其他項目） 的來源必須使用/符合 4.2 版或更新版本。 舊版不適用於 SQL Server on Linux。

當設定 NFS 伺服器上共用資料夾，請確定它們會遵照這些方針的一般選項：
- `rw`以確保該資料夾可以是讀取和寫入
- `sync`若要確保保證寫入至資料夾
- 請勿使用`no_root_squash`做為選項; 它會被視為有安全性風險
- 請確認資料夾擁有完整權限 (777) 套用

請確定您的安全性標準會強制執行存取。 當設定資料夾，請確定只有參與 FCI 伺服器應該會看到 NFS 資料夾。 修改 /etc/exports 以 Linux 為基礎的 NFS 解決方案的範例如下所示資料夾限於 FCIN1 和 FCIN2。

![05 nfsacl][1]

## <a name="instructions"></a>Instructions

1. 選擇其中一個伺服器，為即將加入 FCI 組態中。 不論哪一個。 

2. 請檢查伺服器，可以看到 mount(s) NFS 伺服器上。

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer > 是您要使用的 NFS 伺服器的 IP 位址。

3. 系統資料庫或儲存在預設資料位置的任何項目，請遵循下列步驟。 否則，請跳至步驟 4。
 
   * 請確定 SQL Server 會停止您正在使用的伺服器上。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * 參數完全是超級使用者。 如果成功，則不會收到任何通知。

    ```bash
    sudo -i
    ```

   * Mssql 使用者參數。 如果成功，則不會收到任何通知。

    ```bash
    su mssql
    ```

   * 建立暫存目錄來儲存 SQL Server 資料和記錄檔。 如果成功，則不會收到任何通知。

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir > 資料夾的名稱。 下列範例會建立名為 /var/opt/mssql/tmp 的資料夾。

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * 將 SQL Server 資料和記錄檔複製到暫存目錄。 如果成功，則不會收到任何通知。
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > 是從上一個步驟的資料夾名稱。

   * 請確認檔案是目錄中。

    ```bash
    ls TempDir
    ```

    \<TempDir > 是從步驟 d 資料夾的名稱。

   * 從現有的 SQL Server 資料目錄刪除檔案。 如果成功，則不會收到任何通知。

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   * 請確認已刪除的檔案。 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * 輸入 exit，切換到以根使用者。

   * 掛接 NFS 共用的 SQL Server data 資料夾中。 如果成功，則不會收到任何通知。

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > 是您要使用的 NFS 伺服器的 IP 位址 

    \<FolderOnNFSServer > NFS 共用的名稱。 下列範例語法符合 NFS 資訊從步驟 2。

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * 請查看掛接成功發出掛接不使用任何參數。

    ```bash
    mount
    ```

    ![10 mountnoswitches][2]

   * 切換至 mssql 使用者。 如果成功，則不會收到任何通知。

    ```bash
    su mssql
    ```

   * 從暫存目錄 /var/opt/mssql/data 複製檔案。 如果成功，則不會收到任何通知。

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * 請確認檔案有。

    ```bash
    ls /var/opt/mssql/data
    ```

   * 輸入不是 mssql 結束 
    
   * 輸入不是 根的結束

   * 啟動 SQL Server。 如果所有項目已正確複製，並套用安全性是否正確，SQL Server 應該會顯示為已啟動。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * 建立測試安全性已正確設定資料庫。 下列範例會顯示完成後透過 TRANSACT-SQL;它可以透過 SSMS 來完成。
 
    ![CreateTestdatabase][3]

   * 停止 SQL Server 並確認它已關閉。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * 如果您沒有建立任何其他 NFS 掛接，請取消掛接共用。 如果您是，未卸載。

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > 是您要使用的 NFS 伺服器的 IP 位址

    \<FolderOnNFSServer > NFS 共用的名稱

    \<FolderMountedIn > 是上一個步驟中建立的資料夾。 

4. 進行的非系統資料庫，例如使用者資料庫或備份，請遵循下列步驟。 如果只使用的預設位置，請跳至步驟 5。

   * 參數是超級使用者。 如果成功，則不會收到任何通知。

    ```bash
    sudo -i
    ```

   * 建立將 SQL Server 所使用的資料夾。 

    ```bash
    mkdir <FolderName>
    ```

    \<資料夾名稱 > 資料夾的名稱。 將資料夾的完整路徑必須指定如果不在正確的位置。 下列範例會建立名為 /var/opt/mssql/userdata 的資料夾。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * 掛接 NFS 共用，在上一個步驟中建立的資料夾中。 如果成功，則不會收到任何通知。

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > 是您要使用的 NFS 伺服器的 IP 位址

    \<FolderOnNFSServer > NFS 共用的名稱

    \<FolderToMountIn > 是上一個步驟中建立的資料夾。 以下是範例。 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * 請查看掛接成功發出掛接不使用任何參數。
  
   * 輸入 exit，不再是超級使用者。

   * 若要測試，請在該資料夾中建立的資料庫。 如下所示的範例會使用 sqlcmd 建立資料庫，切換至該內容，確認檔案存在於作業系統層級，然後再刪除暫存位置。 您可以使用 SSMS。

    ![15-createtestdatabase][4]
 
   * 取消掛接共用 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > 是您要使用的 NFS 伺服器的 IP 位址
    
    \<FolderOnNFSServer > NFS 共用的名稱

    \<FolderMountedIn > 是上一個步驟中建立的資料夾。 以下是範例。 
 
5. 重複步驟，在其他節點上。


## <a name="next-steps"></a>後續的步驟

[設定容錯移轉叢集執行個體的 SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
