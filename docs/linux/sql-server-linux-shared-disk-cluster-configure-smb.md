---
title: 設定 SMB 儲存體 FCI - Linux 上的 SQL Server
description: 了解如何使用 Linux 上的 SQL Server SMB 儲存體，設定容錯移轉叢集執行個體 (FCI)。
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 5e78e131e9a328a49bd63182e7ae74db54c50d92
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235629"
---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>設定容錯移轉叢集執行個體 - SMB - Linux 上的 SQL Server

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

此文章說明如何針對 Linux 上的容錯移轉叢集執行個體 (FCI) 設定 SMB 儲存體。 
 
在非 Windows 的世界中，SMB 通常稱為通用網際網路檔案系統 (CIFS) 共用，並透過 Samba 執行。 在 Windows 世界中，存取 SMB 共用的方式如下：\\SERVERNAME\SHARENAME。 針對 Linux 型 SQL Server 安裝，SMB 共用必須以資料夾的形式掛接。

## <a name="important-source-and-server-information"></a>重要的來源和伺服器資訊

以下是成功使用 SMB 的一些提示和注意事項：
- SMB 共用可以在 Windows、Linux 或甚至是設備上，只要它使用 SMB 3.0 或更新版本即可。 如需 Samba 和 SMB 3.0 的詳細資訊，請參閱 [SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) \(英文\)，以查看您的 Samba 實作為是否符合 SMB 3.0 的規範。
- SMB 共用應為高可用性。
- 必須在 SMB 共用上妥善設定安全性。 以下是來自 /etc/samba/smb.conf 的範例，其中 SQLData1 是共用的名稱。

![顯示 SQLData1 是共用名稱的螢幕擷取畫面。][1]

## <a name="instructions"></a>Instructions

1. 選擇將會參與 FCI 設定的其中一部伺服器。 任何一部伺服器都可以。
   
1. 取得 mssql 使用者的資訊。
   
   ```bash
    sudo id mssql
   ```
   
   記下 uid、gid 和群組。 
   
1. 執行 `sudo smbclient -L //NameOrIP/ShareName -U User`。
   
   \<NameOrIP> 是裝載 SMB 共用的伺服器其 DNS 名稱或 IP 位址。
   
   \<ShareName> 是 SMB 共用的名稱。 
   
1. 針對系統資料庫或任何儲存在預設資料位置的內容，請遵循這些步驟。 否則，請跳到步驟 5。 
   
   1. 確定您正在處理之伺服器上的 SQL Server 已經停止。
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 完全切換成超級使用者。 如果成功，您將不會收到任何通知。
      
      ```bash
      sudo -i
      ```
      
   1. 切換成 mssql 使用者。 如果成功，您將不會收到任何通知。
      
      ```bash
      su mssql
      ```
      
   1. 建立暫存目錄來儲存 SQL Server 資料和記錄檔。 如果成功，您將不會收到任何通知。
      
      ```bash
      mkdir <TempDir>
      ```
      
      \<TempDir> 是資料夾的名稱。 下列範例會建立名為 /var/opt/mssql/tmp 的資料夾。
      
      ```bash
      mkdir /var/opt/mssql/tmp
      ```
      
   1. 將 SQL Server 資料和記錄檔複製到暫存目錄。 如果成功，您將不會收到任何通知。
      
      ```bash
      cp /var/opt/mssql/data/* <TempDir>
      ```
      
      \<TempDir> 是上一個步驟中的資料夾名稱。
      
   1. 確認檔案位於目錄中。
      
      ```bash
      ls <TempDir>
      ```
      
      \<TempDir> 是步驟 d 中資料夾的名稱。
      
   1. 將檔案從現有的 SQL Server 資料目錄中刪除。 如果成功，您將不會收到任何通知。
      
      ```bash
      rm - f /var/opt/mssql/data/*
      ```
      
   1. 確認檔案已被刪除。 
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. 輸入 exit 以切換回根使用者。
      
   1. 將 SMB 共用掛接在 SQL Server 的 data 資料夾中。 如果成功，您將不會收到任何通知。 此範例顯示連線到 Windows Server 型 SMB 3.0 共用的語法。
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName> 是具有 SMB 共用的伺服器其名稱
      
      \<ShareName> 是共用的名稱
      
      \<UserName> 是要存取共用的使用者其名稱
      
      \<Password> 是使用者的密碼
      
      \<domain> 是 Active Directory 的名稱
      
      \<mssqlUID> 是 mssql 使用者的 UID 
      
      \<mssqlGID> 是 mssql 使用者的 GID
      
   1. 透過發出不含參數的 mount 來檢查掛接是否成功。
      
      ```bash
      mount
      ```
      
   1. 切換成 mssql 使用者。 如果成功，您將不會收到任何通知。
      
      ```bash
      su mssql
      ```
      
   1. 複製暫存目錄 /var/opt/mssql/data 中的檔案。 如果成功，您將不會收到任何通知。
      
      ```bash
      cp /var/opt/mssql/tmp/* /var/opt/mssql/data
      ```
      
   1. 驗證檔案存在。
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. 輸入 exit 以退出 mssql 使用者 
      
   1. 輸入 exit 以退出根使用者
   
   1. 啟動 SQL Server。 如果所有內容皆已正確複製，並正確地套用安全性，SQL Server 應該會顯示為已啟動。
      
      ```bash
      sudo systemctl start mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 若要進一步測試，請建立資料庫以確保權限正常。 下列範例使用 Transact-SQL，您可以使用 SSMS。
      
      ![10_testcreatedb][2] 
      
   1. 停止 SQL Server 並驗證它已關閉。 如果您要新增或測試其他磁碟，請勿關閉 SQL Server，直到它們都已新增和測試為止。
      
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. 只有在完成後，才將共用取消掛接。 如果未完成，請在完成測試/新增任何其他磁碟之後才取消掛接。
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName> 是 SMB 主機的 IP 位址或名稱
      
      \<ShareName> 是共用的名稱
      
      \<FolderMountedIn> 是掛接 SMB 的資料夾名稱
      
5. 針對系統資料庫以外的其他內容 (例如，使用者資料庫或備份)，請遵循這些步驟。 如果僅使用預設位置，請跳到步驟 14。
   
   1. 切換成超級使用者。 如果成功，您將不會收到任何通知。
      
      ```bash
      sudo -i
      ```
      
   1. 建立 SQL Server 將會使用的資料夾。 
      
      ```bash
      mkdir <FolderName>
      ```
      
      \<FolderName> 是資料夾的名稱。 如果資料夾不是位於正確的位置，則必須指定其完整路徑。 下列範例會建立名為 /var/opt/mssql/userdata 的資料夾。
      
      ```bash
      mkdir /var/opt/mssql/userdata
      ```
      
   1. 將 SMB 共用掛接在 SQL Server 的 data 資料夾中。 如果成功，您將不會收到任何通知。 此範例顯示連線到 Samba 型 SMB 3.0 共用的語法。
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName> 是具有 SMB 共用的伺服器其名稱
      
      \<ShareName> 是共用的名稱
      
      \<FolderName> 是在最後步驟中所建立資料夾的名稱  
      
      \<UserName> 是要存取共用的使用者其名稱
      
      \<Password> 是使用者的密碼
      
      \<mssqlUID> 是 mssql 使用者的 UID
      
      \<mssqlGID> 是 mssql 使用者的 GID。
      
   1. 透過發出不含參數的 mount 來檢查掛接是否成功。
   
   1. 輸入 exit 來退出超級使用者。
   
   1. 若要進行測試，請在該資料夾中建立資料庫。 下列範例使用 sqlcmd 來建立資料庫，將內容切換至它，驗證檔案存在於 OS 層級，然後刪除暫存位置。 您可以使用 SSMS。
   
   1. 將共用取消掛接 
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName> 是 SMB 主機的 IP 位址或名稱
      
      \<ShareName> 是共用的名稱
      
      \<FolderMountedIn> 是掛接 SMB 的資料夾名稱。
   
1. 對其他節點重複這些步驟。

您現在已準備好設定 FCI。

## <a name="next-steps"></a>後續步驟

[設定容錯移轉叢集執行個體 - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
