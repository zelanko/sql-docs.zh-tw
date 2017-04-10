---
title: "保護散發者 | Microsoft Docs"
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
  - "安全性 [SQL Server 複寫], 散發者"
  - "散發者 [SQL Server 複寫], 安全性"
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 保護散發者
  下列複寫代理程式連接到「散發者」：記錄讀取代理程式、快照集代理程式、佇列讀取器代理程式、散發代理程式及合併代理程式。 為遵循授與所需最小權限的原則，並同時保護所有密碼的儲存，有必要為這些代理程式中的每一個提供適當的登入。  
  
-   管理登入和密碼的相關資訊，請參閱 [管理登入和密碼的複寫](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)。  
  
-   如需每個代理程式所需的權限的詳細資訊，請參閱 [複寫代理程式安全性模型](../../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
 除了適當地管理登入和密碼，請務必了解所扮演的角色 **repl_distributor** 遠端伺服器的連結和 **distributor_admin** 帳戶。  
  
## 設定從發行者到散發者連接的安全性  
 若要支援所需的通訊，在散發者端的發行者和更新資訊的系統管理的預存程序執行時，複寫會自動設定遠端伺服器 **repl_distributor**。  **Repl_distributor** 遠端伺服器項目都會用於至散發資料庫，不論是否散發資料庫是否包含在 「 發行者 」 執行個體 （本機散發者） 內還是位於遠端通訊 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體 （遠端散發者）。  
  
 當散發資料庫包含在本機執行個體上時，系統會自動產生並設定一個隨機密碼。 當散發資料庫位於遠端執行個體上時，系統管理員在 「 發行者 」 與 「 散發者 」; 在安裝期間設定共用的密碼此密碼則用來提供驗證的流量會周遊 **repl_distributor** 連結。  
  
 散發者 」 使用 **repl_distributor** 遠端伺服器項目，以驗證呼叫端的伺服器設定為發行者在散發者、 驗證 「 發行者 」 所提供的密碼和驗證預存程序是複寫預存程序期間執行。  
  
 密碼設定為 **repl_distributor** 遠端伺服器項目，在安裝期間已相關聯 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入， **distributor_admin**, ，已新增到 **sysadmin** 散發者端的固定的伺服器角色。  **Distributor_admin** 登入由複寫預存程序連接到散發者時。  
  
> [!NOTE]  
>  未變更的密碼 **distributor_admin** 手動。 一律使用 **sp_changedistributor_password** 預存程序，或 **散發者屬性** 或 **更新複寫密碼** 中的對話方塊 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], ，因為密碼自動變更，然後套用到本機發行集。  
  
## 快照集資料夾安全性  
 確定快照集共用已將讀取權限授與「合併代理程式」(針對合併式複寫) 或「散發代理程式」(針對快照式或異動複寫) 執行時所使用的帳戶，並且已將寫入權限授與「快照集代理程式」執行時所使用的帳戶。 如需快照集資料夾的詳細資訊，請參閱 [保護快照集資料夾](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
## 另請參閱  
 [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [啟用加密的連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)   
 [複寫安全性最佳做法](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全性和保護 & #40。複寫 & #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  