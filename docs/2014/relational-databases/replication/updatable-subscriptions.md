---
title: 可更新的訂閱 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.updatablesubscriptions.f1
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 00d51c24583231f28ec15dd86c1848ba95c345d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63255384"
---
# <a name="updatable-subscriptions"></a>可更新的訂閱
  若為異動複寫，重複的資料應當成唯讀處理；然而，您可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者端使用可更新的訂閱，來修改複寫的資料。 如果您需要修改訂閱者端的資料，請視您的需求，使用下列其中一個選項。  
  
|可更新的訂閱類型|需求|  
|---------------------------------|------------------|  
|立即更新|發行者及訂閱者必須已建立連接，才能更新訂閱者端的資料。|  
|佇列更新|發行者和訂閱者不需要連接，即可更新訂閱者端的資料。 可以在離線時進行更新，並於稍後在發行者和訂閱者之間進行同步處理。|  
  
## <a name="options"></a>選項。  
 **複寫訂閱者變更**  
 針對每個應該能夠執行更新的訂閱者，選取 **[複寫]** 資料行中的核取方塊。 針對能夠執行更新的訂閱者，請從 **[在發行者端認可]** 資料行的下拉式清單方塊中，選取適當的選項：  
  
-   針對立即更新訂閱，請選取 **[同時認可變更]** 。  
  
-   針對佇列更新訂閱，請選取 **[佇列變更且儘可能認可]** 。  
  
## <a name="see-also"></a>另請參閱  
 [建立提取訂閱](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [訂閱發行集](subscribe-to-publications.md)   
 [異動複寫的可更新訂閱](transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
