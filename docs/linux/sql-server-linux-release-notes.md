---
title: Linux 上的 SQL Server 2017 版本資訊
description: 此文章包含在 Linux 上執行之 SQL Server 2017 的版本資訊和支援功能。 其中包含最新版本和數個先前版本的版本資訊。
author: VanMSFT
ms.author: vanto
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: a585314a26e90b76d18117be2eafe6f78e399dc3
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2020
ms.locfileid: "97322053"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Linux 上的 SQL Server 2017 版本資訊

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

下列版本資訊適用於在 Linux 上執行的 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 此文章已針對每個版本細分為數個小節。 GA 版本會列出詳細的可支援性和已知問題。 每個累積更新 (CU) 或一般發行版本 (GDR) 除了有 Linux 套件下載連結之外，還有說明 CU 變更的支援文章連結。

> [!TIP]
> 這些版本資訊是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 版本的專屬資訊。 如需有關新 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的詳細資訊，請參閱 [Linux 上的 SQL Server 2019 預覽版本資訊](sql-server-linux-release-notes-2019.md?view=sql-server-ver15&preserve-view=true)。

## <a name="supported-platforms"></a>支援的平台

| 平台 | 檔案系統 | 安裝指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 - 7.8，或 8.0 - 8.3 伺服器 | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 - SP5 | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04 LTS、18.04 LTS | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker Engine 1.8+ | N/A | [安裝指南](quickstart-install-connect-docker.md) | 

> [!TIP]
> 如需詳細資訊，請檢閱適用於 Linux 上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的[系統需求](sql-server-linux-setup.md#system)。 如需適用於 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的最新支援原則，請參閱 [Microsoft SQL Server 的技術支援原則](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

## <a name="tools"></a>工具

以 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 為目標的大部分現有用戶端工具都可以順暢地以在 Linux 上執行的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 為目標。 某些工具可能需要特定版本，才能與 Linux 良好搭配運作。 如需 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工具的完整清單，請參閱[適用於 SQL Server 的 SQL 工具和公用程式](../tools/overview-sql-tools.md)。

## <a name="release-history"></a>版本歷程記錄

下表列出 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的版本歷程記錄。

| 版本               | 版本       | 發行日期 |
|-----------------------|---------------|--------------|
| [CU22](#CU22)         | 14.0.3356.20  | 2020-09-10   |
| [CU21](#CU21)         | 14.0.3335.7   | 2020-07-01   |
| [CU20](#CU20)         | 14.0.3294.2   | 2020-04-10   |
| [CU19](#CU19)         | 14.0.3281.6   | 2020-02-05   |
| [CU18](#CU18)         | 14.0.3257.3   | 2019-12-09   |
| [CU17](#CU17)         | 14.0.3238.1   | 2019-10-08   |
| [CU16](#CU16)         | 14.0.3223.3   | 2019-08-01   |
| [CU15](#CU15)         | 14.0.3162.1   | 2019-05-23   |
| [CU14](#CU14)         | 14.0.3076.1   | 2019-03-25   |
| [CU13](#CU13)         | 14.0.3048.4   | 2018-12-18   |
| [CU12](#CU12)         | 14.0.3045.24  | 2018-10-24   |
| [CU11](#CU11)         | 14.0.3038.14  | 2018-09-20   |
| [CU10](#CU10)         | 14.0.3037.1   | 2018-08-27   |
| [CU9-GDR2](#CU9-GDR2) | 14.0.3035.2   | 2018-08-18   |
| [GDR2](#GDR2)         | 14.0.2002.14  | 2018-08-18   |
| [CU9](#CU9)           | 14.0.3030.27  | 2018-07-18   |
| [CU8](#CU8)           | 14.0.3029.16  | 2018-06-21   |
| [CU7](#CU7)           | 14.0.3026.27  | 2018-05-24   |
| [CU6](#CU6)           | 14.0.3025.34  | 2018-04-19   |
| [CU5](#CU5)           | 14.0.3023.8   | 2018-03-20   |
| [CU4](#CU4)           | 14.0.3022.28  | 2018-02-20   |
| [CU3](#CU3)           | 14.0.3015.40  | 2018-01-03   |
| [GDR1](#GDR1)         | 14.0.2000.63  | 2018-01-03   |
| [CU2](#CU2)           | 14.0.3008.27  | 2017-11-28   |
| [CU1](#CU1)           | 14.0.3006.16  | 2017-10-24   |
| [GA](#GA)             | 14.0.1000.169 | 2017-10-02   |

## <a name="how-to-install-updates"></a><a id="cuinstall"></a> 如何安裝更新

如果您已設定 CU 存放庫 (**mssql-server-2017**)，您就會在執行新安裝時取得 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 套件的最新 CU。 CU 存放庫是適用於 Linux 上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之所有套件安裝發行項的預設值。 如果您已設定 GDR 存放庫 (**mssql-server-2017-gdr**)，則只會取得自 GA 之後發行的重大安全性更新。 如果您需要 Docker 容器 CU 或 GDR 更新，請參閱[適用於 Docker 引擎之 Linux 上的 Microsoft SQL Server](https://hub.docker.com/r/microsoft/mssql-server) \(英文\) 的官方映像。 如需有關存放庫設定的詳細資訊，請參閱[針對 Linux 上的 SQL Server 設定存放庫](sql-server-linux-change-repo.md)。

如果您正在更新現有的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 套件，請針對每個套件執行適當的更新命令以取得最新的 CU。 如需每個套件的特定更新指示，請參閱下列安裝指南：

- [安裝 SQL Server 套件](sql-server-linux-setup.md#upgrade)
- [安裝全文檢索搜尋套件](sql-server-linux-setup-full-text-search.md)
- [安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [啟用 SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a name="cu22-september-2020"></a><a id="CU22"></a> CU22 (2020 年 9 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 22 (CU22) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本為 14.0.3356.20。 如需此版本中的修正和改善資訊，請參閱 <https://support.microsoft.com/help/4577467>。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

> [!NOTE]
> 從 CU20 開始，SQL Server 2017 現在支援 **Ubuntu 18.04** 和 **RHEL 8**。
>
> 除了 SSIS 套件之外 (Ubuntu 18.04 無法使用)，Ubuntu 的離線套件安裝連結會指向 Ubuntu 18.04 套件。 若要尋找 Ubuntu 16.04 套件，請參閱下載路徑 <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/>。
>
> 除了 SSIS 套件之外 (RHEL 8 無法使用)，Red Hat 的離線套件安裝連結會指向 RHEL 8 套件。 如果您要尋找 RHEL 7 套件，請參閱下載路徑 <https://packages.microsoft.com/rhel/7/mssql-server-2017/>。

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3356.20-23 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-14.0.3356.20-23.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-ha-14.0.3356.20-23.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-fts-14.0.3356.20-23.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3356.20-23 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3356.20-23.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3356.20-23.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3356.20-23.x86_64.rpm) | 
| Ubuntu 18.04 Debian 套件 | 14.0.3356.20-23 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3356.20-23_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3356.20-23_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3356.20-23_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu21-july-2020"></a><a id="CU21"></a> CU21 (2020 年 7 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 21 (CU21) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本為 14.0.3335.7。 如需此版本中的修正和改善資訊，請參閱 <https://support.microsoft.com/help/4557397>。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

> [!NOTE]
> 從 CU20 開始，SQL Server 2017 現在支援 **Ubuntu 18.04** 和 **RHEL 8**。
>
> 除了 SSIS 套件之外 (Ubuntu 18.04 無法使用)，Ubuntu 的離線套件安裝連結會指向 Ubuntu 18.04 套件。 若要尋找 Ubuntu 16.04 套件，請參閱下載路徑 <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/>。
>
> 除了 SSIS 套件之外 (RHEL 8 無法使用)，Red Hat 的離線套件安裝連結會指向 RHEL 8 套件。 如果您要尋找 RHEL 7 套件，請參閱下載路徑 <https://packages.microsoft.com/rhel/7/mssql-server-2017/>。

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3335.7-17 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-14.0.3335.7-17.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-ha-14.0.3335.7-17.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-fts-14.0.3335.7-17.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3335.7-17 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3335.7-17.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3335.7-17.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3335.7-17.x86_64.rpm) | 
| Ubuntu 18.04 Debian 套件 | 14.0.3335.7-17 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3335.7-17_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3335.7-17_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3335.7-17_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu20-april-2020"></a><a id="CU20"></a> CU20 (2020 年 4 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 20 (CU20) 版。 此版次的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本為 14.0.3294.2。 如需此版本中的修正和改善資訊，請參閱 <https://support.microsoft.com/help/4541283>。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

> [!NOTE]
> 從 CU20 開始，SQL Server 2017 現在支援 **Ubuntu 18.04** 和 **RHEL 8**。
>
> 除了 SSIS 套件之外 (Ubuntu 18.04 無法使用)，Ubuntu 的離線套件安裝連結會指向 Ubuntu 18.04 套件。 若要尋找 Ubuntu 16.04 套件，請參閱下載路徑 <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/>。
>
> 除了 SSIS 套件之外 (RHEL 8 無法使用)，Red Hat 的離線套件安裝連結會指向 RHEL 8 套件。 如果您要尋找 RHEL 7 套件，請參閱下載路徑 <https://packages.microsoft.com/rhel/7/mssql-server-2017/>。

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3294.2-27 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-14.0.3294.2-27.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-ha-14.0.3294.2-27.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-fts-14.0.3294.2-27.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3294.2-27 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3294.2-27.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3294.2-27.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3294.2-27.x86_64.rpm) | 
| Ubuntu 18.04 Debian 套件 | 14.0.3294.2-27 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3294.2-27_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3294.2-27_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3294.2-27_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu19-february-2020"></a><a id="CU19"></a> CU19 (2020 年 2 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 19 (CU19) 版本。 此版次的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本為 14.0.3281.6。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4535007](https://support.microsoft.com/help/4535007)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3281.6-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3281.6-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3281.6-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3281.6-2.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3281.6-2 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3281.6-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3281.6-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3281.6-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3281.6-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3281.6-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3281.6-2_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3281.6-2_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu18-december-2019"></a><a id="CU18"></a> CU18 (2019 年 12 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 18 (CU18) 版本。 此版本 (Release) 的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本 (Version) 是 14.0.3257.3。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4527377](https://support.microsoft.com/help/4527377)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3257.3-13 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3257.3-13.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3257.3-13.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3257.3-13.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3257.3-13 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3257.3-13.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3257.3-13.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3257.3-13.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3257.3-13 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3257.3-13_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3257.3-13_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3257.3-13_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

### <a name="added-support"></a>新增了支援

- 從 CU18 開始，Linux 上的 SQL Server 2017 可支援異動資料擷取 (CDC)。
- 從 CU18 開始，Linux 上的 SQL Server 2017 可支援異動複寫。

### <a name="remarks"></a>備註

SQL Server 2017 容器現在有新的標記模式，如下所述，其中包含範例。

- `mcr.microsoft.com/mssql/server:<SQL Server Version>-<update>-<Linux Distribution>-<Linux Distribution Version>`

  這會使用標記中所述的組合來提取容器映像。

- `mcr.microsoft.com/mssql/server:<SQL Server Version>-latest`

    這會在最新支援的 Ubuntu 版本上提取最新的 SQL Server 版本。

**範例：**

`mcr.microsoft.com/mssql/server:2017-CU18-ubuntu-16.04`

這會根據 Ubuntu 16.04 容器提取 SQL Server 2017 CU18。

`mcr.microsoft.com/mssql/server:2017-latest`

這會根據 Ubuntu 16.04 容器，提取最新的 SQL Server 2017 版本 (撰寫此文章時為 CU18)。

> [!NOTE]
> 未來，我們將不再針對 SQL Server 2017 容器的其他標記模式發佈容器。


## <a name="cu17-october-2019"></a><a id="CU17"></a> CU17 (2019 年 10 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 17 (CU17) 版本。 此版本 (Release) 的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本 (Version) 是 14.0.3238.1。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4515579](https://support.microsoft.com/help/4515579)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3238.1-19 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3238.1-19.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3238.1-19.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3238.1-19.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3238.1-19 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3238.1-19.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3238.1-19.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3238.1-19.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3238.1-19 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3238.1-19_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3238.1-19_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3238.1-19_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu16-august-2019"></a><a id="CU16"></a> CU16 (2019 年 8 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 16 (CU16) 版本。 此版本 (Release) 的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本 (Version) 是 14.0.3223.3。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4508218](https://support.microsoft.com/help/4508218)。

### <a name="whats-new"></a>新功能

|新功能或更新 | 詳細資料 |
|:---|:---|
| MSDTC 支援 | SQL Sever 2017 的 Microsoft Distributed Transaction Coordinator (MSDTC) 支援。 如需詳細資訊，請參閱[如何在 Linux 上設定 Microsoft Distributed Transaction Coordinator (MSDTC)](sql-server-linux-configure-msdtc.md)。 |

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3223.3-15 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3223.3-15.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3223.3-15.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3223.3-15.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3223.3-15 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3223.3-15.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3223.3-15.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3223.3-15.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3223.3-15 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3223.3-15_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3223.3-15_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3223.3-15_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu15-may-2019"></a><a id="CU15"></a> CU15 (2019 年 5 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 15 (CU15) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3162.1。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4498951](https://support.microsoft.com/help/4498951)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3162.1-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3162.1-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3162.1-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3162.1-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3162.1-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3162.1-1_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu14-mar-2019"></a><a id="CU14"></a> CU14 (2019 年 3 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 14 (CU14) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3076.1。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4484710](https://support.microsoft.com/help/4484710)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3076.1-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3076.1-2 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3076.1-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3076.1-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3076.1-2_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3076.1-2_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu13-dec-2018"></a><a id="CU13"></a> CU13 (2018 年 12 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 13 (CU13) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3048.4。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4466404](https://support.microsoft.com/help/4466404)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3048.4-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3048.4-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3048.4-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu12-oct-2018"></a><a id="CU12"></a> CU12 (2018 年 10 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 12 (CU12) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3045.24。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4464082](https://support.microsoft.com/help/4464082)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3045.24-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3045.24-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3045.24-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu11-sept-2018"></a><a id="CU11"></a> CU11 (2018 年 9 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 11 (CU11) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3038.14。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4462262](https://support.microsoft.com/help/4462262)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3038.14-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3038.14-2 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3038.14-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu10-aug-2018"></a><a id="CU10"></a> CU10 (2018 年 8 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 10 (CU10) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3037.1。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4342123](https://support.microsoft.com/help/4342123)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3037.1-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3037.1-2 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3037.1-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu9-gdr2-aug-2018"></a><a id="CU9-GDR2"></a> CU9-GDR2 (2018 年 8 月)

這是也包含先前發行之 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] CU (CU9) 的安全性更新。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3035.2。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4293805](https://support.microsoft.com/help/4293805)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3035.2-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| SLES RPM 套件 | 14.0.3035.2-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3035.2-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a name="gdr2-aug-2018"></a><a id="GDR2"></a> GDR2 (2018 年 8 月)

這是只包含 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] GDR2 (和 GDR1) 安全性修正的安全性更新。  此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.2002.14。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4293803](https://support.microsoft.com/help/4293803)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.2002.14-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.2002.14-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.2002.14-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a name="cu9-jul-2018"></a><a id="CU9"></a> CU9 (2018 年 7 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 9 (CU9) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3030.27。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4341265](https://support.microsoft.com/help/4341265)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3030.27-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3030.27-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3030.27-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu8-jun-2018"></a><a id="CU8"></a> CU8 (2018 年 1 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 8 (CU8) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3029.16。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4338363](https://support.microsoft.com/help/4338363)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3029.16-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3029.16-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3029.16-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu7-may-2018"></a><a id="CU7"></a> CU7 (2018 年 5 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 7 (CU7) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3026.27。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4229789](https://support.microsoft.com/help/4229789)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3026.27-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3026.27-2 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3026.27-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu6-apr-2018"></a><a id="CU6"></a> CU6 (2018 年 4 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 6 (CU6) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3025.34。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4101464](https://support.microsoft.com/help/4101464)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3025.34-3 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3025.34-3 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3025.34-3 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu5-mar-2018"></a><a id="CU5"></a> CU5 (2018 年 3 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 5 (CU5) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3023.8。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4092643](https://support.microsoft.com/help/4092643)。

### <a name="known-upgrade-issue"></a>已知的升級問題

從舊版升級至 CU5 時，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可能會因下列錯誤而無法啟動"：

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

若要解決此錯誤，請使用下列命令來啟用 SQL Server Agent 及重新啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]：

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3023.8-5 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3023.8-5 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3023.8-5 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu4-feb-2018"></a><a id="CU4"></a> CU4 (2018 年 2 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 4 (CU4) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3022.28。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4056498](https://support.microsoft.com/help/4056498)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

> [!NOTE]
> 從 CU4 開始，已不再將 SQL Server Agent 當作個別套件來安裝。 它會隨引擎套件一起安裝，且必須啟用才能使用。

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3022.28-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3022.28-2 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3022.28-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="gdr1-jan-2018"></a><a id="GDR1"></a> GDR1 (2018 年 1 月)

這是只包含 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] GDR1 安全性修正的安全性更新。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.2000.63。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4057122](https://support.microsoft.com/help/4057122)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.2000.63-3 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.2000.63-3 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.2000.63-3 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a name="cu3-jan-2018"></a><a id="CU3"></a> CU3 (2018 年 1 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 3 (CU3) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3015.40。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4052987](https://support.microsoft.com/help/4052987)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3015.40-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3015.40-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3015.40-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[SQL Server Agent Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu2-nov-2017"></a><a id="CU2"></a> CU2 (2017 年 11 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 2 (CU2) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3008.27。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3008.27-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3008.27-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3008.27-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[SQL Server Agent Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu1-oct-2017"></a><a id="CU1"></a> CU1 (2017 年 10 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的累積更新 1 (CU1) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.3006.16。 如需有關此版本中的修正和改進資訊，請參閱 [https://support.microsoft.com/help/KB4053439](https://support.microsoft.com/help/4038634)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以運用下表中的資訊下載 RPM 和 Debian 套件：

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3006.16-3 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3006.16-3 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3006.16-3 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server Agent Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="ga-oct-2017"></a><a id="GA"></a> GA (2017 年 10 月)

這是 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的正式運作 (GA) 版。 此版本的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 版本是 14.0.1000.169。

### <a name="package-details"></a>套件詳細資料

下表列出 RPM 和 Debian 套件的套件詳細資料和下載位置。 如果您使用下列安裝指南中的步驟，則不需要直接下載這些套件：

- [安裝 SQL Server 套件](sql-server-linux-setup.md)
- [安裝全文檢索搜尋套件](sql-server-linux-setup-full-text-search.md)
- [安裝 SQL Server Agent 套件](sql-server-linux-setup-sql-agent.md)
- [安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| Package | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.1000.169-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.1000.169-2 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.1000.169-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server Agent Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="known-issues"></a>已知問題

下列各節說明 Linux 上的 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 正式運作 (GA) 版已知問題。

#### <a name="general"></a>一般

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝位置的主機名稱長度必須等於或少於 15 個字元。 

    - **解決方法**：將 /etc/hostname 中的名稱長度變更為等於或少於 15 個字元。

- 手動將系統時間設定成過去的時間會造成 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 停止更新 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 內的內部系統時間。

    - **解決方法**：重新啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。

- 僅支援單一執行個體安裝。

    - **解決方法**：如果您想要在指定的主機上有多個執行個體，請考慮使用 VM 或 Docker 容器。 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager 無法連線至 Linux 上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。

- **sa** 登入的預設語言是英文。

    - **解決方法**：使用 **ALTER LOGIN** 陳述式來變更 **sa** 登入的語言。

#### <a name="databases"></a>資料庫

- 無法使用 mssql-conf 公用程式來移動 master 資料庫。 可以使用 mssql-conf 來移動其他系統資料庫。

- 還原在 Windows 上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 備份的資料庫時，您必須使用 Transact-SQL 陳述式中的 **WITH MOVE** 子句。

- 某些適用於「傳輸層安全性」(TLS) 的演算法 (加密套件) 在 Linux 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 上正常運作。 這除了會導致在高可用性群組中的複本之間建立連線時發生問題，也會導致在嘗試連線至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 時連線失敗。

   - **解決方法**：透過執行下列動作，修改 Linux 上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 **mssql.conf** 設定指令碼以停用有問題的加密套件：

      1. 將下列內容新增至 /var/opt/mssql/mssql.conf。

         ```
         [network]
         tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
         ```

         > [!NOTE]
         > 在上述程式碼中，`!` 會否定運算式。 這告訴 OpenSSL 不要使用下列加密套件。  

      1. 使用下列命令來重新啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。

         ```bash
         sudo systemctl restart mssql-server
         ```

- 無法在 Linux 的 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 上還原 Windows 上使用記憶體內部 OLTP 的 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 資料庫。 若要還原使用記憶體內部 OLTP 的 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 資料庫，請先在 Windows 上將資料庫升級至 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 或 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]，再透過備份/還原或中斷連結/連結，將它們移至 Linux 上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。

- Linux 上目前不支援 **ADMINISTER BULK OPERATIONS** 使用者權限。

#### <a name="networking"></a>網路功能

下列兩個條件都成立時，涉及來自 sqlservr 程序之連出 TCP 連線的功能 (例如連結的伺服器或可用性群組) 可能無法運作：

1. 以主機名稱的形式而不是 IP 位址來指定目標伺服器。

1. 來源執行個體的核心中已停用 IPv6。 若要確認您系統的核心中是否已啟用 IPv6，必須通過下列所有測試：

   - `cat /proc/cmdline` 會列印目前核心的開機 cmdline。 輸出不得包含 `ipv6.disable=1`。
   - /proc/sys/net/ipv6/ 目錄必須存在。
   - 呼叫 `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` 的 C 程式應該成功 - syscall 必須傳回 fd != -1 且未因 EAFNOSUPPORT 而發生失敗。

確切的錯誤需視功能而定。 就連結的伺服器而言，這會顯示為登入逾時錯誤。 就可用性群組而言，次要複本上的 `ALTER AVAILABILITY GROUP JOIN` DDL 會在 5 分鐘後因下載設定逾時錯誤而發生失敗。

若要解決這個問題，請執行下列其中一個動作：

1. 使用 IP 而不是主機名稱來指定 TCP 連線的目標。

1. 從開機 cmdline 中移除 `ipv6.disable=1` 以在核心中啟用 IPv6。 執行此動作的方式取決於 Linux 發行版本和開機載入器 (例如 grub)。 如果您想要停用 IPv6，您仍然可以透過在 `sysctl` 設定 (例如 `/etc/sysctl.conf`) 中設定 `net.ipv6.conf.all.disable_ipv6 = 1` 來予以停用。 這將仍然防止系統的網路介面卡取得 IPv6 位址，但可允許 sqlservr 功能正常運作。

#### <a name="network-file-system-nfs"></a>網路檔案系統 (NFS)
如果您在生產環境中使用 **網路檔案系統 (NFS)** 遠端共用，請注意下列支援需求：

- 使用 NFS 版本 **4.2 或更新的版本**。 舊版 NFS 不支援現代檔案系統常用的必要功能，例如 fallocate 和疏鬆檔案建立。
- 僅尋找 NFS 掛接上的 **/var/opt/mssql** 目錄。 其他檔案 (例如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 系統二進位檔案) 並不受支援。
- 確定 NFS 用戶端在裝載遠端共用時使用 'nolock' 選項。

#### <a name="localization"></a>當地語系化

- 如果在設定期間您的地區設定不是英文 (en_us)，您就必須在 bash 工作階段/終端機中使用 UTF-8 編碼。 如果您使用 ASCII 編碼，可能會看到類似以下的錯誤：

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   如果您無法使用 UTF-8 編碼，請使用 MSSQL_LCID 環境變數來指定您的語言選擇以執行設定。

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- 執行 mssql-conf 設定及執行非英文的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝時，「正在設定 SQL Server...」當地語系化文字後面會顯示不正確的擴充字元。 或者，針對非拉丁文的安裝，此句子可能會完全遺失。 遺失的句子應該會顯示下列當地語系化字串：「已成功處理授權 PID。 新的版本為 [\<Name\> 版本]」。 此字串的輸出只是用來提供資訊，下一個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 累積更新將會處理所有語言的這個問題。 這不會以任何方式影響成功的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝。 

#### <a name="full-text-search"></a>全文檢索搜尋

- 此版本並未提供所有篩選，包括適用於 Office 文件的篩選。 如需所支援篩選的清單，請參閱[在 Linux 上安裝 SQL Server 全文檢索搜尋](sql-server-linux-setup-full-text-search.md#filters)。

#### <a name="sql-server-integration-services-ssis"></a><a id="ssis"></a> SQL Server Integration Services (SSIS)

- 此版本中在 SUSE 上不支援 **mssql-server-is** 套件。 目前在 Ubuntu 和 Red Hat Enterprise Linux (RHEL) 上支援此套件。

- 透過 Linux CTP 2.1 Refresh 和更新版本上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 套件可以在 Linux 上使用 ODBC 連接。 此功能已進行過 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 MySQL ODBC 驅動程式的測試，但也應該能夠與任何遵循 ODBC 規格的 Unicode ODBC 驅動程式搭配運作。 在設計階段，您可以提供 DSN 或連接字串來連接到 ODBC 資料；您也可以使用 Windows 驗證。 如需詳細資訊，請參閱[宣佈在 Linux 上提供 ODBC 支援的部落格文章](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/) \(英文\)。

- 在 Linux 上執行 SSIS 套件時，此版本不支援下列功能：
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 類別目錄資料庫
  - SQL Agent 排定的套件執行
  - Windows 驗證
  - 協力廠商元件
  - 異動資料擷取 (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Scale Out
  - 適用於 SSIS 的 Azure Feature Pack
  - Hadoop 和 HDFS 支援
  - Microsoft Connector for SAP BW

如需目前不支援或支援但有限制的內建 SSIS 元件清單，請參閱 [Linux 上的 SSIS 限制和已知問題](sql-server-linux-ssis-known-issues.md#components)。

如需有關 Linux 上 SSIS 的詳細資訊，請參閱下列文章：
-   [宣佈對 Linux 提供 SSIS 支援的部落格文章](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/) \(英文\)。
-   [在 Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [使用 SSIS 在 Linux 上擷取、轉換和載入資料](sql-server-linux-migrate-ssis.md)

#### <a name="sql-server-management-studio-ssms"></a><a id="ssms"></a> SQL Server Management Studio (SSMS)

以下限制適用於 Windows 上連線至 Linux 上 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。

- 不支援維護計劃。

- 不支援 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的管理資料倉儲 (MDW) 和資料收集器。 

- 具有 Windows 驗證或 Windows 事件記錄檔選項的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] UI 元件無法與 Linux 搭配使用。 您仍然可以將這些功能與其他選項搭配使用，例如 SQL 登入。 

- 無法修改要保留的記錄檔數目。

## <a name="next-steps"></a>後續步驟

若要開始使用，請參閱下列快速入門：

- [在 Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [在 Docker 上執行](quickstart-install-connect-docker.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [執行與連線 - 雲端](quickstart-install-connect-clouds.md)

如需常見問題的解答，請參閱 [Linux 上的 SQL Server 常見問題集](sql-server-linux-faq.md)。
