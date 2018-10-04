---
title: Linux 上的 SQL Server 2017 的版本資訊 |Microsoft Docs
description: 本文包含的版本資訊，並在 Linux 上執行的 SQL Server 2017 的支援的功能。 版本資訊會包含最新版本和先前的數個版本。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: d21f9edbc35ecf8f13d6f96f1d4f3ec9c85f31e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47752446"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Linux 上的 SQL Server 2017 的版本資訊

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

下列版本資訊適用於 SQL Server 2017 Linux 上執行。 這篇文章會分成區段，每個版本。 GA 版本已可支援性和詳細的已知問題所列。 每個累計更新 (CU) 或一般發行版本 (GDR) 具有描述 CU 的變更，以及連結至 Linux 套件下載技術支援文件的連結。

> [!TIP]
> 這些版本資訊可為 SQL Server 2017 版本。 如需有關新的 SQL Server 2019 預覽版本的詳細資訊，請參閱[在 Linux 上的 SQL Server 2019 預覽的版本資訊](sql-server-linux-release-notes-2019.md?view=sql-server-ver15)。

## <a name="supported-platforms"></a>支援的平台

| 平台 | 檔案系統 | 安裝指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 或 7.4 工作站、 伺服器和桌面 | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-ubuntu.md) | 
| Docker 引擎 1.8 以上版本 Windows、 Mac 或 Linux 上 | 不適用 | [安裝指南](quickstart-install-connect-docker.md) | 

> [!TIP]
> 如需詳細資訊，請檢閱[系統需求](sql-server-linux-setup.md#system)Linux 上的 SQL Server。 SQL Server 2017 的最新支援原則，請參閱 < [Microsoft SQL Server 的技術支援原則](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

## <a name="tools"></a>工具

大部分現有的用戶端工具的目標 SQL Server 可以順暢地，針對 Linux 上執行的 SQL Server。 有些工具可能會有適用於 Linux 的特定版本需求。 如需 SQL Server 工具的完整清單，請參閱 < [SQL Tools 和 SQL Server 公用程式](../tools/overview-sql-tools.md)。

## <a name="release-history"></a>版本歷程記錄

下表列出 SQL Server 2017 的版本歷程記錄。

| 版本               | 版本       | 發行日期 |
|-----------------------|---------------|--------------|
| [CU11](#CU11)         | 14.0.3038.14  | 2018-09-20   |
| [CU10](#CU10)         | 14.0.3037.1   | 2018-08-27   |
| [CU9 GDR2](#CU9-GDR2) | 14.0.3035.2   | 2018-08-18   |
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
| [正式運作](#GA)             | 14.0.1000.169 | 2017-10-02   |

## <a id="cuinstall"></a> 如何將更新安裝

如果您已設定的 CU 的儲存機制 (**mssql server 2017**)，則會收到最新的 SQL Server 的 CU 封裝，當您執行全新安裝。 CU 的存放庫是在 Linux 上的 SQL Server 的所有封裝安裝文章的預設值。 如果您已設定的 GDR 存放庫 (**mssql server 2017-gdr**)，只會收到重大安全性更新發行後 ga。 如果您需要 Docker 容器 CU 或 GDR 更新，請參閱官方的映像[Microsoft SQL Server on Linux 的 Docker 引擎](https://hub.docker.com/r/microsoft/mssql-server)。 如需有關存放庫組態的詳細資訊，請參閱[在 Linux 上的 SQL server 設定存放庫](sql-server-linux-change-repo.md)。

如果您要更新現有的 SQL Server 封裝、 執行適當的更新命令，針對每個封裝，以取得最新的 CU。 特定更新每個套件的指示，請參閱下列的安裝指南：

- [安裝 SQL Server 套件](sql-server-linux-setup.md#upgrade)
- [安裝全文檢索搜尋套件](sql-server-linux-setup-full-text-search.md)
- [安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [啟用 SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a id="CU11"></a> CU11 (年 9 月 2018)

這是 SQL Server 2017 的累積更新 11 (CU11) 版本。 此版本的 SQL Server 引擎版本是 14.0.3038.14。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/en-us/help/4462262 ](https://support.microsoft.com/en-us/help/4462262)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3038.14-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3038.14-2 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.3038.14-2 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a> CU10 (年 8 月 2018)

這是 SQL Server 2017 的累計更新 10 (CU10) 版本。 此版本的 SQL Server 引擎版本是 14.0.3037.1。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/en-us/help/4342123 ](https://support.microsoft.com/en-us/help/4342123)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3037.1-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3037.1-2 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.3037.1-2 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a> CU9 GDR2 (年 8 月 2018)

這是 SQL Server 2017 也包含先前發行的 CU (CU9) 的安全性更新。 此版本的 SQL Server 引擎版本是 14.0.3035.2。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/en-us/help/4293805 ](https://support.microsoft.com/en-us/help/4293805)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3035.2-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| SLES RPM 套件 | 14.0.3035.2-1 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.3035.2-1 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a> GDR2 (年 8 月 2018)

這是僅包含 SQL Server 2017 的 GDR2 （和 GDR1） 安全性修正程式的安全性更新。  此版本的 SQL Server 引擎版本是 14.0.2002.14。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/en-us/help/4293803 ](https://support.microsoft.com/en-us/help/4293803)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.2002.14-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.2002.14-1 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.2002.14-1 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a> CU9 (7 月 2018)

這是 SQL Server 2017 的累計更新 9 (CU9) 版本。 此版本的 SQL Server 引擎版本是 14.0.3030.27。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/en-us/help/4341265 ](https://support.microsoft.com/en-us/help/4341265)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3030.27-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3030.27-1 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.3030.27-1 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a> CU8 (第 2018 年 6 月)

這是 SQL Server 2017 的累積更新 8 (CU8) 版本。 此版本的 SQL Server 引擎版本是 14.0.3029.16。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/en-us/help/4338363 ](https://support.microsoft.com/en-us/help/4338363)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3029.16-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3029.16-1 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.3029.16-1 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a> CU7 (2018 年)

這是 SQL Server 2017 的累積更新 7 (CU7) 版本。 此版本的 SQL Server 引擎版本是 14.0.3026.27。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/en-us/help/4229789 ](https://support.microsoft.com/en-us/help/4229789)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3026.27-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3026.27-2 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.3026.27-2 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a> CU6 (第 2018 年 4 月)

這是 SQL Server 2017 的累計更新 6 (CU6) 版本。 此版本的 SQL Server 引擎版本是 14.0.3025.34。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3025.34-3 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3025.34-3 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.3025.34-3 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a> CU5 (第 2018 年 3 月)

這是 SQL Server 2017 的累計更新 5 (CU5) 版本。 此版本的 SQL Server 引擎版本是 14.0.3023.8。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/help/4092643 ](https://support.microsoft.com/help/4092643)。

### <a name="known-upgrade-issue"></a>已知的升級問題

當您從舊版升級至 CU5 時，SQL Server 可能無法啟動，發生下列錯誤：

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

若要解決這個錯誤，請啟用 SQL Server Agent 使用下列命令重新啟動 SQL Server:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3023.8-5 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3023.8-5 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.3023.8-5 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a> CU4 (第 2018 年 2 月)

這是 SQL Server 2017 的累計更新 4 (CU4) 版本。 此版本的 SQL Server 引擎版本是 14.0.3022.28。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/en-us/help/4056498 ](https://support.microsoft.com/en-us/help/4056498)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

> [!NOTE]
> 截至 CU4，SQL Server Agent 不會再安裝為個別的套件。 它會隨引擎套件，必須啟用才能使用。

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3022.28-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3022.28-2 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.3022.28-2 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a> GDR1 (第 2018 年 1 月)

這是僅包含 SQL Server 2017 的安全性問題修正 GDR1 安全性更新。 此版本的 SQL Server 引擎版本是 14.0.2000.63。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/en-us/help/4057122 ](https://support.microsoft.com/en-us/help/4057122)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.2000.63-3 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.2000.63-3 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.2000.63-3 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a> Cu3 開始 (第 2018 年 1 月)

這是 SQL Server 2017 的累積更新 3 (CU3) 版本。 此版本的 SQL Server 引擎版本是 14.0.3015.40。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/en-us/help/4052987 ](https://support.microsoft.com/en-us/help/4052987)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3015.40-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 代理程式的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3015.40-1 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 代理程式的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.3015.40-1 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[SQL Server Agent 中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (11 月 2017)

這是 SQL Server 2017 的累積更新 2 (CU2) 版本。 此版本的 SQL Server 引擎版本是 14.0.3008.27。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/help/4052574 ](https://support.microsoft.com/help/4052574)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3008.27-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 代理程式的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3008.27-1 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 代理程式的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.3008.27-1 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[SQL Server Agent 中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (年 10 月 2017)

這是 SQL Server 2017 的累計更新 1 (CU1) 版本。 此版本的 SQL Server 引擎版本是 14.0.3006.16。 如需此版本中的改進與修正資訊，請參閱[ https://support.microsoft.com/help/KB4053439 ](https://support.microsoft.com/help/4038634)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3006.16-3 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 代理程式的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3006.16-3 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 代理程式的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.3006.16-3 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server Agent 中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> GA (年 10 月 2017)

這是公開上市 (GA) 版本的 SQL Server 2017。 此版本的 SQL Server 引擎版本是 14.0.1000.169。

### <a name="package-details"></a>套件詳細資料

下表詳列套件詳細資料和 RPM 和 Debian 套件的下載位置。 請注意，您不需要直接下載這些套件，如果您使用下列的安裝指南中的步驟：

- [安裝 SQL Server 套件](sql-server-linux-setup.md)
- [安裝全文檢索搜尋套件](sql-server-linux-setup-full-text-search.md)
- [安裝 SQL Server 代理程式套件](sql-server-linux-setup-sql-agent.md)
- [安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.1000.169-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 代理程式的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.1000.169-2 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 代理程式的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 的 Debian 套件 | 14.0.1000.169-2 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server Agent 中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a> 不支援的功能與服務

下列功能和服務不在 Linux 上使用當時的 GA 版本。 經過一段時間都將啟用越來越多的這些功能的支援。

| 區域 | 不支援的功能或服務 |
|-----|-----|
| **資料庫引擎** | 異動複寫 |
| &nbsp; | 合併式複寫 |
| &nbsp; | Stretch DB |
| &nbsp; | PolyBase |
| &nbsp; | 分散式的查詢與第 3 方連線 |
| &nbsp; | SQL Server 以外的資料來源的連結的伺服器 |
| &nbsp; | 系統擴充預存程序 （XP_CMDSHELL 等） |
| &nbsp; | Filetable，FILESTREAM |
| &nbsp; | EXTERNAL_ACCESS 或 UNSAFE 權限的 CLR 組件設定 |
| &nbsp; | 緩衝集區擴充 |
| **SQL Server Agent** |  子系統： CmdExec、 PowerShell、 佇列讀取器、 SSIS、 SSAS、 SSRS |
| &nbsp; | 警示 |
| &nbsp; | 記錄讀取器代理程式 |
| &nbsp; | 異動資料擷取 |
| &nbsp; | 受管理備份 |
| **高可用性** | 資料庫鏡像  |
| **Security** | 可延伸金鑰管理 |
| &nbsp; | 連結伺服器的 AD 驗證 | 
| &nbsp; | 可用性群組 (Ag) 的 AD 驗證 | 
| &nbsp; | 第 3 個合作對象 AD 工具 (Centrify，Vintela，Powerbroker) | 
| **服務** | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |
| &nbsp; | 分散式的交易協調器 (DTC) |

## <a name="known-issues"></a>已知問題

下列各節說明在 Linux 上的公開上市 (GA) 版本的 SQL Server 2017 的已知的問題。

#### <a name="general"></a>一般

- 只能從 CTP 2.1 或更新版本支援升級至 GA 版本的 SQL Server 2017。 

- SQL Server 安裝，需要 15 個字元或更少所在的主機名稱的長度。 

    - **解析**: eg /etc/ 主機名稱中的將名稱變更為東西 15 個字元長或較少。

- 回溯的時間手動設定系統時間將會停止更新 SQL Server 中的內部系統時間的 SQL Server。

    - **解析**： 重新啟動 SQL Server。

- 支援只是單一執行個體安裝。

    - **解析**： 如果您想要指定的主機上有多個執行個體，請考慮使用 Vm 或 Docker 容器。 

- SQL Server 組態管理員無法連線到 Linux 上的 SQL Server。

- 預設語言**sa**登入是英文。

    - **解析度**： 變更語言**sa**登入**ALTER LOGIN**陳述式。

#### <a name="databases"></a>資料庫

- 使用 mssql conf 公用程式無法移動 master 資料庫。 其他系統資料庫可以移動與 mssql 設定

- 還原在 Windows 上的 SQL Server 備份資料庫時，您必須使用**WITH MOVE** TRANSACT-SQL 陳述式中的子句。

- 在 Linux 上執行的 SQL Server 上不支援分散式交易，需要 Microsoft Distributed Transaction Coordinator 服務。 SQL Server 到 SQL Server，除非它們包含 DTC 支援連結的伺服器。 如需詳細資訊，請參閱 <<c0> [ 在 Linux 上執行的 SQL Server 不支援分散式交易，需要 Microsoft Distributed Transaction Coordinator 服務](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/)。

- Linux 上的 SQL Server 特定的演算法 （加密套件） 的傳輸層安全性 (TLS) 無法正常運作。 這會導致連線失敗，當您嘗試連接到 SQL Server 時，以及建立高可用性群組中的複本之間的連線問題。

   - **解析度**： 修改**mssql.conf**停用有問題的加密套件，執行下列的 Linux 上的 SQL Server 的組態指令碼：

      1. 新增下列內容到 /var/opt/mssql/mssql.conf。

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. 使用下列命令，重新啟動 SQL Server。

      ```bash
      sudo systemctl restart mssql-server
      ```

- 無法還原使用記憶體內部 OLTP 的 Windows 上的 SQL Server 2014 資料庫，在 Linux 上的 SQL Server 2017。 若要還原使用記憶體內部 OLTP 的 SQL Server 2014 資料庫，先將資料庫升級至 SQL Server 2016 或 Windows 上的 SQL Server 2017 之前將其移至 SQL Server on Linux 透過備份/還原或卸離/附加。

- 使用者的權限**ADMINISTER BULK OPERATIONS**目前不支援在 Linux 上。

#### <a name="networking"></a>網路

如果符合下列條件，牽涉到從 sqlservr 程序，例如連結的伺服器 」 或 「 可用性群組的輸出 TCP 連線的功能可能無法運作：

1. 目標伺服器指定為主機名稱，而不是 IP 位址。

1. 來源執行個體已停用核心中的 IPv6。 若要確認您的系統是否在核心中啟用 IPv6，必須通過所有下列測試：

   - `cat /proc/cmdline` 將列印的目前的核心開機 cmdline。 輸出不能包含`ipv6.disable=1`。
   - / Proc/sys/net/ipv6/目錄必須存在。
   - C 程式中呼叫`socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)`應該會成功-syscall 必須傳回 fd ！ =-1，且不會與 EAFNOSUPPORT 容錯。

確切的錯誤視功能而定。 連結的伺服器，這會顯示為登入逾時錯誤。 針對可用性群組，`ALTER AVAILABILITY GROUP JOIN`下載組態逾時錯誤的 5 分鐘之後將會失敗的次要複本上的 DDL。

若要解決此問題，請執行下列其中一項：

1. 若要指定 TCP 連線的目標，而不是主機名稱使用 Ip。

1. 藉由移除啟用核心中的 IPv6`ipv6.disable=1`從開機 cmdline。 若要這樣做的方式取決於 Linux 散發套件和開機載入器，例如 grub。 如果您想要停用 IPv6，您可以仍然停用它藉由設定`net.ipv6.conf.all.disable_ipv6 = 1`中`sysctl`組態 (例如`/etc/sysctl.conf`)。 這仍會防止系統的網路介面卡取得 IPv6 位址，但是允許 sqlservr 功能運作。

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
如果您使用**網路檔案系統 (NFS)** 遠端共用，在實際執行環境，請注意下列的支援需求：

- 使用 NFS 版本**4.2 或更新版本**。 NFS 較舊版本不支援必要的功能，例如 fallocate 及通用的最新的檔案系統的疏鬆檔案建立。
- 只找出 **/var/opt/mssql**上 NFS 掛接的目錄。 不支援其他檔案，例如 SQL Server 的系統二進位檔案。
- 請確定 NFS 用戶端在掛接的遠端共用時，會使用 'nolock' 選項。

#### <a name="localization"></a>當地語系化

- 如果您的地區設定不是英文 (en_us) 在安裝期間，您必須使用 utf-8 編碼方式在 bash 工作階段/終端機。 如果您使用 ASCII 編碼方式，您可能會看到類似下面的錯誤：

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   如果您無法使用 utf-8 編碼方式，執行安裝程式指定自選的語言使用 MSSQL_LCID 環境變數。

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- 當執行 mssql conf 安裝程式，並執行非英文版安裝的 SQL Server，不正確，擴充字元會顯示當地語系化文字，也就是 「 設定 SQL Server...」 後面。 或者，您也可以針對非拉丁型安裝，句子可能會遺漏完全。 遺漏的句子應該會顯示下列當地語系化的字串: 「 已成功處理授權 PID。  新的版本是 [\<名稱\>edition]"。 此字串資訊僅供，輸出與下一步 的 SQL Server 累計更新將解決此問題適用於所有語言。 這不會影響以任何方式安裝成功的 SQL Server。 

#### <a name="full-text-search"></a>全文檢索搜尋

- 並非所有的篩選器可用於此版本中，包括 Office 文件的篩選器。 如需支援的篩選器的清單，請參閱 <<c0> [ 在 Linux 上安裝 SQL Server 全文檢索搜尋](sql-server-linux-setup-full-text-search.md#filters)。

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- **Mssql server 是**封裝在 SUSE 上不支援此版本中。 目前支援在 Ubuntu 上和在 Red Hat Enterprise Linux (RHEL)。

- 使用重新整理 Linux CTP 2.1 和更新版本的 SSIS，SSIS 封裝可以在 Linux 上使用 ODBC 連接。 這項功能經過 SQL Server 和 MySQL ODBC 驅動程式，但也應該使用 ODBC 規格會觀察到的任何 Unicode ODBC 驅動程式。 在設計階段，您可以提供 DSN 或連接字串來連接到 ODBC 資料;您也可以使用 Windows 驗證。 如需詳細資訊，請參閱 <<c0> [ 部落格文章宣佈的 ODBC 支援在 Linux 上](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

- 在 Linux 上執行 SSIS 封裝時，下列功能不支援此版本中：
  - SSIS 目錄資料庫
  - SQL Agent 排程的封裝執行
  - Windows 驗證
  - 第三方元件
  - 異動資料擷取 (CDC)
  - SSIS 相應放大
  - Azure Feature Pack for SSIS
  - Hadoop 和 HDFS 支援
  - Microsoft Connector for SAP BW

如需內建的 SSIS 元件的目前不支援，或是支援有限制的清單，請參閱 <<c0> [ 限制與已知的問題適用於 Linux 上的 SSIS](sql-server-linux-ssis-known-issues.md#components)。

如需 Linux 上的 SSIS 的詳細資訊，請參閱下列文章：
-   [適用於 Linux 的 SSIS 支援部落格文章發表](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。
-   [在 Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [擷取、 轉換和載入與 SSIS Linux 上的資料](sql-server-linux-migrate-ssis.md)

#### <a name="-a-idssmsa-sql-server-management-studio-ssms"></a>< a ="ssms"></a> SQL Server Management Studio (SSMS)

下列限制適用於連線到 SQL Server on Linux 的 Windows 上的 SSMS。

- 維護計畫不支援。

- 不支援管理資料倉儲 (MDW) 和 SSMS 中的資料收集器。 

- SSMS UI 元件的 Windows 驗證] 或 [Windows 事件記錄檔選項不適用於 Linux。 您仍然可以使用這些功能與其他選項，例如 SQL 登入。 

- 若要保留的記錄檔數目不能修改。

## <a name="next-steps"></a>後續步驟

若要開始，請參閱下列快速入門：

- [在 Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [在 Docker 上執行](quickstart-install-connect-ubuntu.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
- [執行與連線 - 雲端](quickstart-install-connect-clouds.md)

如需常見問題的解答，請參閱[Linux 常見問題集 > 的 SQL Server](sql-server-linux-faq.md)。
