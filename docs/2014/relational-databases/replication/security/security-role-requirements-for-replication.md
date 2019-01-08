---
title: 複寫的安全性角色需求 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], roles
- roles [SQL Server], replication
ms.assetid: b324a80f-4319-4cb2-847b-1910c49d90e0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dea87fd8144863d8098c88ee9e038cebda0b0060
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52816650"
---
# <a name="security-role-requirements-for-replication"></a>複寫的安全性角色需求
  基於使用者登入所對應之角色，複寫會限制使用者執行的特定動作。 複寫會將部份權限授與 **系統管理員 (sysadmin)** 固定伺服器角色、 **db_owner** 固定資料庫角色，以及發行集存取清單 (PAL) 中的登入。  
  
## <a name="security-role-requirements-for-replication-setup"></a>複寫設定的安全性角色需求  
 下表摘要描述了一般複寫設定工作所需的驗證層級：  
  
|設定工作|成員需求|  
|----------------|----------------------------|  
|啟用「散發者」、「發行者」或「訂閱者」。|發行者上的**系統管理員 (sysadmin)** 伺服器角色。|  
|啟用資料庫進行複寫|發行者上的**系統管理員 (sysadmin)** 伺服器角色。|  
|建立發行集。|發行者之發行集資料庫上的**db_owner** 資料庫角色，或發行者上的 **系統管理員 (sysadmin)** 伺服器角色。|  
|檢視發行集屬性。|「發行者」端的 PAL 成員，「發行者」端發行集資料庫上的 **db_owner** 資料庫角色，或「發行者」上的 **系統管理員 (sysadmin)** 伺服器角色。|  
|建立訂閱。|發行者之發行集資料庫上的**db_owner** 資料庫角色，或發行者上的 **系統管理員 (sysadmin)** 伺服器角色。<br /><br /> 發行者之訂閱資料庫上的**db_owner** 資料庫角色，或訂閱者上的 **系統管理員 (sysadmin)** 伺服器角色。|  
|設定代理程式設定檔。|「散發者」上的**系統管理員 (sysadmin)** 伺服器角色。|  
  
## <a name="security-role-requirements-for-replication-maintenance"></a>複寫維護的安全性角色需求  
 下表摘要描述了一般複寫維護工作所需的驗證層級：  
  
|維護工作|成員需求|  
|----------------------|----------------------------|  
|修改或卸除「散發者」、「發行者」或「訂閱者」。|適當伺服器上的**系統管理員 (sysadmin)** 伺服器角色。|  
|修改或卸除發行集。|發行者之發行集資料庫上的**db_owner** 資料庫角色，或發行者上的 **系統管理員 (sysadmin)** 伺服器角色。|  
|在「發行者」端修改或卸除訂閱。|發行者之發行集資料庫上的**db_owner** 資料庫角色，或發行者上的 **系統管理員 (sysadmin)** 伺服器角色。|  
|在「訂閱者」端修改或卸除訂閱。|發行者之訂閱資料庫上的**db_owner** 資料庫角色，或訂閱者上的 **系統管理員 (sysadmin)** 伺服器角色。|  
|標記訂閱以便重新初始化。|發送訂閱：「發行者」端之發行集資料庫中的 **db_owner** 資料庫角色，或在「發行者」上的 **系統管理員 (sysadmin)** 伺服器角色。<br /><br /> 提取訂閱：「訂閱者」端之訂閱資料庫中的 **db_owner** 資料庫角色，或在「訂閱者」上的 **系統管理員 (sysadmin)** 伺服器角色。|  
|使用「複寫監視器」來檢視複寫活動、錯誤與記錄。 除非使用者是 **系統管理員 (sysadmin)** 伺服器角色的成員，否則使用者無法修改代理程式設定檔、排程等等。|「散發者」端之散發資料庫上的**replmonitor** 資料庫角色，或「散發者」上的 **系統管理員 (sysadmin)** 伺服器角色。|  
|維護複寫代理程式。|適當資料庫中的**db_owner** 資料庫角色，或在適當伺服器上的 **系統管理員 (sysadmin)** 伺服器角色。<br /><br /> 如果由 **系統管理員 (sysadmin)** 角色的使用者建立了代理程式，且尚未為代理程式指定 Proxy 帳戶，則代理程式會在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 帳戶的內容下執行。 在此狀況下， **db_owner** 角色的使用者無法修改與代理程式相關聯的作業。|  
|啟動或停止複寫代理程式。|代理程式作業的擁有者或適當伺服器上的 **系統管理員 (sysadmin)** 伺服器角色。|  
  
## <a name="see-also"></a>另請參閱  
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [安全性與保護 &#40;複寫&#41;](security-and-protection-replication.md)  
  
  
