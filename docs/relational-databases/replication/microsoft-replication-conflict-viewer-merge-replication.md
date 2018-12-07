---
title: Microsoft 複寫衝突檢視器 (合併式複寫) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replconflictviewer.cvmerge.f1
ms.assetid: bfef5e21-ac04-4bc5-a55e-595421e34923
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 10b67088d8c7fde760db975070bf7bc53860d107
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52545676"
---
# <a name="microsoft-replication-conflict-viewer-merge-replication"></a>Microsoft 複寫衝突檢視器 (合併式複寫)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  複寫衝突檢視器可以讓您檢視在複寫同步處理過程中發生的任何衝突。 如果在兩個不同的伺服器端 (例如，在發行者端和訂閱者端，或在兩個不同的訂閱者端) 修改相同的資料，就會發生衝突。 複寫會使用建立發行項時選取的 Conflict Resolver 以自動解決衝突。 不過，複寫衝突檢視器可讓您在必要時選擇衝突的不同解決方案。 會發生下列衝突：  
  
-   更新衝突。 更新衝突發生於相同的資料在兩個位置同時更改時。 一個變更成功，而另一個變更失敗。 您可以選擇保存現有的資料 (成功的資料)、以衝突的資料覆寫現有的資料 (失敗的資料)，或者合併成功與失敗的資料並更新現有的資料。  
  
-   插入衝突。 當資料列插入的位置在合併其他位置的變更時違反某些資料一致性規則時，就會發生插入衝突。 您可以選擇保存現有的資料 (成功的資料)、以衝突的資料覆寫現有的資料 (失敗的資料)，或者合併成功與失敗的資料並更新現有的資料。  
  
-   刪除衝突。 當資料列在一處已遭刪除，而在另一處已被更新，就會發生此衝突。  
  
 同步處理期間解決衝突時，遺失之資料列的資料會寫入衝突資料表。 不論您接受原始解決方案或為衝突選擇不同的解決方案，都會從衝突資料表刪除記錄的衝突資料列。 您應該定期檢閱衝突，以協助減少衝突追蹤資料表的大小。  
  
> [!NOTE]  
>  「衝突檢視器」中不會顯示涉及邏輯記錄的衝突。 若要檢視這些衝突的相關資訊，請使用複寫預存程序。 如需詳細資訊，請參閱[檢視合併式發行集的衝突資訊 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md)。  
  
## <a name="options"></a>選項。  
 複寫衝突檢視器會劃分為兩個區段。 對話方塊的上半段會顯示選取之資料表的衝突清單。 當您按一下衝突清單中的某個項目時，對話方塊的下半段中會顯示衝突的詳細資料。  
  
 描述為何發生衝突的資訊 (例如，同時在發行者與訂閱者端更新相同的資料列)，會顯示在對話方塊的下半段中。 下半段中的衝突資料，會在兩個對應的資料行 (**[衝突成功者]** 和 **[衝突失敗者]**) 中顯示。 如果衝突是發生在已更新和已刪除的資料之間，那麼衝突中已刪除的一方可能沒有資料可以顯示。 在此情況下，複寫衝突檢視器會在其中一個資料行裡顯示訊息，指出刪除一個位置的資料列而更新另一個位置的資料列。 它也會指出建議的解決方式。  
  
 無法在複寫衝突檢視器中編輯的資料 (例如， **rowguid** 資料)，會使用陰影方塊以唯讀顯示。  
  
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
 按一下即可從檢視器中移除選取的衝突，以及從複寫系統資料表中移除其相關聯的中繼資料。 相當於為所選的每個衝突按一下 [提交成功者] 按鈕 (不對資料做任何變更)。  
  
 **顯示所有資料行**  
 選取即可顯示資料表的所有資料行。  
  
 **顯示前五個資料行和有衝突資料的其他資料行。**  
 選取即可顯示前五個資料行和有衝突的任何資料行。 當資料表有大量資料行，但是您只想查看與解決衝突最相關的資料行時，這很有用。 前五個資料行一律會包含在此檢視中做為識別資料列的欄位，例如主索引鍵或名稱欄位，通常是在資料表的前幾個資料行中。  
  
 **顯示資料行資訊** ([...])  
 按一下即可檢視資料行資訊： **[資料表名稱]**、 **[資料行名稱]**、 **[資料類型]** 和 **[資料行值]**。 **[資料行值]** 是可編輯的，除非以唯讀顯示該值。  
  
 **提交成功者**  
 按一下即可使 Conflict Resolver 所決定的資料列仍是成功者。 按一下此按鈕之前，可以變更非顯示為唯讀之任何資料行的值。  
  
 **提交失敗者**  
 按一下即可接受 Conflict Resolver 所決定的資料列為失敗者。 按一下此按鈕之前，可以變更非顯示為唯讀之任何資料行的值。  
  
 **記錄衝突的詳細資料**  
 選取此方塊即可將衝突的詳細資料記錄到檔案。 若要指定檔案的位置，請指向 **[檢視]** 功能表，然後按一下 **[選項]**。 輸入一個值，或按一下瀏覽 (**...**)，然後導覽至適當的檔案。 按一下 **[確定]** 即可結束 **[選項]** 對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [檢視並解決合併式發行集的資料衝突 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
