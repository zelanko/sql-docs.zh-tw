---
title: 設定 Linux 存放庫的 SQL Server 2017 和 2019年 |Microsoft Docs
description: 請檢查並設定 SQL Server 2019 和 Linux 上的 SQL Server 2017 的來源存放庫。 來源儲存機制會影響在安裝和升級時套用的 SQL Server 的版本。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/11/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
zone_pivot_groups: ld2-linux-distribution
ms.openlocfilehash: 2cc95a36a83307667b3f3678ccd19f7712dc54b3
ms.sourcegitcommit: 009bee6f66142c48477849ee03d5177bcc3b6380
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2019
ms.locfileid: "56230985"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>設定存放庫進行安裝及升級 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: zone pivot="ld2-rhel"
本文說明如何在 Linux 上設定正確的存放庫的 SQL Server 2017 和 SQL Server 2019 的安裝和升級。 在頂端，您目前的選取範圍是**Red 有 (RHEL)**。
::: zone-end

::: zone pivot="ld2-sles"
本文說明如何在 Linux 上設定正確的存放庫的 SQL Server 2017 和 SQL Server 2019 的安裝和升級。 在頂端，您目前的選取範圍是**SUSE (SLES)**。
::: zone-end

::: zone pivot="ld2-ubuntu"
本文說明如何在 Linux 上設定正確的存放庫的 SQL Server 2017 和 SQL Server 2019 的安裝和升級。 在頂端，您目前的選取範圍是**Ubuntu**。
::: zone-end

> [!TIP]
> SQL Server 2019 預覽版已正式推出 ！ 若要試用，請使用本文來設定新**mssql server 預覽版**存放庫。 然後使用中的指示來安裝[安裝指南](sql-server-linux-setup.md)。

## <a id="repositories"></a> 存放庫

當您在 Linux 上安裝 SQL Server 時，您必須設定 Microsoft 存放庫。 此存放庫用來取得資料庫引擎套件中， **mssql server**，和相關的 SQL Server 封裝。 目前有三個主要的存放庫：

| Repository | 名稱 | 描述 |
|---|---|---|
| **預覽 (2017)** | **mssql-server** | SQL Server 2017 CTP 和 RC 存放庫 （停止）。 |
| **預覽 (2019)** | **mssql-server-preview** | SQL Server 2019 預覽版，RC 的存放庫。 |
| **CU** | **mssql-server-2017** | SQL Server 2017 累積更新 (CU) 存放庫。 |
| **GDR** | **mssql-server-2017-gdr** | 只有重大更新的 SQL Server 2017 的 GDR 存放庫。 |

## <a id="cuversusgdr"></a> 與 GDR 的累計更新

請務必請注意，有兩種類型的每個散發的存放庫：

- **累計更新 (CU)**:累計更新 (CU) 存放庫包含自從該版本的基底的 SQL Server 版本，以及任何錯誤修正或改進的套件。 累計更新特有的發行版本，例如 SQL Server 2017。 在一般的步調發行。

- **GDR**:GDR 存放庫包含自從該版本的基底的 SQL Server 版本及只有重大修正程式和安全性更新的封裝。 這些更新也會新增至下一步 的 CU 版本。

每個 CU 和 GDR 版本包含完整的 SQL Server 封裝和所有先前的更新，該存放庫。 從 GDR 版本更新為 CU 版本都支援變更 SQL Server 設定的儲存機制。 您也可以[降級](sql-server-linux-setup.md#rollback)您主要的版本中的任何版本 (例如：2017).

> [!NOTE]
> 您可以更新從 GDR 發行 CU 版本隨時藉由變更存放庫。 更新不支援從 CU GDR 發行的版本。

## <a name="configure-repositories"></a>設定存放庫

::: zone pivot="ld2-rhel"
使用下列各節中的步驟，設定存放庫上 Red Hat Enterprise Server (RHEL)。
::: zone-end

::: zone pivot="ld2-sles"
使用下列各節中的步驟，設定存放庫在 SUSE Linux Enterprise Server (SLES)。
::: zone-end

::: zone pivot="ld2-ubuntu"
使用下列各節中的步驟，在 Ubuntu 上設定存放庫。
::: zone-end

## <a name="check-for-previously-configured-repositories"></a>檢查先前設定的存放庫

<!--RHEL-->
::: zone pivot="ld2-rhel"
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

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
先確認是否已註冊的 SQL Server 儲存機制。

1. 使用**zypper 資訊**取得任何先前設定的儲存機制的資訊。

   ```bash
   sudo zypper info mssql-server
   ```

2. **存放庫**屬性是設定的儲存機制。 您可以使用中的資料表來識別它[存放庫](#repositories)一節。

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
先確認是否已註冊的 SQL Server 儲存機制。

1. 檢視的內容 **/etc/apt/sources.list**檔案。

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. 檢查 mssql 伺服器的封裝 URL。 您可以使用中的資料表來識別它[存放庫](#repositories)一節。

::: zone-end

## <a name="remove-old-repository"></a>移除舊的存放庫

<!--RHEL-->
::: zone pivot="ld2-rhel"
如有需要，移除舊的存放庫，使用下列命令。

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

此命令假設，如上一節中所識別的檔案命名為**mssql server.repo**。

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
如有需要，移除舊的存放庫。 使用其中一個下列的命令，根據先前設定的存放庫的類型。

| Repository | 若要移除的命令 |
|---|---|
| **預覽 (2017)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **預覽 (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
如有需要，移除舊的存放庫。 使用其中一個下列的命令，根據先前設定的存放庫的類型。

| Repository | 若要移除的命令 |
|---|---|
| **預覽 (2017)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |
| **預覽 (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

::: zone-end

## <a name="configure-new-repository"></a>設定新的存放庫

<!--RHEL-->
::: zone pivot="ld2-rhel"
設定新的存放庫，若要使用 SQL Server 安裝與升級。 使用下列命令之一來設定您選擇的存放庫。

| Repository | 版本 | 命令 |
|---|---|---|
| **預覽 (2019)** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
設定新的存放庫，若要使用 SQL Server 安裝與升級。 使用下列命令之一來設定您選擇的存放庫。

| Repository | 版本 | 命令 |
|---|---|---|
| **預覽 (2019)** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
設定新的存放庫，若要使用 SQL Server 安裝與升級。

1. 匯入公用存放庫 GPG 金鑰。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 使用下列命令之一來設定您選擇的存放庫。

   | Repository | 版本 | 命令 |
   |---|---|---|
   | **預覽 (2019)** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"` |
   | **CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. 執行**apt get 更新**。

   ```bash
   sudo apt-get update
   ```

::: zone-end

## <a name="next-steps"></a>後續步驟

您已設定正確的存放庫之後，您可以繼續進行[安裝](sql-server-linux-setup.md#platforms)或是[更新](sql-server-linux-setup.md#upgrade)SQL Server，以及任何相關封裝的新的儲存機制中。

::: zone pivot="ld2-rhel"
> [!IMPORTANT]
> 此時，如果您選擇使用[RHEL 快速入門](quickstart-install-connect-red-hat.md)，請記住，您已設定目標存放庫。 在教學課程中不重複該步驟。 這是特別有用，如果您設定的 GDR 存放庫，因為快速入門會使用 CU 的存放庫。
::: zone-end

::: zone pivot="ld2-sles"
> [!IMPORTANT]
> 此時，如果您選擇使用[SLES 快速入門](quickstart-install-connect-suse.md)，請記住，您已設定目標存放庫。 在教學課程中不重複該步驟。 這是特別有用，如果您設定的 GDR 存放庫，因為快速入門會使用 CU 的存放庫。
::: zone-end

::: zone pivot="ld2-ubuntu"
> [!IMPORTANT]
> 此時，如果您選擇使用[Ubuntu 快速入門](quickstart-install-connect-ubuntu.md)，請記住，您已設定目標存放庫。 在教學課程中不重複該步驟。 這是特別有用，如果您設定的 GDR 存放庫，因為快速入門會使用 CU 的存放庫。
::: zone-end

如需有關如何在 Linux 上安裝 SQL Server 2017 的詳細資訊，請參閱 <<c0> [ 在 Linux 上的 SQL Server 的安裝指引](sql-server-linux-setup.md)。
