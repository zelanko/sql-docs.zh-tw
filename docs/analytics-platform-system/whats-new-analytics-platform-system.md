---
title: Analytics Platform System-向外延展資料倉儲中最新消息
description: 請參閱什麼是 Microsoft® Analytics Platform System 的新功能，擴充內部部署裝載 MPP SQL Server Parallel Data Warehouse 的設備。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b1eee6b3ca692c7935b061696b37842cda0f8326
ms.sourcegitcommit: 1d81c645dd4fb2f0a6f090711719528995a34583
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/30/2018
ms.locfileid: "37137887"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>Analytics Platform System，向外延展 MPP 資料倉儲中最新消息
請參閱什麼是最新的應用裝置更新的 Microsoft® Analytics Platform System (APS) 的新功能。 APS 是裝載 MPP SQL Server Parallel Data Warehouse 的向外延展內部部署設備。 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"

## <a name="aps-au7"></a>APS AU7
APS 2016 是升級至 AU7 的必要條件。 以下是 AP AU7 的新功能：

### <a name="auto-create-and-auto-update-statistics"></a>自動建立 」 與 「 自動更新統計資料
APS AU7 建立，並根據預設，自動更新統計資料。 若要更新統計資料設定，系統管理員可以使用中的新功能切換功能表項目[Configuration Manager](appliance-configuration.md#CMTasks)。 [功能切換](appliance-feature-switch.md)控制 auto-create、 自動更新和非同步更新統計資料的行為。 您也可以更新使用統計資料設定[ALTER DATABASE （平行資料倉儲）](/sql/t-sql/statements/alter-database-parallel-data-warehouse)陳述式。

### <a name="t-sql"></a>T-SQL
選取@var現在支援。 如需詳細資訊，請參閱 [選取的本機變數] （/ sql/t-sql/language-elements/select-local-variable-transact-sql） 

現在支援雜湊和訂單群組的查詢提示。 如需詳細資訊，請參閱 [Hints(Transact-SQL)-查詢] （/sql/t-sql/查詢/提示-transact-sql 的查詢）

### <a name="feature-switch"></a>功能參數
APS AU7 導入了在功能切換[Configuration Manager](launch-the-configuration-manager.md)。 現在已可設定的選項，系統管理員可以變更的 AutoStatsEnabled 和 DmsProcessStopMessageTimeoutInSeconds。

### <a name="known-issues"></a>已知問題
APS AU7 軟體 Intel BIOS 更新會提供其描述為問題的修正*推測性執行旁路攻擊*。 攻擊的目標是要利用所謂*Spectre 與 Meltdown 弱點*。 雖然封裝以及 AP，手動安裝的 BIOS 更新，而不是 AP AU7 軟體安裝的一部分。

Microsoft 建議所有客戶安裝 BIOS 更新。 Microsoft 已在各種環境中的各種 SQL 工作負載來測量核心虛擬位址的遮蔽功能 (KVAS)、 核心分頁表間接取值 (KPTI) 和間接的分支預測風險降低 (IBP) 的效果。 測量結果找到某些工作負載顯著降低。 根據結果，建議您測試的效能影響，再將它們部署在生產環境中啟用 BIOS 更新。 請參閱 SQL Server 指導方針[此處](https://support.microsoft.com/en-us/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)。

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"

## <a name="aps-2016"></a>APS 2016
針對 APS 2016 AU6 這一節所述的新功能。

### <a name="sql-server-2016"></a>SQL Server 2016

APS AU6 上最新的 SQL Server 2016 版本中，執行，並使用預設資料庫的相容性層級 130。 SQL Server 2016 可支援新的功能，例如：

- 叢集資料行存放區索引的次要索引。
- 針對 PolyBase Kerberos。

### <a name="t-sql"></a>T-SQL
APS AU6 支援這些 T-SQL 的相容性改進。  這些額外的語言項目，請從 SQL Server 和其他資料來源移轉的工作變得更容易。 

- [資料行層級 SQL 定序][]現已支援，除了 Windows 定序。
- [在叢集資料行存放區索引上的非叢集索引][]改善叢集資料行存放區索引中的特定值搜尋的查詢效能。 
- [選取此項目...到][] 
- [sp_spaceused()][]顯示使用的磁碟空間，或保留在資料表或資料庫中。
- [寬型資料表][]支援是 SQL Server 2016 相同。 32k 的資料列大小先前的限制不存在。 

**資料類型**

- [VARCHAR(MAX)][]， [NVARCHAR(MAX)][]並[varbinary （max)][]。 這些 LOB 資料型別有大小上限為 2 GB。 若要將這些物件使用[bcp Utility][]。 Polybase 和 dwloader 目前不支援這些資料類型。 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- [NUMERIC][]和十進位資料類型。

**視窗函式**

- [ROWS 或 RANGE][] OVER 子句的 SELECT 陳述式中。
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**安全性函式**

- [CHECKSUM()][]和[BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**其他函式**

- [NEWID()][]
- [RAND()][]

### <a name="polybasehadoop-enhancements"></a>PolyBase/Hadoop 的增強功能

- Hortonworks HDP 2.4 版和 HDP 2.5 相容性
- Kerberos 支援透過資料庫範圍認證
- 使用 Azure 儲存體 Blob 的認證支援

### <a name="install-and-upgrade-enhancements"></a>安裝和升級的增強功能

**企業架構更新**AP AU6 來升級您現有的應用裝置安裝最新的韌體和驅動程式更新，其中包括安全性修正程式。 

新的裝置，從 HPE 或 DELL 包含所有最新的更新再加上：

- 最新的產生處理器支援 (Broadwell)
- 更新為搭載 DDR4 Dimm
- 改善的 DIMM 輸送量

**整合**

- 完整網域名稱 (FQDN) 支援讓您能夠設定到設備的網域信任。 
- 若要使用 FQDN，您需要執行完整的升級且在升級期間。 

**減少停機時間**安裝或升級至 AP AU6 的速度，而且需要較少的停機時間，比之前的版本。 若要減少停機時間、 安裝或升級： 

 - 簡化使用包含截至 2016 年 6 月的所有更新的映像套用 WSUS 更新
 - 套用安全性更新的驅動程式和韌體更新
 - 會最新的 hotfix 和設備驗證公用程式 (PAV) 放在您的應用裝置，讓它們準備好要安裝不需要下載它們。

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[資料行層級 SQL 定序]: ~/relational-databases/collations/collation-and-unicode-support.md

[在叢集資料行存放區索引上的非叢集索引]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR(MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR(MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY （MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[選取此項目...到]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[寬型資料表]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp Utility]:/sql/tools/bcp-utility
[UNIQUEIDENTIFIER]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[NUMERIC]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[ROWS 或 RANGE]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[CHECKSUM()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[NEWID()]:/sql/t-sql/functions/newid-transact-sql
[RAND()]:/sql/t-sql/functions/rand-transact-sql


  

  


