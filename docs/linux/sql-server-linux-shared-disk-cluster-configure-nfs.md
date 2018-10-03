---
title: 設定容錯移轉叢集執行個體存放區 NFS-Linux 上的 SQL Server |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 63ebce5a8e78829cbdad8dede0be7cb9285c7c37
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788453"
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>設定容錯移轉叢集執行個體-NFS-Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章說明如何在 Linux 上設定容錯移轉叢集執行個體 (FCI) 的 NFS 儲存體。 

NFS 或網路檔案系統，是共用磁碟，在 Linux 領域，但沒有 Windows 其中一個常見的方法。 類似於 iSCSI，NFS 可以設定某種應用裝置或儲存體單位或的伺服器上，只要它符合 SQL Server 的儲存體需求。

## <a name="important-nfs-server-information"></a>NFS 伺服器的重要資訊

裝載 NFS （在 Linux 伺服器或其他項目） 的來源必須使用/遵守 4.2 版或更新版本。 較早版本不適用於 SQL Server on Linux。

設定 NFS 伺服器上共用資料夾，請確定它們遵循這些指導方針的一般選項：
- `rw` 若要確認資料夾可以是讀取和寫入
- `sync` 若要確保保證的寫入至資料夾
- 請勿使用`no_root_squash`選擇; 它會被視為安全性風險
- 請確認資料夾擁有完整權限 (777) 套用

請確定您的安全性標準會強制執行存取。 當設定的資料夾，請確定只有 FCI 中參與的伺服器應該會看到 NFS 資料夾。 修改過的 /etc/exports 上以 Linux 為基礎的 NFS 解決方案的範例如下所示其中資料夾是限制為 FCIN1 及 FCIN2。

![05 nfsacl][1]

## <a name="instructions"></a>Instructions

1. 您可以選擇其中一個將參與的伺服器 FCI 組態中。 不論哪一個。 

2. 請檢查伺服器，可以查看 mount(s) NFS 伺服器上。

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer > 是您要使用的 NFS 伺服器的 IP 位址。

3. 系統資料庫或儲存在預設資料位置的任何項目，請遵循下列步驟。 否則，請跳至步驟 4。
 
   * 請確定 SQL Server 已停止您正在使用的伺服器上。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * 全面轉換成是超級使用者的參數。 如果成功，則不會收到任何通知。

    ```bash
    sudo -i
    ```

   * 要使用 mssql 使用者的參數。 如果成功，則不會收到任何通知。

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

   * 確認目錄中的檔案。

    ```bash
    ls TempDir
    ```

    \<TempDir > 會從步驟 d 資料夾的名稱。

   * 從現有的 SQL Server 資料目錄中刪除檔案。 如果成功，則不會收到任何通知。

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   * 請確認已刪除的檔案。 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * 若要切換回根使用者的輸入 exit。

   * 掛接 NFS 共用的 SQL Server data 資料夾中。 如果成功，則不會收到任何通知。

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > 是您要使用的 NFS 伺服器的 IP 位址 

    \<FolderOnNFSServer > NFS 共用的名稱。 下列的範例語法會比對步驟 2 中的 NFS 資訊。

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * 請確認掛接已成功發出掛接不使用任何參數。

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

   * 啟動 SQL Server。 如果所有項目已正確地複製和套用的安全性是否正確，SQL Server 應該會顯示為已啟動。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * 建立資料庫來測試安全性已正確設定。 下列範例顯示完成後透過 Transact SQL;它可以透過 SSMS 來完成。
 
    ![CreateTestdatabase][3]

   * 停止 SQL Server，並確認它已關閉。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * 如果您未建立任何其他的 NFS 掛接，取消掛接共用。 如果您是，請勿卸載。

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > 是您要使用的 NFS 伺服器的 IP 位址

    \<FolderOnNFSServer > 是的 NFS 共用名稱

    \<FolderMountedIn > 是上一個步驟中建立的資料夾。 

4. 項目以外的系統資料庫，例如使用者資料庫或備份，請遵循下列步驟。 如果僅使用預設位置，請跳至步驟 5。

   * 切換到是超級使用者。 如果成功，則不會收到任何通知。

    ```bash
    sudo -i
    ```

   * 建立將由 SQL Server 的資料夾。 

    ```bash
    mkdir <FolderName>
    ```

    \<資料夾名稱 > 是資料夾的名稱。 資料夾的完整路徑必須指定如果不在正確的位置。 下列範例會建立名為 /var/opt/mssql/userdata 的資料夾。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * 掛接在上一個步驟中建立的資料夾中的 NFS 共用。 如果成功，則不會收到任何通知。

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > 是您要使用的 NFS 伺服器的 IP 位址

    \<FolderOnNFSServer > 是的 NFS 共用名稱

    \<FolderToMountIn > 是上一個步驟中建立的資料夾。 以下是範例。 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * 請確認掛接已成功發出掛接不使用任何參數。
  
   * 請輸入 exit，不再是超級使用者。

   * 若要測試，請在該資料夾中建立資料庫。 下列範例會使用 sqlcmd 建立資料庫、 切換到它的內容，請確認檔案存在於 OS 層級，然後刪除 暫存位置。 您可以使用 SSMS。

    ![15-createtestdatabase][4]
 
   * 取消掛接共用 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > 是您要使用的 NFS 伺服器的 IP 位址
    
    \<FolderOnNFSServer > 是的 NFS 共用名稱

    \<FolderMountedIn > 是上一個步驟中建立的資料夾。 以下是範例。 
 
5. 重複的步驟，在其他節點上。


## <a name="next-steps"></a>後續步驟

[設定容錯移轉叢集執行個體-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
