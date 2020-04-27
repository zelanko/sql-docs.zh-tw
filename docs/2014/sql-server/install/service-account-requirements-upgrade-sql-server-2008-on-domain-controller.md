---
title: 在網域控制站上升級至 SQL Server 2008 的服務帳戶需求 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- domain controllers
- service accounts
- network service accounts
- local service accounts
ms.assetid: 574245b6-11e2-4849-b0ca-836d673ecd0d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bb703e42edcbf128ff78ca294e08fc487f06d8f8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092260"
---
# <a name="service-account-requirements-for-upgrading-to-sql-server-2008-on-a-domain-controller"></a>在網域控制站上升級至 SQL Server 2008 的服務帳戶需求
  Upgrade Advisor 偵測到在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]網域控制站上的網路服務或本地服務帳戶底下執行的實例。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 網域控制站上安裝 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務不能以本機服務帳戶或網路服務帳戶權限執行。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 請確定所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶都指派給網域帳戶或本機系統帳戶。 如果無法在升級之前進行這項變更，系統將封鎖安裝程式。 但是，SQL 寫入器、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Active Directory Helper 服務等服務帳戶除外，因為這些服務都已硬式編碼至網路服務帳戶而且無法變更。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
