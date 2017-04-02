---
title: "指定結構描述選項 | Microsoft Docs"
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
  - "結構描述 [SQL Server 複寫]，選項"
  - "發行項 [SQL Server 複寫]、交易式複寫選項"
  - "發行項 [SQL Server 複寫]、合併複寫選項"
  - "發行項 [SQL Server 複寫]、結構描述選項"
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 指定結構描述選項
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中指定結構描述選項。 當您發行資料表或檢視表時，您可以控制針對發行之物件複寫的物件建立選項。 您可以在建立發行項時設定這些選項，而且也可以在之後變更這些選項。 如果您不明確針對發行項指定這些選項，將會定義一組預設選項。  
  
> [!NOTE]  
>  使用複寫預存程序時的預設結構描述選項，可能會與使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 加入發行項時的預設選項不同。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
-   **若要指定結構描述選項，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果在建立發行集之後變更結構描述選項，則必須產生新的快照。  
  
###  <a name="Recommendations"></a> 建議  
  
-   結構描述選項的完整清單，請參閱 **@schema_option** 參數 [sp_addarticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 和 [sp_addmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 指定結構描述選項，例如是否要複製的條件約束和觸發程序到 「 訂閱者 」 上 **屬性** ] 索引標籤的 **發行項屬性-\< 發行項>** 對話方塊。 此索引標籤會在新增發行集精靈和 **發行集屬性-\< 發行集>** 對話方塊。 如需使用精靈，並存取此對話方塊的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md) 和 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 若要指定結構描述選項  
  
1.  在 **文章** 新的發行集精靈] 頁面或 **發行集屬性-\< 發行集>** 對話方塊中，選取文件，然後按一下 **發行項屬性**。  
  
2.  選取哪些結構描述選項變更應套用至：  
  
    -   按一下 [ **設定的反白顯示屬性 \< ObjectType> 文章** 啟動 **發行項屬性-\< ObjectName>** ] 對話方塊中，屬性在此對話方塊中所做的變更只會套用到的物件，會在 [物件] 窗格上反白顯示 **文章** 頁面。  
  
    -   按一下 [ **設定屬性的所有 \< ObjectType> 文章** 啟動 **所有屬性 \< ObjectType> 文章** ] 對話方塊中，屬性在此對話方塊中所做的變更套用至該類型的物件] 窗格的所有物件上 **文章** ] 頁面上，包括尚未選取 [發行集。  
  
        > [!NOTE]  
        >  屬性中所做的變更 **所有屬性 \< ObjectType> 文章** 對話方塊覆寫任何先前所做的 **發行項屬性-\< o b j>** 對話方塊。 例如，若要設定所有屬於某物件類型之發行項的一些預設值，但同時要設定個別物件的某些屬性，則請先設定所有發行項的預設值， 然後再設定個別物件的屬性。  
  
3.  在 **複製物件和設定到訂閱者** 和 **目的地物件** 區段 **屬性** ] 索引標籤的 **發行項屬性-\< 發行項>** 對話方塊方塊中，指定選項的值。  
  
4.  必要時修改任何屬性，然後按一下 **[確定]**。  
  
5.  如果您是在 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **確定** 儲存並關閉對話方塊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 結構描述選項會指定為十六進位值 [|(位元 OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) 一個或多個選項的結果。 如需詳細資訊，請參閱 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 和 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。  
  
> [!NOTE]  
>  在執行位元運算之前，您必須將結構描述選項值從 **binary** 轉換成 **int** 。 如需詳細資訊，請參閱 [CAST 和 CONVERT & #40。TRANSACT-SQL & #41;](../../../t-sql/functions/cast-and-convert-transact-sql.md)。  
  
#### 在針對快照式或交易式發行集定義發行項時，指定結構描述選項  
  
1.  在發行集資料庫的發行者，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定發行項所屬的發行集名稱 **@publication**, ，發行項的名稱 **@article**, 發行的資料庫物件、 **@source_object**, 的資料庫物件類型 **@type**, ，而 [|(位元 OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) 結果的一個或多個結構描述選項 **@schema_option**。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
#### 在針對合併式發行集定義發行項時，指定結構描述選項  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定發行項所屬的發行集名稱 **@publication**, ，發行項的名稱 **@article**, 發行的資料庫物件、 **@source_object**, ，而 [|(位元 OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) 結果的一個或多個結構描述選項 **@schema_option**。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
#### 針對快照式或交易式發行集中的現有發行項變更結構描述選項  
  
1.  在發行集資料庫的發行者，執行 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)。 針對 **@publication** 指定發行項所屬的發行集名稱，並針對 **@article**指定發行項的名稱。 記下的值 **schema_option** 結果集資料行。  
  
2.  執行 [& (位元 AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) 作業使用的值從步驟 1 和所需的結構描述選項值，以判斷是否已設定的選項。  
  
    -   如果結果是 **0**，表示未設定此選項。  
  
    -   如果結果是此選項值，表示已設定此選項。  
  
3.  如果未設定選項，執行 [|(位元 OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) 使用步驟 1 中的值和所需的結構描述選項值的作業。  
  
4.  在發行集資料庫的發行者，執行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)。 指定發行項所屬的發行集名稱 **@publication**, ，針對發行項名稱 **@article**, ，值為 **schema_option** 的 **@property**, ，和步驟 3 中的十六進位結果 **@value**。  
  
5.  執行快照集代理程式來產生新的快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
#### 變更合併發行中現有發行項的結構描述選項  
  
1.  在發行集資料庫的發行者，執行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。 針對 **@publication** 指定發行項所屬的發行集名稱，並針對 **@article**指定發行項的名稱。 記下的值 **schema_option** 結果集資料行。  
  
2.  執行 [& (位元 AND)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) 作業使用的值從步驟 1 和所需的結構描述選項值，以判斷是否已設定的選項。  
  
    -   如果結果是 **0**，表示未設定此選項。  
  
    -   如果結果是此選項值，表示已設定此選項。  
  
3.  如果未設定選項，執行 [|(位元 OR)](../Topic/%7C%20\(Bitwise%20OR\)%20\(Transact-SQL\).md) 使用步驟 1 中的值和所需的結構描述選項值的作業。  
  
4.  在發行集資料庫的發行者，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定發行項所屬的發行集名稱 **@publication**, ，針對發行項名稱 **@article**, ，值為 **schema_option** 的 **@property**, ，和步驟 3 中的十六進位結果 **@value**。  
  
5.  執行快照集代理程式來產生新的快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
## 另請參閱  
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [異動複寫的發行項選項](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  