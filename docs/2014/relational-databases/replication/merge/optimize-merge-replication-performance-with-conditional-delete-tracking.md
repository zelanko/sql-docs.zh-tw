---
title: 使用條件式刪除追蹤最佳化合併式複寫效能 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- conditional delete tracking [SQL Server replication]
- merge replication [SQL Server replication], conditional delete tracking
- articles [SQL Server replication], conditional delete tracking
ms.assetid: 58f120a3-ea3a-4e97-93f0-0eb4e580ecf2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a93eed388f494b7d0aeaac127b95bc0d87c76963
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68210696"
---
# <a name="optimize-merge-replication-performance-with-conditional-delete-tracking"></a>使用條件式刪除追蹤最佳化合併式複寫效能
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 您可以使用合併式複寫，來指定一或多個發行項的刪除不由複寫觸發程序與系統資料表來追蹤。 如果您為發行項指定了此選項，則不會從「發行者」或任何「訂閱者」追蹤或複寫這些刪除。 此選項可支援一些應用程式實例，並在不需要或不想要對刪除的複寫時提供效能最佳化。 有三種方法可以提升效能：不儲存刪除的中繼資料；同步處理期間不列舉刪除；不在「訂閱者」端複寫及套用刪除。  
  
> [!NOTE]  
>  若要使用僅限下載發行項，發行集的相容性層級必須至少為 90RTM。  
  
 如果應用程式要求複寫某些刪除，而其餘的則不複寫 (例如批次刪除)，則可以在發行集建立或在 ON 與 OFF 之間切換時指定選項。 以下範例說明此選項在應用程式中可能的用法：  
  
-   行動銷售團隊所使用的應用程式一般都具有資料表，例如 **SalesOrderHeader**、 **SalesOrderDetail** 和 **Product**。 在「訂閱者」端輸入訂單 (通常將資料提供給訂單實行系統)，然後再將其複寫至「發行者」。 許多行動工作者使用含有限儲存的手持式裝置：訂單在「發行者」端接收後，可以在「訂閱者」端刪除。 刪除不會傳播到「發行者」，因為此訂單在系統中仍為使用中訂單。  
  
     在此狀況下，不會追蹤 **SalesOrderHeader** 和 **SalesOrderDetail** 資料表的刪除。 
  **Product** 資料表的刪除也不會被追蹤，因為在「發行者」端刪除產品後，刪除會被傳送到「訂閱者」，以使產品清單保持最新。  
  
-   應用程式可以將記錄資料儲存在資料表 (例如 **TransactionHistory**，它會定期清除一年前的舊記錄) 中。 資料表可以使用篩選，以便「訂閱者」僅接收當月的交易資料。 儘管「發行者」端每月進行的批次刪除 (即清除舊資料) 與「訂閱者」無關，但依預設它們仍會被追蹤及列舉。  
  
     在此狀況下，可以在批次處理前停止系統中的作業，並讓應用程式停用對刪除的追蹤。 處理完成後，追蹤可再次啟用。  
  
> [!IMPORTANT]  
>  如果其他作業在「發行者」端繼續，您必須確定在停用刪除追蹤時，不會發生應傳播給「訂閱者」的刪除。  
  
 **若要指定不應追蹤刪除**  
  
-   複寫 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 程式設計︰[指定不應該為合併發行項追蹤刪除 &#40;複寫 Transact-SQL 程式設計&#41;](..//publish/specify-merge-replication-properties.md#tracking-deletes)  
  
## <a name="see-also"></a>另請參閱  
 [合併式複寫的發行項選項](article-options-for-merge-replication.md)   
 [使用僅限下載的發行項最佳化合併式複寫效能](optimize-merge-replication-performance-with-download-only-articles.md)  
  
  
