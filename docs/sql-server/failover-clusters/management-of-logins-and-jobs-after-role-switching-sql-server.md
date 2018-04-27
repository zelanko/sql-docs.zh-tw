---
title: 角色切換後針對登入和作業進行管理 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: failover-clusters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- role switching [SQL Server]
ms.assetid: fc2fc949-746f-40c7-b5d4-3fd51ccfbd7b
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 56aae267723d9a590d7a5b0d673dbdda49dbab04
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="management-of-logins-and-jobs-after-role-switching-sql-server"></a>角色切換後針對登入和作業進行管理 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫部署高可用性或災害復原解決方案時，為該資料庫儲存的相關資訊務必完整重現於 **master** 或 **msdb** 資料庫中。 這類相關資訊通常包括主要/主體資料庫的各項作業，以及需要連接到該資料庫的使用者或處理序的登入。 您應將此資訊複寫於裝載次要/鏡像資料庫的任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上。 可能的話，最好在角色切換之後，以程式設計方式在新的主要/主體資料庫上重現此資訊。  
  
## <a name="logins"></a>登入  
 您應該在裝載資料庫副本的每個伺服器執行個體上，重現對主體資料庫具有存取權限的登入。 當主要/主體角色切換時，只有其登入存在於新的主要/主體伺服器執行個體上的使用者才能存取新的主要/主體資料庫。 凡是未在新的主要/主體伺服器執行個體上定義登入的使用者都將遭到遺棄，以致無法存取資料庫。  
  
 若有使用者遭到遺棄，請在新的主要/主體伺服器執行個體上建立其登入並執行 [sp_change_users_login](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md)。 如需詳細資訊，請參閱 [孤立的使用者疑難排解 &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)。  
  
###  <a name="SSauthentication"></a> 使用 SQL Server 驗證或本機 Windows 登入的應用程式登入  
 如果應用程式使用 SQL Server 驗證或本機 Windows 登入，可能會由於 SID 不相符造成遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體無法解析該應用程式的登入。 SID 不相符將導致此登入成為遠端伺服器執行個體上的被遺棄使用者。 若應用程式是在容錯移轉後連接到鏡像資料庫或記錄傳送資料庫，或者連接到從備份初始化的複寫訂閱者資料庫，可能就會發生這個問題。  
  
 建議您在設定這類應用程式而要使用由遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體所裝載的資料庫時，應採取預防措施以避免此問題。 預防的方法包括從本機 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體傳送登入和密碼到遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 如需如何預防此問題的詳細資訊，請參閱知識庫文章 918992：[如何在 SQL Server 的執行個體之間傳送登入和密碼](http://support.microsoft.com/kb/918992/)。  
  
> [!NOTE]  
>  此問題會影響位於不同電腦上的 Windows 本機帳戶。 但是，網域帳戶不至於發生此問題，因為每一部電腦上的 SID 都相同。  
  
 如需詳細資訊，請參閱 Database Engine 部落格文章： [Orphaned Users with Database Mirroring and Log Shipping](http://blogs.msdn.com/b/sqlserverfaq/archive/2009/04/13/orphaned-users-with-database-mirroring-and-log-shipping.aspx) (孤立的使用者與資料庫鏡像及記錄傳送)。  
  
## <a name="jobs"></a>中稱為  
 像是備份工作這類的工作，也需要特別注意。 通常在角色切換之後，資料庫擁有者或系統管理員必須為新的主要/主體資料庫重新建立各項作業。  
  
 一旦原先的主要/主體伺服器執行個體已可使用，您便應該刪除前述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上的原始作業。 請注意，由於目前的鏡像資料庫是在 RESTORING 狀態以致無法使用，該資料庫上的作業都將失敗。  
  
> [!NOTE]  
>  不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體可能以不同的磁碟機代號等方式個別進行設定。 每個夥伴的工作都必須允許此種差異。  
  
## <a name="see-also"></a>另請參閱  
 [在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [孤立的使用者疑難排解 &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)  
  
  
