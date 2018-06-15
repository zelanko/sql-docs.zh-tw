---
title: 設定容錯移轉叢集執行個體存放區 SMB-SQL Server on Linux |Microsoft 文件
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: b762740be742aa2d716b9d354c26fe87bb170732
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34322969"
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>設定容錯移轉叢集執行個體-SMB-SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文說明如何在 Linux 上設定容錯移轉叢集執行個體 (FCI) 的 SMB 存放裝置。 
 
在非 Windows 世界中，SMB 是通常參照為 Common Internet File System (CIFS) 共用，而且透過 Samba 實作。 在 Windows 世界中，在存取 SMB 共用達成這種方式： \\SERVERNAME\SHARENAME。 以 Linux 為基礎的 SQL Server 安裝中，SMB 共用必須可掛接為資料夾。

## <a name="important-source-and-server-information"></a>來源和伺服器的重要資訊

以下是一些秘訣和成功使用 SMB 的附註：
- 在 Windows、 Linux、 或甚至是從作為長，因為它使用 SMB 3.0 或更高的應用裝置，可以是 SMB 共用。 如需有關 Samba 和 SMB 3.0 的詳細資訊，請參閱[SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) Samba 實作是否與 SMB 3.0 相容。
- SMB 共用必須提供高可用性。
- 安全性必須設定 SMB 共用上的正確。 以下是共用的範例 /etc/samba/smb.conf，SQLData1 所在名稱。

![05 smbsource][1]

## <a name="instructions"></a>Instructions

1.  選擇其中一個伺服器，為即將加入 FCI 組態中。 不論哪一個。

2.  取得 mssql 使用者的相關資訊。

    ```bash
    sudo id mssql
    ```
    
    請注意 uid、 gid 和群組。 

3. 執行 `sudo smbclient -L //NameOrIP/ShareName -U User`。

    \<NameOrIP > 的 DNS 名稱或 IP 位址裝載 SMB 共用的伺服器。

    \<共用名稱 > 是 SMB 共用的名稱。 

4. 系統資料庫或儲存在預設資料位置的任何項目，請遵循下列步驟。 否則請跳至步驟 5。 

   *    請確定 SQL Server 會停止您正在使用的伺服器上。
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    參數完全是超級使用者。 如果成功，則不會收到任何通知。

    ```bash
    sudo -i
    ```

   *    Mssql 使用者參數。 如果成功，則不會收到任何通知。

    ```bash
    su mssql
    ```

   *    建立暫存目錄來儲存 SQL Server 資料和記錄檔。 如果成功，則不會收到任何通知。

    ```bash
    mkdir <TempDir>
    ```

    <TempDir> 是資料夾的名稱。 下列範例會建立名為 /var/opt/mssql/tmp 的資料夾。

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   *    將 SQL Server 資料和記錄檔複製到暫存目錄。 如果成功，則不會收到任何通知。

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<TempDir > 是從上一個步驟的資料夾名稱。
    
   *    請確認檔案是目錄中。

    ```bash
    ls <TempDir>
    ```

    \<TempDir > 是從步驟 d 資料夾的名稱。
    
   *    從現有的 SQL Server 資料目錄刪除檔案。 如果成功，則不會收到任何通知。
 
    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   *    請確認已刪除的檔案。 

    ```bash
    ls /var/opt/mssql/data
    ```
 
   *    輸入 exit，切換到以根使用者。

   *    裝載 SQL Server data 資料夾中的 SMB 共用。 如果成功，則不會收到任何通知。 這個範例會顯示連線到 Windows Server 為基礎的 SMB 3.0 共用的語法。

    ```bash
    Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
    ```

    \<伺服器名稱 > 是 SMB 共用的伺服器名稱
    
    \<共用名稱 > 是共用的名稱

    \<使用者名稱 > 是要存取此共用的使用者名稱

    \<密碼 > 使用者的密碼

    \<網域 > 是 Active Directory 的名稱

    \<mssqlUID > 是 mssql 使用者的 UID 
 
    \<mssqlGID > 是在 mssql 使用者 GID
 
   *    請查看掛接成功發出掛接不使用任何參數。

    ```bash
    mount
    ```
 
   *    切換至 mssql 使用者。 如果成功，則不會收到任何通知。

    ```bash
    su mssql
    ```

   *    從暫存目錄 /var/opt/mssql/data 複製檔案。 如果成功，則不會收到任何通知。

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssql/data
    ```

   *    請確認檔案有。

    ```bash
    ls /var/opt/mssql/data
    ```

   *    輸入不是 mssql 結束 

   *    輸入不是 根的結束

   *    啟動 SQL Server。 如果所有項目已正確複製，並套用安全性是否正確，SQL Server 應該會顯示為已啟動。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
 
   *    若要進一步測試，建立資料庫，以確定是正常的權限。 下列範例使用 Transact SQL。您可以使用 SSMS。

    ![10_testcreatedb][2] 
  
   *    停止 SQL Server 並確認它已關閉。 如果您要新增或測試其他的磁碟，不會關閉 SQL Server 之前所加入和測試。

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    只有當完成後，請取消掛接共用。 否則，請取消掛接後完成測試/新增任何其他磁碟。

    ```bash
    sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
    ```

    \<IPAddressOrServerName > 是的 IP 位址或 SMB 主機的名稱

    \<共用名稱 > 是共用的名稱
    
    \<FolderMountedIn > 是 SMB 掛接的資料夾名稱

5.  進行的非系統資料庫，例如使用者資料庫或備份，請遵循下列步驟。 如果只使用的預設位置，請跳至步驟 14。
    
   *    參數是超級使用者。 如果成功，則不會收到任何通知。

    ```bash
    sudo -i
    ```
    
   *    建立將 SQL Server 所使用的資料夾。 

    ```bash
    mkdir <FolderName>
    ```

    \<資料夾名稱 > 資料夾的名稱。 將資料夾的完整路徑必須指定如果不在正確的位置。 下列範例會建立名為 /var/opt/mssql/userdata 的資料夾。

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    裝載 SQL Server data 資料夾中的 SMB 共用。 如果成功，則不會收到任何通知。 這個範例會顯示連線到 Samba 為基礎的 SMB 3.0 共用的語法。

    ```bash
    Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
    ```

    \<伺服器名稱 > 是 SMB 共用的伺服器名稱

    \<共用名稱 > 是共用的名稱

    \<資料夾名稱 > 的最後一個步驟中建立的資料夾名稱  

    \<使用者名稱 > 是要存取此共用的使用者名稱

    \<密碼 > 使用者的密碼

    \<mssqlUID > 是 mssql 使用者的 UID

    \<mssqlGID > 是在 mssql 使用者 GID。
 
   * 請查看掛接成功發出掛接不使用任何參數。
 
   * 輸入 exit，不再是超級使用者。

   * 若要測試，請在該資料夾中建立的資料庫。 下列範例會使用 sqlcmd 建立資料庫，切換至該內容，確認檔案存在於作業系統層級，然後再刪除暫存位置。 您可以使用 SSMS。
 
   * 取消掛接共用 

    ```bash
    sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
    ```
    
    \<IPAddressOrServerName > 是的 IP 位址或 SMB 主機的名稱
 
    \<共用名稱 > 是共用的名稱
 
    \<FolderMountedIn > 是 SMB 掛接資料夾的名稱。
 
6.  重複步驟，在其他節點上。

現在您已經準備好要設定 FCI。

## <a name="next-steps"></a>後續的步驟

[設定容錯移轉叢集執行個體的 SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
