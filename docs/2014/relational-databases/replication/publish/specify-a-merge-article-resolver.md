---
title: 指定合併發行項解析程式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
- merge replication conflict resolution [SQL Server replication], merge article resolvers
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 388d400160e3fa7b3240c7a9c014bcf36ae25f3a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68212098"
---
# <a name="specify-a-merge-article-resolver"></a>指定合併發行項解析程式
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中指定合併發行項解析程式。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
-   **若要指定合併發行項解析程式，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   合併式複寫允許下列類型的發行項解決器：  
  
    -   預設解決器。 預設解決器的行為視訂閱是客訂閱還是主訂閱而定。 如需指定訂閱類型的詳細資訊，請參閱[指定合併訂閱類型和衝突解決方法優先權 &#40;SQL Server Management Studio&#41;](../specify-a-merge-subscription-type-and-conflict-resolution-priority.md)。  
  
    -   您撰寫的自訂解決器可以是商務邏輯處理常式 (以 Managed 程式碼撰寫) 或是以 COM 為基礎的自訂解決器。 如需詳細資訊，請參閱 [Advanced Merge Replication Conflict Detection and Resolution](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)中指定合併發行項解析程式。 如果您需要實作針對每一個複寫之資料列執行的自訂邏輯，而不只是針對衝突的資料列，請參閱＜ [為合併發行項實作商務邏輯處理常式](../implement-a-business-logic-handler-for-a-merge-article.md)中指定合併發行項解析程式。  
  
    -   以 COM 為基礎的標準解決器，包含在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中。  
  
-   若要使用預設解決器以外的其他解決器，您必須將解決器複製到執行「合併代理程式」的電腦，然後註冊它 (如果您使用的是商務邏輯處理常式，則還必須在「發行者」端對其進行註冊)。 「合併代理程式」在以下位置上執行：  
  
    -   發送訂閱的「散發者」端  
  
    -   提取訂閱的「訂閱者」端  
  
    -   使用 Web 同步處理來提取訂閱的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 註冊解析程式之後，您可以指定發行項應該使用 [發行項屬性 - \<發行項>]  對話方塊之 [解析程式]  索引標籤上的解析程式，此對話方塊位於 [新增發行集精靈] 和 [發行集屬性 - \<發行集>]  對話方塊中。 如需使用精靈及存取對話方塊的詳細資訊，請參閱[建立發行集](create-a-publication.md)和[檢視及修改發行集屬性](view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-a-resolver"></a>若要指定解決器  
  
1.  在 [新增發行集精靈] 的 [發行項]  頁面上，或是在 [發行集屬性 - \<發行集>]  對話方塊中，選取一個資料表。  
  
2.  按一下 **[發行項屬性]** ，然後按一下 **[設定反白顯示資料表發行項的屬性]** 。  
  
3.  在 [發行項屬性 - \<發行項>]  頁面上，按一下 [解析程式]  索引標籤。  
  
4.  選取 **[使用自訂解決器 (已在散發者註冊)]** ，然後在清單中按一下解決器。  
  
5.  如果解決器需要輸入 (例如資料行名稱)，請在 **[輸入解決器所需的資訊]** 文字方塊中指定它。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  對於每個需要解決器的發行項重複此處理。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-register-a-custom-conflict-resolver"></a>註冊自訂衝突解決器  
  
1.  如果您打算註冊您自己自訂的衝突解決器，請建立以下其中一種類型：  
  
    -   以 Managed 程式碼為基礎的解決器，當做商務邏輯處理常式。 如需詳細資訊，請參閱 [為合併發行項實作商務邏輯處理常式](../implement-a-business-logic-handler-for-a-merge-article.md)。  
  
    -   以預存程序為基礎的解析程式以及以 COM 為基礎的解析程式。 如需詳細資訊，請參閱 [針對合併發行項實作自訂衝突解析程式](../implement-a-custom-conflict-resolver-for-a-merge-article.md)。  
  
2.  若要判斷是否已經註冊想要的解決程式，請在任何資料庫的發行者端執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)。 這樣會顯示自訂解決器的描述以及在散發者上註冊之每一個以 COM 為基礎之解決器的類別識別碼 (CLSID)，或是在散發者上註冊之每一個商務邏輯處理常式的 Managed 組件相關資訊。  
  
3.  如果尚未註冊所要的自訂解析程式，請在散發者端執行 [sp_registercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql)。 針對 **@article_resolver** 指定解決器名稱；對於商務邏輯處理常式而言，這是組件的易記名稱。 以 COM 為基礎的解決器，指定的 dll 的 CLSID **@resolver_clsid** ，和商務邏輯處理常式中，指定其值為`true`for **@is_dotnet_assembly** ，組件的名稱 **@dotnet_assembly_name** ，和完整類別的名稱會覆寫<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule>for **@dotnet_class_name** 。  
  
    > [!NOTE]  
    >  如果商務邏輯處理常式組件未部署在與合併代理程式可執行檔相同的目錄中、與同步啟動合併代理程式之應用程式相同的目錄中，或是全域組件快取 (GAC) 中，您就必須將 **@dotnet_assembly_name** 中指定合併發行項解析程式。  
  
4.  如果此解決器是以 COM 為基礎的解決器：  
  
    -   將自訂解決器 DLL 複製到發送訂閱的散發者上，或是提取訂閱的訂閱者上。  
  
        > [!NOTE]  
        >  可以在[!INCLUDE[msCoName](../../../includes/msconame-md.md)] COM 目錄中找到 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]自訂解決器。  
  
    -   使用 regsvr32.exe 向作業系統註冊自訂解決器 DLL。 例如，從命令提示字元執行以下命令可註冊 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Additive Conflict Resolver：  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  如果此解決器是商務邏輯處理常式，請將組件部署在與合併代理程式可執行檔 (replmerg.exe) 相同的資料夾中、與叫用合併代理程式之應用程式相同的資料夾中，或是針對步驟 3 中 **@dotnet_assembly_name** 參數指定的資料夾中。  
  
    > [!NOTE]  
    >  合併代理程式可執行檔的預設安裝位置為 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM。  
  
#### <a name="to-specify-a-custom-resolver-when-defining-a-merge-article"></a>在定義合併發行項時，指定自訂解決器  
  
1.  如果您打算使用自訂衝突解決器，請使用以上的程序建立及註冊解決器。  
  
2.  在發行者端，執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)，並記下結果集中 [value]  欄位內所需的自訂解析程式名稱。  
  
3.  在發行集資料庫的發行者端，執行 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 針對 **@article_resolver** 指定步驟 2 中的解決器名稱，並使用 **@resolver_info** 參數指定自訂解決器的任何必要輸入。 如果是以預存程序為基礎的自訂解決器， **@resolver_info** 會是預存程序的名稱。 如需 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 提供之解析程式所需輸入的詳細資訊，請參閱 [Microsoft 以 COM 為基礎的解析程式](../merge/advanced-merge-replication-conflict-com-based-resolvers.md)。  
  
#### <a name="to-specify-or-change-a-custom-resolver-for-an-existing-merge-article"></a>針對現有的合併發行項指定或變更自訂解決器  
  
1.  若要判斷是否已針對發行項定義自訂解析程式，或是要取得解析程式的名稱，請執行 [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)。 如果已針對發行項定義自訂解決器，它的名稱會顯示在 **article_resolver** 欄位中。 為解決器提供的任何輸入都會顯示在結果集的 **resolver_info** 欄位中。  
  
2.  在發行者端，執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)，並記下結果集中 [value]  欄位內所需的自訂解析程式名稱。  
  
3.  在發行集資料庫的發行者端，執行 [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 針對 **article_resolver**指定 **@property** 的值，包括商務邏輯處理常式的完整路徑，並針對 **@value** 中指定合併發行項解析程式。  
  
4.  若要變更自訂解析程式的任何必要輸入，請再次執行 [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 針對 **resolver_info** @is_dotnet_assembly **@property** 的值，並針對 **@value** 中指定合併發行項解析程式。 如果是以預存程序為基礎的自訂解決器， **@resolver_info** 會是預存程序的名稱。 如需必要輸入的詳細資訊，請參閱 [Microsoft 以 COM 為基礎的解析程式](../merge/advanced-merge-replication-conflict-com-based-resolvers.md)。  
  
#### <a name="to-unregister-a-custom-conflict-resolver"></a>取消註冊自訂衝突解決器  
  
1.  在發行者端，執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)，並記下結果集中 [value]  欄位內所需的自訂解析程式名稱。  
  
2.  在散發者端，執行 [sp_unregistercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql)。 針對 **@article_resolver** 中指定合併發行項解析程式。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會建立新的發行項，並指定在發生衝突時，應該使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Averaging Conflict Resolver 來計算 **UnitPrice** 資料行的平均值。  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../snippets/tsql/SQL15/replication/howto/tsql/mergearticleresolvers.sql#sp_addmerge_resolver)]  
  
 這個範例會變更要指定的發行項，其方式是在發生衝突時使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Additive Conflict Resolver 計算 **UnitsOnOrder** 資料行的總和。  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../snippets/tsql/SQL15/replication/howto/tsql/mergearticleresolvers.sql#sp_changemerge_resolver)]  
  
## <a name="see-also"></a>另請參閱  
 [進階合併式複寫衝突偵測與解決](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [為合併發行項實作商務邏輯處理常式](../implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
