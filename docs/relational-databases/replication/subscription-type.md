---
title: "訂閱類型 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newsubwizard.subscriptiontype.f1
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
caps.latest.revision: "20"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cfd1ed68438aa7c79a5a6f2037cec5310fd60ce8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="subscription-type"></a>訂閱類型
  合併式複寫提供兩種訂閱類型：主訂閱與客訂閱 (對照舊版 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分別為全域與本機)。 擁有主訂閱的訂閱者可以：  
  
-   重新發行資料給其他訂閱者。  
  
-   作為替代同步夥伴。  
  
-   根據您設定的優先權解決衝突。  
  
 大多數的訂閱者不需要此功能，因此可以使用客訂閱。 客訂閱仍然允許衝突的偵測和解決，但是不會指派優先權給訂閱者：第一個提交變更至發行者的訂閱者，就會是可能引起之任何衝突的成功者。  
  
> [!NOTE]  
>  建立訂閱之後，就無法變更訂閱類型。  
  
## <a name="options"></a>選項  
 **訂閱屬性**  
 針對每個訂閱者，請從 **[訂閱類型]** 資料行的下拉式清單方塊中選取 **[客訂閱]** 或 **[主訂閱]** 。 針對擁有主訂閱的訂閱者，請在 **[衝突解決的優先權]** 資料行中輸入介於 0 和 99.99 之間的數字 (數字愈高，訂閱者的優先權就愈高)。  
  
## <a name="see-also"></a>另請參閱  
 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
