---
title: 解決升級問題 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Upgrade Advisor [SQL Server], reference
- component issue resolution [Upgrade Advisor]
- resolving upgrade issues
- upgrade blocks [Upgrade Advisor]
- detecting upgrade issues
- finding upgrade issues
- Upgrade Advisor [SQL Server], blocking issues
- configurations preventing upgrading [Upgrade Advisor]
- locating upgrade issues
- blocking issues [Upgrade Advisor]
- issues preventing upgrading [Upgrade Advisor]
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, reference
- analyzing system [Upgrade Advisor], resolving issues
- settings preventing upgrading [Upgrade Advisor]
- upgrade issue reference [Upgrade Advisor]
- identifying upgrade issues
- fixing upgrade issues [Upgrade Advisor]
ms.assetid: 113eb435-8d36-4ed6-9790-b5e4c14809c8
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c00b08d40bc8c17013e6af19b5d11b0b7ad78c4b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058987"
---
# <a name="resolving-upgrade-issues"></a>解決升級問題
  本節中的主題描述可以偵測以及無法偵測但會影響升級或升級後續經驗的升級問題。 這些問題會依照 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件組織。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [最新升級問題](../../../2014/sql-server/install/late-breaking-upgrade-issues.md)  
  
-   [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
-   [全文檢索搜尋升級問題](../../../2014/sql-server/install/full-text-search-upgrade-issues.md)  
  
-   [複寫升級問題](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
-   [&#40;Upgrade Advisor Reporting Services 升級問題&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
-   [SQL Server Agent 升級問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
## <a name="issues-that-prevent-upgrading"></a>妨礙升級的問題  
 舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中有少數組態或設定會使您無法升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 如果安裝程式在您安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時偵測到這些問題，它會停止升級程序並要求您執行 Upgrade Advisor 並修正任何封鎖的問題。  
  
### [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
 如果下列工作列在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 升級報表上，您就必須執行必要的動作，然後才能升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]：  
  
-   [中斷連結資料庫識別碼 32767](../../../2014/sql-server/install/detach-database-id-32767.md)  
  
-   [為符合固定伺服器角色名稱的登入重新命名](../../../2014/sql-server/install/rename-logins-matching-fixed-server-role-names.md)  
  
-   [為使用者 sys 重新命名](../../../2014/sql-server/install/rename-user-sys.md)  
  
-   [使用 sp_rename 重新命名重複的索引名稱](../../../2014/sql-server/install/use-sp-rename-to-rename-duplicate-index-name.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
