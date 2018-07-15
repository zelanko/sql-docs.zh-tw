---
title: 複寫訂閱者及 AlwaysOn 可用性群組 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- failover subscribers with AlwaysOn
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 0995f269-0580-43ed-b8bf-02b9ad2d7ee6
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5b61d999215af224e626929d4b2766e045571715
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37176465"
---
# <a name="replication-subscribers-and-alwayson-availability-groups-sql-server"></a>複寫訂閱者及 AlwaysOn 可用性群組 (SQL Server)
  當包含複寫訂閱者資料庫的 AlwaysOn 可用性群組容錯移轉時，複寫訂閱可能會失敗。 如果是交易式訂閱者，當訂閱使用訂閱者的可用性群組接聽程式名稱時，散發代理程式會繼續自動複寫。 如果是合併訂閱者，複寫管理員必須透過重新建立訂閱，手動重新設定訂閱者。  
  
## <a name="what-is-supported"></a>支援項目  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫支援發行者的自動容錯移轉、交易式訂閱者的自動容錯移轉，以及合併訂閱者的手動容錯移轉。 不支援可用性資料庫的散發者容錯移轉。 AlwaysOn 無法結合 Websync 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Compact 案例。  
  
 **合併提取訂閱的容錯移轉**  
  
 提取訂閱在可用性群組容錯移轉時失敗，因為提取代理程式找不到儲存在裝載主要複本之伺服器執行個體的 **msdb** 資料庫中的作業，這個伺服器執行個體已失敗，因此無法使用。  
  
 **合併發送訂閱的容錯移轉**  
  
 發送訂閱在可用性群組容錯移轉時失敗，因為發送代理程式無法再連接至原始訂閱者上的原始訂閱資料庫。  
  
## <a name="how-to-create-transactional-subscription-in-an-alwayson-environment"></a>如何在 AlwaysOn 環境中建立交易式訂閱  
 對於異動複寫，請使用下列步驟來設定和容錯移轉訂閱者可用性群組：  
  
1.  在建立訂閱之前，將訂閱者資料庫加入至適當的 AlwaysOn 可用性群組。  
  
2.  將訂閱者的可用性群組接聽程式做為連結的伺服器加入至可用性群組的所有節點。 這個步驟可確保所有可能的容錯移轉夥伴都知道且可以連接到接聽程式。  
  
3.  使用下列＜ **建立異動複寫發送訂閱** ＞一節中的指令碼，使用訂閱者的可用性群組接聽程式名稱來建立訂閱。 在容錯移轉之後，接聽程式名稱一定會維持有效，而訂閱者的實際伺服器名稱將取決於成為新主要複本的實際節點。  
  
    > [!NOTE]  
    >  訂閱必須使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼來建立，無法使用 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]來建立。  
  
4.  如果建立提取訂閱：  
  
    1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]，在主要訂閱者節點上開啟 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 樹狀結構。  
  
    2.  識別 **提取散發代理程式** 作業，並且編輯作業。  
  
    3.  在 **執行代理程式** 作業步驟，檢查 `-Publisher` 和 `-Distributor` 參數。 確定這些參數包含發行者和散發者伺服器的正確直接伺服器和執行個體名稱。  
  
    4.  將 `-Subscriber` 參數變更為訂閱者的可用性群組接聽程式名稱。  
  
 依照這些步驟建立訂閱時，在容錯移轉後就不需要執行任何動作。  
  
## <a name="creating-a-transactional-replication-push-subscription"></a>建立異動複寫發送訂閱  
  
```  
-- commands to execute at the publisher, in the publisher database:  
use [<publisher database name>]  
EXEC sp_addsubscription @publication = N'<publication name>',   
       @subscriber = N'<availability group listener name>',   
       @destination_db = N'<subscriber database name>',   
       @subscription_type = N'Push',   
       @sync_type = N'automatic', @article = N'all', @update_mode = N'read only', @subscriber_type = 0;  
GO  
  
EXEC sp_addpushsubscription_agent @publication = N'<publication name>',   
       @subscriber = N'<availability group listener name>',   
       @subscriber_db = N'<subscriber database name>',   
       @job_login = null, @job_password = null, @subscriber_security_mode = 1;  
GO  
```  
  
## <a name="to-resume-the-merge-agents-after-the-availability-group-of-the-subscriber-fails-over"></a>若要在訂閱者的可用性群組容錯移轉之後繼續合併代理程式  
 如果是合併式複寫，複寫管理員必須透過下列步驟手動重新設定訂閱者：  
  
1.  執行`sp_subscription_cleanup`移除訂閱者端的舊訂用帳戶。 在新的主要複本 (原來為次要複本) 上執行此動作。  
  
2.  從新快照集開始建立新訂閱，重新建立訂閱。  
  
> [!NOTE]  
>  目前的程序不適用於合併式複寫訂閱者，但是合併式複寫的主要案例是非連接的使用者 (桌上型電腦、筆記型電腦、手持式裝置)，這些使用者不會在訂閱者上使用 AlwaysOn 可用性群組。  
  
  
