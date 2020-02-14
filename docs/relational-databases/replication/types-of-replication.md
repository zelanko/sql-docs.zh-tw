---
title: 複寫類型 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], types
ms.assetid: c1655e8d-d14c-455a-a7f9-9d2f43e88ab4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: aa6cc0eb253c0f21a1b66870f9dac2607f65e2e3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68769302"
---
# <a name="types-of-replication"></a>複寫類型
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供下列可用於分散式應用程式的複寫類型：  

| **型別** | **說明** |
|:-------- | :-------------- |
| [異動複寫](transactional/transactional-replication.md)| 發行者的變更，會在發生時傳遞給訂閱者 (近乎即時)。 當在發行者上發生變更資料時，會以相同順序和在相同交易界限內套用到訂閱者。 | 
| [合併式複寫](merge/merge-replication.md) | 您可以變更發行者和訂閱者的資料，並使用觸發程式來追蹤。 該「訂閱者」在連接到網路時會與「發行者」同步，並且在「發行者」與「訂閱者」之間交換自上次同步處理後進行過變更的所有資料列。 | 
| [快照式複寫](snapshot-replication.md) | 將快照集從發行者套用到訂閱者，這會完全依照資料出現在特定時間點的方式來散發資料，而不會監視資料的更新。 在進行同步處理的時候，會產生整個快照集並傳送至「訂閱者」。| 
| [點對點](transactional/peer-to-peer-transactional-replication.md) | 點對點複寫是以異動複寫為基礎，會以接近即時、交易式的方式，在多個伺服器執行個體之間傳播一致的變更。 | 
| [雙向](transactional/bidirectional-transactional-replication.md)| 雙向異動複寫是一種特殊的異動複寫拓撲，它可讓兩台伺服器彼此之間交換變更：每台伺服器都會發行資料，然後向發行集訂閱另一台伺服器上相同的資料。 | 
| [可更新的訂閱](transactional/updatable-subscriptions-for-transactional-replication.md) | 建置於異動複寫的基礎，當訂閱者的資料更新為可更新訂閱時，其會先傳播至發行者，再傳播到其他訂閱者。 | 
  
 
為應用程式選擇的複寫類型取決於許多因素，包括實體複寫環境、要複寫的資料類型和數量，以及資料是否在「訂閱者」端更新。 實體環境包括複寫所涉及的電腦數量和位置，以及這些電腦是用戶端 (工作站、膝上型電腦或手持式裝置) 還是伺服器。  
  
各種類型的複寫通常會先對「發行者」和「訂閱者」之間的發行物件進行初始同步處理。 此初始同步處理可由複寫使用 *「快照集」* (發行集指定之所有物件和資料的副本) 來執行。 快照集建立後會傳遞到「訂閱者」。 對於某些應用程式，只需執行快照式複寫即可。 對於其他類型的應用程式，有必要讓後續的資料變更累加地流動至「訂閱者」。 某些應用程式還要求「訂閱者」端的變更流回「發行者」端。 異動複寫與合併式複寫可為這些類型的應用程式提供選項。  
  
 
## <a name="see-also"></a>另請參閱  
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)
  
  
