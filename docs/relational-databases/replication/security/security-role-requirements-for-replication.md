---
title: "複寫的安全性角色需求 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "安全性 [SQL Server 複寫], 角色"
  - "角色 [SQL Server 複寫], 複寫"
ms.assetid: b324a80f-4319-4cb2-847b-1910c49d90e0
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 複寫的安全性角色需求
  基於使用者登入所對應之角色，複寫會限制使用者執行的特定動作。 複寫已授與特定的權限 **sysadmin** 固定伺服器角色、 **db_owner** 固定資料庫角色和登入的發行集存取清單 (PAL)。  
  
## 複寫設定的安全性角色需求  
 下表摘要描述了一般複寫設定工作所需的驗證層級：  
  
|設定工作|成員需求|  
|----------------|----------------------------|  
|啟用「散發者」、「發行者」或「訂閱者」。|**sysadmin** 在 「 發行者 」 伺服器角色。|  
|啟用資料庫進行複寫|**sysadmin** 在 「 發行者 」 伺服器角色。|  
|建立發行集。|**db_owner** 在發行者端發行集資料庫的資料庫角色或 **sysadmin** 在 「 發行者 」 伺服器角色。|  
|檢視發行集屬性。|在 「 發行者 」 的 PAL 成員 **db_owner** 在 「 發行者 」 的發行集資料庫的資料庫角色或 **sysadmin** 在 「 發行者 」 伺服器角色。|  
|建立訂閱。|**db_owner** 在發行者端發行集資料庫的資料庫角色或 **sysadmin** 在 「 發行者 」 伺服器角色。<br /><br /> **db_owner** 訂閱者的訂閱資料庫的資料庫角色或 **sysadmin** 「 訂閱者 」 的伺服器角色。|  
|設定代理程式設定檔。|**sysadmin** 「 散發者 」 的伺服器角色。|  
  
## 複寫維護的安全性角色需求  
 下表摘要描述了一般複寫維護工作所需的驗證層級：  
  
|維護工作|成員需求|  
|----------------------|----------------------------|  
|修改或卸除「散發者」、「發行者」或「訂閱者」。|**sysadmin** 適當伺服器上的伺服器角色。|  
|修改或卸除發行集。|**db_owner** 在發行者端發行集資料庫的資料庫角色或 **sysadmin** 在 「 發行者 」 伺服器角色。|  
|在「發行者」端修改或卸除訂閱。|**db_owner** 在發行者端發行集資料庫的資料庫角色或 **sysadmin** 在 「 發行者 」 伺服器角色。|  
|在「訂閱者」端修改或卸除訂閱。|**db_owner** 訂閱者的訂閱資料庫的資料庫角色或 **sysadmin** 「 訂閱者 」 的伺服器角色。|  
|標記訂閱以便重新初始化。|發送訂閱︰ **db_owner** 發行者的發行集資料庫中的資料庫角色或 **sysadmin** 在 「 發行者 」 伺服器角色。<br /><br /> 提取訂閱︰ **db_owner** 在 「 訂閱者 」 的訂閱資料庫中的資料庫角色或 **sysadmin** 「 訂閱者 」 的伺服器角色。|  
|使用「複寫監視器」來檢視複寫活動、錯誤與記錄。 使用者無法修改代理程式設定檔、 排程和等等，，除非使用者是屬於 **sysadmin** 伺服器角色。|**replmonitor** 散發者端的散發資料庫的資料庫角色或 **sysadmin** 「 散發者 」 的伺服器角色。|  
|維護複寫代理程式。|**db_owner** 適當的資料庫中的資料庫角色或 **sysadmin** 適當伺服器上的伺服器角色。<br /><br /> 如果代理程式所建立的使用者 **sysadmin** 角色和 proxy 帳戶未指定代理程式時，代理程式的內容下執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理程式帳戶。 在此情況下，使用者在 **db_owner** 角色不能修改代理程式相關聯的工作。|  
|啟動或停止複寫代理程式。|代理程式作業擁有者或 **sysadmin** 適當伺服器上的伺服器角色。|  
  
## 另請參閱  
 [複寫安全性最佳做法](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全性和保護 & #40。複寫 & #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  