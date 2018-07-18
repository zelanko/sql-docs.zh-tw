---
title: 壓縮的快照集 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], compressed
- snapshot replication [SQL Server], compressed snapshots
- compressed snapshots [SQL Server replication]
ms.assetid: 979ffa7c-3a88-4e70-8cf2-b8d452fd7a7f
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34a397f4c6597751d50aa676f07d42cc694e9c39
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303688"
---
# <a name="compressed-snapshots"></a>壓縮的快照集
  當您透過通訊緩慢的網路傳送快照集時，或將快照集儲存到抽取式媒體中，且未壓縮的快照集過大而未能放入媒體時，適合壓縮快照集檔案。 在這種狀況下，壓縮快照集檔案非常有用，但是壓縮會增加產生及套用快照集的時間。  
  
 將壓縮的快照集檔案以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 檔案格式寫入，可以壓縮 2 GB 或更小的檔案 (如果快照集檔案大於 2 GB，則不能壓縮)。 若要壓縮檔案，必須將它們寫入替代的快照集資料夾 (不能壓縮寫入預設快照集資料夾的檔案)。 如需替代快照集資料夾位置的詳細資訊，請參閱[替代快照集資料夾位置](alternate-snapshot-folder-locations.md)。  
  
 檔案在執行「散發代理程式」或「合併式代理程式」的位置解壓縮；發送訂閱通常與壓縮的快照集一起使用，以便檔案在「訂閱者」端解壓縮。 當「訂閱者」收到壓縮檔案時，檔案最初會寫入暫存位置。 壓縮的檔案複製到「訂閱者」之後，壓縮檔案中的快照集檔案會被解壓縮，CAB 公用程式會依順序一次解壓縮一個檔案。 「訂閱者」端需要的空間是壓縮檔案加上最大未壓縮檔案的大小。  
  
> [!NOTE]  
>  在某些情況下，壓縮的快照集可以改善網路之間傳送快照集檔案的效能。 不過，壓縮快照集需要由快照集代理程式在產生快照集檔案時，進行其他處理動作；並於套用快照集檔案時，進行散發代理程式或合併代理程式。 如此可能會減緩快照集的產生且在某些情況下會增加套用快照集的時間。 此外，若發生網路失敗，則無法繼續壓縮快照集；因此並不適合不穩定的網路。 透過網路使用壓縮快照集時，仔細考量這些權衡問題。  
  
 **若要壓縮及傳遞快照集檔案**  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]：[壓縮快照集檔案 &#40;SQL Server Management Studio&#41;](publish/compress-snapshot-files-sql-server-management-studio.md)  
  
-   複寫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式設計：[設定快照集屬性 &#40;複寫 Transact-SQL 程式設計&#41;](publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用快照集初始化訂閱](initialize-a-subscription-with-a-snapshot.md)   
 [快照集選項](snapshot-options.md)  
  
  
