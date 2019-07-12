---
title: 在 Linux 上設定快照集資料夾共用 SQL Server 複寫
description: 本文說明如何在 Linux 上設定的快照集資料夾共用 SQL Server 複寫。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4091bd6f1a3afcf32431af78ad47089ffc9a1620
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834783"
---
# <a name="configure-replication-snapshot-folder-with-shares"></a>設定透過共用的複寫快照集資料夾

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

快照集資料夾是您已為共用; 指定的目錄讀取和寫入到這個資料夾的代理程式必須有足夠的存取權限。

![複寫圖表][1]

### <a name="replication-snapshot-folder-share-explained"></a>複寫快照集資料夾共用說明

之前範例中，讓我們逐步解說 SQL Server 複寫中所使用的 samba 共用。 以下是其運作方式的基本範例。

1. Samba 共用已設定的檔案寫入`/local/path1`複寫在發行者上的代理程式可以看到 「 訂閱者 」
2. SQL Server 設定為使用共用路徑，使所有執行個體看起來在設定發佈伺服器上的 「 發行者 」 時 `//share/path`
3. SQL Server 會尋找從本機路徑`//share/path`知道從何處尋找檔案
4. SQL Server 讀取/寫入對受到 samba 共用的本機路徑


## <a name="configure-a-samba-share-for-the-snapshot-folder"></a>設定 samba 共用快照集資料夾 

複寫代理程式需要存取其他電腦上的快照集資料夾的複寫主機之間的共用的目錄。 比方說，在交易式提取複寫中，「 散發代理程式位於訂閱者上，而這需要存取散發者來取得文章。 在本節中，我們將探討如何複寫的主機上設定 samba 共用的範例。


## <a name="steps"></a>步驟

例如，我們將主機 1 （「 散發者 」） 與主機 2 （訂閱者） 使用 Samba 共用上設定快照集資料夾。 

### <a name="install-and-start-samba-on-both-machines"></a>安裝並啟動兩台電腦上的 Samba 

在 Ubuntu 上：

```bash
sudo apt-get -y install samba
sudo service smbd restart
```

在 RHEL:

```bash
sudo yum install samba
sudo service smb start
sudo service smb status
```

### <a name="on-host-1-distributor-set-up-the-samba-share"></a>在主控件 1 （「 散發者 」） 設定 Samba 共用 

1. 設定使用者和密碼 samba:

  ```bash
  sudo smbpasswd -a mssql 
  ```

1. 編輯`/etc/samba/smb.conf`包含下列項目，並填寫*share_name*並*路徑*欄位
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

### <a name="on-host-2-subscriber--mount-the-samba-share"></a>主機 2 （訂閱者） 上掛接 Samba 共用

編輯具有正確的路徑的命令，並在 machine2 中執行下列命令：

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

### <a name="on-both-hosts--configure-sql-server-on-linux-instances-to-use-snapshot-share"></a>在兩個主機設定上的 SQL Server 使用快照集共用的 Linux 執行個體

新增下列區段，以`mssql.conf`兩台電腦上。 只要使用 / 共用/路徑 samba 共用。 在此範例中，它會是 `//host1/mssql_data`

  ```bash
  [uncmapping]
  //share/path = /local/path/on/hosts/
  ```

  **範例**

  在 host1:

  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/1
  ```

  在 host2:
  
  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/2
  ```

### <a name="configuring-publisher-with-shared-paths"></a>設定發行者共用路徑

* 當設定複寫時，使用的共用路徑 （例如 `//host1/mssql_data`
* 地圖`//host1/mssql_data`到本機目錄，並新增至對應`mssql.conf`。

## <a name="next-steps"></a>後續步驟

[概念：在 Linux 上的 SQL Server 複寫](sql-server-linux-replication.md)

[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

[1]: ./media/sql-server-linux-replication-snapshot-shares/image1.png
