---
title: 新增或編輯篩選 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.addeditfilter.f1
ms.assetid: bdd7c71d-1c59-4044-bfe8-c85f908345bb
caps.latest.revision: 27
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c29de77be7dc0a36ce7311055fa081a3ca9a36d6
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37358120"
---
# <a name="add-or-edit-filter"></a>加入或編輯篩選
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[加入篩選]** 和 **[編輯篩選]** 對話方塊可讓您加入和編輯靜態資料列篩選與參數化資料列篩選器。  
  
> [!NOTE]  
>  編輯現有發行集內的篩選需要該發行集的新快照集。 如果發行集有訂閱，就必須重新初始化訂閱。 如需屬性變更的詳細資訊，請參閱[變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
 所有發行集類型可以包含靜態篩選；合併式發行集也可以包含參數化篩選。 在建立發行集時評估靜態篩選：發行集的所有訂閱者會收到相同資料。 在複寫同步處理期間評估參數化篩選：不同的訂閱者可能會收到資料的不同資料分割，根據每個訂閱者的登入或電腦名稱而定。 按一下對話方塊中的 **[範例陳述式]** 連結，即可查看每個類型之篩選的範例。 如需篩選選項的詳細資訊，請參閱[篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)。  
  
 使用資料列篩選，您可以指定要從資料表發行的資料列子集。 資料列篩選可用來刪除使用者不需要查看的資料列 (例如包含敏感性或機密性資訊的資料列)，或建立傳送給不同訂閱者之資料的不同資料分割。 發行資料的不同資料分割給不同的訂閱者，也有助於避免多個訂閱者更新相同資料所引起的衝突。  
  
## <a name="options"></a>選項。  
 此對話方塊包含交易式發行集與快照集發行集的兩個步驟處理序，以及合併式發行集的三個步驟處理序。 所有的發行集類型都需要您選取要篩選的資料表，以及一或多個要包含在篩選中的資料行；此篩選定義為標準的 WHERE 子句。  
  
1.  **選取要篩選的資料表**  
  
     如果您正在編輯現有的篩選，就不可以變更資料表選取範圍。 如果您正在加入新的篩選，請從下拉式清單方塊中選取資料表。 只有在 **[發行項]** 頁面上已選取資料表，而且尚未有資料列篩選時，才會在清單方塊中顯示資料表。 如果資料表有資料列篩選，而且您要定義新的篩選：  
  
    1.  按一下 **[加入篩選]** 對話方塊中的 **[取消]** 。  
  
    2.  選取 **[篩選資料表的資料列]** 頁面上之篩選窗格中的資料表，然後按一下 **[編輯]**。  
  
    3.  在 **[編輯篩選]** 對話方塊中編輯現有的篩選。  
  
2.  **完成篩選陳述式來識別訂閱者將接收哪些資料表資料列。**  
  
     定義新的篩選陳述式或編輯現有的篩選陳述式。 **[資料行]** 清單方塊會列出您要從 **[請選取要篩選的資料表]** 中選取之資料表發行的所有資料行。 **[篩選陳述式]** 文字區域包括預設文字，其格式為：  
  
     `SELECT <published_columns> FROM [schema].[tablename] WHERE`  
  
     無法變更此文字；請使用標準 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法在 WHERE 關鍵字之後鍵入篩選子句。 如果發行者是 Oracle 發行者，則 WHERE 子句必須與 Oracle 查詢語法相容。 儘可能避免使用複雜的篩選。 靜態與參數化篩選都會增加發行集的處理時間；因此，您應該儘可能保持篩選陳述式愈簡單愈好。  
  
    > [!IMPORTANT]  
    >  基於效能的考量，建議您不要將函數套用至合併式發行集的參數化資料列篩選器子句 (例如 `LEFT([MyColumn]) = SUSER_SNAME()`) 中的資料行名稱。 如果在篩選子句中使用 HOST_NAME，並且覆寫 HOST_NAME 值，則可能需要使用 CONVERT 來轉換資料類型。 如需有關此案例之最佳做法的詳細資訊，請參閱主題＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞中的「覆寫 HOST_NAME() 值」一節。  
  
3.  **指定多少訂閱會從這個資料表接收資料**  
  
     僅限[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新的版本；僅限合併式複寫。 合併式複寫可以讓您指定最適合您的資料與應用程式的資料分割類型。 如果您選取 **[這個資料表中的一個資料列只會提供給一個訂閱]**，合併式複寫會設定非重疊資料分割選項。 非重疊資料分割配合預先計算的資料分割使用可以提升效能，其中非重疊資料分割會最小化與預先計算之資料分割相關聯的上傳成本。 當使用的參數化篩選和聯結篩選越複雜時，非重疊資料分割在效能上的益處更為醒目。 如果您選取此選項，必須確定分割資料的方式不會讓一個資料列複寫到一個以上的訂閱者。 如需進一步資訊，請參閱主題＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞中的「設定資料分割選項」。  
  
 您加入或編輯篩選之後，請按一下 **[確定]** 以儲存變更並關閉對話方塊。 您指定的篩選會被剖析，並會針對 SELECT 子句中的資料表執行。 如果篩選陳述式包含語法錯誤或其他問題，則會通知您，且您可以編輯該篩選陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
