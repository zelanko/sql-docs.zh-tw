---
title: "編寫複寫指令碼 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "指令碼 [SQL Server 複寫], 複寫物件"
  - "合併式複寫指令碼 [SQL Server 複寫]"
  - "複寫 [SQL Server], 指令碼處理"
  - "快照式複寫 [SQL Server], 指令碼"
  - "指令碼 [SQL Server 複寫]"
  - "異動複寫, 指令碼"
ms.assetid: e50fac44-54c0-470c-a4ea-9c111fa4322b
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 編寫複寫指令碼
  拓撲中的所有複寫元件都應作為損毀復原計畫的一部份來編寫指令碼，而指令碼也可以用於自動執行重複性工作。 指令碼包含實作已編寫指令碼之複寫元件所必要的 Transact-SQL 系統預存程序，例如，發行集或訂閱。 可以建立指令碼，在精靈中 （例如新的發行集精靈 」），或在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立元件之後。 您可以檢視、 修改和執行指令碼使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 **sqlcmd**。 指令碼可以和備份檔案一起儲存，萬一必須重新設定複寫拓撲時即可使用。  
  
 如果對任何屬性進行了變更，則應對該元件重新編寫指令碼。 若您在異動複寫中使用自訂預存程序，每個程序副本會與指令碼同時儲存；若程序變更，則副本必須更新 (程序通常在結構描述變更或改變應用程式需求時進行更新)。 如需自訂程序的詳細資訊，請參閱 [指定如何傳播變更的交易式發行項](../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)。  
  
 對於使用參數化篩選的合併式複寫，發行集指令碼包含對建立資料分割的預存程序呼叫。 指令碼提供所建立資料分割的參考，並提供必要時重新建立一或多個資料分割的方式。  
  
## 利用指令碼自動化工作的範例  
 請考慮 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]，它實作合併式複寫以將資料散發到它的遠端銷售團隊。 一個銷售代表使用提取訂閱下載與其區域客戶有關的所有資料。 離線工作時，該銷售代表可以更新資料並輸入新的客戶與訂單。 由於 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 在各地共有 50 位以上的銷售代表，若是利用「新增訂閱精靈」在每個「訂閱者」上建立不同的訂閱，將相當耗時。 反之，複寫管理員可遵循下列步驟：  
  
1.  使用根據銷售代表或其區域所進行之資料分割設定必要的合併式發行集。  
  
2.  為一個「訂閱者」建立提取訂閱。  
  
3.  根據該提取訂閱產生指令碼。  
  
4.  修改指令碼，變更例如「訂閱者」名稱等的值。  
  
5.  在多個「訂閱者」端執行指令碼以產生需要的提取訂閱。  
  
## 撰寫複寫物件的指令碼  
 從複寫精靈或從複寫物件編寫指令碼 **複寫** 資料夾中的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如果您從精靈編寫指令碼，可以選擇建立物件並編寫其指令碼，也可以選擇只編寫其指令碼。  
  
> [!IMPORTANT]  
>  所有密碼的指令碼都會編寫為 NULL。 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您將認證儲存在指令碼檔案中，必須保護該檔案免於未經授權的存取。  
  
 如需使用複寫精靈的詳細資訊，請參閱：  
  
-   [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
-   [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)  
  
-   [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)  
  
#### 若要從複寫精靈編寫物件指令碼  
  
1.  在 **精靈動作** 頁面的精靈中，選取核取方塊適用於精靈︰  
  
    -   **產生含有建立發行集步驟的指令碼檔案**  
  
    -   **產生含有建立訂閱步驟的指令碼檔案**  
  
    -   **產生含有設定散發步驟的指令碼檔案**  
  
2.  在指定的選項 **指令碼檔案屬性** 頁面。  
  
3.  完成精靈。  
  
#### 若要從 Management Studio 編寫物件指令碼  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的散發者、發行者或訂閱者，然後展開伺服器節點。  
  
2.  展開 **複寫** 資料夾，然後展開 **本機發行集** 資料夾或 **本機訂閱** 資料夾。  
  
3.  發行集或訂閱，以滑鼠右鍵按一下，然後按一下 [ **產生指令碼**。  
  
4.  中指定選項 **產生 SQL 指令碼-\< ReplicationObject>** 對話方塊。  
  
5.  按一下 [ **指令碼至檔案**。  
  
6.  輸入檔案名稱中的 **指令碼檔案位置** ] 對話方塊中，然後按一下 **儲存**。 就會顯示狀態訊息。  
  
7.  按一下 [ **確定**, ，然後按一下 [ **關閉**。  
  
#### 若要從 Management Studio 編寫多個物件的指令碼  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的散發者、發行者或訂閱者，然後展開伺服器節點。  
  
2.  以滑鼠右鍵按一下 **複寫** 資料夾，然後再按一下 **產生指令碼**。  
  
3.  中指定選項 **產生 SQL 指令碼** 對話方塊。  
  
4.  按一下 [ **指令碼至檔案**。  
  
5.  輸入檔案名稱中的 **指令碼檔案位置** ] 對話方塊中，然後按一下 **儲存**。 就會顯示狀態訊息。  
  
6.  按一下 [ **[確定]，然後** 按一下 **關閉**。  
  
  