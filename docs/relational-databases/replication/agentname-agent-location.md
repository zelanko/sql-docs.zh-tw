---
title: '&lt;代理程式名稱&gt; 代理程式位置 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.agentlocation.f1
ms.assetid: dc664d80-fbe3-4586-aba8-a71fa62d14f0
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c44303cdfde6549c908e024a199f7b4635b46c7f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730242"
---
# <a name="ltagentnamegt-agent-location"></a>&lt;代理程式名稱&gt; 代理程式位置
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  合併代理程式 (用於合併訂閱) 和散發代理程式 (用於交易式與快照式訂閱) 會在散發者端或在訂閱者端執行。 如果代理程式是在散發者端執行，訂閱就稱為發送訂閱；如果代理程式是在訂閱者端執行，訂閱就稱為提取訂閱。 如需發送和提取訂閱的詳細資訊，請參閱[訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)。 透過精靈在此過程中建立的所有訂閱，都屬於選取的類型。 若要建立兩種類型的訂閱，您就必須執行精靈兩次。  
  
> [!NOTE]  
>  建立訂閱之後，就無法變更訂閱類型。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
