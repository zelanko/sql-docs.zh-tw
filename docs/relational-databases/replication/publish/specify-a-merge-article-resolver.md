---
title: "指定合併發行項解析程式 | Microsoft Docs"
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
  - "發行項 [SQL Server 複寫], 衝突解決"
  - "衝突解決 [SQL Server 複寫], 合併式複寫"
  - "合併式複寫衝突解決 [SQL Server 複寫], 合併發行項解析程式"
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 指定合併發行項解析程式
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中指定合併發行項解析程式。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
-   **若要指定合併發行項解析程式，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   合併式複寫允許下列類型的發行項解決器：  
  
    -   預設解決器。 預設解決器的行為視訂閱是客訂閱還是主訂閱而定。 如需指定訂閱類型的詳細資訊，請參閱 [指定合併訂閱類型和衝突解決優先權 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/specify a merge subscription type and conflict resolution priority.md)。  
  
    -   您撰寫的自訂解決器可以是商務邏輯處理常式 (以 Managed 程式碼撰寫) 或是以 COM 為基礎的自訂解決器。 如需詳細資訊，請參閱 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。 如果您需要實作自訂邏輯，如每個複寫的資料列，不只是針對衝突的資料列，請參閱執行 [為合併發行項實作商務邏輯處理常式](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)。  
  
    -   標準 COM 型解析程式，隨附於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
-   若要使用預設解決器以外的其他解決器，您必須將解決器複製到執行「合併代理程式」的電腦，然後註冊它 (如果您使用的是商務邏輯處理常式，則還必須在「發行者」端對其進行註冊)。 「合併代理程式」在以下位置上執行：  
  
    -   發送訂閱的「散發者」端  
  
    -   提取訂閱的「訂閱者」端  
  
    -   使用 Web 同步處理來提取訂閱的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS)   
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 解析程式註冊之後，就必須指定發行項上，使用解析程式 **解析程式** ] 索引標籤的 **發行項屬性-\< 發行項>** 對話方塊中，也就是在新增發行集精靈和 **發行集屬性-\< 發行集>** 對話方塊。 如需使用精靈，並存取此對話方塊的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md) 和 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 若要指定解決器  
  
1.  在 **文章** 新的發行集精靈] 頁面或 **發行集屬性-\< 發行集>** 對話方塊中，選取的資料表。  
  
2.  按一下 **[發行項屬性]**，然後按一下 **[設定反白顯示資料表發行項的屬性]**。  
  
3.  在 **發行項屬性-\< 發行項>** 頁面上，按一下 **解析程式** ] 索引標籤。  
  
4.  選取 **使用自訂解析程式 （已在散發者註冊）**, ，然後在清單中，按一下 [解決器。  
  
5.  如果解析程式時需要輸入 （例如資料行名稱），指定在 **輸入解析程式所需的資訊** 文字方塊。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  對於每個需要解決器的發行項重複此處理。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 註冊自訂衝突解決器  
  
1.  如果您打算註冊您自己自訂的衝突解決器，請建立以下其中一種類型：  
  
    -   以 Managed 程式碼為基礎的解決器，當做商務邏輯處理常式。 如需相關資訊，請參閱 [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)。  
  
    -   以預存程序為基礎的解析程式以及以 COM 為基礎的解析程式。 如需詳細資訊，請參閱 [Implement a Custom Conflict Resolver for a Merge Article](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)。  
  
2.  若要判斷是否已經註冊所需的解析程式，請執行 [sp_enumcustomresolvers & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 在任何資料庫中的 「 發行者 」。 這樣會顯示自訂解決器的描述以及在散發者上註冊之每一個以 COM 為基礎之解決器的類別識別碼 (CLSID)，或是在散發者上註冊之每一個商務邏輯處理常式的 Managed 組件相關資訊。  
  
3.  如果您尚未註冊所需的自訂解析程式，執行 [sp_registercustomresolver & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) 在散發者 」。 指定名稱的解析程式 **@article_resolver**; 對於商務邏輯處理常式，這是組件的易記名稱。 以 COM 為基礎的解析程式指定的 DLL 的 CLSID **@resolver_clsid**, ，和商務邏輯處理常式中，指定其值為 **，則為 true** 的 **@is_dotnet_assembly**, ，組件名稱 **@dotnet_assembly_name**, ，並覆寫此類別的完整限定名稱 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 的 **@dotnet_class_name**。  
  
    > [!NOTE]  
    >  如果商務邏輯處理常式組件未部署在合併代理程式可執行檔相同的目錄中，應用程式的相同目錄中，同步啟動合併代理程式，或在全域組件快取 (GAC) 中，您需要指定的組件名稱的完整路徑 **@dotnet_assembly_name**。  
  
4.  如果此解決器是以 COM 為基礎的解決器：  
  
    -   將自訂解決器 DLL 複製到發送訂閱的散發者上，或是提取訂閱的訂閱者上。  
  
        > [!NOTE]  
        >  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 自訂解析程式可以找到在 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM 目錄。  
  
    -   使用 regsvr32.exe 向作業系統註冊自訂解決器 DLL。 例如，從命令提示字元執行以下命令可註冊 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Additive Conflict Resolver：  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  如果商務邏輯處理常式的解析程式，部署與合併代理程式可執行檔 (replmerg.exe)，相同的資料夾中的組件會叫用合併代理程式的應用程式相同的資料夾中或在指定的資料夾中 **@dotnet_assembly_name** 在步驟 3 中的參數。  
  
    > [!NOTE]  
    >  合併代理程式可執行檔的預設安裝位置為 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM。  
  
#### 在定義合併發行項時，指定自訂解決器  
  
1.  如果您打算使用自訂衝突解決器，請使用以上的程序建立及註冊解決器。  
  
2.  在 「 發行者 」 執行 [sp_enumcustomresolvers & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 記下所需的自訂解析程式中的名稱和 **值** 結果集的欄位。  
  
3.  在發行集資料庫的發行者，執行 [sp_addmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定步驟 2 的解析程式的名稱 **@article_resolver** 以及任何所需使用自訂解析程式輸入 **@resolver_info** 參數。 預存程序為基礎的自訂解析程式，如 **@resolver_info** 是預存程序的名稱。 如需有關必要輸入解析程式所提供的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)], ，請參閱 [Microsoft 以 COM 為基礎的解析程式](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md)。  
  
#### 針對現有的合併發行項指定或變更自訂解決器  
  
1.  若要判斷發行項，是否已定義自訂解決器或取得解析程式的名稱，執行 [sp_helpmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。 如果沒有為發行項定義自訂解決器，其名稱會顯示在 **article_resolver** 欄位。 解析程式所提供的任何輸入將會顯示在 **resolver_info** 結果集的欄位。  
  
2.  在 「 發行者 」 執行 [sp_enumcustomresolvers & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 記下所需的自訂解析程式中的名稱和 **值** 結果集的欄位。  
  
3.  在發行集資料庫的發行者，執行 [sp_changemergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 指定的值為 **article_resolver**, ，包括商務邏輯處理常式的完整路徑 **@property**, ，和步驟 2 所需的自訂解決器名稱 **@value**。  
  
4.  若要變更任何自訂解析程式所需的資訊，請執行 [sp_changemergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 一次。 指定的值為 **resolver_info** 的 **@property** 和任何必要的自訂解析程式輸入 **@value**。 預存程序為基礎的自訂解析程式，如 **@resolver_info** 是預存程序的名稱。 如需必要輸入的詳細資訊，請參閱 [Microsoft 以 COM 為基礎的解析程式](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md)。  
  
#### 取消註冊自訂衝突解決器  
  
1.  在 「 發行者 」 執行 [sp_enumcustomresolvers & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 記下移除中的自訂解決器名稱 **值** 結果集的欄位。  
  
2.  執行 [sp_unregistercustomresolver & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md) 在散發者 」。 指定步驟 1 中的自訂解決器的完整名稱 **@article_resolver**。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會建立新的發行項，並指定在發生衝突時，應該使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Averaging Conflict Resolver 來計算 **UnitPrice** 資料行的平均值。  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_1.sql)]  
  
 這個範例會變更要指定的發行項，其方式是在發生衝突時使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Additive Conflict Resolver 計算 **UnitsOnOrder** 資料行的總和。  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_2.sql)]  
  
## 另請參閱  
 [進階合併式複寫衝突偵測與解決](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [為合併發行項實作商務邏輯處理常式](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  