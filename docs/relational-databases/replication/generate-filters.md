---
title: "產生篩選 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.generatefilters.f1
ms.assetid: be28515c-5d6d-467b-b933-d7c8d97a45b4
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2aa276ac1c58809cb97ef0ce002de76db32e1fa3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="generate-filters"></a>產生篩選
  **[產生篩選]** 對話方塊可讓您在合併式發行集內定義一個資料表的資料列篩選；然後複寫會自動將篩選擴充至透過外部索引鍵關聯性相關的其他資料表。 例如，若您定義客戶資料表的篩選，使其只包含 French 客戶的資料，則複寫會擴充該篩選，使相關的訂單與訂單的詳細資料只包含與 French 客戶相關的資料。  
  
## <a name="options"></a>選項  
 此對話方塊包含三個步驟的處理序，可在資料表上建立資料列篩選。 接著，篩選會透過主索引鍵和外部索引鍵關聯性擴充到與已篩選資料表相關的資料表。 例如，指定三個資料表 **Customer**、 **SalesOrderHeader**以及 **SalesOrderDetail**， **Customer** 和 **SalesOrderHeader**之間具有關聯性，而 **SalesOrderHeader** 和 **SalesOrderDetail**之間具有關聯性，將資料列篩選套用至 **Customer**，複寫會將篩選擴充至 **SalesOrderHeader** 和 **SalesOrderDetail**。  
  
1.  **選取要篩選的資料表。**  
  
     從下拉式清單方塊中選取資料表。 只有在 **[發行項]** 頁面上選取資料表時，資料表才會出現在清單方塊中。  
  
2.  **完成篩選陳述式來識別訂閱者將接收哪些資料表資料列。**  
  
     定義新的篩選陳述式。 **[資料行]** 清單方塊會列出您要從 **[請選取要篩選的資料表]**中選取之資料表發行的所有資料行。 **[篩選陳述式]** 文字區域包括預設文字，其格式為：  
  
     `SELECT <published_columns> FROM [tableowner].[tablename] WHERE`  
  
     無法變更此文字；請使用標準 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法在 WHERE 關鍵字之後鍵入篩選子句。  
  
    > [!IMPORTANT]  
    >  基於效能的考量，建議您不要在參數化資料列篩選器子句中的資料行名稱套用函數，例如 `LEFT([MyColumn]) = SUSER_SNAME()`。 如果在篩選子句中使用 HOST_NAME，並且覆寫 HOST_NAME 值，則可能需要使用 CONVERT 來轉換資料類型。 如需有關此案例之最佳做法的詳細資訊，請參閱主題＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。  
  
3.  **指定多少訂閱會從這個資料表接收資料。**  
  
     僅限[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本。 合併式複寫可以讓您指定最適合您的資料與應用程式的資料分割類型。 如果您選取 **[這個資料表中的一個資料列只會提供給一個訂閱]**，合併式複寫會設定非重疊資料分割選項。 非重疊資料分割配合預先計算的資料分割使用可以提升效能，其中非重疊資料分割會最小化與預先計算之資料分割相關聯的上傳成本。 當使用的參數化篩選和聯結篩選越複雜時，非重疊資料分割在效能上的益處更為醒目。 如果您選取此選項，必須確定分割資料的方式不會讓一個資料列複寫到一個以上的訂閱者。 如需進一步資訊，請參閱主題＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞中的「設定資料分割選項」。  
  
 您加入篩選之後，按一下 **[確定]** 即可結束並關閉對話方塊。 您指定的篩選會被剖析，並會針對 SELECT 子句中的資料表執行。 如果篩選陳述式包含語法錯誤或其他問題，則系統會通知您，然後您可以編輯該篩選陳述式。  
  
 剖析陳述式之後，複寫會建立必要的聯結篩選。 如果尚未針對此精靈執行的發行者設定散發者，就會提示您進行設定。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視和修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [篩選發行的資料](../../relational-databases/replication/publish/filter-published-data.md)   
 [聯結篩選](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
