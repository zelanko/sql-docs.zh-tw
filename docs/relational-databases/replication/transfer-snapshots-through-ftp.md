---
title: "透過 FTP 傳送快照集 | Microsoft 文件"
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
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 55c30791-cd2a-420b-8ba7-5700e005cb45
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0c76a4c3b3ad80c46c16ba0c1c200a1a95f9c975
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="transfer-snapshots-through-ftp"></a>透過 FTP 傳送快照集
  依預設，快照集儲存在定義為「通用命名慣例」(UNC) 共用的資料夾中。 複寫還允許您指定「檔案傳輸通訊協定」(FTP) 共用，而不是 UNC 共用。 若要使用 FTP，您必須設定 FTP 伺服器，然後設定使用 FTP 的一個發行集和一個或多個訂閱。 如需有關如何設定 FTP 伺服器的詳細資訊，請參閱 Internet Information Services (IIS) 文件集。 如果您為發行集指定 FTP 資訊，依預設，該發行集的訂閱會使用 FTP。 只有當執行 IIS 的電腦與「散發者」之間被防火牆隔開時，Web 同步處理才會使用 FTP。 在此情況下，可以使用 FTP，從散發者和執行 IIS 的電腦來傳送快照集 (快照集一定會使用 HTTPS 傳送到訂閱者)。  
  
> [!IMPORTANT]  
>  建議您使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證和 UNC 共用，而不要使用 FTP 共用，因為若是 FTP 共用則必須儲存 FTP 密碼，並且該密碼會以純文字格式從訂閱者或執行 IIS 的電腦 (使用 Web 同步處理時) 傳送到 FTP 伺服器。 此外，因為對快照集共用的存取由單一帳戶控制，所以無法確定已篩選的合併式發行集之「訂閱者」僅從其資料分割存取快照集檔案。  
  
 若要透過 FTP 傳遞快照集，請參閱＜ [Deliver a Snapshot Through FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [合併式複寫的 Web 同步處理](../../relational-databases/replication/web-synchronization-for-merge-replication.md)   
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Snapshot Options](../../relational-databases/replication/snapshot-options.md)  
  
  
