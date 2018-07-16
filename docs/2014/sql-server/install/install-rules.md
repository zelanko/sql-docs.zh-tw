---
title: 安裝規則 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SCC
- System Configuration Check, Setup
helpviewer_keywords:
- System Configuration Check page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, System Configuration Check page
- SCC [SQL Server]
ms.assetid: 168c0445-5651-42fc-91f4-d9f27d9e2281
caps.latest.revision: 49
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: df13e2ac5e6caf247f633e7f59ac397b2c5d22c7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251490"
---
# <a name="install-rules"></a>安裝規則
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式作業完成之前，安裝程式會驗證您的電腦組態。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間，System Configuration Checker (SCC) 會掃描將安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦。 SCC 會檢查是否有任何狀況阻止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝作業成功。 在安裝程式啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈以前，SCC 會擷取每一個項目的狀態。 然後它會比較所需條件的結果，並提供解決封鎖問題的指引。  
  
 系統組態檢查會產生報告，其中包含每個已執行規則以及執行狀態的簡短描述。 系統組態檢查報告位於 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM&AMP;GT >\\。  
  
 執行安裝作業之前，請檢閱下列主題：  
  
1.  [安裝 SQL Server 2014 的硬體與軟體需求](hardware-and-software-requirements-for-installing-sql-server.md)  
  
2.  [SQL Server 2014 各版本所支援的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
3.  [SQL Server 安裝的安全性考量](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
4.  [SQL Server 中的地區語言版本](../../../2014/sql-server/install/local-language-versions-in-sql-server.md)  
  
 其他參考資料：  
  
1.  [支援的版本與版本升級](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
2.  [安裝容錯移轉叢集之前](../failover-clusters/install/before-installing-failover-clustering.md)  
  
## <a name="additional-rule-topics"></a>其他規則主題  
 請參閱下列主題中有關特定狀況的安裝程式規則：  
  
-   [安裝規則](../../../2014/sql-server/install/installation-rules.md)  
  
-   [功能規則&#40;升級&#41;](../../../2014/sql-server/install/feature-rules-upgrade.md)  
  
-   [版本升級規則](../../../2014/sql-server/install/edition-upgrade-rules.md)  
  
-   [解除安裝規則](../../../2014/sql-server/install/uninstallation-rules.md)  
  
-   [準備映像規則](../../../2014/sql-server/install/prepare-image-rules.md)  
  
-   [完成映像規則](../../../2014/sql-server/install/complete-image-rules.md)  
  
  
