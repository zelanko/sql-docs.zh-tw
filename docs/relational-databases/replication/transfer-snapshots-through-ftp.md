---
title: "透過 FTP 傳送快照集 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 55c30791-cd2a-420b-8ba7-5700e005cb45
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 75fca2ac2aedcb2ff44a4c63d8026a736cf0fc1d
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="transfer-snapshots-through-ftp"></a>透過 FTP 傳送快照集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  依預設，快照集儲存在定義為「通用命名慣例」(UNC) 共用的資料夾中。 複寫還允許您指定「檔案傳輸通訊協定」(FTP) 共用，而不是 UNC 共用。 若要使用 FTP，您必須設定 FTP 伺服器，然後設定使用 FTP 的一個發行集和一個或多個訂閱。 如需有關如何設定 FTP 伺服器的詳細資訊，請參閱 Internet Information Services (IIS) 文件集。 如果您為發行集指定 FTP 資訊，依預設，該發行集的訂閱會使用 FTP。 只有當執行 IIS 的電腦與「散發者」之間被防火牆隔開時，Web 同步處理才會使用 FTP。 在此情況下，可以使用 FTP，從散發者和執行 IIS 的電腦來傳送快照集 (快照集一定會使用 HTTPS 傳送到訂閱者)。  
  
> [!IMPORTANT]  
>  建議您使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證和 UNC 共用，而不要使用 FTP 共用，因為若是 FTP 共用則必須儲存 FTP 密碼，並且該密碼會以純文字格式從訂閱者或執行 IIS 的電腦 (使用 Web 同步處理時) 傳送到 FTP 伺服器。 此外，因為對快照集共用的存取由單一帳戶控制，所以無法確定已篩選的合併式發行集之「訂閱者」僅從其資料分割存取快照集檔案。  
  
 若要透過 FTP 傳遞快照集，請參閱＜ [Deliver a Snapshot Through FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [合併式複寫的 Web 同步處理](../../relational-databases/replication/web-synchronization-for-merge-replication.md)   
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [快照集選項](../../relational-databases/replication/snapshot-options.md)  
  
  
