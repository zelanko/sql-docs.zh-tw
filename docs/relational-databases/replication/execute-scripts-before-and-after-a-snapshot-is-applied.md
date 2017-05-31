---
title: "在套用快照集之前及之後執行指令碼 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4352dbbbabdbd2d1aa8aa9b724f4e0aa41720bbd
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="execute-scripts-before-and-after-a-snapshot-is-applied"></a>在套用快照集之前及之後執行指令碼
  在 [發行集屬性 - \<發行集>] 對話方塊之 [快照集] 頁面上套用快照集的前後，指定要執行的選擇性指令碼。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
> [!NOTE]  
>  如果 **[快照集格式]** 選項設定為 **[字元]**，這些選項則不可用。  
  
### <a name="to-execute-a-script-before-or-after-a-snapshot-is-applied"></a>若要在套用快照集的前後執行指令碼  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [快照集] 頁面上：  
  
    -   若要在套用快照集之前指定要執行的指令碼，請按一下 **[瀏覽]** 以瀏覽到指令碼，或在 **[套用快照前執行此指令碼]** 文字方塊中輸入指令碼的路徑。  
  
        > [!NOTE]  
        >  「散發代理程式」或「合併代理程式」必須具有指定目錄的讀取權限。 如果使用提取訂閱，則必須指定一個共用目錄作為通用命名慣例 (UNC) 路徑，例如 \\\電腦名稱\scripts\myscript.sql。  
  
    -   若要在套用快照集之後指定要執行的指令碼，請按一下 **[瀏覽]** 以瀏覽到指令碼，或在 **[套用快照後執行此指令碼]** 文字方塊中輸入指令碼的路徑。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [設定快照集屬性 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [在套用快照集之前及之後執行指令碼](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
