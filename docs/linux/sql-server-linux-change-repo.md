---
title: 為 SQL Server 2017 和 2019 設定 Linux 存放庫
description: 檢查並設定 Linux 上 SQL Server 2019 和 SQL Server 2017 的來源存放庫。 來源存放庫會影響安裝和升級期間所套用的 SQL Server 版本。
author: VanMSFT
ms.author: vanto
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
zone_pivot_groups: ld2-linux-distribution
ms.openlocfilehash: 7253fb18ea783a1fb7aeec77aa73b9a899ec6ae9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301699"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>設定用於安裝和升級 Linux 上 SQL Server 的存放庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: zone pivot="ld2-rhel"
本文描述如何為 Linux 上的 SQL Server 2017 和 SQL Server 2019 安裝和升級設定正確的存放庫。 您目前在頂端選取的是 **Red Hat (RHEL)** 。
::: zone-end

::: zone pivot="ld2-sles"
本文描述如何為 Linux 上的 SQL Server 2017 和 SQL Server 2019 安裝和升級設定正確的存放庫。 您目前在頂端選取的是 **SUSE (SLES)** 。
::: zone-end

::: zone pivot="ld2-ubuntu"
本文描述如何為 Linux 上的 SQL Server 2017 和 SQL Server 2019 安裝和升級設定正確的存放庫。 您目前在頂端選取的是 **Ubuntu**。
::: zone-end

> [!TIP]
> SQL Server 2019 現已可供使用！ 若要試用，請使用本文來設定新的 **mssql-server-2019** 存放庫。 然後利用[安裝指南](sql-server-linux-setup.md)中的指示進行安裝。

## <a name="repositories"></a><a id="repositories"></a> 存放庫

當您在 Linux 上安裝 SQL Server 時，您必須設定 Microsoft 存放庫。 此存放庫可用來取得資料庫引擎套件、**mssql-server** 及相關的 SQL Server 套件。 目前有五個主要存放庫：

| Repository | 名稱 | 描述 |
|---|---|---|
| **2019** | **mssql-server-2019** | SQL Server 2019 累積更新 (CU) 存放庫。 |
| **2019 GDR** | **mssql-server-2019-gdr** | 僅限重大更新的 SQL Server 2019 GDR 存放庫。 |
| **2019 Preview** | **mssql-server-preview** | SQL Server 2019 Preview 和 RC 存放庫。 |
| **2017** | **mssql-server-2017** | SQL Server 2017 累積更新 (CU) 存放庫。 |
| **2017 GDR** | **mssql-server-2017-gdr** | 僅限重大更新的 SQL Server 2017 GDR 存放庫。 |

## <a name="cumulative-update-versus-gdr"></a><a id="cuversusgdr"></a> 累積更新與 GDR 的比較

請務必注意，每個發行版本都有兩種主要的存放庫類型：

- **累積更新 (CU)** ：累積更新 (CU) 存放庫包含基底 SQL Server 版本套件，並包含該版本之後的全部錯誤 (bug) 修正或改進。 累積更新特定於某個發行版本，例如 SQL Server 2019。 它們會定期發行。

- **GDR**：GDR 存放庫包含基底 SQL Server 版本套件，並只包含該版本之後的重大修正和安全性更新。 這些更新也會新增至下一個 CU 版本。

每個 CU 和 GDR 版本都包含該存放庫的完整 SQL Server 套件和先前的所有更新。 您可以變更為 SQL Server 設定的存放庫，從 GDR 版本更新為 CU 版本。 您也可以[降級](sql-server-linux-setup.md#rollback)為主要版本 (例如：2017) 內的任意版本。

> [!NOTE]
> 您可以隨時變更存放庫，從 GDR 版本更新為 CU 版本。 不支援從 CU 版本更新為 GDR 版本。

## <a name="configure-repositories"></a>設定存放庫

::: zone pivot="ld2-rhel"
使用下列各節中的步驟，設定 Red Hat Enterprise Server (RHEL) 上的存放庫。
::: zone-end

::: zone pivot="ld2-sles"
使用下列各節中的步驟，設定 SUSE Linux Enterprise Server (SLES) 上的存放庫。
::: zone-end

::: zone pivot="ld2-ubuntu"
使用下列各節中的步驟，設定 Ubuntu 上的存放庫。
::: zone-end

## <a name="check-for-previously-configured-repositories"></a>檢查是否有先前設定的存放庫

<!--RHEL-->
::: zone pivot="ld2-rhel"
請先確認您是否已註冊 SQL Server 存放庫。

1. 使用下列命令檢視 **/etc/yum.repos.d** 目錄中的檔案：

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. 尋找設定 SQL Server 目錄的檔案，例如 **mssql-server.repo**。

3. 列印出檔案的內容。

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. **name** 屬性是已設定的存放庫。 您可以從本文中[存放庫](#repositories)一節的表格識別出來。

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
請先確認您是否已註冊 SQL Server 存放庫。

1. 使用 **zypper info** 取得先前設定存放庫的相關資訊。

   ```bash
   sudo zypper info mssql-server
   ```

2. **Repository** 屬性是已設定的存放庫。 您可以從本文中[存放庫](#repositories)一節的表格識別出來。

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
請先確認您是否已註冊 SQL Server 存放庫。

1. 檢視 **/etc/apt/sources.list** 檔案的內容。

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. 檢查 mssql-server 的套件 URL。 您可以從本文中[存放庫](#repositories)一節的表格識別出來。

::: zone-end

## <a name="remove-old-repository"></a>移除舊的存放庫

<!--RHEL-->
::: zone pivot="ld2-rhel"
如果需要，請使用下列命令移除舊的存放庫。

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

此命令假設上一節中識別的檔案名為 **mssql-server.repo**。

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
如果需要，請移除舊的存放庫。 根據先前設定的存放庫類型，使用下列其中一個命令。

| Repository | 要移除的命令 |
|---|---|
| **Preview (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **2019 CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2019'` |
| **2019 GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2019-gdr'`|
| **2017 CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **2017 GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
如果需要，請移除舊的存放庫。 根據先前設定的存放庫類型，使用下列其中一個命令。

> [!NOTE]
> 從 SQL Server 2019 CU3 和 SQL Server 2017 CU20 開始支援 Ubuntu 18.04。 如果您正在使用 Ubuntu 16.04，請將下列路徑變更為 `/ubuntu/16.04`，而非 `/ubuntu/18.04`，並使用正確的[散發代號](https://releases.ubuntu.com/)。

| Repository | 要移除的命令 |
|---|---|
| **Preview (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **2019 CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019 bionic main'` | 
| **2019 GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/18.04/mssql-server-2019-gdr bionic main'` |
| **2017 CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **2017 GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

::: zone-end

## <a name="configure-new-repository"></a>設定新的存放庫

<!--RHEL-->
::: zone pivot="ld2-rhel"
設定要用於 SQL Server 安裝和升級的新存放庫。 使用下列其中一個命令，設定您所選擇的存放庫。

> [!NOTE]
> 下列 SQL Server 2019 命令會指向 RHEL 8 存放庫。 SQL Server 需要使用 python2，但 RHEL 8 未預先安裝。 如需詳細資訊，請參閱下列說明如何安裝 python2 並將其設為預設解譯器的部落格： https://www.redhat.com/en/blog/installing-microsoft-sql-server-red-hat-enterprise-linux-8-beta 。
>
> 從 SQL Server 2017 CU20 開始支援 RHEL 8。
>
> 如果您使用的是 RHEL 7 或 RHEL 8，請確定路徑符合 `/rhel/7` 或 `/rhel/8`。

| Repository | 版本 | Command |
|---|---|---|
| **2019 CU** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo` |
| **2019 GDR** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019-gdr.repo` |
| **2017 CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2017.repo` |
| **2017 GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2017-gdr.repo` |

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
設定要用於 SQL Server 安裝和升級的新存放庫。 使用下列其中一個命令，設定您所選擇的存放庫。

| Repository | 版本 | Command |
|---|---|---|
| **2019 CU** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019.repo` |
| **2019 GDR** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2019-gdr.repo` |
| **2017 CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **2017 GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
設定要用於 SQL Server 安裝和升級的新存放庫。

> [!NOTE]
> 從 SQL Server 2019 CU3 和 SQL Server 2017 CU20 開始支援 Ubuntu 18.04。 下列命令會指向 Ubuntu 18.04 存放庫。
>
> 如果您正在使用 Ubuntu 16.04，請將下列路徑變更為 `/ubuntu/16.04`，而非 `/ubuntu/18.04`。

1. 匯入公開存放庫 GPG 金鑰。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 使用下列其中一個命令，設定您所選擇的存放庫。

   | Repository | 版本 | Command |
   |---|---|---|
   | **2019 CU** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"` |
   | **2019 GDR** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019-gdr.list)"` |
   | **2017 CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2017.list)"` |
   | **2017 GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2017-gdr.list)"` |

3. 執行 **apt-get update**。

   ```bash
   sudo apt-get update
   ```

::: zone-end

## <a name="next-steps"></a>後續步驟

設定正確的存放庫之後，您可以繼續從新的存放庫[安裝](sql-server-linux-setup.md#platforms)或[更新](sql-server-linux-setup.md#upgrade) SQL Server 及所有相關的套件。

::: zone pivot="ld2-rhel"
> [!IMPORTANT]
> 此時，如果您選擇使用 [RHEL 快速入門](quickstart-install-connect-red-hat.md)，請記住您已設定目標存放庫。 請勿在教學課程中重複該步驟。 如果您設定 GDR 存放庫，這特別適用，因為快速入門使用的是 CU 存放庫。
::: zone-end

::: zone pivot="ld2-sles"
> [!IMPORTANT]
> 此時，如果您選擇使用 [SLES 快速入門](quickstart-install-connect-suse.md)，請記住您已設定目標存放庫。 請勿在教學課程中重複該步驟。 如果您設定 GDR 存放庫，這特別適用，因為快速入門使用的是 CU 存放庫。
::: zone-end

::: zone pivot="ld2-ubuntu"
> [!IMPORTANT]
> 此時，如果您選擇使用 [Ubuntu 快速入門](quickstart-install-connect-ubuntu.md)，請記住您已設定目標存放庫。 請勿在教學課程中重複該步驟。 如果您設定 GDR 存放庫，這特別適用，因為快速入門使用的是 CU 存放庫。
::: zone-end

如需如何在 Linux 上安裝 SQL Server 2017 的詳細資訊，請參閱 [Linux 上的 SQL Server 安裝指引](sql-server-linux-setup.md)。
