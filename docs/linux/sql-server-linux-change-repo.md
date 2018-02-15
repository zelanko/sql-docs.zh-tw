---
title: "設定 SQL Server on Linux 的儲存機制 |Microsoft 文件"
description: "請檢查並設定在 Linux 上的 SQL Server 2017 來源儲存機制。 來源儲存機制會影響安裝和升級期間會套用的 SQL Server 的版本。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/14/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Active
ms.openlocfilehash: 33f02349d10cfd0ada76325c378d0259ec931002
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>設定安裝與升級 SQL Server on Linux 的儲存機制

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文說明如何在 Linux 上設定 SQL Server 2017 安裝與升級的正確儲存機制。

> [!IMPORTANT]
> 如果您先前安裝 CTP 或 RC 版本的 SQL Server 2017，您必須使用本文章中的步驟來註冊通用版本上市 (GA) 存放庫和升級或重新安裝。 SQL Server 2017 的 preview 版本不支援，而且將到期。

## <a id="repositories"></a> 儲存機制

當您安裝 SQL Server on Linux 時，您必須設定 Microsoft 儲存機制。 這個儲存機制用來取得資料庫引擎的封裝， **mssql 伺服器**，和相關的 SQL Server 封裝。 目前有三個主要的儲存機制：

| Repository | 名稱 | Description |
|---|---|---|
| **預覽** | **mssql-server** | CTP 與 RC 版本的 SQL Server 的預覽存放庫。 SQL Server 2017 不支援此儲存機制。 |
| **CU** | **mssql-server-2017** | SQL Server 2017 累計更新 (CU) 儲存機制。 |
| **GDR** | **mssql-server-2017-gdr** | SQL Server 2017 GDR 儲存機制僅適用於重要更新。 |

## <a id="cuversusgdr"></a> 與 GDR 累計更新

請務必注意，有兩種類型的儲存機制的每個散發：

- **累計更新 (CU)**: 累計更新 (CU) 儲存機制自該版本包含基底的 SQL Server 版本和 bug 修正或改進的封裝。 累計更新的發行版本，例如 SQL Server 2017 特有。 它們會以一般的步調發行。

- **GDR**: GDR 儲存機制 含有該發行以來的基底的 SQL Server 版本和僅重大修正程式和安全性更新的封裝。 這些更新也會新增到下一個 CU 版本。

每個 CU 和 GDR 版本包含完整的 SQL Server 封裝和所有先前的更新，該儲存機制。 從 GDR 發行更新至目前的版本支援適用於 SQL Server 變更設定的儲存機制。 您也可以[降級](sql-server-linux-setup.md#rollback)至您的主要版本內任何發佈 (例如： 2017年)。

> [!NOTE]
> 您可以更新從 GDR 發行 CU 釋放隨時藉由變更儲存機制。 更新不支援從 CU GDR 發行的版本。 

## <a id="configure"></a> 將設定儲存機制

下列章節說明如何確認及設定下列支援的平台的儲存機制：

- [Red Hat Enterprise Server](#rhel)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#sles)

## <a id="rhel"></a> 設定 RHEL 儲存機制
您可以使用下列步驟來設定儲存機制上 Red Hat Enterprise Server (RHEL)。

### <a name="check-for-previously-configured-repositories-rhel"></a>請檢查先前設定的儲存機制 (RHEL)
先確認是否已註冊的 SQL Server 儲存機制。

1. 檢視中的檔案**/etc/yum.repos.d**目錄使用下列命令：

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. 尋找檔案，以設定 SQL Server 目錄，例如**mssql server.repo**。

3. 列印檔案的內容。

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. **名稱**屬性是設定的儲存機制。 您可以將它識別中的資料表[儲存機制](#repositories)本文一節。

### <a name="remove-old-repository-rhel"></a>移除舊的儲存機制 (RHEL)
如有必要，請移除舊的儲存機制，使用下列命令。

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

此命令假設，如上一節中所識別的檔案命名為**mssql server.repo**。

### <a name="configure-new-repository-rhel"></a>設定新的儲存機制 (RHEL)
設定要用於 SQL Server 安裝與升級新的儲存機制。 使用下列命令之一來設定您選擇的儲存機制。

| Repository | Command |
|---|---|
| **CU** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

## <a id="sles"></a> 設定 SLES 儲存機制
使用下列步驟來設定儲存機制上 SLES。

### <a name="check-for-previously-configured-repositories-sles"></a>請檢查先前設定的儲存機制 (SLES)
先確認是否已註冊的 SQL Server 儲存機制。

1. 使用**zypper 資訊**來取得任何先前設定的儲存機制的相關資訊。

   ```bash
   sudo zypper info mssql-server
   ```

2. **儲存機制**屬性是設定的儲存機制。 您可以將它識別中的資料表[儲存機制](#repositories)本文一節。

### <a name="remove-old-repository-sles"></a>移除舊的儲存機制 (SLES)
如有必要，請移除舊的儲存機制。 使用下列命令，根據先前設定的儲存機制類型之一。

| Repository | 若要移除的命令 |
|---|---|
| **預覽** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

### <a name="configure-new-repository-sles"></a>設定新的儲存機制 (SLES)
設定要用於 SQL Server 安裝與升級新的儲存機制。 使用下列命令之一來設定您選擇的儲存機制。

| Repository | Command |
|---|---|
| **CU** | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

## <a id="ubuntu"></a> 設定 Ubuntu 儲存機制
使用下列步驟來設定儲存機制在 Ubuntu 上。

### <a name="check-for-previously-configured-repositories-ubuntu"></a>請檢查先前設定的儲存機制 (Ubuntu)
先確認是否已註冊的 SQL Server 儲存機制。

1. 檢視的內容**/etc/apt/sources.list**檔案。

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. 檢查 mssql 伺服器的套件 URL。 您可以將它識別中的資料表[儲存機制](#repositories)本文一節。

### <a name="remove-old-repository-ubuntu"></a>移除舊的儲存機制 (Ubuntu)
如有必要，請移除舊的儲存機制。 使用下列命令，根據先前設定的儲存機制類型之一。

| Repository | 若要移除的命令 |
|---|---|
| **預覽** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` 
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

### <a name="configure-new-repository-ubuntu"></a>設定新的儲存機制 (Ubuntu)
設定要用於 SQL Server 安裝與升級新的儲存機制。

1. 匯入公用儲存機制 GPG 索引鍵。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 使用下列命令之一來設定您選擇的儲存機制。

   | Repository | Command |
   |---|---|
   | **CU** | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. 執行**apt get 更新**。

   ```bash
   sudo apt-get update
   ```

## <a name="next-steps"></a>後續的步驟

您已設定正確的儲存機制之後，您可以繼續進行[安裝](sql-server-linux-setup.md#platforms)或[更新](sql-server-linux-setup.md#upgrade)SQL Server 和任何相關封裝從新的儲存機制。

> [!IMPORTANT]
> 此時，如果您選擇使用其中安裝文件中，例如[快速入門](sql-server-linux-setup.md#platforms)，請記住您已設定目標存放庫。 教學課程中不重複該步驟。 特別是如果您設定的 GDR 儲存機制，因為快速入門使用 CU 儲存機制。

如需有關如何在 Linux 上安裝 SQL Server 2017 的詳細資訊，請參閱[SQL Server on Linux 的安裝指南](sql-server-linux-setup.md)。
