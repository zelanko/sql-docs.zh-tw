---
title: Analytics Platform System-向外延展資料倉儲中最新消息
description: 請參閱什麼是 Microsoft® Analytics Platform System 的新功能，向外延展內部部署裝載 MPP SQL Server 平行資料倉儲應用裝置。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c2408e84e7ff81f54ad00a98f85cd8dce7b04131
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/25/2018
ms.locfileid: "34550639"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>分析平台系統，向外延展 MPP 資料倉儲中最新消息
請參閱什麼是最新的應用裝置更新的 Microsoft® 分析平台 System (APS) 的新功能。 APS 是裝載 MPP SQL Server Parallel Data Warehouse 的向外延展內部部署應用裝置。 


## <a name="aps-au7"></a>APS AU7
APS2016 是升級到 AU7 的必要條件。 以下是 AP AU7 的新功能：

### <a name="auto-create-and-auto-update-statistics"></a>自動建立與 「 自動更新統計資料
APS AU7 建立，並根據預設，自動更新統計資料。 若要更新統計資料設定，系統管理員可以使用中的新功能切換功能表項目[Configuration Manager](appliance-configuration.md#CMTasks)。 [功能切換](appliance-feature-switch.md)控制 auto-create、 自動更新和非同步更新統計資料的行為。 您也可以更新統計資料設定與[ALTER DATABASE (Parallel Data Warehouse)](/sql/t-sql/statements/alter-database-parallel-data-warehouse)陳述式。

### <a name="t-sql"></a>T-SQL
選取@var現在支援。 如需詳細資訊，請參閱 [選取的本機變數] （/ sql/t-sql/language-elements/select-local-variable-transact-sql） 

現在支援雜湊和 ORDER GROUP 查詢提示。 如需詳細資訊，請參閱 [Hints(Transact-SQL)-查詢] （/sql/t-sql/查詢/提示-transact-sql 的查詢）

### <a name="feature-switch"></a>功能參數
APS AU7 導入了中的功能切換[Configuration Manager](launch-the-configuration-manager.md)。 AutoStatsEnabled 和 DmsProcessStopMessageTimeoutInSeconds 現在是系統管理員可以變更的可設定選項。

### <a name="known-issues"></a>已知問題
APS AU7 軟體，我們會封裝並提供 Intel BIOS 更新所修正"推測執行側邊通道攻擊 」 （也稱為。 Spectre 及溶解弱點）。 雖然封裝在一起，BIOS 更新手動安裝並不屬於 AP AU7 軟體安裝。 Microsoft 建議所有客戶安裝 BIOS 更新。 Microsoft 有衡量核心虛擬位址，以遮蔽 (KVAS)、 核心網頁資料表間接取值 (KPTI) 和間接分支預測防護 (IBP) 在不同環境中的各種 SQL 工作負載的效果，並大幅降低找到部分上工作負載。 我們建議您測試的效能影響，再將它們部署在生產環境中啟用 BIOS 更新。 如果啟用這些功能的效能影響現有應用程式太高，您可以考慮是否隔離您的 APS 應用裝置，從執行不受信任的程式碼是您的應用程式更佳防護功能。 請參閱 SQL Server 指導方針[這裡](https://support.microsoft.com/en-us/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)。

## <a name="aps-2016"></a>APS 2016
這些是 AP 2016 的新功能：

### <a name="sql-server-2016"></a>SQL Server 2016

APS 2016 最新的 SQL Server 2016 版本上執行，並使用預設的資料庫相容性等級 130。  SQL Server 2016 可讓您能夠支援某些新的功能，例如次要索引的叢集資料行存放區索引和 Kerberos polybase。 


### <a name="t-sql"></a>T-SQL
APS 2016 支援這些 T-SQL 的相容性增強功能。  這些額外的語言項目讓您更容易從 SQL Server 和其他資料來源移轉。 

- [資料行層級 SQL 定序][]現已支援除了 Windows 定序。
- [在叢集資料行存放區索引上的非叢集索引][]改善搜尋叢集資料行存放區索引中的特定值的查詢效能。 
- [選取此項目...到][] 
- [sp_spaceused()][]顯示使用的磁碟空間，或在資料表或資料庫中保留。
- [寬型資料表][]支援等同於 SQL Server 2016。 32k，資料列大小的前一個限制不存在。 

**資料類型**

- [VARCHAR(MAX)][]， [NVARCHAR(MAX)][]和[varbinary （max)][]。 這些 LOB 資料型別有大小上限為 2 GB。 這些載入物件使用[bcp Utility][]。 Polybase 和 dwloader 目前不支援這些資料類型。 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- [NUMERIC][]和十進位資料類型。

**視窗函數**

- [ROWS 或 RANGE][] OVER 子句的 SELECT 陳述式中。
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**安全性函數**

- [CHECKSUM()][]和[BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**其他函式**

- [NEWID()][]
- [RAND()][]

### <a name="polybasehadoop-enhancements"></a>PolyBase/Hadoop 增強功能

- 2.4 的 Hortonworks HDP 與 HDP 2.5 相容性
- 透過資料庫範圍認證的 Kerberos 支援
- 使用 Azure 儲存體 Blob 的認證支援

### <a name="install-and-upgrade-enhancements"></a>安裝和升級的增強功能

**企業架構更新**AP 2016 以升級您現有的應用裝置安裝最新的韌體和驅動程式更新，包括安全性修正程式。 

新的裝置從 HPE 或 DELL 包含所有最新的更新加上：

- 最新的層代處理器支援 (Broadwell)
- 更新至 DDR4 dimm 也可能
- 提升的 DIMM 產能

**整合**

- 完整網域名稱 (FQDN) 支援讓您能夠設定至應用裝置的網域信任。 
- 若要使用 FQDN，您需要執行完整的升級，並選擇在升級期間。 

**減少停機時間**安裝或升級至 AP 2016 速度會加快，需要較少的停機時間比先前的版本。 若要減少停機時間、 安裝或升級： 

 - 簡化使用包含到 2016 年 6 月的所有更新的映像套用 WSUS 更新
 - 套用安全性更新的驅動程式和韌體更新
 - 應用裝置上將最新的 hotfix 以及應用裝置驗證公用程式 (PAV)，因此，他們就可以不需要進行下載與安裝。


<!--MSDN references-->
[database compatibility level 130]:/sql/t-sql/statements/alter-database-transact-sql-compatibility-level
[資料行層級 SQL 定序]:/sql/relational-databases/collations/collation-and-unicode-support
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


  

  


