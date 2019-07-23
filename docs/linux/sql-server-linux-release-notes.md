---
title: Linux 上的 SQL Server 2017 版本資訊
description: 本文包含 Linux 上執行之 SQL Server 2017 的版本資訊和支援的功能。 版本資訊包含在最新版本和數個先前版本中。
author: VanMSFT
ms.author: vanto
ms.date: 06/25/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: 5b6fce0bdde7e320eea0371125a61627652de80d
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388408"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Linux 上的 SQL Server 2017 版本資訊

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

下列版本資訊適用[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]于在 Linux 上執行的。 本文會細分為每個版本的各節。 GA 版本具有列出的詳細支援和已知問題。 每個累計更新 (CU) 或一般發行版本 (GDR) 都有一個支援文章的連結, 其中說明 CU 變更以及 Linux 套件下載的連結。

> [!TIP]
> 這些版本資訊特別適用于[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]發行。 如需新[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]的詳細資訊, 請參閱[Linux 上的 SQL Server 2019 preview 的版本](sql-server-linux-release-notes-2019.md?view=sql-server-ver15)資訊。

## <a name="supported-platforms"></a>支援的平台

| 平台 | 檔案系統 | 安裝指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3、7.4、7.5 或7.6 伺服器 | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker Engine 1.8 + | N/A | [安裝指南](quickstart-install-connect-docker.md) | 

> [!TIP]
> 如需詳細資訊, 請參閱 Linux [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上的[系統需求](sql-server-linux-setup.md#system)。 如需的最新支援[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]原則, 請參閱[Microsoft SQL Server 的技術支援原則](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

## <a name="tools"></a>工具

目標[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的大部分現有用戶端工具都可以[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]順暢地以 Linux 上的執行為目標。 某些工具可能有特定的版本需求, 可以與 Linux 搭配運作。 如需完整的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]工具清單, 請參閱 SQL Server 的[SQL 工具和公用程式](../tools/overview-sql-tools.md)。

## <a name="release-history"></a>發行歷程記錄

下表列出的發行歷程記錄[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。

| 版本               | Version       | 發行日期 |
|-----------------------|---------------|--------------|
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

## <a id="cuinstall"></a>如何安裝更新

如果您已設定 CU 存放庫 (**mssql-伺服器-2017**), 則當您執行新的安裝時[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , 將會取得最新的封裝 CU。 CU 存放庫是 Linux [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上所有套件安裝發行項的預設值。 如果您已設定 GDR 存放庫 (**mssql-server-2017-GDR**), 將只會取得自 GA 之後發行的重大安全性更新。 如果您需要 Docker 容器 CU 或 GDR 更新, 請參閱適用[于 Docker 引擎的 Linux 上的 Microsoft SQL Server](https://hub.docker.com/r/microsoft/mssql-server)官方映射。 如需存放庫設定的詳細資訊, 請參閱[Configure repository for Linux 上的 SQL Server](sql-server-linux-change-repo.md)。

如果您要更新現有[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的封裝, 請針對每個套件執行適當的更新命令, 以取得最新的 CU。 如需每個套件的特定更新指示, 請參閱下列安裝指南:

- [安裝 SQL Server 套件](sql-server-linux-setup.md#upgrade)
- [安裝全文檢索搜尋封裝](sql-server-linux-setup-full-text-search.md)
- [安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [啟用 SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a id="CU15"></a>CU15 (5 月 2019)

這是的累計更新 15 (CU15) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3162.1。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/en-us/help/4498951](https://support.microsoft.com/en-us/help/4498951)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3162.1-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3162.1-1 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3162.1-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3162.1-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3162.1-1_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3162.1-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU14"></a>CU14 (Mar 2019)

這是的累計更新 14 (CU14) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3076.1。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4484710](https://support.microsoft.com/help/4484710)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3076.1-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3076.1-2 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3076.1-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3076.1-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3076.1-2_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3076.1-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU13"></a>CU13 (2018 年12月)

這是的累計更新 13 (CU13) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3048.4。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4466404](https://support.microsoft.com/help/4466404)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3048.4-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3048.4-1 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3048.4-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU12"></a>CU12 (2018 年10月)

這是的累計更新 12 (CU12) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3045.24。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4464082](https://support.microsoft.com/help/4464082)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3045.24-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3045.24-1 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3045.24-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU11"></a>CU11 開始 (2018 年9月)

這是的累計更新 11 (CU11 開始) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3038.14。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4462262](https://support.microsoft.com/help/4462262)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3038.14-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3038.14-2 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3038.14-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a>CU10 (2018 年8月)

這是的累計更新 10 (CU10) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3037.1。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4342123](https://support.microsoft.com/help/4342123)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3037.1-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3037.1-2 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3037.1-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a>CU9-GDR2 (2018 年8月)

這是一種安全性更新, 其中也包含先前發行的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]CU (CU9)。 這一版的版本是14.0.3035.2。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4293805](https://support.microsoft.com/help/4293805)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3035.2-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| SLES RPM 套件 | 14.0.3035.2-1 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3035.2-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a>GDR2 (2018 年8月)

此安全性更新僅包含的 GDR2 (和 GDR1) 安全性修正[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。  這一版的版本是14.0.2002.14。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4293803](https://support.microsoft.com/help/4293803)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.2002.14-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.2002.14-1 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.2002.14-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a>CU9 (2018 年7月)

這是的累計更新 9 (CU9) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3030.27。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4341265](https://support.microsoft.com/help/4341265)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3030.27-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3030.27-1 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3030.27-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a>CU8 (2018 年6月)

這是的累計更新 8 (CU8) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3029.16。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4338363](https://support.microsoft.com/help/4338363)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3029.16-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3029.16-1 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3029.16-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a>CU7 (5 月 2018)

這是的累計更新 7 (CU7) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3026.27。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4229789](https://support.microsoft.com/help/4229789)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3026.27-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3026.27-2 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3026.27-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a>CU6 (Apr 2018)

這是的累計更新 6 (CU6) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3025.34。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4101464](https://support.microsoft.com/help/4101464)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3025.34-3 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3025.34-3 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3025.34-3 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a>CU5 (Mar 2018)

這是的累計更新 5 (CU5) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3023.8。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4092643](https://support.microsoft.com/help/4092643)請參閱。

### <a name="known-upgrade-issue"></a>已知的升級問題

當您從舊版升級至 CU5 時, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]可能會因為下列錯誤而無法啟動:

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

若要解決此錯誤, 請啟用 SQL Server Agent [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]並使用下列命令重新開機:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3023.8-5 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3023.8-5 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3023.8-5 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a>CU4 (2018 年2月)

這是的累計更新 4 (CU4) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3022.28。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4056498](https://support.microsoft.com/help/4056498)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

> [!NOTE]
> 從 CU4, 不會再將 SQL Server Agent 安裝為個別套件。 它會與引擎套件一起安裝, 而且必須啟用才能使用。

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3022.28-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3022.28-2 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3022.28-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a>GDR1 (2018 年1月)

這是僅包含 GDR1 安全性修正[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]的安全性更新。 這一版的版本是14.0.2000.63版。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4057122](https://support.microsoft.com/help/4057122)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.2000.63-3 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.2000.63-3 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.2000.63-3 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a>CU3 (2018 年1月)

這是的累積更新 3 (CU3) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3015.40。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4052987](https://support.microsoft.com/help/4052987)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3015.40-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3015.40-1 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3015.40-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[SQL Server Agent Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a>CU2 (2017 年11月)

這是的累積更新 2 (CU2) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3008.27。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3008.27-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3008.27-1 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3008.27-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[SQL Server Agent Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a>CU1 (2017 年10月)

這是的累積更新 1 (CU1) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.3006.16。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 如需此版本中修正和改善的詳細資訊, [https://support.microsoft.com/help/KB4053439](https://support.microsoft.com/help/4038634)請參閱。

### <a name="package-details"></a>封裝詳細資料

針對手動或離線套件安裝, 您可以使用下表中的資訊下載 RPM 和 Debian 套件:

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3006.16-3 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3006.16-3 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.3006.16-3 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server Agent Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a>GA (2017 年10月)

這是的公開上市 (GA) 版本[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]。 這一版的版本是14.0.1000.169。[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]

### <a name="package-details"></a>封裝詳細資料

下表列出 RPM 和 Debian 套件的套件詳細資料和下載位置。 請注意, 如果您使用下列安裝指南中的步驟, 則不需要直接下載這些套件:

- [安裝 SQL Server 套件](sql-server-linux-setup.md)
- [安裝全文檢索搜尋封裝](sql-server-linux-setup-full-text-search.md)
- [安裝 SQL Server Agent 套件](sql-server-linux-setup-sql-agent.md)
- [安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.1000.169-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.1000.169-2 | [mssql-伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server Agent RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 套件 | 14.0.1000.169-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server Agent Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a>不支援的功能 & 服務

在 GA 發行時, Linux 上不提供下列功能和服務。 這些功能的支援會隨著時間逐漸啟用。

| 區域 | 不支援的功能或服務 |
|-----|-----|
| **資料庫引擎** | 異動複寫 |
| &nbsp; | 合併式複寫 |
| &nbsp; | 變更資料捕獲 (請參閱 SQL Server Agent) |
| &nbsp; | Stretch DB |
| &nbsp; | PolyBase |
| &nbsp; | 具有協力廠商連接的分散式查詢 |
| &nbsp; | 連結的伺服器至以外的資料來源[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  |
| &nbsp; | 系統擴充預存程式 (XP_CMDSHELL 等) |
| &nbsp; | Filetable、FILESTREAM |
| &nbsp; | 具有 EXTERNAL_ACCESS 或 UNSAFE 許可權集合的 CLR 元件 |
| &nbsp; | 緩衝集區擴充 |
| **SQL Server Agent** |  分系統CmdExec, PowerShell, 佇列讀取器, SSIS, SSAS, SSRS |
| &nbsp; | 警示 |
| &nbsp; | 記錄讀取器代理程式 |
| &nbsp; | 異動資料擷取 (CDC) |
| &nbsp; | 受管理備份 |
| **高可用性** | 資料庫鏡像  |
| **安全性** | 可延伸金鑰管理 |
| &nbsp; | 連結伺服器的 AD 驗證 | 
| &nbsp; | 可用性群組的 AD 驗證 (Ag) | 
| &nbsp; | 協力廠商 AD 工具 (Centrify、Vintela、Powerbroker) | 
| **服務** | SQL Server Browser |
| &nbsp; | SQL Server R 服務 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |
| &nbsp; | 分散式交易協調器 (DTC) |

## <a name="known-issues"></a>已知問題

下列各節說明 Linux 上公開上市 (GA) 版本的[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]已知問題。

#### <a name="general"></a>一般

- 已安裝之主機名稱[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的長度必須少於或等於15個字元。 

    - **解決**方式:將/etc/hostname 中的名稱變更為少於或等於15個字元。

- 手動設定時間回溯的系統時間, 將會[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]導致停止更新內[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的內部系統時間。

    - **解決**方式:重新啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。

- 僅支援單一實例安裝。

    - **解決**方式:如果您想要在指定的主機上有一個以上的實例, 請考慮使用 Vm 或 Docker 容器。 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Configuration Manager 無法連接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Linux 上的。

- **Sa**登入的預設語言是英文。

    - **解決**方式:使用**ALTER login**語句變更**sa**登入的語言。

#### <a name="databases"></a>資料庫

- Master 資料庫無法與 mssql 工具公用程式一起移動。 其他系統資料庫則可以使用 mssql-會議來移動。

- 還原在 Windows 上備份[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的資料庫時, 您必須在 transact-sql 語句中使用**WITH MOVE**子句。

- 在 Linux 上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行時, 不支援需要 Microsoft 分散式交易協調器服務的分散式交易。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]除非[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]連結的伺服器牽涉到 DTC, 否則會予以支援。 如需詳細資訊, 請參閱[在 Linux 上執行的 SQL Server 不支援需要 Microsoft 分散式交易協調器服務的分散式交易](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/)。

- 傳輸層安全性 (TLS) 的特定演算法 (加密套件) 無法[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上正常運作。 這會導致嘗試連接到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]時發生連線失敗, 以及在高可用性群組中的複本之間建立連接的問題。

   - **解決**方式:修改 Linux  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上的 mssql 設定腳本, 以停用有問題的加密套件, 方法是執行下列動作:

      1. 將下列新增至/var/opt/mssql/mssql.conf。

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. 使用[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]下列命令重新開機。

      ```bash
      sudo systemctl restart mssql-server
      ```

- [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]使用記憶體內部 OLTP 的 Windows 資料庫無法在 Linux 上還原[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 。 若要還原[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]使用記憶體內部 OLTP 的資料庫, 請先將資料庫升級至[!INCLUDE[ssSQL15](../includes/sssql15-md.md)]或[!INCLUDE[ssSQL17](../includes/sssql17-md.md)] (在 Windows 上), [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]然後再透過備份/還原或卸離/附加將它們移至 Linux。

- Linux 目前不支援**管理大量作業**的使用者許可權。

#### <a name="networking"></a>網路

如果符合下列兩個條件, 則涉及來自 sqlservr.exe 進程之輸出 TCP 連線的功能 (例如連結的伺服器或可用性群組) 可能無法運作:

1. 目標伺服器指定為主機名, 而不是 IP 位址。

1. 來源實例在核心中已停用 IPv6。 若要確認您的系統是否已在核心中啟用 IPv6, 下列所有測試都必須通過:

   - `cat /proc/cmdline`會列印目前核心的開機 cmdline。 輸出不得包含`ipv6.disable=1`。
   - /Proc/sys/net/ipv6/目錄必須存在。
   - 呼叫`socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)`應會成功的 C 程式-syscall 必須傳回 fd! =-1, 而不會因 EAFNOSUPPORT 而失敗。

確切的錯誤取決於功能。 針對連結的伺服器, 此資訊清單為登入逾時錯誤。 針對可用性群組, 次要`ALTER AVAILABILITY GROUP JOIN`複本上的 DDL 將會在5分鐘後失敗, 並出現下載設定逾時錯誤。

若要解決此問題, 請執行下列其中一項動作:

1. 使用 Ip 而不是主機名稱來指定 TCP 連線的目標。

1. 從開機 cmdline 中移除`ipv6.disable=1` , 以在核心中啟用 IPv6。 執行此動作的方式取決於 Linux 散發套件和開機載入器, 例如 grub。 如果您想要停用 IPv6, 您仍然可以藉由設定`net.ipv6.conf.all.disable_ipv6 = 1` `sysctl` (例如`/etc/sysctl.conf`) 來停用它。 這仍會防止系統的網路介面卡取得 IPv6 位址, 但允許 sqlservr.exe 功能正常執行。

#### <a name="network-file-system-nfs"></a>網路檔案系統 (NFS)
如果您在生產環境中使用**網路檔案系統 (NFS)** 遠端共用, 請注意下列支援需求:

- 使用 NFS **4.2 版或更高**版本。 舊版的 NFS 不支援必要的功能, 例如 fallocate 和 sparse 檔案建立, 通常是現代檔案系統的通用檔案。
- 僅尋找 NFS 掛接上的 **/var/opt/mssql**目錄。 不支援其他檔案, 例如[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]系統二進位檔案。
- 請確定 NFS 用戶端在裝載遠端共用時使用 ' nolock ' 選項。

#### <a name="localization"></a>當地語系化

- 如果您的地區設定在安裝期間不是英文 (en_us), 您必須在 bash 會話/終端機中使用 UTF-8 編碼。 如果您使用 ASCII 編碼, 您可能會看到類似下面的錯誤:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   如果您無法使用 UTF-8 編碼, 請使用 MSSQL_LCID 環境變數來執行安裝程式, 以指定您的語言選擇。

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- 執行 mssql 會議安裝程式, 並執行非英文版的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]安裝時, 不正確的擴充字元會顯示在當地語系化的文字後面「正在設定 SQL Server ...」。 或者, 對於非拉丁的安裝, 句子可能完全遺失。 遺漏的句子應該會顯示下列當地語系化字串:「已成功處理授權 PID。 新的版本是 [\<Name\> edition]。 此字串僅作為資訊用途的輸出, 而下一個[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]累計更新則會針對所有語言解決此情況。 這不會[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]以任何方式影響的成功安裝。 

#### <a name="full-text-search"></a>全文檢索搜尋

- 此版本並未提供所有篩選, 包括 Office 檔的篩選。 如需支援的篩選器清單, 請參閱[在 Linux 上安裝 SQL Server 全文檢索搜尋](sql-server-linux-setup-full-text-search.md#filters)。

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- 在此版本中, SUSE 不支援**mssql 伺服器-is**封裝。 它目前在 Ubuntu 和 Red Hat Enterprise Linux (RHEL) 上受到支援。

- 在 linux CTP 2.1 重新整理和更新版本[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]上, 封裝可以在 linux 上使用 ODBC 連接。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 這種功能已經過[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]和 MySQL ODBC 驅動程式的測試, 但也應該與遵循 odbc 規格的任何 Unicode ODBC 驅動程式搭配使用。 在設計階段, 您可以提供 DSN 或連接字串來連接到 ODBC 資料;您也可以使用 Windows 驗證。 如需詳細資訊, 請參閱在[Linux 上宣佈 ODBC 支援的 blog 文章](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

- 當您在 Linux 上執行 SSIS 套件時, 此版本不支援下列功能:
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]目錄資料庫
  - SQL 代理程式的排程封裝執行
  - Windows 驗證
  - 協力廠商元件
  - 異動資料擷取 (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]Scale Out
  - 適用于 SSIS 的 Azure Feature Pack
  - Hadoop 和 HDFS 支援
  - Microsoft Connector for SAP BW

如需目前不支援或受限制支援的內建 SSIS 元件清單, 請參閱[Linux 上的 SSIS 的限制和已知問題](sql-server-linux-ssis-known-issues.md#components)。

如需有關 Linux 上 SSIS 的詳細資訊, 請參閱下列文章:
-   [宣佈適用于 Linux 的 SSIS 支援的 Blog 文章](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。
-   [在 Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [擷取、 轉換和載入與 SSIS Linux 上的資料](sql-server-linux-migrate-ssis.md)

#### <a id="ssms"></a> SQL Server Management Studio (SSMS)

下列限制適用[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]于在 Linux 上連線到[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的 Windows。

- 不支援維護計畫。

- 不支援管理資料倉儲 (MDW) 和中[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的資料收集器。 

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]具有「Windows 驗證」或「Windows 事件記錄檔」選項的 UI 元件無法與 Linux 搭配使用。 您仍然可以使用這些功能搭配其他選項, 例如 SQL 登入。 

- 無法修改要保留的記錄檔數目。

## <a name="next-steps"></a>後續步驟

若要開始使用, 請參閱下列快速入門:

- [在 Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [在 Docker 上執行](quickstart-install-connect-ubuntu.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [執行與連線 - 雲端](quickstart-install-connect-clouds.md)

如需常見問題的解答, 請參閱[LINUX 上的 SQL SERVER 常見問題](sql-server-linux-faq.md)。
