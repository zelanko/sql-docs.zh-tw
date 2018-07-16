---
title: 功能規則 （升級） |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 653b15db-a984-4b4b-b224-81b0285b099b
caps.latest.revision: 18
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c4a14e6c82ac731bed6fe5097a27d9be01fc04f9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257794"
---
# <a name="feature-rules-upgrade"></a>功能規則 (升級)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式作業完成之前，安裝程式會驗證您的電腦組態。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間，系統會掃描將安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦，並檢查妨礙 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝作業的狀況。 在安裝程式啟動升級精靈之前，會先擷取每個項目的狀態。 然後它會比較所需條件的結果，並提供解決封鎖問題的指引。  
  
 系統組態檢查會產生報告，其中包含每個已執行規則以及執行狀態的簡短描述。 系統組態檢查報告位於 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM&AMP;GT >\\。  
  
 執行安裝作業之前，請檢閱下列主題：  
  
1.  [安裝 SQL Server 2014 的硬體與軟體需求](hardware-and-software-requirements-for-installing-sql-server.md)  
  
2.  [SQL Server 2014 各版本所支援的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
3.  [SQL Server 安裝的安全性考量](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
4.  [SQL Server 中的地區語言版本](../../../2014/sql-server/install/local-language-versions-in-sql-server.md)  
  
 其他參考資料：  
  
1.  [支援的版本與版本升級](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
2.  [安裝容錯移轉叢集之前](../failover-clusters/install/before-installing-failover-clustering.md)  
  
## <a name="see-also"></a>另請參閱  
 [安裝規則](../../../2014/sql-server/install/install-rules.md)  
  
  
