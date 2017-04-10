---
title: "雙向異動複寫 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "雙向複寫"
  - "異動複寫, 雙向複寫"
  - "雙向異動複寫"
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# 雙向異動複寫
  雙向異動複寫是一種特殊的異動複寫拓撲，它可讓兩台伺服器彼此之間交換變更：每台伺服器都會發行資料，然後向發行集訂閱另一台伺服器上相同的資料。  **@Loopback_detection** 參數 [sp_addsubscription & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 設定為 TRUE 可確保變更才會傳送給訂閱者，而不會導致在變更傳送回 「 發行者 」。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本中，對等的交易式複寫，也支援此拓撲，但雙向複寫可提升的效能。  
  
## 另請參閱  
 [點對點異動複寫](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  