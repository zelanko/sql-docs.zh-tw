---
title: "在 Linux 上的 SQL Server 2017 的版本資訊 |Microsoft 文件"
description: "本文章包含版本資訊，並支援在 Linux 上執行的 SQL Server 2017 的功能。 版本資訊會包含最新的版次和數個先前發行的版本。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.workload: Active
ms.openlocfilehash: a661da062d65ca699627bc2b5bf0683e5fe08806
ms.sourcegitcommit: 7e9380e53341755df13fce130ab3287918a8e44c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/21/2018
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>在 Linux 上的 SQL Server 2017 的版本資訊

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

下列版本資訊適用於 SQL Server 2017 在 Linux 上執行。 這篇文章會分成區段，每個版本。 GA 版本具有可支援性和詳細的已知問題所列。 每個累計更新 (CU) 發行版本有支援文件，說明了 CU 變更以及 Linux 套件下載連結的連結。

## <a name="supported-platforms"></a>支援的平台

| 平台 | 檔案系統 | 安裝指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 或 7.4 工作站、 伺服器和桌面 | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-ubuntu.md) | 
| Docker 引擎 1.8 + Windows、 Mac 或 Linux 上 | 해당 사항 없음 | [安裝指南](quickstart-install-connect-docker.md) | 

> [!TIP]
> 如需詳細資訊，請檢閱[系統需求](sql-server-linux-setup.md#system)for SQL Server on Linux。 SQL Server 2017 最新的支援原則，請參閱[Microsoft SQL Server 的技術支援人員原則](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

## <a name="supported-client-tools"></a>支援的用戶端工具

| 工具 | 最小版本 |
|-----|-----|
| [SQL Server Management Studio (SSMS) for Windows](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools for Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com)與[mssql 延伸模組](https://aka.ms/mssql-marketplace) | 最新 |

## <a name="release-history"></a>發行記錄

下表列出 SQL Server 2017 的發行記錄。

| 版本 | 版本 | 發行日期 |
|-----|-----|-----|
| [CU4](#CU4) | 14.0.3022.28 | 2-2018 |
| [CU3](#CU3) | 14.0.3015.40 | 1-2018 |
| [CU2](#CU2) | 14.0.3008.27 | 11-2017 |
| [CU1](#CU1) | 14.0.3006.16 | 10-2017 |
| [GA](#GA) | 14.0.1000.169 | 10-2017 |

## <a id="cuinstall"></a> 如何安裝累計更新

如果您已設定的累計更新儲存機制，您會收到 SQL Server 封裝的最新累積更新時執行的新安裝。 累計更新儲存機制是所有 SQL Server on Linux 的封裝安裝發行項的預設值。 如需儲存機制設定的詳細資訊，請參閱[儲存機制設定 SQL Server on Linux](sql-server-linux-change-repo.md)。

如果您要更新現有的 SQL Server 封裝、 執行取得最新累計更新每個套件的適當更新命令。 每個套件的特定更新指示，請參閱下列的安裝指南：

- [安裝 SQL Server 封裝](sql-server-linux-setup.md#upgrade)
- [安裝全文檢索搜尋的套件](sql-server-linux-setup-full-text-search.md)
- [安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [啟用 SQL Server 代理程式](sql-server-linux-setup-sql-agent.md)

## <a id="CU4"></a> CU4 (年 2 月 2018)

這是 SQL Server 2017 的累計更新 4 (CU4) 版本。 此版本的 SQL Server 引擎版本是 14.0.3022.28。 此版本中的改進與修正的相關資訊，請參閱[https://support.microsoft.com/en-us/help/4056498](https://support.microsoft.com/en-us/help/4056498)。

### <a name="package-details"></a>封裝詳細資料

手動或離線的封裝安裝，您可以下載 RPM 和 Debian 封裝與下表中的資訊：

> [!NOTE]
> 為準，CU4，SQL Server 代理程式已不再安裝為個別的封裝。 它會隨引擎套件，並必須啟用才能使用。

| 封裝 | 封裝版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3022.28-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3022.28-2 | [mssql 伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 封裝 | 14.0.3022.28-2 | [引擎 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[高可用性 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU3"></a> CU3 (年 1 月 2018)

這是 SQL Server 2017 的累積更新 3 (CU3) 版本。 此版本的 SQL Server 引擎版本是 14.0.3015.40。 此版本中的改進與修正的相關資訊，請參閱[https://support.microsoft.com/en-us/help/4052987](https://support.microsoft.com/en-us/help/4052987)。

### <a name="package-details"></a>封裝詳細資料

手動或離線的封裝安裝，您可以下載 RPM 和 Debian 封裝與下表中的資訊：

| 封裝 | 封裝版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3015.40-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 代理程式 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3015.40-1 | [mssql 伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[SQL Server 代理程式 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 封裝 | 14.0.3015.40-1 | [引擎 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[高可用性 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[SQL Server Agent Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (11 月版 2017)

這是 SQL Server 2017 的累計更新 2 (CU2) 版本。 此版本的 SQL Server 引擎版本是 14.0.3008.27。 此版本中的改進與修正的相關資訊，請參閱[https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574)。

### <a name="package-details"></a>封裝詳細資料

手動或離線的封裝安裝，您可以下載 RPM 和 Debian 封裝與下表中的資訊：

| 封裝 | 封裝版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3008.27-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 代理程式 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3008.27-1 | [mssql 伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[SQL Server 代理程式 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 封裝 | 14.0.3008.27-1 | [引擎 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[高可用性 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[SQL Server Agent Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (第 2017 年 10 月)

這是 SQL Server 2017 的累計更新 1 (CU1) 版本。 此版本的 SQL Server 引擎版本是 14.0.3006.16。 此版本中的改進與修正的相關資訊，請參閱[https://support.microsoft.com/help/KB4053439](https://support.microsoft.com/help/4038634)。

### <a name="package-details"></a>封裝詳細資料

手動或離線的封裝安裝，您可以下載 RPM 和 Debian 封裝與下表中的資訊：

| 封裝 | 封裝版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.3006.16-3 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 代理程式 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.3006.16-3 | [mssql 伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[SQL Server 代理程式 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Ubuntu 16.04 Debian 封裝 | 14.0.3006.16-3 | [引擎 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[高可用性 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[SQL Server Agent Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> GA (第 2017 年 10 月)

這是 SQL Server 2017 的通用版本上市 (GA) 版本。 此版本的 SQL Server 引擎版本是 14.0.1000.169。

### <a name="package-details"></a>封裝詳細資料

下表中會列出套件詳細資料及針對 RPM 和 Debian 封裝的下載位置。 請注意，您不需要直接下載這些封裝，如果您使用下列的安裝指南中的步驟：

- [安裝 SQL Server 封裝](sql-server-linux-setup.md)
- [安裝全文檢索搜尋的套件](sql-server-linux-setup-full-text-search.md)
- [安裝 SQL Server 代理程式套件](sql-server-linux-setup-sql-agent.md)
- [安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| 封裝 | 封裝版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 14.0.1000.169-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 代理程式 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS 封裝](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 套件 | 14.0.1000.169-2 | [mssql 伺服器引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 代理程式 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 封裝 | 14.0.1000.169-2 | [引擎 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[高可用性 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[全文檢索搜尋 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server Agent Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS 封裝](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a> 不支援的功能與服務

下列功能和服務並不適用於 Linux 的 GA 版本時。 經過一段時間會逐漸啟用這些功能的支援。

| 區域 | 不支援的功能或服務 |
|-----|-----|
| **資料庫引擎** | 異動複寫 |
| &nbsp; | 合併式複寫 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | 合作對象第 3 層連線與分散式的查詢 |
| &nbsp; | 系統擴充預存程序 （XP_CMDSHELL 等等） |
| &nbsp; | Filetable，FILESTREAM |
| &nbsp; | CLR 組件與 EXTERNAL_ACCESS 或 UNSAFE 權限設定 |
| &nbsp; | 緩衝集區擴充 |
| **SQL Server Agent** |  子系統： CmdExec、 PowerShell、 佇列讀取器、 SSIS、 SSAS、 SSRS |
| &nbsp; | 警示 |
| &nbsp; | 記錄讀取器代理程式 |
| &nbsp; | 異動資料擷取 |
| &nbsp; | 受管理備份 |
| **高可用性** | 資料庫鏡像  |
| **安全性** | 可延伸金鑰管理 |
| &nbsp; | 連結伺服器的 AD 驗證 | 
| &nbsp; | 可用性群組 (Ag) 的 AD 驗證 | 
| &nbsp; | 第 3 個合作對象 AD 工具 (Centrify，Vintela，Powerbroker) | 
| **服務** | SQL Server Browser |
| &nbsp; | SQL Server R 服務 |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

## <a name="known-issues"></a>已知問題

下列章節說明在 Linux 上的 SQL Server 2017 的通用版本上市 (GA) 版本的已知的問題。

#### <a name="general"></a>一般

- 只能從 CTP 2.1 或更新版本支援升級至 GA 版本的 SQL Server 2017。 

- SQL Server 安裝，需要 15 個字元或更少所在的主機名稱的長度。 

    - **解析**: /etc/hosts 主機名稱中的將名稱變更為項目 15 個字元長或較少。

- 回溯時間手動將系統時間會導致 SQL Server 停止更新 SQL Server 中的內部系統時間。

    - **解析**： 重新啟動 SQL Server。

- 支援只有單一執行個體安裝。

    - **解析**： 如果您想要在指定的主機上有多個執行個體，請考慮使用 Vm 或 Docker 容器。 

- SQL Server 組態管理員無法連線到 SQL Server on Linux。

- 預設語言**sa**登入是英文。

    - **解析**： 變更語言**sa**登入，而且**ALTER LOGIN**陳述式。

#### <a name="databases"></a>資料庫

- Master 資料庫無法移動 mssql conf 公用程式。 可將其他系統資料庫移具備 mssql configuration manager

- 還原 Windows 上的 SQL Server 備份資料庫時，您必須使用**WITH MOVE**子句在 TRANSACT-SQL 陳述式中的。

- 在 Linux 上執行的 SQL Server 上不支援需要 Microsoft 分散式交易協調器服務的分散式交易。 除非所涉及的 DTC 支援連結的伺服器的 SQL server 的 SQL Server。 如需詳細資訊，請參閱[需要 Microsoft 分散式交易協調器服務的分散式交易不支援在 Linux 上執行的 SQL Server 上](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/)。

- 某些演算法 （加密套件） 的傳輸層安全性 (TLS) 無法正常運作的 SQL Server on Linux。 這會導致連接失敗時嘗試連線到 SQL Server，以及建立高可用性群組複本之間的連線問題。

   - **解析**： 修改**mssql.conf**組態指令碼的 SQL Server on Linux 停用有問題的加密套件，執行下列步驟：

      1. 將下列加入至 /var/opt/mssql/mssql.conf。

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

- 在 Linux 上的 SQL Server 2017，無法還原使用記憶體內部 OLTP 的 Windows 上的 SQL Server 2014 資料庫。 若要還原使用記憶體內部 OLTP 的 SQL Server 2014 資料庫，先將資料庫升級到 SQL Server 2016 或 Windows 上的 SQL Server 2017 之前將其移至 SQL Server on Linux 透過備份/還原或卸離/附加。

- 使用者的權限**ADMINISTER BULK OPERATIONS**此時不支援在 Linux 上。

#### <a name="networking"></a>網路

如果符合下列條件，可能無法運作的功能，需要從 sqlservr 程序，例如連結的伺服器或可用性群組的輸出 TCP 連線：

1. 目標伺服器已指定為主機名稱而不是 IP 位址。

1. 來源執行個體已在核心中停用 IPv6。 若要確認您的系統是否在核心中啟用 IPv6 的情況，必須通過所有下列測試：

   - `cat /proc/cmdline` 將會列印目前的核心的開機 cmdline。 輸出不能包含`ipv6.disable=1`。
   - Proc/sys/網路/ipv6/目錄必須存在。
   - C 程式中呼叫`socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)`應該會成功-syscall 必須傳回 fd ！ =-1，而且不會因 EAFNOSUPPORT。

確切的錯誤而定的功能。 連結的伺服器，這表示做為登入逾時錯誤。 可用性群組，`ALTER AVAILABILITY GROUP JOIN`因下載設定逾時錯誤的 5 分鐘之後將會失敗的次要複本上的 DDL。

若要解決此問題，請執行下列其中一項：

1. 若要指定 TCP 連線的目標，而不是主機名稱使用 Ip。

1. 藉由移除啟用 ipv6 環境中，核心`ipv6.disable=1`從開機 cmdline。 若要這樣做的方式取決於 Linux 散發套件和開機載入器，例如幼蟲。 如果您想要停用 IPv6，您仍可停用它藉由設定`net.ipv6.conf.all.disable_ipv6 = 1`中`sysctl`組態 (例如`/etc/sysctl.conf`)。 這仍會避免系統的網路介面卡 IPv6 位址，但是允許 sqlservr 功能運作。

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
如果您使用**網路檔案系統 (NFS)**遠端共用實際執行環境，請注意下列的支援需求：

- 使用 NFS 版本**4.2 或更新版本**。 NFS 的舊版本不支援必要的功能，例如 fallocate 和通用的現代的檔案系統的疏鬆檔案建立。
- 只尋找**/var/opt/mssql**上 NFS 掛接的目錄。 不支援其他檔案，例如 SQL Server 系統二進位檔。
- 確定 NFS 用戶端在掛接的遠端共用時，會使用 'nolock' 選項。

#### <a name="localization"></a>當地語系化

- 如果您的地區設定不是英文 (en_us) 在安裝期間，您必須使用 utf-8 編碼您 bash 工作階段/終端機中。 如果您使用 ASCII 編碼方式，您可能會看到類似下面的錯誤：

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   如果您無法使用 utf-8 編碼方式，執行安裝程式使用 MSSQL_LCID 環境變數來指定您選擇的語言。

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- 當當地語系化文字，[設定 SQL Server] 則會顯示執行 mssql conf 安裝和執行擴充字元不正確的 SQL Server 的非英文版安裝。 或者，若為非拉丁型安裝，句子可能會遺失完全。 遺失一句應該會顯示下列的當地語系化的字串:"授權 PID 已順利處理。  新的版本是 [\<名稱\>edition]"。 這個字串資訊僅供參考，輸出和 下一步的 SQL Server 累計更新可解決此適用於所有語言。 這不會影響以任何方式安裝成功的 SQL Server。 

#### <a name="full-text-search"></a>全文檢索搜尋

- 並非所有的篩選是適用於此版本中，包括 Office 文件的篩選。 如需支援的篩選器的清單，請參閱[Linux 上安裝 SQL Server 全文檢索搜尋](sql-server-linux-setup-full-text-search.md#filters)。

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- **Mssql 伺服器是**封裝 SUSE 上不支援此版本中。 目前支援在 Ubuntu 上及在 Red Hat Enterprise Linux (RHEL)。

- 在重新整理 Linux CTP 2.1 和更新版本的 SSIS，SSIS 封裝可以使用 ODBC 連接 on Linux。 這項功能經過測試可與 SQL Server 及 MySQL ODBC 驅動程式，但也應該使用 ODBC 規格會觀察到的任何 Unicode ODBC 驅動程式。 在設計階段，您可以提供 DSN 或連接字串連接至 ODBC 資料;您也可以使用 Windows 驗證。 如需詳細資訊，請參閱[部落格文章發表的 ODBC 支援在 Linux 上](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

- 當您在 Linux 上執行 SSIS 封裝時，下列功能不支援此版本中：
  - SSIS 目錄資料庫
  - SQL Agent 排程的封裝執行
  - Windows 驗證
  - 第三方元件
  - 異動資料擷取 (CDC)
  - SSIS 向外延展
  - 適用於 SSIS 的 azure 功能套件
  - Hadoop 和 HDFS 的支援
  - Microsoft Connector for SAP BW

如需內建的 SSIS 元件，目前不支援，或是支援有限制的清單，請參閱[限制與已知的問題適用於 Linux 上的 SSIS](sql-server-linux-ssis-known-issues.md#components)。

如需在 Linux 上的 SSIS 的詳細資訊，請參閱下列文章：
-   [部落格文章宣佈適用於 SSIS 支援適用於 Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。
-   [Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [擷取、 轉換和載入與 SSIS Linux 上的資料](sql-server-linux-migrate-ssis.md)

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)

下列限制適用於 SSMS 連接到 SQL Server on Linux 的 Windows 上。

- 維護計畫不支援。

- 不支援管理資料倉儲 (MDW) 和資料收集器，在 SSMS 中。 

- SSMS UI 元件的 Windows 驗證或 Windows 事件記錄檔選項與 Linux 無法運作。 您仍然可以使用這些功能與其他選項，例如 SQL 登入。 

- 若要保留的記錄檔的數目不能修改。

## <a name="next-steps"></a>後續的步驟

若要開始，請參閱下列快速入門：

- [Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [執行 docker](quickstart-install-connect-ubuntu.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
- [執行與連線 - 雲端](quickstart-install-connect-clouds.md)
