---
title: 訂閱類型 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.subscriptiontype.f1
ms.assetid: 9a50f588-ee45-4a87-826f-372ff0798587
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b3809a0f7b3113ccf1c0cfb605ae01655ecdd89e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928000"
---
# <a name="subscription-type"></a>訂閱類型
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  合併式複寫提供兩種訂閱類型：主訂閱與客訂閱 (對照舊版 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分別為全域與本機)。 擁有主訂閱的訂閱者可以：  
  
-   重新發行資料給其他訂閱者。  
  
-   作為替代同步夥伴。  
  
-   根據您設定的優先權解決衝突。  
  
 大多數的訂閱者不需要此功能，因此可以使用客訂閱。 客訂閱仍然允許衝突的偵測和解決，但是不會指派優先權給訂閱者：第一個提交變更至發行者的訂閱者，就會是可能引起之任何衝突的成功者。  
  
> [!NOTE]  
>  建立訂閱之後，就無法變更訂閱類型。  
  
## <a name="options"></a>選項。  
 **訂閱屬性**  
 針對每個訂閱者，請從 **[訂閱類型]** 資料行的下拉式清單方塊中選取 **[客訂閱]** 或 **[主訂閱]** 。 針對擁有主訂閱的訂閱者，請在 **[衝突解決的優先權]** 資料行中輸入介於 0 和 99.99 之間的數字 (數字愈高，訂閱者的優先權就愈高)。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
