---
title: "雙向異動複寫 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: "27"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa0124b90d473d3960891b67901c972aa0f51b81
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="bidirectional-transactional-replication"></a>雙向異動複寫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 雙向異動複寫是一種特殊的異動複寫拓撲，它可讓兩部伺服器彼此之間交換變更：每部伺服器都會發行資料，然後向發行集訂閱另一部伺服器上相同的資料。 [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 的 **@loopback_detection** 參數已設定為 TRUE，以確定變更僅傳送到「訂閱者」，而不會將變更傳回給「發行者」。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 及更新的版本中，點對點異動複寫也支援此拓撲，但雙向複寫可提升效能。  
  
## <a name="see-also"></a>另請參閱  
 [@loopback_detection](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
