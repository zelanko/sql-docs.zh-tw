---
title: "雙向異動複寫 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5357fa35dcc99b260049788238a446dbaac38808
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="bidirectional-transactional-replication"></a>雙向異動複寫
  雙向異動複寫是一種特殊的異動複寫拓撲，它可讓兩台伺服器彼此之間交換變更：每台伺服器都會發行資料，然後向發行集訂閱另一台伺服器上相同的資料。 [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 的 **@loopback_detection** 參數已設定為 TRUE，以確定變更僅傳送到「訂閱者」，而不會將變更傳回給「發行者」。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 及更新的版本中，點對點異動複寫也支援此拓撲，但雙向複寫可提升效能。  
  
## <a name="see-also"></a>另請參閱  
 [@loopback_detection](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
