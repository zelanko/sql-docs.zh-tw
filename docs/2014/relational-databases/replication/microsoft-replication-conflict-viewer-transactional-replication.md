---
title: Microsoft 複寫衝突檢視器 (異動複寫) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.replconflictviewer.cvqueued.f1
ms.assetid: eec59d8e-cadb-4623-a31f-9f42ec09c97f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 003450f73ae1026a294827a6d52c50f38d259b52
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072478"
---
# <a name="microsoft-replication-conflict-viewer-transactional-replication"></a>Microsoft 複寫衝突檢視器 (異動複寫)
  「複寫衝突檢視器」可讓您檢視在點對點異動複寫和具有佇列更新訂閱之異動複寫的同步處理期間發生的衝突。 如需詳細資訊，請參閱[檢視交易式發行集的資料衝突 &#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)。  
  
> [!NOTE]  
>  「複寫衝突檢視器」會顯示在合併式複寫和異動複寫中發生的衝突。 若為異動複寫，您可以使用「複寫衝突檢視器」來檢視衝突資料，但是無法針對衝突選擇不同的解決方案。  
  
## <a name="options"></a>選項。  
 複寫衝突檢視器會劃分為兩個區段。 對話方塊的上半段會顯示選取之資料表的衝突清單。 當您按一下衝突清單中的某個項目時，對話方塊的下半段中會顯示衝突的詳細資料。  
  
 下半段中的衝突資料，會在兩個對應的資料行 (**[衝突成功者]** 和 **[衝突失敗者]**) 中顯示。 如果衝突是發生在已更新和已刪除的資料之間，那麼衝突中已刪除的一方可能沒有資料可以顯示。 在此情況下，複寫衝突檢視器會在其中一個資料行裡顯示訊息，這表示資料列在一處已遭刪除，而在另一處已被更新。 它也會指出建議的解決方式。  
  
 **[資料庫備份]**  
 選擇包含有衝突之發行集的資料庫。  
  
 **發行集**  
 選擇包含有衝突之資料表的發行集。  
  
 **Table**  
 選擇包含衝突的資料表。  
  
 **定義篩選**  
 按一下即可開啟 **[定義篩選]** 對話方塊。  
  
 **套用或移除篩選**  
 按一下即可套用或移除在 **[定義篩選]** 對話方塊中已定義的篩選。  
  
 **全選**  
 按一下即可選取在方格中列出的所有衝突。  
  
 **全部不選**  
 按一下即可取消選取方格中列出的所有衝突。  
  
 **移除**  
 按一下即可從檢視器中移除選取的衝突，以及從複寫系統資料表中移除其相關聯的中繼資料。  
  
 **顯示所有資料行**  
 選取即可顯示資料表的所有資料行。  
  
 **顯示前五個資料行和有衝突資料的其他資料行。**  
 選取即可顯示前五個資料行和有衝突的任何資料行。 當資料表有大量資料行，但是您只想查看與解決衝突最相關的資料行時，這很有用。 前五個資料行一律會包含在此檢視中做為識別資料列的欄位，例如主索引鍵或名稱欄位，通常是在資料表的前幾個資料行中。  
  
 **顯示資料行資訊** (**...**)  
 按一下即可檢視資料行資訊： **[資料表名稱]**、 **[資料行名稱]**、 **[資料類型]** 和 **[資料行值]**。  
  
 **記錄衝突的詳細資料**  
 選取此方塊即可將衝突的詳細資料記錄到檔案。 若要指定檔案的位置，請指向 **[檢視]** 功能表，然後按一下 **[選項]**。 輸入一個值，或按一下瀏覽 (**...**)，然後導覽至適當的檔案。 按一下 **[確定]** 即可結束 **[選項]** 對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [點對點複寫中的衝突偵測](transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)   
 [檢視交易式發行集的資料衝突 &#40;SQL Server Management Studio&#41;](view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
  
