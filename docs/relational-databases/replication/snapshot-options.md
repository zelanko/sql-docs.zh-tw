---
title: "快照集選項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "快照式複寫 [SQL Server], 選項"
  - "快照集 [SQL Server 複寫], 選項"
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# 快照集選項
  使用快照集初始化訂閱時，可以使用下列選項：  
  
-   指定代替預設快照集資料夾位置的替代快照集資料夾位置，或同時指定這兩個位置。 如需詳細資訊，請參閱 [替代快照集資料夾位置](../../relational-databases/replication/alternate-snapshot-folder-locations.md)。  
  
-   壓縮快照集以儲存在抽取式媒體，或者透過慢速網路傳送。 如需詳細資訊，請參閱 [壓縮的快照集](../../relational-databases/replication/compressed-snapshots.md)。  
  
-   在套用快照集之前或之後執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 如需詳細資訊，請參閱 [執行指令碼之前和之後套用快照集](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)。  
  
-   使用檔案傳輸通訊協定 (FTP) 傳送快照集檔案。 如需詳細資訊，請參閱 [透過 FTP 傳送快照集](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。  
  
## 另請參閱  
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  