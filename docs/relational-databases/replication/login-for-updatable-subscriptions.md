---
title: "可更新訂閱的登入 | Microsoft Docs"
ms.custom: 
ms.date: 08/25/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newsubwizard.updatablesubscriptionslogin.f1
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bd0c4bab5c8a4474a3864df385af997febf656d9
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="login-for-updatable-subscriptions"></a>可更新訂閱的登入
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 如果您在此精靈的 [可更新的訂閱] 頁面上選取 [複寫]，就必須以訂閱者端指定帳戶，並使用此帳戶建立發行者的連線，以進行立即更新。 
  
 在訂閱者端引發的觸發程序，會使用這些連接將變更傳播至發行者。 即使您已選取 [可更新的訂閱] 頁面上的 [佇列變更且盡可能認可]，仍需要此帳戶。 [新增訂閱精靈] 依預設會設定已排入佇列的更新能夠視需要切換到立即更新。  
  
> **重要！！** 對於複寫在發行集資料庫中建立的檢視，為連接指定的帳戶應該只被授與插入、更新及刪除資料的權限。 它不應該被授與任何其他權限。 對於發行集資料庫中以 **syncobj_**\< 十六進位數字>** 格式命名的檢視，您在每一個訂閱者端設定的帳戶都應該被授與這些檢視的權限。  
  
 此連接類型有三個選項可用：  
  
-   您已定義的連結伺服器或遠端伺服器。  
  
-   複寫建立的連結伺服器；以您在此精靈中指定的認證來建立連接。  
  
-   複寫建立的連結伺服器；以在訂閱者端執行變更的使用者認證來建立連接。  
  
 此精靈中可以指定前兩個選項。 最後一個選項只能使用 [sp_link_publication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 指定；指定 **1** 給 **@security_mode** 參數。  
  
## <a name="options"></a>選項。  
 **建立使用下列 SQL Server 驗證登入進行連接的連結伺服器：**  
 複寫會使用 **[登入]** 和 **[密碼]** 欄位中指定的認證，來建立連結伺服器。  
  
 **[登入]**  
 輸入只具有此主題描述之權限的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 **[密碼]**  
 為 **[登入]**中指定的登入輸入增強式密碼。  
    
 **使用您已定義的連結伺服器或遠端伺服器。**  
 此選項需要您已定義的連結伺服器或遠端伺服器。 如需詳細資訊，請參閱[連結的伺服器 &#40;Database Engine&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md) 和[遠端伺服器](../../database-engine/configure-windows/remote-servers.md)。 請確定連結伺服器或遠端伺服器使用的登入具有增強式密碼，且只具有此主題所描述的權限。  
  
## <a name="see-also"></a>另請參閱  
 [建立交易式發行集的可更新訂閱](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [檢視及修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [異動複寫的可更新訂閱](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
