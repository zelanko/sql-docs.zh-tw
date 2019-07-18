---
title: 設定容錯移轉叢集執行個體的儲存體 SMB-Linux 上的 SQL Server
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: e93b7fac2f75758a0a95a4053ee0a989e410c70e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032319"
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>設定容錯移轉叢集執行個體-SMB-Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章說明如何在 Linux 上設定容錯移轉叢集執行個體 (FCI) 的 SMB 存放裝置。 
 
在非 Windows 世界中，SMB 通常是指為 Common Internet File System (CIFS) 共用，而且透過 Samba 實作。 在 Windows 世界中，存取 SMB 共用會進行這種方式：\\SERVERNAME\SHARENAME。 對於以 Linux 為基礎的 SQL Server 安裝中，SMB 共用必須可掛接為資料夾。

## <a name="important-source-and-server-information"></a>來源和伺服器的重要資訊

以下是一些秘訣和成功使用 SMB 的附註：
- SMB 共用可以是 Windows，Linux，或甚至是從長，因為它使用 SMB 3.0 或更高版本的應用裝置。 如需有關 Samba 和 SMB 3.0 的詳細資訊，請參閱[SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) Samba 實作是否含 SMB 3.0 相容。
- SMB 共用必須提供高可用性。
- 安全性必須設定 SMB 共用上的正確。 以下是共用的從 /etc/samba/smb.conf，範例 SQLData1 所在名稱。

![05 smbsource][1]

## <a name="instructions"></a>Instructions

1. 您可以選擇其中一個將參與的伺服器 FCI 組態中。 不論哪一個。
   
1. 取得 mssql 使用者的相關資訊。
   
   ```bash
    sudo id mssql
   ```
   
   請注意 uid、 gid 和群組。 
   
1. 執行 `sudo smbclient -L //NameOrIP/ShareName -U User`。
   
   \<NameOrIP > 是裝載 SMB 共用的伺服器的 IP 位址的 DNS 名稱。
   
   \<共用名稱 > 是 SMB 共用的名稱。 
   
1. 系統資料庫或儲存在預設資料位置的任何項目，請遵循下列步驟。 否則請跳至步驟 5。 
   
   1. 請確定 SQL Server 已停止您正在使用的伺服器上。
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 全面轉換成是超級使用者的參數。 如果成功，則不會收到任何通知。
      
      ```bash
      sudo -i
      ```
      
   1. 要使用 mssql 使用者的參數。 如果成功，則不會收到任何通知。
      
      ```bash
      su mssql
      ```
      
   1. 建立暫存目錄來儲存 SQL Server 資料和記錄檔。 如果成功，則不會收到任何通知。
      
      ```bash
      mkdir <TempDir>
      ```
      
      \<TempDir > 資料夾的名稱。 下列範例會建立名為 /var/opt/mssql/tmp 的資料夾。
      
      ```bash
      mkdir /var/opt/mssql/tmp
      ```
      
   1. 將 SQL Server 資料和記錄檔複製到暫存目錄。 如果成功，則不會收到任何通知。
      
      ```bash
      cp /var/opt/mssql/data/* <TempDir>
      ```
      
      \<TempDir > 是從上一個步驟的資料夾名稱。
      
   1. 確認目錄中的檔案。
      
      ```bash
      ls <TempDir>
      ```
      
      \<TempDir > 會從步驟 d 資料夾的名稱。
      
   1. 從現有的 SQL Server 資料目錄中刪除檔案。 如果成功，則不會收到任何通知。
      
      ```bash
      rm - f /var/opt/mssql/data/*
      ```
      
   1. 請確認已刪除的檔案。 
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. 若要切換回根使用者的輸入 exit。
      
   1. 掛接 SMB 共用的 SQL Server data 資料夾中。 如果成功，則不會收到任何通知。 此範例會顯示連線到 Windows Server 為基礎的 SMB 3.0 共用的語法。
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<伺服器名稱 > 是 SMB 共用的伺服器名稱
      
      \<共用名稱 > 是共用的名稱
      
      \<使用者名稱 > 是要存取共用的使用者名稱
      
      \<密碼 > 使用者的密碼
      
      \<網域 > 是 Active Directory 的名稱
      
      \<mssqlUID > 是 mssql 使用者的 UID 
      
      \<mssqlGID > 是在 mssql 使用者 GID
      
   1. 請確認掛接已成功發出掛接不使用任何參數。
      
      ```bash
      mount
      ```
      
   1. 切換至 mssql 使用者。 如果成功，則不會收到任何通知。
      
      ```bash
      su mssql
      ```
      
   1. 從暫存目錄 /var/opt/mssql/data 複製檔案。 如果成功，則不會收到任何通知。
      
      ```bash
      cp /var/opt/mssql/tmp/* /var/opt/mssql/data
      ```
      
   1. 請確認檔案有。
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. 輸入不是 mssql 結束 
      
   1. 輸入不是 根的結束
   
   1. 啟動 SQL Server。 如果所有項目已正確地複製和套用的安全性是否正確，SQL Server 應該會顯示為已啟動。
      
      ```bash
      sudo systemctl start mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 若要進一步測試，建立資料庫，以確保是正常的權限。 下列範例使用 TRANSACT-SQL;您可以使用 SSMS。
      
      ![10_testcreatedb][2] 
      
   1. 停止 SQL Server，並確認它已關閉。 如果您要新增或測試的其他磁碟，不會關閉 SQL Server 之前所新增和測試。
      
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 只有當完成時，取消掛接共用。 如果沒有，完成測試/新增任何額外的磁碟取消掛接。
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName > 是的 IP 位址或 SMB 主機的名稱
      
      \<共用名稱 > 是共用的名稱
      
      \<FolderMountedIn > 是的 SMB 掛接所在的資料夾名稱
      
5. 項目以外的系統資料庫，例如使用者資料庫或備份，請遵循下列步驟。 如果僅使用預設位置，請跳至步驟 14。
   
   1. 切換到是超級使用者。 如果成功，則不會收到任何通知。
      
      ```bash
      sudo -i
      ```
      
   1. 建立將由 SQL Server 的資料夾。 
      
      ```bash
      mkdir <FolderName>
      ```
      
      \<資料夾名稱 > 是資料夾的名稱。 資料夾的完整路徑必須指定如果不在正確的位置。 下列範例會建立名為 /var/opt/mssql/userdata 的資料夾。
      
      ```bash
      mkdir /var/opt/mssql/userdata
      ```
      
   1. 掛接 SMB 共用的 SQL Server data 資料夾中。 如果成功，則不會收到任何通知。 此範例會顯示連線至 Samba 型 SMB 3.0 共用的語法。
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<伺服器名稱 > 是 SMB 共用的伺服器名稱
      
      \<共用名稱 > 是共用的名稱
      
      \<資料夾名稱 > 是的最後一個步驟中建立的資料夾名稱  
      
      \<使用者名稱 > 是要存取共用的使用者名稱
      
      \<密碼 > 使用者的密碼
      
      \<mssqlUID > 是 mssql 使用者的 UID
      
      \<mssqlGID > 是在 mssql 使用者 GID。
      
   1. 請確認掛接已成功發出掛接不使用任何參數。
   
   1. 請輸入 exit，不再是超級使用者。
   
   1. 若要測試，請在該資料夾中建立資料庫。 下列範例會使用 sqlcmd 建立資料庫、 切換到它的內容，請確認檔案存在於 OS 層級，然後刪除 暫存位置。 您可以使用 SSMS。
   
   1. 取消掛接共用 
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName > 是的 IP 位址或 SMB 主機的名稱
      
      \<共用名稱 > 是共用的名稱
      
      \<FolderMountedIn > 是的 SMB 掛接所在的資料夾名稱。
   
1. 重複的步驟，在其他節點上。

您現在已準備好設定 FCI。

## <a name="next-steps"></a>後續步驟

[設定容錯移轉叢集執行個體-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
