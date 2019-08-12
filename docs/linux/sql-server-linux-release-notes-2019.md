---
title: Linux 上的 SQL Server 2019 預覽版本資訊
description: 此文章包含在 Linux 上執行的 SQL Server 2019 預覽的版本資訊和支援功能。 其中包含最新版本和數個先前版本的版本資訊。
author: VanMSFT
ms.author: vanto
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 296581ab8052a7eab384721664fc10d675bb2d06
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68476025"
---
# <a name="release-notes-for-sql-server-2019-preview-on-linux"></a>Linux 上的 SQL Server 2019 預覽版本資訊

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

下列版本資訊適用於在 Linux 上執行的 SQL Server 2019 預覽。 此文章已針對每個版本細分為數個小節。 每個版本都具有描述 CU 變更的支援文章連結，以及能下載 Linux 套件的連結。

> [!TIP]
> 若要了解 SQL Server 2019 中的新 Linux 功能，請參閱 [SQL Server 2019 中的新功能](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux)。

## <a name="supported-platforms"></a>支援的平台

| 平台 | 檔案系統 | 安裝指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3、7.4、7.5 或 7.6 伺服器 | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS 或 EXT4 | [安裝指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker Engine 1.8+ | 不適用 | [安裝指南](quickstart-install-connect-docker.md) | 

> [!TIP]
> 如需詳細資訊，請檢閱適用於 Linux 上的 SQL Server 的[系統需求](sql-server-linux-setup.md#system)。 如需適用於 SQL Server 2017 的最新支援原則，請參閱 [Microsoft SQL Server 的技術支援原則](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

## <a name="tools"></a>工具

以 SQL Server 為目標的大部分現有用戶端工具，都可以順暢地以在 Linux 上執行的 SQL Server 為目標。 某些工具可能具有特定版本需求以和 Linux 搭配運作。 如需 SQL Server 工具的完整清單，請參閱[適用於 SQL Server 的 SQL 工具和公用程式](../tools/overview-sql-tools.md)。

## <a name="release-history"></a>版本歷程記錄

下表會列出 SQL Server 2019 預覽 CTP 版本的版本歷程記錄。

| 版本               | Version       | 發行日期 |
|-----------------------|---------------|--------------|
| [CTP 3.2](#CTP32)     | 15.0.1800.32  | 2019-7-24    |
| [CTP 3.1](#CTP31)     | 15.0.1700.37  | 2019-6-26    |
| [CTP 3.0](#CTP30)     | 15.0.1600.8   | 2019-5-22    |
| [CTP 2.5](#CTP25)     | 15.0.1500.28  | 2019-4-24    |
| [CTP 2.4](#CTP24)     | 15.0.1400.75  | 2019-3-27    |
| [CTP 2.3](#CTP23)     | 15.0.1300.359 | 2019-3-01    |
| [CTP 2.2](#CTP22)     | 15.0.1200.24  | 2018-12-11   |
| [CTP 2.1](#CTP21)     | 15.0.1100.94  | 2018-11-06   |
| [CTP 2.0](#CTP20)     | 15.0.1000.34  | 2018-09-24   |

## <a id="cuinstall"></a> 如何安裝更新

如果您已設定預覽存放庫 (**mssql-server-preview**)，則您將會在執行新安裝時取得最新版本的 SQL Server CTP 套件。 如果您需要 Docker 容器映像，請參閱[適用於 Docker 引擎之 Linux 上的 Microsoft SQL Server](https://hub.docker.com/r/microsoft/mssql-server/) \(英文\) 的官方映像。 如需存放庫設定的詳細資訊，請參閱[針對 Linux 上的 SQL Server 設定存放庫](sql-server-linux-change-repo.md)。

如果您正在更新現有的 SQL Server 套件，請針對每個套件執行適當的更新命令以取得最新的 CU。 針對每個套件的特定更新指示，請參閱下列安裝指南：

- [安裝 SQL Server 套件](sql-server-linux-setup.md#upgrade)
- [安裝全文檢索搜尋套件](sql-server-linux-setup-full-text-search.md)
- [安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [在 Linux 上安裝 SQL Server 2019 預覽機器學習服務 R 和 Python 支援](sql-server-linux-setup-machine-learning.md)
- [安裝 PolyBase 套件](../relational-databases/polybase/polybase-linux-setup.md)
- [啟用 SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a id="CTP32"></a> CTP 3.2 (2019 年 7 月)

下列各節會提供 CTP 3.2 版的套件位置和已知問題。 若要深入了解 SQL Server 2019 上適用於 Linux 的新功能，請參閱 [SQL Server 2019 中的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以搭配下表中的資訊下載 RPM 和 Debian 套件：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1800.32-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1800.32-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1800.32-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1800.32-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1800.32-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1800.32-1.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1800.32-1.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1800.32-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1800.32-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1800.32-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1800.32-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1800.32-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1800.32-1.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1800.32-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 套件 | 15.0.1800.32-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1800.32-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1800.32-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1800.32-1_amd64.deb)</br>[擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1800.32-1_amd64.deb)</br>[Java 擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1800.32-1_amd64.deb)</br>[PolyBase Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1800.32-1_amd64.deb)|

## <a id="CTP31"></a> CTP 3.1 (2019 年 6 月)

下列各節會提供 CTP 3.1 版的套件位置和已知問題。 若要深入了解 SQL Server 2019 上適用於 Linux 的新功能，請參閱 [SQL Server 2019 中的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以搭配下表中的資訊下載 RPM 和 Debian 套件：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1700.37-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1700.37-2 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 套件 | 15.0.1700.37-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1700.37-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1700.37-2_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1700.37-2_amd64.deb)</br>[擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1700.37-2_amd64.deb)</br>[Java 擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1700.37-2_amd64.deb)</br>[PolyBase RPM 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1700.37-2_amd64.deb)|

## <a id="CTP30"></a> CTP 3.0 (2019 年 5 月)

下列各節會提供 CTP 3.0 版的套件位置和已知問題。 若要深入了解 SQL Server 2019 上適用於 Linux 的新功能，請參閱 [SQL Server 2019 中的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以搭配下表中的資訊下載 RPM 和 Debian 套件：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1600.8-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1600.8-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 套件 | 15.0.1600.8-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1600.8-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1600.8-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1600.8-1_amd64.deb)</br>[擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1600.8-1_amd64.deb)</br>[Java 擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1600.8-1_amd64.deb)</br>[PolyBase RPM 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1600.8-1_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a id="msdtc"></a> Microsoft 分散式交易協調器

目前，MSDTC 會要求未經驗證的交易。 例如，如果您使用從 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的連結的伺服器，或是使用 Windows 用戶端應用程式來針對 Linux 上的 SQL Server 啟動分散式交易，則 Windows 伺服器/用戶端上的 MSDTC 便必須使用 [不需要驗證] 選項。

## <a id="CTP25"></a> CTP 2.5 (2019 年 4 月)

下列各節會提供 CTP 2.5 版的套件位置和已知問題。 若要深入了解 SQL Server 2019 上適用於 Linux 的新功能，請參閱 [SQL Server 2019 中的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以搭配下表中的資訊下載 RPM 和 Debian 套件：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1500.28-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1500.28-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[PolyBase RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 套件 | 15.0.1500.28-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1500.28-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1500.28-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1500.28-1_amd64.deb)</br>[擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1500.28-1_amd64.deb)</br>[Java 擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1500.28-1_amd64.deb)</br>[PolyBase RPM 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1500.28-1_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a id="msdtc"></a> Microsoft 分散式交易協調器

目前，MSDTC 會要求未經驗證的交易。 例如，如果您使用從 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的連結的伺服器，或是使用 Windows 用戶端應用程式來針對 Linux 上的 SQL Server 啟動分散式交易，則 Windows 伺服器/用戶端上的 MSDTC 便必須使用 [不需要驗證] 選項。

## <a id="CTP24"></a> CTP 2.4 (2019 年 3 月)

下列各節會提供 CTP 2.4 版的套件位置和已知問題。 若要深入了解 SQL Server 2019 上適用於 Linux 的新功能，請參閱 [SQL Server 2019 中的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以搭配下表中的資訊下載 RPM 和 Debian 套件：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1400.75-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1400.75-2 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 套件 | 15.0.1400.75-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1400.75-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1400.75-2_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1400.75-2_amd64.deb)</br>[擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1400.75-2_amd64.deb)</br>[Java 擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1400.75-2_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a id="msdtc"></a> Microsoft 分散式交易協調器

目前，MSDTC 會要求未經驗證的交易。 例如，如果您使用從 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的連結的伺服器，或是使用 Windows 用戶端應用程式來針對 Linux 上的 SQL Server 啟動分散式交易，則 Windows 伺服器/用戶端上的 MSDTC 便必須使用 [不需要驗證] 選項。

## <a id="CTP23"></a> CTP 2.3 (2019 年 2 月)

下列各節會提供 CTP 2.3 版的套件位置和已知問題。 若要深入了解 SQL Server 2019 上適用於 Linux 的新功能，請參閱 [SQL Server 2019 中的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以搭配下表中的資訊下載 RPM 和 Debian 套件：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1300.359-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1300.359-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 套件 | 15.0.1300.359-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1300.359-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1300.359-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1300.359-1_amd64.deb)</br>[擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1300.359-1_amd64.deb)</br>[Java 擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1300.359-1_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a id="msdtc"></a> Microsoft 分散式交易協調器

目前，MSDTC 會要求未經驗證的交易。 例如，如果您使用從 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的連結的伺服器，或是使用 Windows 用戶端應用程式來針對 Linux 上的 SQL Server 啟動分散式交易，則 Windows 伺服器/用戶端上的 MSDTC 便必須使用 [不需要驗證] 選項。

## <a id="CTP22"></a> CTP 2.2 (2018 年 12 月)

下列各節會提供 CTP 2.2 版的套件位置和已知問題。 若要深入了解 SQL Server 2019 上適用於 Linux 的新功能，請參閱 [SQL Server 2019 中的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以搭配下表中的資訊下載 RPM 和 Debian 套件：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1200.24-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1200.24-2 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 套件 | 15.0.1200.24-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1200.24-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1200.24-2_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1200.24-2_amd64.deb)</br>[擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1200.24-2_amd64.deb)</br>[Java 擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1200.24-2_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a id="msdtc"></a> Microsoft 分散式交易協調器

目前，MSDTC 會要求未經驗證的交易。 例如，如果您使用從 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的連結的伺服器，或是使用 Windows 用戶端應用程式來針對 Linux 上的 SQL Server 啟動分散式交易，則 Windows 伺服器/用戶端上的 MSDTC 便必須使用 [不需要驗證] 選項。

## <a id="CTP21"></a> CTP 2.1 (2018 年 11 月)

下列各節會提供 CTP 2.1 版的套件位置和已知問題。 若要深入了解 SQL Server 2019 上適用於 Linux 的新功能，請參閱 [SQL Server 2019 中的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以搭配下表中的資訊下載 RPM 和 Debian 套件：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1100.94-1 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1100.94-1 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Ubuntu 16.04 Debian 套件 | 15.0.1100.94-1 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1100.94-1_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1100.94-1_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1100.94-1_amd64.deb)</br>[擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1100.94-1_amd64.deb)</br>[Java 擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1100.94-1_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft 分散式交易協調器

目前，MSDTC 會要求未經驗證的交易。 例如，如果您使用從 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的連結的伺服器，或是使用 Windows 用戶端應用程式來針對 Linux 上的 SQL Server 啟動分散式交易，則 Windows 伺服器/用戶端上的 MSDTC 便必須使用 [不需要驗證] 選項。

## <a id="CTP20"></a> CTP 2.0 (2018 年 9 月)

下列各節會提供 CTP 2.0 版的套件位置和已知問題。 若要深入了解 SQL Server 2019 上適用於 Linux 的新功能，請參閱 [SQL Server 2019 中的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)。

### <a name="package-details"></a>套件詳細資料

針對手動或離線套件安裝，您可以搭配下表中的資訊下載 RPM 和 Debian 套件：

| 封裝 | 套件版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 套件 | 15.0.1000.34-2 | [引擎 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| SLES RPM 套件 | 15.0.1000.34-2 | [mssql-server 引擎 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[高可用性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[全文檢索搜尋 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Java 擴充性 RPM 套件](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Ubuntu 16.04 Debian 套件 | 15.0.1000.34-2 | [引擎 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1000.34-2_amd64.deb)</br>[高可用性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1000.34-2_amd64.deb)</br>[全文檢索搜尋 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1000.34-2_amd64.deb)</br>[擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1000.34-2_amd64.deb)</br>[Java 擴充性 Debian 套件](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1000.34-2_amd64.deb)|

### <a name="known-issues"></a>已知問題

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft 分散式交易協調器

目前，MSDTC 會要求未經驗證的交易。 例如，如果您使用從 Windows 上的 SQL Server 到 Linux 上的 SQL Server 的連結的伺服器，或是使用 Windows 用戶端應用程式來針對 Linux 上的 SQL Server 啟動分散式交易，則 Windows 伺服器/用戶端上的 MSDTC 便必須使用 [不需要驗證] 選項。

## <a name="next-steps"></a>後續步驟

若要開始使用，請參閱下列其中一個快速入門：

- [在 Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [在 Docker 上執行](quickstart-install-connect-ubuntu.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [執行與連線 - 雲端](quickstart-install-connect-clouds.md)

如需常見問題的解答，請參閱 [Linux 上的 SQL Server 常見問題集](sql-server-linux-faq.md)。
