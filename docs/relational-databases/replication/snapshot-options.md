---
title: "快照集選項 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dee907844ee1e7b2a1eb85a54283313d86b06e2c
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="snapshot-options"></a>快照集選項
  使用快照集初始化訂閱時，可以使用下列選項：  
  
-   指定代替預設快照集資料夾位置的替代快照集資料夾位置，或同時指定這兩個位置。 如需相關資訊，請參閱 [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md)。  
  
-   壓縮快照集以儲存在抽取式媒體，或者透過慢速網路傳送。 如需詳細資訊，請參閱＜ [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md)＞。  
  
-   在套用快照集之前或之後執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 如需詳細資訊，請參閱[在套用快照集之前及之後執行指令碼](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)。  
  
-   使用檔案傳輸通訊協定 (FTP) 傳送快照集檔案。 如需詳細資訊，請參閱[透過 FTP 傳送快照集](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
