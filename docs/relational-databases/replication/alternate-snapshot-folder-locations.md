---
title: "替代快照集資料夾位置 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: eac6520e46f252855d84dced89d9b79f5f8aed2b
ms.lasthandoff: 04/11/2017

---
# <a name="alternate-snapshot-folder-locations"></a>替代快照集資料夾位置
  替代的快照集位置可以讓您將快照集檔案儲存到預設位置以外的地方，通常是位於「散發者」。 替代位置可以位於其他伺服器、網路磁碟機或抽取式媒體 (例如 CD-ROM 或抽取式磁碟)。  
  
 替代的快照集位置會儲存為發行集的屬性。 因為替代快照集位置是一種發行集屬性，「散發代理程式」和「合併代理程式」可以尋找適當的快照集做為同步處理的一部份。  
  
 如果您要指定替代快照集的資料夾位置或是壓縮快照集檔，請立即建立發行集 (但不要立刻建立初始快照集)、設定快照集位置的發行集屬性，然後對此發行集執行「快照集代理程式」(Snapshot Agent)。 如果您在建立初始快照集後變更替代位置，則不會將發行集任何產生的快照集重新放置到新的替代位置。 在此狀況下，「合併代理程序」或「散發代理程序」可能無法在新的替代位置找到快照集檔案，這取決於此發行集的設定。  
  
> [!NOTE]  
>  請勿使用 [發行集屬性] 對話方塊或 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) 指定與預設快照集資料夾位置相同的替代位置。  
  
> [!CAUTION]  
>  請勿同時使用 WebSync 和替代快照集資料夾位置。  
  
 **若要設定替代的快照集位置**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Specify an Alternate Snapshot Folder Location &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   複寫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式設計：[設定快照集屬性 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Snapshot Options](../../relational-databases/replication/snapshot-options.md)  
  
  
