---
title: 伺服器組態選項 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- surface area configuration [SQL Server], sp_configure
- configuration options [SQL Server], when take effect
- server management [SQL Server], configuration options
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], configuring
- configuration options [SQL Server], setting
- options [SQL Server], configuration
- RECONFIGURE statement
- performance [SQL Server], servers
- configuration options [SQL Server]
- RECONFIGURE WITH OVERRIDE statement
- SQL Server, configuring
- sp_configure
- stored procedures [SQL Server], configuration options
- server configuration [SQL Server]
- administering SQL Server, configuration options
ms.assetid: 9f38eba6-39b1-4f1d-ba24-ee4f7e2bc969
caps.latest.revision: 116
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b1ae5c91b9ffebf1b4c5aba1ecaf4c2f19401d68
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035966"
---
# <a name="server-configuration-options-sql-server"></a>伺服器組態選項 (SQL Server)
  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 sp_configure 系統預存程序，透過組態選項來管理及最佳化 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 資源。 最常使用的伺服器組態選項可以透過 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來使用，而所有組態選項都可以透過 sp_configure 來存取。 在設定這些選項前，請仔細考慮這些選項對系統所造成的效果。 如需詳細資訊，請參閱[檢視或變更伺服器屬性 &#40;SQL Server&#41;](view-or-change-server-properties-sql-server.md)。  
  
> [!IMPORTANT]  
>  只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員，才可變更進階選項。  
  
## <a name="categories-of-configuration-options"></a>設定選項的範疇  
 設定選項的生效方式可能是其中之一：  
  
-   在設定選項並發出 RECONFIGURE 陳述式 (在某些情況下是 RECONFIGURE WITH OVERRIDE) 後立即生效。  
  
     -或-  
  
-   執行上述動作並重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體後。  
  
 需要重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的選項最初只會在 value 資料行中顯示變更後的值。 重新啟動之後，新值將同時出現在 value 資料行及 value_in_use 資料行。  
  
 有些選項需要重新啟動伺服器，新的組態值才能生效。 如果在重新啟動伺服器之前就設定新值並執行 sp_configure 的話，新值會出現在組態選項的 value 資料行，但不會出現在 value_in_use 資料行。 重新啟動伺服器之後，新的值就會出現在 value_in_use 資料行。  
  
 自我設定的選項是指 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會根據系統需要而自行調整的選項。 在大多數情況下，都不需以手動方式來設定這些值。 範例包括 min server memory 與 max server memory 選項，以及 user connections 選項。  
  
## <a name="configuration-options-table"></a>組態選項表  
 下表列出所有可用的組態選項、可能的設定範圍以及預設值。 組態選項會加上字母標示，如下所示：  
  
-   A= 進階選項，只能由有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員來變更，而且必須將 show advanced 選項設定為 1。  
  
-   RR = 需要重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的選項。  
  
-   SC = 自我設定的選項。  
  
    |組態選項|最小值|最大值|預設|  
    |--------------------------|-------------------|-------------------|-------------|  
    |[access check cache bucket count](access-check-cache-server-configuration-options.md) (A)|0|16384|0|  
    |[access check cache quota](access-check-cache-server-configuration-options.md) (A)|0|2147483647|0|  
    |[ad hoc distributed queries](ad-hoc-distributed-queries-server-configuration-option.md) (A)|0|@shouldalert|0|  
    |[affinity I/O mask](affinity-input-output-mask-server-configuration-option.md) (A、RR)|-2147483648|2147483647|0|  
    |[affinity64 I/O mask](affinity64-input-output-mask-server-configuration-option.md) (A，只能在 64 位元版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上使用)|-2147483648|2147483647|0|  
    |[affinity mask](affinity-mask-server-configuration-option.md) (A)|-2147483648|2147483647|0|  
    |[affinity64 mask](affinity64-mask-server-configuration-option.md) (A、RR)，只能用於 64 位元版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|-2147483648|2147483647|0|  
    |[Agent XPs](agent-xps-server-configuration-option.md) (A)|0|@shouldalert|0<br /><br /> ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟動時將變成 1。 如果在安裝期間將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 設定為自動啟動，預設值就是 0)。|  
    |[allow updates](allow-updates-server-configuration-option.md) (已過時。 請勿使用。 否則會在重新設定期間導致錯誤)。|0|@shouldalert|0|  
    |[備份總和檢查碼預設](../backup-checksum-default.md)|0|@shouldalert|0|  
    |[backup compression default](view-or-configure-the-backup-compression-default-server-configuration-option.md)|0|@shouldalert|0|  
    |[已封鎖的處理序臨界值](blocked-process-threshold-server-configuration-option.md) (A)|0|86400|0|  
    |[c2 audit mode](c2-audit-mode-server-configuration-option.md) (A、RR)|0|@shouldalert|0|  
    |[clr enabled](clr-enabled-server-configuration-option.md)|0|@shouldalert|0|  
    |[common criteria compliance enabled](common-criteria-compliance-enabled-server-configuration-option.md) (A、RR)|0|@shouldalert|0|  
    |[自主資料庫驗證](contained-database-authentication-server-configuration-option.md)|0||0|  
    |[平行處理原則的成本臨界值](configure-the-cost-threshold-for-parallelism-server-configuration-option.md) (A)|0|32767|5|  
    |[cross db ownership chaining](cross-db-ownership-chaining-server-configuration-option.md)|0|@shouldalert|0|  
    |[資料指標臨界值](configure-the-cursor-threshold-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[Database Mail XPs](database-mail-xps-server-configuration-option.md) (A)|0|@shouldalert|0|  
    |[預設全文檢索語言](configure-the-default-full-text-language-server-configuration-option.md) (A)|0|2147483647|1033|  
    |[default language](configure-the-default-language-server-configuration-option.md)|0|9999|0|  
    |[預設追蹤已啟用](default-trace-enabled-server-configuration-option.md) (A)|0|@shouldalert|@shouldalert|  
    |[不允許來自觸發程序的結果](disallow-results-from-triggers-server-configuration-option.md) (A)|0|@shouldalert|0|  
    |[EKM provider enabled](ekm-provider-enabled-server-configuration-option.md)|0|@shouldalert|0|  
    |[filestream_access_level](filestream-access-level-server-configuration-option.md)|0|2|0|  
    |[fill factor](configure-the-fill-factor-server-configuration-option.md) (A、RR)|0|100|0|  
    |ft crawl bandwidth (max)，請參閱 [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft crawl bandwidth (min)，請參閱 [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |ft notify bandwidth (max)，請參閱 [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft notify bandwidth (min)，請參閱 [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |[index create memory](configure-the-index-create-memory-server-configuration-option.md) (A、SC)|704|2147483647|0|  
    |[in-doubt xact resolution](in-doubt-xact-resolution-server-configuration-option.md) (A)|0|2|0|  
    |[lightweight pooling](lightweight-pooling-server-configuration-option.md) (A、RR)|0|@shouldalert|0|  
    |[locks](configure-the-locks-server-configuration-option.md) (A、RR、SC)|5000|2147483647|0|  
    |[max degree of parallelism](configure-the-max-degree-of-parallelism-server-configuration-option.md) (A)|0|32767|0|  
    |[max full-text crawl range](max-full-text-crawl-range-server-configuration-option.md) (A)|0|256|4|  
    |[max server memory](server-memory-server-configuration-options.md) (A、SC)|16|2147483647|2147483647|  
    |[max text repl size](configure-the-max-text-repl-size-server-configuration-option.md)|0|2147483647|65536|  
    |[max worker threads](configure-the-max-worker-threads-server-configuration-option.md) (A)|128|32767<br /><br /> (1024 是 32 位元 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的最大建議值，64 位元 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 則為 2048。)|0<br /><br /> 零表示自動設定最大的工作者執行緒數目，而這個數目是根據處理器數目，透過用於 32 位元 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的公式 (256+(\<處理器> -4) * 8) 來決定，而 64 位元 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 則為該數目的兩倍。|  
    |[media retention](configure-the-media-retention-server-configuration-option.md) (A、RR)|0|365|0|  
    |[min memory per query](configure-the-min-memory-per-query-server-configuration-option.md) (A)|512|2147483647|1024|  
    |[min server memory](server-memory-server-configuration-options.md) (A、SC)|0|2147483647|0|  
    |[巢狀觸發程序](configure-the-nested-triggers-server-configuration-option.md)|0|@shouldalert|@shouldalert|  
    |[network packet size](configure-the-network-packet-size-server-configuration-option.md) (A)|512|32767|4096|  
    |[Ole Automation Procedures](ole-automation-procedures-server-configuration-option.md) (A)|0|@shouldalert|0|  
    |[open objects](open-objects-server-configuration-option.md) (A、RR，已過時)|0|2147483647|0|  
    |[optimize for ad hoc workloads](optimize-for-ad-hoc-workloads-server-configuration-option.md) (A)|0|@shouldalert|0|  
    |[PH_timeout](ph-timeout-server-configuration-option.md) (A)|@shouldalert|3600|60|  
    |[precompute rank](precompute-rank-server-configuration-option.md) (A)|0|@shouldalert|0|  
    |[priority boost](configure-the-priority-boost-server-configuration-option.md) (A、RR)|0|@shouldalert|0|  
    |[query governor cost limit](configure-the-query-governor-cost-limit-server-configuration-option.md) (A)|0|2147483647|0|  
    |[query wait](configure-the-query-wait-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[recovery interval](configure-the-recovery-interval-server-configuration-option.md) (A、SC)|0|32767|0|  
    |[remote access](configure-the-remote-access-server-configuration-option.md) (RR)|0|@shouldalert|@shouldalert|  
    |[remote admin connections](remote-admin-connections-server-configuration-option.md)|0|@shouldalert|0|  
    |[remote login timeout](configure-the-remote-login-timeout-server-configuration-option.md)|0|2147483647|10|  
    |[remote proc trans](configure-the-remote-proc-trans-server-configuration-option.md)|0|@shouldalert|0|  
    |[remote query timeout](configure-the-remote-query-timeout-server-configuration-option.md)|0|2147483647|600|  
    |[Replication XPs Option](replication-xps-server-configuration-option.md) (A)|0|@shouldalert|0|  
    |[scan for startup procs](configure-the-scan-for-startup-procs-server-configuration-option.md) (A、RR)|0|@shouldalert|0|  
    |[server trigger recursion](server-trigger-recursion-server-configuration-option.md)|0|@shouldalert|@shouldalert|  
    |[set working set size](set-working-set-size-server-configuration-option.md) (A、RR，已過時)|0|@shouldalert|0|  
    |[show advanced options](show-advanced-options-server-configuration-option.md)|0|@shouldalert|0|  
    |[SMO and DMO XPs](smo-and-dmo-xps-server-configuration-option.md) (A)|0|@shouldalert|@shouldalert|  
    |[transform noise words](transform-noise-words-server-configuration-option.md) (A)|0|@shouldalert|0|  
    |[two digit year cutoff](configure-the-two-digit-year-cutoff-server-configuration-option.md) (A)|1753|9999|2049|  
    |[user connections](configure-the-user-connections-server-configuration-option.md) (A、RR、SC)|0|32767|0|  
    |[user options](configure-the-user-options-server-configuration-option.md)|0|32767|0|  
    |[xp_cmdshell](xp-cmdshell-server-configuration-option.md) (A)|0|@shouldalert|0|  
  
## <a name="see-also"></a>另請參閱  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
