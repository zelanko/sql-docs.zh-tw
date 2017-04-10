---
title: "估計資料表的大小 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "頁面 [SQL Server], 空間"
  - "空間 [SQL Server], 資料表"
  - "資料列大小 [SQL Server]"
  - "大小 [SQL Server], 資料表"
  - "資料行大小 [SQL Server]"
  - "預測資料表大小 [SQL Server]"
  - "資料表大小 [SQL Server]"
  - "估計資料表大小"
  - "叢集索引, 資料表大小"
  - "磁碟空間 [SQL Server], 資料表"
  - "空間配置 [SQL Server], 資料表大小"
  - "設計資料庫 [SQL Server], 估計大小"
  - "每分頁保留的可用資料列 [SQL Server]"
  - "計算資料表大小"
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# 估計資料表的大小
  您可以使用下列步驟來估計將資料儲存於資料表中所需的空間量：  
  
1.  遵循[估計堆積的大小](../../relational-databases/databases/estimate-the-size-of-a-heap.md)或[估計叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)中的指示，來計算堆積或叢集索引所需的空間。  
  
2.  對於每個非叢集索引，請遵循[估計非叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)中的指示，來計算其所需的空間。  
  
3.  新增步驟 1 和 2 中計算的值。  
  
## 另請參閱  
 [估計資料庫的大小](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [估計堆積的大小](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [估計叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [估計非叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  