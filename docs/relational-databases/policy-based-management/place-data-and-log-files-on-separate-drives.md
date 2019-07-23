---
title: 將資料檔和記錄檔放在不同的磁碟機上 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 6cbedc27-4d77-44ad-bed2-c23b628475a7
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 54f469f8ab9f0daaf6f37c8f6bad1878bc716dbd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086933"
---
# <a name="place-data-and-log-files-on-separate-drives"></a>將資料檔和記錄檔放在不同的磁碟機上
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此規則會檢查資料檔和記錄檔是否放在不同的邏輯磁碟機上。 將資料檔和記錄檔放在相同的裝置上可能會造成該裝置的競爭情況，並產生效能不佳的情況。 將這些檔案放在不同的磁碟機上可允許同時針對資料檔和記錄檔發生 I/O 活動。  
  
## <a name="recommendations"></a>建議  
 當您建立新的資料庫時，請針對資料和記錄指定個別的磁碟機。 若要在建立資料庫之後移動檔案，必須讓該資料庫離線。 請使用下列其中一種方法來移動檔案：  
  
> [!NOTE]  
>  這個原則無法透過掛接點偵測個別的實體裝置  
  
-   使用具有 WITH MOVE 選項的 RESTORE DATABASE 陳述式從備份還原資料庫。  
  
-   卸離然後附加資料庫，為資料和記錄裝置指定不同的位置。  
  
-   執行具有 MODIFY FILE 選項的 ALTER DATABASE 陳述式然後重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，以指定新的位置。  
  
## <a name="for-more-information"></a>詳細資訊  
 [移動資料庫檔案](../../relational-databases/databases/move-database-files.md)  
  
 [移動使用者資料庫](../../relational-databases/databases/move-user-databases.md)  
  
 [資料庫卸離與附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
