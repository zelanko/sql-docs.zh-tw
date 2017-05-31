---
title: "保護散發者 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [SQL Server replication], Distributors
- Distributors [SQL Server replication], security
ms.assetid: 76d78229-0ff2-4aa4-9b4e-ad97534c5296
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0455938e9a9b0c017da7f8546821a9f318a85d6b
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="secure-the-distributor"></a>保護散發者
  下列複寫代理程式連接到「散發者」：記錄讀取代理程式、快照集代理程式、佇列讀取器代理程式、散發代理程式及合併代理程式。 為遵循授與所需最小權限的原則，並同時保護所有密碼的儲存，有必要為這些代理程式中的每一個提供適當的登入。  
  
-   如需管理登入和密碼的資訊，請參閱[管理複寫的登入與密碼](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)。  
  
-   如需各代理程式所需權限的詳細資訊，請參閱＜ [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)＞。  
  
 除了正確管理登入與密碼外，還有必要了解 **repl_distributor** 遠端伺服器連結的角色與 **distributor_admin** 帳戶。  
  
## <a name="securing-the-connection-from-the-publisher-to-the-distributor"></a>設定從發行者到散發者連接的安全性  
 為了支援管理預存程序在「發行者」端執行並在「散發者」端更新資訊時的必要通訊，複寫會自動設定遠端伺服器 **repl_distributor**。 不管散發資料庫是包含在「發行者」執行個體 (本機「散發者」) 內還是位於遠端 **執行個體 (遠端「散發者」) 內，** repl_distributor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 遠端伺服器項目都會用於至散發資料庫的通訊。  
  
 當散發資料庫包含在本機執行個體上時，系統會自動產生並設定一個隨機密碼。 當散發資料庫位於遠端執行個體時，管理員會在設定「發行者」與「散發者」期間設定一個共用密碼；然後用這個密碼來提供往返於 **repl_distributor** 連結之傳輸量的驗證。  
  
 「散發者」使用 **repl_distributor** 遠端伺服器項目來確認呼叫伺服器已在「散發者」端設定為「發行者」，驗證「發行者」提供的密碼，並驗證預存程序在執行期間為複寫預存程序。  
  
 在設定期間為 **repl_distributor** 遠端伺服器項目設定的密碼與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入 ( **distributor_admin**，已新增到「散發者」端的 **sysadmin** 固定伺服器角色) 相關聯。 連接到「散發者」時， **distributor_admin** 登入由複寫預存程序使用。  
  
> [!NOTE]  
>  請勿手動變更 **distributor_admin** 的密碼。 請始終使用 **sp_changedistributor_password** 預存程序，或 **中** [散發者屬性] **或** [更新複寫密碼] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]對話方塊，因為密碼變更稍後會自動套用到本機發行集。  
  
## <a name="snapshot-folder-security"></a>快照集資料夾安全性  
 確定快照集共用已將讀取權限授與「合併代理程式」(針對合併式複寫) 或「散發代理程式」(針對快照式或異動複寫) 執行時所使用的帳戶，並且已將寫入權限授與「快照集代理程式」執行時所使用的帳戶。 如需快照集資料夾的詳細資訊，請參閱[保護快照集資料夾](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改複寫安全性設定](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全性與保護 &#40;複寫&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
