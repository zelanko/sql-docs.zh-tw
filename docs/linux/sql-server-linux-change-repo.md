---
title: 為 SQL Server 2017 和 2019 設定 Linux 存放庫
description: 檢查並設定 Linux 上 SQL Server 2019 和 SQL Server 2017 的來源存放庫。 來源存放庫會影響安裝和升級期間所套用的 SQL Server 版本。
author: VanMSFT
ms.author: vanto
ms.date: 02/11/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
zone_pivot_groups: ld2-linux-distribution
ms.openlocfilehash: 33616b9a7767156e4cfd69d233f7dcfe5fc080f6
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67967527"
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
> SQL Server 2019 Preview 現已推出！ 若要試用，請利用本文設定新的 **mssql-server-preview** 存放庫。 然後利用[安裝指南](sql-server-linux-setup.md)中的指示進行安裝。

## <a id="repositories"></a> 存放庫

當您在 Linux 上安裝 SQL Server 時，您必須設定 Microsoft 存放庫。 此存放庫可用來取得資料庫引擎套件、**mssql-server** 及相關的 SQL Server 套件。 目前有三個主要存放庫：

| Repository | [屬性] | Description |
|---|---|---|
| **Preview (2017)** | **mssql-server** | SQL Server 2017 CTP 和 RC 存放庫 (已中止)。 |
| **Preview (2019)** | **mssql-server-preview** | SQL Server 2019 Preview 和 RC 存放庫。 |
| **CU** | **mssql-server-2017** | SQL Server 2017 累積更新 (CU) 存放庫。 |
| **GDR** | **mssql-server-2017-gdr** | 僅限重大更新的 SQL Server 2017 GDR 存放庫。 |

## <a id="cuversusgdr"></a> 累積更新與 GDR 的比較

請務必注意，每個發行版本都有兩種主要的存放庫類型：

- **累積更新 (CU)** ：累積更新 (CU) 存放庫包含基底 SQL Server 版本套件，並包含該版本之後的全部錯誤 (bug) 修正或改進。 累積更新專屬於某個發行版本，例如 SQL Server 2017。 它們會定期發行。

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
| **Preview (2017)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **Preview (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
如果需要，請移除舊的存放庫。 根據先前設定的存放庫類型，使用下列其中一個命令。

| Repository | 要移除的命令 |
|---|---|
| **Preview (2017)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |
| **Preview (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

::: zone-end

## <a name="configure-new-repository"></a>設定新的存放庫

<!--RHEL-->
::: zone pivot="ld2-rhel"
設定要用於 SQL Server 安裝和升級的新存放庫。 使用下列其中一個命令，設定您所選擇的存放庫。

| Repository | Version | 命令 |
|---|---|---|
| **Preview (2019)** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

::: zone-end

<!--SLES-->
::: zone pivot="ld2-sles"
設定要用於 SQL Server 安裝和升級的新存放庫。 使用下列其中一個命令，設定您所選擇的存放庫。

| Repository | Version | 命令 |
|---|---|---|
| **Preview (2019)** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

::: zone-end

<!--Ubuntu-->
::: zone pivot="ld2-ubuntu"
設定要用於 SQL Server 安裝和升級的新存放庫。

1. 匯入公開存放庫 GPG 金鑰。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 使用下列其中一個命令，設定您所選擇的存放庫。

   | Repository | Version | 命令 |
   |---|---|---|
   | **Preview (2019)** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"` |
   | **CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

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
