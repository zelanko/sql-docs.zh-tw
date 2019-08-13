---
title: 在 Linux 上設定快照集資料夾共用 SQL Server 複寫
description: 本文描述如何在 Linux 上設定快照集資料夾共用 SQL Server 複寫。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2513511889c4bc22757f0970269fa9ee7b51857d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68093122"
---
# <a name="configure-replication-snapshot-folder-with-shares"></a>設定包含共用的複寫快照集資料夾

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

快照集資料夾是您指定為共用的目錄；讀取並寫入此資料夾的代理程式，必須具有足夠的權限才能對其進行存取。

![複寫圖表][1]

### <a name="replication-snapshot-folder-share-explained"></a>複寫快照集資料夾共用說明

在瀏覽範例之前，我們先逐步檢視 SQL Server 如何在複寫中使用 Samba 共用。 以下是其運作方式的基本範例。

1. Samba 共用已設定，可讓訂閱者看到發行者端複寫代理程式所寫入 `/local/path1` 的檔案
2. 在分佈伺服器設定發行者時，SQL Server 會設定為使用共用路徑，讓所有執行個體都能查看 `//share/path`
3. SQL Server 會從 `//share/path` 尋找本機路徑，以了解要在哪裡搜尋檔案
4. SQL Server 會由 Samba 共用支援的本機路徑讀取和寫入


## <a name="configure-a-samba-share-for-the-snapshot-folder"></a>設定快照集資料夾的 Samba 共用 

複寫代理程式需要複寫主機之間的共用目錄，才能存取其他電腦上的快照集資料夾。 例如，在交易式提取複寫中，散發代理程式位於訂閱者端，這需要存取散發者才能取得發行項。 我們將在本節中探索範例，以了解如何在兩個複寫主機上設定 Samba 共用。


## <a name="steps"></a>步驟

例如，我們將使用 Samba 來設定與主機 2 (訂閱者) 共用主機 1 (散發者) 端上的快照集資料夾。 

### <a name="install-and-start-samba-on-both-machines"></a>在兩部電腦上安裝並啟動 Samba 

在 Ubuntu 上：

```bash
sudo apt-get -y install samba
sudo service smbd restart
```

在 RHEL 上：

```bash
sudo yum install samba
sudo service smb start
sudo service smb status
```

### <a name="on-host-1-distributor-set-up-the-samba-share"></a>在主機 1 (散發者) 上設定 Samba 共用 

1. 設定 Samba 的使用者和密碼：

  ```bash
  sudo smbpasswd -a mssql 
  ```

1. 編輯 `/etc/samba/smb.conf` 以包含下列項目並填入 *share_name* 和 *path* 欄位
 ```bash
  <[share_name]>
  path = </local/path/on/host/1>
  writable = yes
  create mask = 770
  directory mask 
  valid users = mssql 
  ```

  **範例**

  ```bash
  [mssql_data]    <- Name of the shared directory
  path = /var/opt/mssql/repldata <- location of directory we wish to share
  writable = yes  <- determines if the share is writable from other hosts
  create mask = 770  <- Linux permissions for files created 
  directory mask = 770 <- Linux permissions for directories created
  valid users = mssql   <- list of users who can login to this share
  ```

### <a name="on-host-2-subscriber--mount-the-samba-share"></a>在主機 2 (訂閱者) 上掛接 Samba 共用

以正確的路徑編輯命令，並在電腦 2 上執行下列命令：

  ```bash
  sudo mount //<name_of_host_1>/<share_name> </local/path/on/host/2> -o user=mssql,uid=mssql,gid=mssql
  ```

  **範例**

  ```bash
  mount //host1/mssql_data /var/opt/mssql/repldata_shared -o user=mssql,uid=mssql,gid=mssql

  user=mssql <- sets the login name for samba
  uid=mssql   <- makes the mssql user as the owner of the mounted directory
  gid=mssql   <- sets the mssql group as the owner of the mounted directory
  ```

### <a name="on-both-hosts--configure-sql-server-on-linux-instances-to-use-snapshot-share"></a>在兩部主機上，將 Linux 上的 SQL Server 執行個體設定為使用快照集共用

將下列區段新增至兩部電腦上的 `mssql.conf`。 針對 //share/path 使用 Samba 共用的任何位置。 在此範例中，會是 `//host1/mssql_data`

  ```bash
  [uncmapping]
  //share/path = /local/path/on/hosts/
  ```

  **範例**

  在主機 1 上：

  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/1
  ```

  在主機 2 上：
  
  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/2
  ```

### <a name="configuring-publisher-with-shared-paths"></a>使用共用路徑來設定發行者

* 設定複寫時，請使用共用路徑 (範例 `//host1/mssql_data`
* 將 `//host1/mssql_data` 對應至本機目錄，以及新增至 `mssql.conf` 的對應。

## <a name="next-steps"></a>後續步驟

[概念：Linux 上的 SQL Server 複寫](sql-server-linux-replication.md)

[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

[1]: ./media/sql-server-linux-replication-snapshot-shares/image1.png
