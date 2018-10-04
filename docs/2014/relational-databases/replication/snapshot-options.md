---
title: 快照集選項 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9cb6e432b6c65b7c6c5562cb1b41eb158512966f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183180"
---
# <a name="snapshot-options"></a>快照集選項
  使用快照集初始化訂閱時，可以使用下列選項：  
  
-   指定代替預設快照集資料夾位置的替代快照集資料夾位置，或同時指定這兩個位置。 如需詳細資訊，請參閱＜ [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md)＞。  
  
-   壓縮快照集以儲存在抽取式媒體，或者透過慢速網路傳送。 如需詳細資訊，請參閱＜ [Compressed Snapshots](compressed-snapshots.md)＞。  
  
-   在套用快照集之前或之後執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 如需詳細資訊，請參閱[在套用快照集之前及之後執行指令碼](execute-scripts-before-and-after-the-snapshot-is-applied.md)。  
  
-   使用檔案傳輸通訊協定 (FTP) 傳送快照集檔案。 如需詳細資訊，請參閱[透過 FTP 傳送快照集](transfer-snapshots-through-ftp.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用快照集初始化訂閱](initialize-a-subscription-with-a-snapshot.md)  
  
  
