---
title: Linux 上的 SQL Server 設定存放庫 |Microsoft 文件
description: 請檢查並設定 SQL Server 2017 Linux 上的來源存放庫。 來源儲存機制會影響在安裝和升級時套用的 SQL Server 的版本。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/14/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 361f66fff8fecfd748b1bd573367509e93cc7b87
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086980"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>設定存放庫進行安裝及升級 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文說明如何在 Linux 上設定正確的存放庫的 SQL Server 2017 安裝和升級。

> [!IMPORTANT]
> 如果您先前安裝的 CTP 或 SQL Server 2017 RC 版本，則您必須註冊公開上市 (GA) 存放庫和升級或重新安裝來使用這篇文章中的步驟。 不支援的 SQL Server 2017 preview 版本，而且將到期。

## <a id="repositories"></a> 存放庫

當您在 Linux 上安裝 SQL Server 時，您必須設定 Microsoft 存放庫。 此存放庫用來取得資料庫引擎套件中， **mssql server**，和相關的 SQL Server 封裝。 目前有三個主要的存放庫：

| Repository | 名稱 | 描述 |
|---|---|---|
| **預覽** | **mssql-server** | SQL server 版本的 CTP 與 RC 版本的預覽存放庫。 此存放庫不支援 SQL Server 2017。 |
| **CU** | **mssql-server-2017** | SQL Server 2017 累積更新 (CU) 存放庫。 |
| **GDR** | **mssql-server-2017-gdr** | 只有重大更新的 SQL Server 2017 的 GDR 存放庫。 |

## <a id="cuversusgdr"></a> 與 GDR 的累計更新

請務必請注意，有兩種類型的每個散發的存放庫：

- **累積更新 (CU)**: 累積更新 (CU) 存放庫包含自從該版本的基底的 SQL Server 版本，以及任何錯誤修正或改進的套件。 累計更新特有的發行版本，例如 SQL Server 2017。 在一般的步調發行。

- **GDR**: GDR 存放庫包含自從該版本的基底的 SQL Server 版本及只有重大修正程式和安全性更新的封裝。 這些更新也會新增至下一步 的 CU 版本。

每個 CU 和 GDR 版本包含完整的 SQL Server 封裝和所有先前的更新，該存放庫。 從 GDR 版本更新為 CU 版本都支援變更 SQL Server 設定的儲存機制。 您也可以[降級](sql-server-linux-setup.md#rollback)您主要的版本中的任何版本 (例如： 2017年)。

> [!NOTE]
> 您可以更新從 GDR 發行 CU 版本隨時藉由變更存放庫。 更新不支援從 CU GDR 發行的版本。 

## <a id="configure"></a> 設定的存放庫

下列各節說明如何確認，然後設定下列支援的平台的存放庫：

- [Red Hat Enterprise Server](#rhel)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#sles)

## <a id="rhel"></a> 設定 RHEL 存放庫
使用下列步驟來設定存放庫上 Red Hat Enterprise Server (RHEL)。

### <a name="check-for-previously-configured-repositories-rhel"></a>檢查先前設定的存放庫 (RHEL)
先確認是否已註冊的 SQL Server 儲存機制。

1. 檢視中的檔案 **/etc/yum.repos.d**目錄使用下列命令：

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. 設定 SQL Server 目錄中，這類的檔案看起來**mssql server.repo**。

3. 列印出檔案的內容。

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. **名稱**屬性是設定的儲存機制。 您可以使用中的資料表來識別它[存放庫](#repositories)一節。

### <a name="remove-old-repository-rhel"></a>移除舊的存放庫 (RHEL)
如有需要，移除舊的存放庫，使用下列命令。

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

此命令假設，如上一節中所識別的檔案命名為**mssql server.repo**。

### <a name="configure-new-repository-rhel"></a>設定新的存放庫 (RHEL)
設定新的存放庫，若要使用 SQL Server 安裝與升級。 使用下列命令之一來設定您選擇的存放庫。

| Repository | 命令 |
|---|---|
| **CU** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

## <a id="sles"></a> 設定 SLES 儲存機制
您可以使用下列步驟來在 SLES 上設定存放庫。

### <a name="check-for-previously-configured-repositories-sles"></a>檢查先前設定的存放庫 (SLES)
先確認是否已註冊的 SQL Server 儲存機制。

1. 使用**zypper 資訊**取得任何先前設定的儲存機制的資訊。

   ```bash
   sudo zypper info mssql-server
   ```

2. **存放庫**屬性是設定的儲存機制。 您可以使用中的資料表來識別它[存放庫](#repositories)一節。

### <a name="remove-old-repository-sles"></a>移除舊的存放庫 (SLES)
如有需要，移除舊的存放庫。 使用其中一個下列的命令，根據先前設定的存放庫的類型。

| Repository | 若要移除的命令 |
|---|---|
| **預覽** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

### <a name="configure-new-repository-sles"></a>設定新的存放庫 (SLES)
設定新的存放庫，若要使用 SQL Server 安裝與升級。 使用下列命令之一來設定您選擇的存放庫。

| Repository | 命令 |
|---|---|
| **CU** | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

## <a id="ubuntu"></a> 設定 Ubuntu 存放庫
您可以使用下列步驟來在 Ubuntu 上設定存放庫。

### <a name="check-for-previously-configured-repositories-ubuntu"></a>檢查先前設定的存放庫 (Ubuntu)
先確認是否已註冊的 SQL Server 儲存機制。

1. 檢視的內容 **/etc/apt/sources.list**檔案。

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. 檢查 mssql 伺服器的封裝 URL。 您可以使用中的資料表來識別它[存放庫](#repositories)一節。

### <a name="remove-old-repository-ubuntu"></a>移除舊的存放庫 (Ubuntu)
如有需要，移除舊的存放庫。 使用其中一個下列的命令，根據先前設定的存放庫的類型。

| Repository | 若要移除的命令 |
|---|---|
| **預覽** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` 
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

### <a name="configure-new-repository-ubuntu"></a>設定新的存放庫 (Ubuntu)
設定新的存放庫，若要使用 SQL Server 安裝與升級。

1. 匯入公用存放庫 GPG 金鑰。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 使用下列命令之一來設定您選擇的存放庫。

   | Repository | 命令 |
   |---|---|
   | **CU** | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. 執行**apt get 更新**。

   ```bash
   sudo apt-get update
   ```

## <a name="next-steps"></a>後續步驟

您已設定正確的存放庫之後，您可以繼續進行[安裝](sql-server-linux-setup.md#platforms)或是[更新](sql-server-linux-setup.md#upgrade)SQL Server，以及任何相關封裝的新的儲存機制中。

> [!IMPORTANT]
> 此時，如果您選擇使用其中一個安裝的發行項，例如[快速入門](sql-server-linux-setup.md#platforms)，請記住，您已設定目標存放庫。 在教學課程中不重複該步驟。 這是特別有用，如果您設定的 GDR 存放庫，因為快速入門使用 CU 的存放庫。

如需有關如何在 Linux 上安裝 SQL Server 2017 的詳細資訊，請參閱 <<c0> [ 在 Linux 上的 SQL Server 的安裝指引](sql-server-linux-setup.md)。
