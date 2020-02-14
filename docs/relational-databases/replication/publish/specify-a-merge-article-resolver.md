---
title: 指定合併發行項解析程式 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 4c1267e08bfdb1361223f3a93ec465b3da83d8ce
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "70846566"
---
# <a name="specify-a-merge-article-resolver"></a>指定合併發行項解析程式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中指定合併發行項解析程式。  

  
##  <a name="recommendations"></a>建議  
  
-   合併式複寫允許下列類型的發行項解決器：  
  
    -   預設解決器。 預設解決器的行為視訂閱是客訂閱還是主訂閱而定。 如需指定訂閱類型的詳細資訊，請參閱[指定合併訂閱類型和衝突解決方法優先權 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)。  
  
    -   您撰寫的自訂解決器可以是商務邏輯處理常式 (以 Managed 程式碼撰寫) 或是以 COM 為基礎的自訂解決器。 如需詳細資訊，請參閱 [進階合併式複寫衝突偵測與解決](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。 如果您需要實作針對每一個複寫之資料列執行的自訂邏輯，而不只是針對衝突的資料列，請參閱＜ [為合併發行項實作商務邏輯處理常式](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)中指定合併發行項解析程式。  
  
    -   以 COM 為基礎的標準解決器，包含在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中。  
  
-   若要使用預設解決器以外的其他解決器，您必須將解決器複製到執行「合併代理程式」的電腦，然後註冊它 (如果您使用的是商務邏輯處理常式，則還必須在「發行者」端對其進行註冊)。 「合併代理程式」在以下位置上執行：  
  
    -   發送訂閱的「散發者」端  
  
    -   提取訂閱的「訂閱者」端  
  
    -   使用 Web 同步處理來提取訂閱的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 註冊解析程式之後，您可以指定發行項應該使用 [發行項屬性 - \<發行項>]  對話方塊之 [解析程式]  索引標籤上的解析程式，此對話方塊位於 [新增發行集精靈] 和 [發行集屬性 - \<發行集>]  對話方塊中。 如需使用精靈及存取對話方塊的詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)和[檢視及修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
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
  
    -   以 Managed 程式碼為基礎的解決器，當做商務邏輯處理常式。 如需詳細資訊，請參閱 [為合併發行項實作商務邏輯處理常式](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)。  
  
    -   以預存程序為基礎的解析程式以及以 COM 為基礎的解析程式。 如需詳細資訊，請參閱 [針對合併發行項實作自訂衝突解析程式](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)。  
  
2.  若要判斷是否已經註冊想要的解決程式，請在任何資料庫的發行者端執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)。 這樣會顯示自訂解決器的描述以及在散發者上註冊之每一個以 COM 為基礎之解決器的類別識別碼 (CLSID)，或是在散發者上註冊之每一個商務邏輯處理常式的 Managed 組件相關資訊。  
  
3.  如果尚未註冊所要的自訂解析程式，請在散發者端執行 [sp_registercustomresolver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)。 為 **\@article_resolver** 指定解析程式名稱；對於商務邏輯處理常式而言，這是組件的易記名稱。 若是 COM 解析程式，請將 **\@resolver_clsid** 指定為 DLL 的 CLSID，然後為商務邏輯處理常式，將 **\@is_dotnet_assembly** 指定為 **true** 值、將 **\@dotnet_assembly_name** 指定為組件的名稱，並將 **\@dotnet_class_name** 指定為覆寫 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 的類別完整名稱。  
  
    > [!NOTE]  
    >  如果商務邏輯處理常式組件未部署在合併代理程式可執行檔的相同目錄中、同步啟動合併代理程式的應用程式相同目錄中，或是全域組件快取 (GAC) 中，您就必須將 **\@dotnet_assembly_name** 指定為包含組件名稱的完整路徑。  
  
4.  如果此解決器是以 COM 為基礎的解決器：  
  
    -   將自訂解決器 DLL 複製到發送訂閱的散發者上，或是提取訂閱的訂閱者上。  
  
        > [!NOTE]  
        >  可以在[!INCLUDE[msCoName](../../../includes/msconame-md.md)] COM 目錄中找到 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]自訂解決器。  
  
    -   使用 regsvr32.exe 向作業系統註冊自訂解決器 DLL。 例如，從命令提示字元執行以下命令可註冊 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Additive Conflict Resolver：  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  如果解析程式是商務邏輯處理常式，請將組件部署在合併代理程式可執行檔 (replmerg.exe) 的相同資料夾中、叫用合併代理程式的應用程式相同資料夾中，或是為步驟 3 中 **\@dotnet_assembly_name** 參數指定的資料夾中。  
  
    > [!NOTE]  
    >  合併代理程式可執行檔的預設安裝位置為 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM。  
  
## <a name="specify-a-custom-resolver-when-defining-a-merge-article"></a>在定義合併發行項時，指定自訂解析程式  
  
1.  如果您打算使用自訂衝突解決器，請使用以上的程序建立及註冊解決器。  
  
2.  在發行者端，執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)，並記下結果集中 [value]  欄位內所需的自訂解析程式名稱。  
  
3.  在發行集資料庫的發行者端，執行 [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 為 **\@article_resolver** 指定步驟 2 中的解析程式名稱，並使用 **\@resolver_info** 參數指定自訂解析程式的任何必要輸入。 如果是以預存程序為基礎的自訂解析程式， **\@resolver_info** 會是預存程序的名稱。 如需 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 提供之解析程式所需輸入的詳細資訊，請參閱 [Microsoft 以 COM 為基礎的解析程式](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)。  
  
## <a name="specify-or-change-a-custom-resolver-for-an-existing-merge-article"></a>針對現有的合併發行項，指定或變更自訂解析程式  
  
1.  若要判斷是否已針對發行項定義自訂解析程式，或是要取得解析程式的名稱，請執行 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)。 如果已針對發行項定義自訂解決器，它的名稱會顯示在 **article_resolver** 欄位中。 為解決器提供的任何輸入都會顯示在結果集的 **resolver_info** 欄位中。  
  
2.  在發行者端，執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)，並記下結果集中 [value]  欄位內所需的自訂解析程式名稱。  
  
3.  在發行集資料庫的發行者端，執行 [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 為 **\@property** 指定 **article_resolver** 值，包括商務邏輯處理常式的完整路徑，並為 **\@value** 指定步驟 2 中所需的自訂解析程式名稱。  
  
4.  若要變更自訂解析程式的任何必要輸入，請再次執行 [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 為 **\@property** 指定 **resolver_info** 值，並為 **\@value** 指定自訂解析程式的任何必要輸入。 如果是以預存程序為基礎的自訂解析程式， **\@resolver_info** 會是預存程序的名稱。 如需必要輸入的詳細資訊，請參閱 [Microsoft 以 COM 為基礎的解析程式](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)。  
  
## <a name="unregister-a-custom-conflict-resolver"></a>將自訂衝突解析程式取消註冊  
  
1.  在發行者端，執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)，並記下結果集中 [value]  欄位內所需的自訂解析程式名稱。  
  
2.  在散發者端，執行 [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)。 為 **\@article_resolver** 指定步驟 1 中自訂解析程式的完整名稱。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會建立新的發行項，並指定在發生衝突時，應該使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Averaging Conflict Resolver 來計算 **UnitPrice** 資料行的平均值。  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_1.sql)]  
  
 這個範例會變更要指定的發行項，其方式是在發生衝突時使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Additive Conflict Resolver 計算 **UnitsOnOrder** 資料行的總和。  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_2.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [進階合併式複寫衝突偵測與解決](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [為合併發行項實作商務邏輯處理常式](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
