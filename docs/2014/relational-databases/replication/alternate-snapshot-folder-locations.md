---
title: 替代快照集資料夾位置 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c86e79928bdadb129ed0aa591e4bd035ffe22c1c
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54128998"
---
# <a name="alternate-snapshot-folder-locations"></a>替代快照集資料夾位置
  替代的快照集位置可以讓您將快照集檔案儲存到預設位置以外的地方，通常是位於「散發者」。 替代位置可以位於其他伺服器、網路磁碟機或抽取式媒體 (例如 CD-ROM 或抽取式磁碟)。  
  
 替代的快照集位置會儲存為發行集的屬性。 因為替代快照集位置是一種發行集屬性，「散發代理程式」和「合併代理程式」可以尋找適當的快照集做為同步處理的一部份。  
  
 如果您要指定替代快照集的資料夾位置或是壓縮快照集檔，請立即建立發行集 (但不要立刻建立初始快照集)、設定快照集位置的發行集屬性，然後對此發行集執行「快照集代理程式」(Snapshot Agent)。 如果您在建立初始快照集後變更替代位置，則不會將發行集任何產生的快照集重新放置到新的替代位置。 在此狀況下，「合併代理程序」或「散發代理程序」可能無法在新的替代位置找到快照集檔案，這取決於此發行集的設定。  
  
> [!NOTE]  
>  請勿使用 [發行集屬性] 對話方塊或 [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) 指定與預設快照集資料夾位置相同的替代位置。  
  
> [!CAUTION]  
>  請勿同時使用 WebSync 和替代快照集資料夾位置。  
  
 **若要設定替代的快照集位置**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:[指定替代快照集資料夾位置](snapshot-options.md#snapshot-folder-locations) 
  
-   複寫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式設計：[設定快照集屬性 &#40;複寫 Transact-SQL 程式設計&#41;](publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用快照集初始化訂閱](initialize-a-subscription-with-a-snapshot.md)   
 [快照集選項](snapshot-options.md)  
  
  
