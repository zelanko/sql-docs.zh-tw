---
title: "訂閱類型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.subscriptiontype.f1"
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 訂閱類型
  合併式複寫提供兩種訂閱類型︰ 伺服器和用戶端 (在舊版中稱為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 做為全域和區域，分別)。 擁有主訂閱的訂閱者可以：  
  
-   重新發行資料給其他訂閱者。  
  
-   作為替代同步夥伴。  
  
-   根據您設定的優先權解決衝突。  
  
 大多數的訂閱者不需要此功能，因此可以使用客訂閱。 客訂閱仍然允許衝突的偵測和解決，但是不會指派優先權給訂閱者：第一個提交變更至發行者的訂閱者，就會是可能引起之任何衝突的成功者。  
  
> [!NOTE]  
>  建立訂閱之後，就無法變更訂閱類型。  
  
## 選項  
 **訂閱屬性**  
 每個訂閱者，請選取 **用戶端** 或 **伺服器** 從下拉式清單方塊中 **訂閱類型** 資料行。 對於具有主訂閱的訂閱者，請輸入數字介於 0 到 99.99 中的 **衝突解決優先權** （數字越大，「 訂閱者 」 的優先順序愈高） 的資料行。  
  
## 另請參閱  
 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  