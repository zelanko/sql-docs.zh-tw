---
title: 保護訂閱者 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], security
- Subscribers [SQL Server replication], security
- security [SQL Server replication], Subscribers
ms.assetid: c8f0d62a-8b5d-4a21-9aec-223da52bb708
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a36049bcbd2d5c043320f3e10d06005bf2f70b2c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47671216"
---
# <a name="secure-the-subscriber"></a>保護訂閱者
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  「合併代理程式」與「散發代理程式」會連接到「訂閱者」。 這些連接會在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入或 Windows 登入的內容下進行。 為遵循授與所需最小權限的原則，並同時保護所有密碼的儲存，有必要為這些代理程式提供適當的登入。 如需有關各代理程式需要的權限資訊，請參閱＜ [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)＞。  
  
## <a name="distribution-agent"></a>散發代理程式  
 每個訂閱都有一個「散發代理程式」(獨立代理程式，在「新增發行集精靈」中所建發行集的預設值)，或者每個發行集資料庫和訂閱資料庫組都有一個「散發代理程式」(共用代理程式)。 T  
  
 若要指定發送訂閱的連接資訊，請參閱[建立發送訂閱](../../../relational-databases/replication/create-a-push-subscription.md)。  
  
 若要指定提取訂閱的連接資訊，請參閱[建立提取訂閱](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
## <a name="merge-agent"></a>[合併代理程式]  
 每個合併訂閱都有其「合併代理程式」，以連接「發行者」和「訂閱者」，並更新這兩者。  
  
 若要指定發送訂閱的連接資訊，請參閱[建立發送訂閱](../../../relational-databases/replication/create-a-push-subscription.md)。  
  
 若要指定提取訂閱的連接資訊，請參閱[建立提取訂閱](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
## <a name="immediate-updating-subscriptions"></a>立即更新訂閱  
 設定立即更新訂閱時，要指定「訂閱者」用來連接到「發行者」的帳戶。 在訂閱者端引發的觸發程序，會使用這些連接將變更傳播至發行者。 此連接類型有三個選項可用：  
  
-   複寫建立的連結伺服器；用您在設定時指定的認證來建立連接。  
  
-   複寫建立的連結伺服器；以在訂閱者端執行變更的使用者認證來建立連接。  
  
-   您已定義的連結伺服器或遠端伺服器。  
  
> [!IMPORTANT]  
>  若要指定連接資訊，請使用 [sp_link_publication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 預存程序。 您也可以使用「新增訂閱精靈」的 **[可更新訂閱的登入]** 頁面，此頁面會呼叫 **sp_link_publication**。 在某些情況下，如果「訂閱者」執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Service Pack 1 (SP1) 或更新版本，且「發行者」執行較舊的版本，此預存程序可能會失敗。 如果在此情況下預存程序失敗，請將「發行者」升級為 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] SP1 或更新版本。  
  
 如需詳細資訊，請參閱[建立交易式發行集的可更新訂閱](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md)和[檢視及修改複寫安全性設定](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
> [!IMPORTANT]  
>  對於複寫在發行集資料庫中建立的檢視，為連接指定的帳戶應該只被授與插入、更新及刪除資料的權限，而不應該被授與任何其他權限。 對於發行集資料庫中以 **syncobj_**\<十六進位數字>** 格式命名的檢視，您在每一個訂閱者端設定的帳戶都應該被授與這些檢視的權限。  
  
## <a name="queued-updating-subscriptions"></a>佇列更新訂閱  
 設定佇列更新訂閱時，請注意與安全性相關的兩方面：  
  
-   每個散發者只能有一個「佇列讀取器代理程式」。 建議為每個「散發者」最多設定一個為佇列更新訂閱啟用的發行集。  
  
-   「佇列讀取器代理程式」可連接到「散發者」、「發行者」及各個「訂閱者」。  
  
    -   代理程式執行和連接到「散發者」時所用的帳戶，會在您建立代理程式時指定 (如果使用「新增訂閱精靈」，則會在建立為更新訂閱啟用的發行集時建立代理程式)。  
  
    -   代理程式連接到「發行者」時所用的帳戶，會在您為「發行者」設定散發時指定。 指定代理程式執行時所用的 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帳戶。  
  
    -   代理程式連接到「訂閱者」時所用的帳戶，會在您建立訂閱時指定。  
  
    > [!IMPORTANT]  
    >  使用「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證」以連接到「訂閱者」，然後為每個「訂閱者」的連接指定不同帳戶。 如果使用提取訂閱，複寫會永遠將連接設定為使用「Windows 驗證」(對於提取訂閱來說，複寫無法存取使用「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證」所需的「訂閱者」端中繼資料)。 在此情況下，請在設定訂閱後，將連接變更為使用「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證」。  
  
     如需詳細資訊，請參閱＜如何：建立交易式發行集的可更新訂閱 (SQL Server Management Studio)＞和[檢視及修改複寫安全性設定](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
## <a name="see-also"></a>另請參閱  
 [啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全性與保護 &#40;複寫&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
