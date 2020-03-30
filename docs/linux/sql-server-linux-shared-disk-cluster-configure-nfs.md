---
title: 設定 NFS 儲存體 FCI - Linux 上的 SQL Server
description: 了解如何使用 Linux 上的 SQL Server NFS 儲存體來設定容錯移轉叢集執行個體 (FCI)。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 35f6dc79756c192419dbe3a8962d5dcdfeea8aef
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "75558333"
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>設定容錯移轉叢集執行個體 - NFS - Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文章說明如何針對 Linux 上的容錯移轉叢集執行個體 (FCI) 設定 NFS 儲存體。 

NFS (或網路檔案系統) 是在 Linux (而非 Windows) 的領域中共用磁碟的常見方法。 NFS 和 iSCSI 類似，可以在伺服器或某種設備或儲存體單位上設定，前提是它必須符合 SQL Server 的儲存體需求。

## <a name="important-nfs-server-information"></a>重要的 NFS 伺服器資訊

裝載 NFS 的來源 (無論是 Linux 伺服器還是其他來源) 必須使用/符合 4.2 版或更新版本。 較舊的版本將無法搭配 Linux 上的 SQL Server 運作。

設定要在 NFS 伺服器上共用的資料夾時，請確保它們會遵循這些指導方針一般選項：
- `rw` 以確保該資料夾可以被讀取及寫入
- `sync` 以保證能寫入該資料夾
- 請不要使用 `no_root_squash` 作為選項；它被視為安全性風險
- 確定已將完整權限 (777) 套用至該資料夾

確定您的安全性標準已針對存取強制執行。 設定資料夾時，請確定只有參與 FCI 的伺服器才能看見 NFS 資料夾。 下面顯示 Linux 型 NFS 解決方案上已修改的 /etc/exports 範例，其中資料夾已限制為 FCIN1 和 FCIN2。

![05-nfsacl][1]

## <a name="instructions"></a>Instructions

1. 選擇將會參與 FCI 設定的其中一部伺服器。 任何一部伺服器都可以。 

2. 檢查該伺服器可以看見 NFS 伺服器上的裝載。

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer> 是您將會使用之 NFS 伺服器的 IP 位址。

3. 針對系統資料庫或任何儲存在預設資料位置的內容，請遵循這些步驟。 否則，請跳到步驟 4。
 
   * 確定您正在處理之伺服器上的 SQL Server 已經停止。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * 完全切換成超級使用者。 如果成功，您將不會收到任何通知。

    ```bash
    sudo -i
    ```

   * 切換成 mssql 使用者。 如果成功，您將不會收到任何通知。

    ```bash
    su mssql
    ```

   * 建立暫存目錄來儲存 SQL Server 資料和記錄檔。 如果成功，您將不會收到任何通知。

    ```bash
    mkdir <TempDir>
    ```

    \<TempDir> 是資料夾的名稱。 下列範例會建立名為 /var/opt/mssql/tmp 的資料夾。

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * 將 SQL Server 資料和記錄檔複製到暫存目錄。 如果成功，您將不會收到任何通知。
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir> 是上一個步驟中的資料夾名稱。

   * 確認檔案位於目錄中。

    ```bash
    ls TempDir
    ```

    \<TempDir> 是步驟 d 中資料夾的名稱。

   * 將檔案從現有的 SQL Server 資料目錄中刪除。 如果成功，您將不會收到任何通知。

    ```bash
    rm - f /var/opt/mssql/data/*
    ```

   * 確認檔案已被刪除。 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * 輸入 exit 以切換回根使用者。

   * 將 NFS 共用裝載在 SQL Server 資料夾中。 如果成功，您將不會收到任何通知。

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer> 是您將會使用之 NFS 伺服器的 IP 位址 

    \<FolderOnNFSServer> 是 NFS 共用的名稱。 下列範例語法會比對來自步驟 2 的 NFS 資訊。

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * 透過發出不含參數的 mount 來檢查掛接是否成功。

    ```bash
    mount
    ```

    ![10-mountnoswitches][2]

   * 切換成 mssql 使用者。 如果成功，您將不會收到任何通知。

    ```bash
    su mssql
    ```

   * 複製暫存目錄 /var/opt/mssql/data 中的檔案。 如果成功，您將不會收到任何通知。

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * 驗證檔案存在。

    ```bash
    ls /var/opt/mssql/data
    ```

   * 輸入 exit 以退出 mssql 使用者 
    
   * 輸入 exit 以退出根使用者

   * 啟動 SQL Server。 如果所有內容皆已正確複製，並正確地套用安全性，SQL Server 應該會顯示為已啟動。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * 建立資料庫以測試已正確設定安全性。 下列範例顯示透過 Transact-SQL 來完成此作業；您也可以透過 SSMS 來完成它。
 
    ![CreateTestdatabase][3]

   * 停止 SQL Server 並驗證它已關閉。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * 如果您不打算建立任何其他 NFS 裝載，請將共用卸載。 如果您打算那麼做，請不要卸載。

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer> 是您將會使用之 NFS 伺服器的 IP 位址

    \<FolderOnNFSServer> 是 NFS 共用的名稱

    \<FolderMountedIn> 是在上一個步驟中所建立的資料夾。 

4. 針對系統資料庫以外的其他內容 (例如，使用者資料庫或備份)，請遵循這些步驟。 如果僅使用預設位置，請跳到步驟 5。

   * 切換成超級使用者。 如果成功，您將不會收到任何通知。

    ```bash
    sudo -i
    ```

   * 建立 SQL Server 將會使用的資料夾。 

    ```bash
    mkdir <FolderName>
    ```

    \<FolderName> 是資料夾的名稱。 如果資料夾不是位於正確的位置，則必須指定其完整路徑。 下列範例會建立名為 /var/opt/mssql/userdata 的資料夾。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * 將 NFS 共用裝載在上一個步驟中所建立的資料夾中。 如果成功，您將不會收到任何通知。

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer> 是您將會使用之 NFS 伺服器的 IP 位址

    \<FolderOnNFSServer> 是 NFS 共用的名稱

    \<FolderToMountIn> 是在上一個步驟中所建立的資料夾。 以下為範例。 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * 透過發出不含參數的 mount 來檢查掛接是否成功。
  
   * 輸入 exit 來退出超級使用者。

   * 若要進行測試，請在該資料夾中建立資料庫。 下列範例使用 sqlcmd 來建立資料庫，將內容切換至它，驗證檔案存在於 OS 層級，然後刪除暫存位置。 您可以使用 SSMS。

    ![15-createtestdatabase][4]
 
   * 將共用取消掛接 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer> 是您將會使用之 NFS 伺服器的 IP 位址
    
    \<FolderOnNFSServer> 是 NFS 共用的名稱

    \<FolderMountedIn> 是在上一個步驟中所建立的資料夾。 以下為範例。 
 
5. 對其他節點重複這些步驟。


## <a name="next-steps"></a>後續步驟

[設定容錯移轉叢集執行個體 - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
