---
title: 指定結構描述選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- schemas [SQL Server replication], options
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- articles [SQL Server replication], schema options
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f01cbdd1dd595e9dd2637a2e9d0ebbe871aabe66
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748641"
---
# <a name="specify-schema-options"></a>指定結構描述選項
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中指定結構描述選項。 當您發行資料表或檢視表時，您可以控制針對發行之物件複寫的物件建立選項。 您可以在建立發行項時設定這些選項，而且也可以在之後變更這些選項。 如果您不明確針對發行項指定這些選項，將會定義一組預設選項。  
  
> [!NOTE]  
>  使用複寫預存程序時的預設結構描述選項，可能會與使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]加入發行項時的預設選項不同。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
-   **若要指定結構描述選項，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果在建立發行集之後變更結構描述選項，則必須產生新的快照。  
  
###  <a name="Recommendations"></a> 建議  
  
-   如需完整結構描述選項清單，請參閱 [sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 和 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 的 **@schema_option** 參數。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在 [發行項屬性 - \<發行項>] 對話方塊的 [屬性] 索引標籤上指定結構描述選項，例如是否將條件約束與觸發程序複製至訂閱者。 [新增發行集精靈] 與 [發行集屬性 - \<發行集>] 對話方塊中都有提供此索引標籤。 如需使用精靈和存取對話方塊的詳細資訊，請參閱[建立發行集](create-a-publication.md)和[檢視及修改發行集屬性](view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-schema-options"></a>若要指定結構描述選項  
  
1.  在 [新增發行集精靈] 的 [發行項] 頁面上，或是在 [發行集屬性 - \<發行集>] 對話方塊中，選取一個發行項，然後按一下 [發行項屬性]。  
  
2.  選取哪些結構描述選項變更應套用至：  
  
    -   按一下 [設定反白顯示 \<物件類型> 發行項的屬性]  啟動 [發行項屬性 - \<物件名稱>] 對話方塊；在這個對話方塊中所做的屬性變更，只會套用至 [發行項] 頁面的物件窗格中反白顯示的物件。  
  
    -   按一下 [設定所有 \<物件類型> 發行項的屬性] 啟動 [所有 \<物件類型> 發行項的屬性] 對話方塊；在這個對話方塊中所做的屬性變更，會套用至 [發行項] 頁面的物件窗格中屬於該類型的所有物件，包括尚未選取發行的物件。  
  
        > [!NOTE]  
        >  在 [所有 \<物件類型> 發行項的屬性] 對話方塊中所做的屬性變更，會覆寫之前在 [發行項屬性 - \<物件名稱>] 對話方塊中所做的任何變更。 例如，若要設定所有屬於某物件類型之發行項的一些預設值，但同時要設定個別物件的某些屬性，則請先設定所有發行項的預設值， 然後再設定個別物件的屬性。  
  
3.  在 [發行項屬性 - \<發行項>] 對話方塊之 [屬性] 索引標籤的 [將物件與設定複製到訂閱者] 與 [目的地物件] 區段中，指定選項的值。  
  
4.  必要時修改任何屬性，然後按一下 **[確定]**。  
  
5.  如果您在 [發行集屬性 - \<發行集>] 對話方塊中，請按一下 [確定] 以儲存並關閉對話方塊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 結構描述選項會指定為十六進位值，這個值是一個或多個選項的 [| (Bitwise OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) 結果。 如需詳細資訊，請參閱＜ [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) ＞和＜ [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)＞。  
  
> [!NOTE]  
>  在執行位元運算之前，您必須將結構描述選項值從 **binary** 轉換成 **int** 。 如需詳細資訊，請參閱 [CAST 和 CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)。  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-snapshot-or-transactional-publication"></a>在針對快照式或交易式發行集定義發行項時，指定結構描述選項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 針對 **@publication**指定發行項所屬的發行集名稱、針對 **@article**指定發行項名稱、針對 **@source_object**指定發行的資料庫物件、針對 **@type**指定資料庫物件的類型，並針對 [| (Bitwise OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) 指定一個或多個結構描述選項的 **@schema_option**中指定結構描述選項。 如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-merge-publication"></a>在針對合併式發行集定義發行項時，指定結構描述選項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 針對 **@publication**指定發行項所屬的發行集名稱、針對 **@article**指定發行項名稱、針對 **@source_object**指定資料庫物件的類型，並針對 [| (Bitwise OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) 指定一個或多個結構描述選項的 **@schema_option**中指定結構描述選項。 如需詳細資訊，請參閱 [定義發行項](define-an-article.md)。  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集中的現有發行項變更結構描述選項  
  
1.  在發行集資料庫的發行者上，執行 [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql)。 針對 **@publication** 指定發行項所屬的發行集名稱，並針對 **@article**中指定結構描述選項。 請記下結果集中 **schema_option** 資料行的值。  
  
2.  請使用步驟 1 中的值及所要的結構描述選項值來執行 [& (Bitwise AND)](/sql/t-sql/language-elements/bitwise-and-transact-sql) 運算，以判斷是否已設定選項。  
  
    -   如果結果是 **0**，表示未設定此選項。  
  
    -   如果結果是此選項值，表示已設定此選項。  
  
3.  如果未設定此選項，請使用步驟 1 中的值及所要的結構描述選項值來執行 [| (Bitwise OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) 運算。  
  
4.  在發行集資料庫的發行者上，執行 [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)。 針對 **@publication**指定發行項所屬的發行集名稱、針對 **@article**指定發行項名稱、針對 **schema_option** 指定 **@property**的值，並針對 **@value**中指定結構描述選項。  
  
5.  執行快照集代理程式來產生新的快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)。  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-merge-publication"></a>變更合併發行中現有發行項的結構描述選項  
  
1.  在發行集資料庫的發行者上，執行 [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)。 針對 **@publication** 指定發行項所屬的發行集名稱，並針對 **@article**中指定結構描述選項。 請記下結果集中 **schema_option** 資料行的值。  
  
2.  請使用步驟 1 中的值及所要的結構描述選項值來執行 [& (Bitwise AND)](/sql/t-sql/language-elements/bitwise-and-transact-sql) 運算，以判斷是否已設定選項。  
  
    -   如果結果是 **0**，表示未設定此選項。  
  
    -   如果結果是此選項值，表示已設定此選項。  
  
3.  如果未設定此選項，請使用步驟 1 中的值及所要的結構描述選項值來執行 [| (Bitwise OR)](/sql/t-sql/language-elements/bitwise-or-transact-sql) 運算。  
  
4.  在發行集資料庫的發行者上，執行 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 針對 **@publication**指定發行項所屬的發行集名稱、針對 **@article**指定發行項名稱、針對 **schema_option** 指定 **@property**的值，並針對 **@value**中指定結構描述選項。  
  
5.  執行快照集代理程式來產生新的快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)。  
  
## <a name="see-also"></a>另請參閱  
 [發行資料和資料庫物件](publish-data-and-database-objects.md)   
 [異動複寫的發行項選項](../transactional/article-options-for-transactional-replication.md)  
  
  
