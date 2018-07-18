---
title: 指定不應該為合併發行項 （複寫 TRANSACT-SQL 程式設計） 追蹤刪除 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- conditional delete tracking [SQL Server replication]
- merge replication [SQL Server replication], conditional delete tracking
ms.assetid: 0fe330ca-5fb5-422e-ad6f-92fb5d6a3b6c
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 65a4ad119dc985c67eeea811f2102f387b7a5419
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37248508"
---
# <a name="specify-that-deletes-should-not-be-tracked-for-merge-articles-replication-transact-sql-programming"></a>指定不應該為合併發行項追蹤刪除 (複寫 Transact-SQL 程式設計)
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 依預設，合併式複寫會同步處理發行者與散發者之間的 DELETE 命令。 合併式複寫可讓您保留訂閱資料庫中的資料列，即時已從發行集中刪除資料列 (反之亦然)。 您可透過程式設計方式指定在建立新的發行項時要忽略 DELETE 命令，或是可以在稍後使用複寫預存程序來啟用這項功能。  
  
> [!IMPORTANT]  
>  啟用這項功能將會導致非聚合的情況，這表示訂閱者上的資料將不會正確反映發行者上的資料。 您必須實作自己的機制，以手動移除刪除的資料列。  
  
### <a name="to-specify-that-deletes-be-ignored-for-a-new-merge-article"></a>指定新的合併發行項要忽略刪除  
  
1.  在發行集資料庫的發行者端，執行 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 指定的值為`false`for **@delete_tracking**。 如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
    > [!NOTE]  
    >  如果發行項的來源資料表已在另一個發行集中發行，則兩個發行項的 **delete_tracking** 值必須相同。  
  
### <a name="to-specify-that-deletes-be-ignored-for-an-existing-merge-article"></a>指定現有的合併發行項要忽略刪除  
  
1.  若要判斷是否已針對發行項啟用錯誤補償，請執行 [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)，並記下結果集中的 **delete_tracking** 值。 如果這個值是 **0**，就表示已經忽略刪除。  
  
2.  如果步驟 1 的值是 **1**，請在發行集資料庫的發行者端執行 [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 指定的值為**delete_tracking** for **@property**，而值為`false`如**@value**。  
  
    > [!NOTE]  
    >  如果發行項的來源資料表已在另一個發行集中發行，則兩個發行項的 **delete_tracking** 值必須相同。  
  
## <a name="see-also"></a>另請參閱  
 [使用條件式刪除追蹤最佳化合併式複寫效能](../merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
