---
title: 在 Linux 上的 SQL Server 2019 preview 版本資訊
description: 這篇文章包含版本資訊和支援的功能，在 Linux 上執行的 SQL Server 2019 preview。 版本資訊會包含最新版本和先前的數個版本。
author: VanMSFT
ms.author: vanto
ms.date: 07/02/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 490b47c43e5a930f42163edc75280b2642e2dabc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67896145"
---
# <a name="release-notes-for-sql-server-2019-preview-on-linux"></a>在 Linux 上的 SQL Server 2019 preview 版本資訊

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

下列版本資訊適用於在 Linux 上執行的 SQL Server 2019 preview。 這篇文章會分成區段，每個版本。 每個版本具有描述 CU 的變更，以及連結至 Linux 套件下載技術支援文件的連結。

> [!TIP]
> 若要深入了解 SQL Server 2019 的新 Linux 功能，請參閱[的新功能 SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux)。

## <a name="supported-platforms"></a>支援的平台

| 平台 | 檔案系統 | 安裝指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3、 7.4、 7.5 或 7.6 Server | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-ubuntu.md) | 
| Docker 引擎 1.8 以上版本 Windows、 Mac 或 Linux 上 | N/A | [安裝指南](quickstart-install-connect-docker.md) | 

> [!TIP]
> 如需詳細資訊，請檢閱[系統需求](sql-server-linux-setup.md#system)Linux 上的 SQL Server。 SQL Server 2017 的最新支援原則，請參閱 < [Microsoft SQL Server 的技術支援原則](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

## <a name="tools"></a>工具

大部分現有的用戶端工具的目標 SQL Server 可以順暢地，針對 Linux 上執行的 SQL Server。 有些工具可能會有適用於 Linux 的特定版本需求。 如需 SQL Server 工具的完整清單，請參閱 < [SQL Tools 和 SQL Server 公用程式](../tools/overview-sql-tools.md)。

## <a name="release-history"></a>版本歷程記錄

下表列出 SQL Server 2019 preview，CTP 版本發行歷程記錄。

| 版本               | Version       | 發行日期 |
|-----------------------|---------------|--------------|
| [CTP 3.1](#CTP31)     | 15.0.1700.37  | 2019-6-26    |
| [CTP 3.0](#CTP30)     | 15.0.1600.8   | 2019-5-22    |
| [CTP 2.5](#CTP25)     | 15.0.1500.28  | 2019-4-24    |
| [CTP 2.4](#CTP24)     | 15.0.1400.75  | 2019-3-27    |
| [CTP 2.3](#CTP23)     | 15.0.1300.359 | 2019-3-01    |
| [CTP 2.2](#CTP22)     | 15.0.1200.24  | 2018-12-11   |
| [CTP 2.1](#CTP21)     | 15.0.1100.94  | 2018-11-06   |
| [CTP 2.0](#CTP20)     | 15.0.1000.34  | 2018-09-24   |

## <a id="cuinstall"></a> 如何將更新安裝

如果您已設定預覽儲存機制 (**mssql server 預覽版**)，則當您執行全新安裝，您會收到最新的 SQL Server CTP 套件。 如果您需要 Docker 容器映像，請參閱官方的映像[Microsoft SQL Server on Linux 的 Docker 引擎](https://hub.docker.com/r/microsoft/mssql-server/)。 如需有關存放庫組態的詳細資訊，請參閱[在 Linux 上的 SQL server 設定存放庫](sql-server-linux-change-repo.md)。

如果您要更新現有的 SQL Server 封裝、 執行適當的更新命令，針對每個封裝，以取得最新的 CU。 特定更新每個套件的指示，請參閱下列的安裝指南：

- [安裝 SQL Server 套件](sql-server-linux-setup.md#upgrade)
- [安裝全文檢索搜尋套件](sql-server-linux-setup-full-text-search.md)
- [安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [在 Linux 上安裝 SQL Server 2019 預覽版機器學習服務 R 和 Python 支援](sql-server-linux-setup-machine-learning.md)
- [安裝 PolyBase 套件](../relational-databases/polybase/polybase-linux-setup.md)
- [啟用 SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a id="CTP31"></a> CTP 3.1 (第 2019 年 6 月)

下列章節提供封裝的位置以及版 CTP 3.1 的已知的問題。 若要深入了解新功能適用於 Linux 上 SQL Server 2019，請參閱[的新功能 SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1700.37-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1700.37-2 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| Ubuntu 16.04 的 Debian 套件 | 15.0.1700.37-2 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1700.37-2_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1700.37-2_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1700.37-2_amd64.deb)</br>[擴充性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1700.37-2_amd64.deb)</br>[Java 擴充性中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1700.37-2_amd64.deb)</br>[PolyBase RPM 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1700.37-2_amd64.deb)|

## <a id="CTP30"></a> CTP 3.0 (2019 年)

下列章節提供封裝的位置以及版針對 CTP 3.0 的已知的問題。 若要深入了解新功能適用於 Linux 上 SQL Server 2019，請參閱[的新功能 SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1600.8-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1600.8-1 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| Ubuntu 16.04 的 Debian 套件 | 15.0.1600.8-1 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1600.8-1_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1600.8-1_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1600.8-1_amd64.deb)</br>[擴充性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1600.8-1_amd64.deb)</br>[Java 擴充性中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1600.8-1_amd64.deb)</br>[PolyBase RPM 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1600.8-1_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a id="msdtc"></a> Microsoft 分散式交易協調器

目前，MSDTC 會需要為未經驗證的交易。 比方說，如果您使用連結的伺服器，從 SQL Server 到 Linux 上的 SQL Server 的 Windows 上，或使用 Windows 用戶端應用程式開始在 Linux 上的 SQL Server 對分散式的交易，然後在 Windows server/用戶端上的 MSDTC 才可使用選項 否需要驗證 」。

## <a id="CTP25"></a> CTP 2.5 (Apr 2019)

下列章節提供封裝的位置以及版 CTP 2.5 的已知的問題。 若要深入了解新功能適用於 Linux 上 SQL Server 2019，請參閱[的新功能 SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1500.28-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1500.28-1 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| Ubuntu 16.04 的 Debian 套件 | 15.0.1500.28-1 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1500.28-1_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1500.28-1_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1500.28-1_amd64.deb)</br>[擴充性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1500.28-1_amd64.deb)</br>[Java 擴充性中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1500.28-1_amd64.deb)</br>[PolyBase RPM 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1500.28-1_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a id="msdtc"></a> Microsoft 分散式交易協調器

目前，MSDTC 會需要為未經驗證的交易。 比方說，如果您使用連結的伺服器，從 SQL Server 到 Linux 上的 SQL Server 的 Windows 上，或使用 Windows 用戶端應用程式開始在 Linux 上的 SQL Server 對分散式的交易，然後在 Windows server/用戶端上的 MSDTC 才可使用選項 否需要驗證 」。

## <a id="CTP24"></a> CTP 2.4 (Mar 2019)

下列各節提供封裝的位置和版的 CTP 2.4 的已知的問題。 若要深入了解新功能適用於 Linux 上 SQL Server 2019，請參閱[的新功能 SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1400.75-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1400.75-2 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Ubuntu 16.04 的 Debian 套件 | 15.0.1400.75-2 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1400.75-2_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1400.75-2_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1400.75-2_amd64.deb)</br>[擴充性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1400.75-2_amd64.deb)</br>[Java 擴充性中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1400.75-2_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a id="msdtc"></a> Microsoft 分散式交易協調器

目前，MSDTC 會需要為未經驗證的交易。 比方說，如果您使用連結的伺服器，從 SQL Server 到 Linux 上的 SQL Server 的 Windows 上，或使用 Windows 用戶端應用程式開始在 Linux 上的 SQL Server 對分散式的交易，然後在 Windows server/用戶端上的 MSDTC 才可使用選項 否需要驗證 」。

## <a id="CTP23"></a> CTP 2.3 (第 2019 年 2 月)

下列章節提供封裝的位置以及版的 CTP 2.3 的已知的問題。 若要深入了解新功能適用於 Linux 上 SQL Server 2019，請參閱[的新功能 SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1300.359-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1300.359-1 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Ubuntu 16.04 的 Debian 套件 | 15.0.1300.359-1 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1300.359-1_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1300.359-1_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1300.359-1_amd64.deb)</br>[擴充性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1300.359-1_amd64.deb)</br>[Java 擴充性中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1300.359-1_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a id="msdtc"></a> Microsoft 分散式交易協調器

目前，MSDTC 會需要為未經驗證的交易。 比方說，如果您使用連結的伺服器，從 SQL Server 到 Linux 上的 SQL Server 的 Windows 上，或使用 Windows 用戶端應用程式開始在 Linux 上的 SQL Server 對分散式的交易，然後在 Windows server/用戶端上的 MSDTC 才可使用選項 否需要驗證 」。

## <a id="CTP22"></a> CTP 2.2 (Dec 2018)

下列章節提供封裝的位置以及版 CTP 2.2 的已知的問題。 若要深入了解新功能適用於 Linux 上 SQL Server 2019，請參閱[的新功能 SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1200.24-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1200.24-2 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Ubuntu 16.04 的 Debian 套件 | 15.0.1200.24-2 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1200.24-2_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1200.24-2_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1200.24-2_amd64.deb)</br>[擴充性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1200.24-2_amd64.deb)</br>[Java 擴充性中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1200.24-2_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a id="msdtc"></a> Microsoft 分散式交易協調器

目前，MSDTC 會需要為未經驗證的交易。 比方說，如果您使用連結的伺服器，從 SQL Server 到 Linux 上的 SQL Server 的 Windows 上，或使用 Windows 用戶端應用程式開始在 Linux 上的 SQL Server 對分散式的交易，然後在 Windows server/用戶端上的 MSDTC 才可使用選項 否需要驗證 」。

## <a id="CTP21"></a> CTP 2.1 (第 2018 年 11 月)

下列章節提供封裝的位置以及版 CTP 2.1 的已知的問題。 若要深入了解新功能適用於 Linux 上 SQL Server 2019，請參閱[的新功能 SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1100.94-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1100.94-1 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Ubuntu 16.04 的 Debian 套件 | 15.0.1100.94-1 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1100.94-1_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1100.94-1_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1100.94-1_amd64.deb)</br>[擴充性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1100.94-1_amd64.deb)</br>[Java 擴充性中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1100.94-1_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft 分散式交易協調器

目前，MSDTC 會需要為未經驗證的交易。 比方說，如果您使用連結的伺服器，從 SQL Server 到 Linux 上的 SQL Server 的 Windows 上，或使用 Windows 用戶端應用程式開始在 Linux 上的 SQL Server 對分散式的交易，然後在 Windows server/用戶端上的 MSDTC 才可使用選項 否需要驗證 」。

## <a id="CTP20"></a> CTP 2.0 (第 2018 年 9 月)

下列章節提供封裝的位置以及版 CTP 2.0 的已知的問題。 若要深入了解新功能適用於 Linux 上 SQL Server 2019，請參閱[的新功能 SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

若為手動或離線套件安裝，您可以下載 RPM 和 Debian 套件使用下表中的資訊：

| 套件 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1000.34-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1000.34-2 | [mssql server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[高可用性的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[全文檢索搜尋的 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Ubuntu 16.04 的 Debian 套件 | 15.0.1000.34-2 | [引擎的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1000.34-2_amd64.deb)</br>[高可用性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1000.34-2_amd64.deb)</br>[全文檢索搜尋中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1000.34-2_amd64.deb)</br>[擴充性的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1000.34-2_amd64.deb)</br>[Java 擴充性中的 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1000.34-2_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft 分散式交易協調器

目前，MSDTC 會需要為未經驗證的交易。 比方說，如果您使用連結的伺服器，從 SQL Server 到 Linux 上的 SQL Server 的 Windows 上，或使用 Windows 用戶端應用程式開始在 Linux 上的 SQL Server 對分散式的交易，然後在 Windows server/用戶端上的 MSDTC 才可使用選項 否需要驗證 」。

## <a name="next-steps"></a>後續步驟

若要開始，請參閱下列快速入門：

- [在 Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [在 Docker 上執行](quickstart-install-connect-ubuntu.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [執行與連線 - 雲端](quickstart-install-connect-clouds.md)

如需常見問題的解答，請參閱[Linux 常見問題集 > 的 SQL Server](sql-server-linux-faq.md)。
