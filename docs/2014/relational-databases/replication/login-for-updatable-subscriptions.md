---
title: 可更新訂閱的登入 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.updatablesubscriptionslogin.f1
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6a5cc9190c77f506b13ba8b5fba0e32d5a925570
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065873"
---
# <a name="login-for-updatable-subscriptions"></a>可更新訂閱的登入
  如果您在此精靈的 **[可更新的訂閱]** 頁面上選取 **[複寫]** ，就必須在訂閱者端指定帳戶，並使用此帳戶建立發行者的連接，以進行立即更新訂閱。 在訂閱者端引發的觸發程序，會使用這些連接將變更傳播至發行者。 即使您在 **[可更新的訂閱]** 頁面上選取 **[佇列變更且儘可能認可]** ，也需要此帳戶，因為 [新增訂閱精靈] 預設會將佇列更新設定為在必要時切換到立即更新。  
  
> [!IMPORTANT]  
>  對於複寫在發行集資料庫中建立的檢視，為連接指定的帳戶應該只被授與插入、更新及刪除資料的權限，而不應該被授與任何其他權限。 授與發行集資料庫中，以**syncobj_** 格式命名之 views 的許可權，以及 _\<HexadecimalNumber>_ 您在每個「訂閱者」上設定的帳戶。  
  
 此連接類型有三個選項可用：  
  
-   您已定義的連結伺服器或遠端伺服器。  
  
-   複寫建立的連結伺服器；以您在此精靈中指定的認證來建立連接。  
  
-   複寫建立的連結伺服器；以在訂閱者端執行變更的使用者認證來建立連接。  
  
 此精靈中可以指定前兩個選項。 您只能使用[sp_link_publication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)來指定最後一個選項;為參數指定**1**的值 **@security_mode** 。  
  
## <a name="options"></a>選項  
 **建立使用下列 SQL Server 驗證登入進行連接的連結伺服器：**  
 複寫會使用 **[登入]** 和 **[密碼]** 欄位中指定的認證，來建立連結伺服器。  
  
 **登入**  
 輸入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只具有本主題所描述之許可權的登入。  
  
 **密碼**  
 為 **[登入]** 中指定的登入輸入增強式密碼。  
  
 **確認密碼**  
 重新輸入密碼，以確認密碼輸入正確  
  
 **使用您已定義的連結伺服器或遠端伺服器。**  
 此選項需要您已定義的連結伺服器或遠端伺服器。 如需詳細資訊，請參閱[連結的伺服器 &#40;Database Engine&#41;](../linked-servers/linked-servers-database-engine.md) 和[遠端伺服器](../../database-engine/configure-windows/remote-servers.md)。 請確定連結伺服器或遠端伺服器使用的登入具有增強式密碼，且只具有此主題所描述的權限。  
  
## <a name="see-also"></a>另請參閱  
 [建立交易式發行集的可更新訂閱](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [查看及修改複寫安全性設定](security/view-and-modify-replication-security-settings.md)   
 [異動複寫的可更新訂閱](transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Subscribe to Publications](subscribe-to-publications.md)  
  
  
