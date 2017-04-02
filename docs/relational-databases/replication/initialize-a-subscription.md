---
title: "初始化訂閱 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "快照式複寫 [SQL Server], 初始化訂閱"
  - "異動複寫, 初始化訂閱"
  - "初始化訂閱 [SQL Server 複寫]"
  - "訂閱 [SQL Server 複寫], 初始化"
  - "初始化訂閱 [SQL Server 複寫], 關於初始化訂閱"
  - "合併式複寫 [SQL Server 複寫], 初始化訂閱"
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# 初始化訂閱
  複寫拓撲中的訂閱者必須初始化，使得它們具有已訂閱發行集中各發行項之結構描述副本和所有需要的複寫物件，例如預存程序、觸發程序和中繼資料表。 另外，「訂閱者」通常會接收初始資料集。 預設初始化方法會使用包含結構描述、複寫物件和資料的完整快照集，但是沒有完整的快照集也可以初始化發行集。  
  
 如需詳細資訊，請參閱 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md) 和 [初始化交易式訂閱不使用快照集](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)。  
  
  