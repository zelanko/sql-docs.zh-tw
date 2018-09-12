---
title: 將資料檔和記錄檔放在不同的磁碟機上 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 6cbedc27-4d77-44ad-bed2-c23b628475a7
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1c3f2d06b00aa024157b7adbf01c25d6bdb493da
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43818574"
---
# <a name="place-data-and-log-files-on-separate-drives"></a>將資料檔和記錄檔放在不同的磁碟機上
  此規則會檢查資料檔和記錄檔是否放在不同的邏輯磁碟機上。 將資料檔和記錄檔放在相同的裝置上可能會造成該裝置的競爭情況，並產生效能不佳的情況。 將這些檔案放在不同的磁碟機上可允許同時針對資料檔和記錄檔發生 I/O 活動。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 當您建立新的資料庫時，請針對資料和記錄指定個別的磁碟機。 若要在建立資料庫之後移動檔案，必須讓該資料庫離線。 請使用下列其中一種方法來移動檔案：  
  
> [!NOTE]  
>  這個原則無法透過掛接點偵測個別的實體裝置  
  
-   使用具有 WITH MOVE 選項的 RESTORE DATABASE 陳述式從備份還原資料庫。  
  
-   卸離然後附加資料庫，為資料和記錄裝置指定不同的位置。  
  
-   執行具有 MODIFY FILE 選項的 ALTER DATABASE 陳述式然後重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，以指定新的位置。  
  
## <a name="for-more-information"></a>詳細資訊  
 [移動資料庫檔案](../databases/move-database-files.md)  
  
 [移動使用者資料庫](../databases/move-user-databases.md)  
  
 [資料庫卸離與附加 &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
