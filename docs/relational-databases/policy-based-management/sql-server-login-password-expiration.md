---
title: "SQL Server 登入密碼逾期 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7e3bf9da-a436-433d-847a-47c30428cad3
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c6955ced9de05755a1846d69b5811c86efa26e76
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-login-password-expiration"></a>SQL Server 登入密碼逾期
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 此規則會檢查每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的「密碼到期」是否已啟用。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證已啟用，而且作業系統版本比 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]舊，則攻擊者可能會重複利用已知的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入密碼。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 我們建議您將作業系統升級到 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]。  
  
 如果您的環境中不需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請使用 Windows 驗證。 如需詳細資訊，請參閱 [選擇驗證模式](../../relational-databases/security/choose-an-authentication-mode.md)。  
  
 針對所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入啟用「密碼逾期」。 使用 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) 來為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入設定密碼原則。  
  
## <a name="for-more-information"></a>詳細資訊  
 [密碼原則](../../relational-databases/security/password-policy.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
