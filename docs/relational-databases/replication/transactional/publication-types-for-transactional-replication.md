---
title: "異動複寫的發行集類型 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: transactional replication, publications
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
caps.latest.revision: "32"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 018a2f804b25211b92dec8bcab89407dcd71022d
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="publication-types-for-transactional-replication"></a>異動複寫的發行集類型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 異動複寫提供三種發行集類型：  
  
|發行集類型|描述|  
|----------------------|-----------------|  
|標準交易式發行集|適合於「訂閱者」端的所有資料均為唯讀狀態 (異動複寫並不在「訂閱者」端強制這個屬性) 的拓撲。<br /><br /> 當使用 Transact-SQL 或 Replication Management Objects (RMO) 時，依預設，會建立標準交易式發行集。 當使用「新增發行集精靈」時，它們會透過選取 **[發行集類型]** 頁面上的 **[交易式發行集]** 來建立。<br /><br /> 如需建立發行集的詳細資訊，請參閱 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)。|  
|點對點拓撲中的交易式發行集|這個發行集類型的特性為：<br /><br /> -每個位置具有相同的資料，以及同時充當「發行者」與「訂閱者」。<br /><br /> -同一資料行一次僅可以在一個位置變更。<br /><br /> -此拓撲最適合於需要高可用性和讀取延展性的伺服器環境。<br /><br /> <br /><br /> 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [異動複寫](../../../relational-databases/replication/transactional/transactional-replication.md)  
  
  
