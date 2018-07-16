---
title: 為合併發行項實作商務邏輯處理常式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], business logic handlers
- merge replication business logic handlers [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
- business logic handlers [SQL Server replication]
- BusinessLogicModule class
ms.assetid: ed477595-6d46-4fa2-b0d3-a5358903ec05
caps.latest.revision: 44
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a0404175f22e6edcb80e4179083555d23acf7db1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169050"
---
# <a name="implement-a-business-logic-handler-for-a-merge-article"></a>為合併發行項實作商務邏輯處理常式
  本主題描述如何使用複寫程式設計或 Replication Management Objects (RMO)，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中實作合併發行項的商務邏輯處理常式。  
  
 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 命名空間會實作一個介面，此介面可讓您撰寫複雜商務邏輯來處理合併複寫同步處理程序期間所發生的事件。 在同步處理期間複寫之每一個變更資料列的複寫程序可以叫用商務邏輯處理常式中的方法。  
  
 實作商務邏輯處理常式的一般程序如下：  
  
1.  建立商務邏輯處理常式組件。  
  
2.  在散發者上註冊此組件。  
  
3.  在合併代理程式執行所在的伺服器上部署此組件。 若為提取訂閱，代理程式會在訂閱者端執行；若為發送訂閱，代理程式會在散發者端執行。 當您正在使用 Web 同步處理時，此代理程式會在 Web 伺服器上執行。  
  
4.  建立使用商務邏輯處理常式的發行項，或是修改現有的發行項來使用商務邏輯處理常式。  
  
 指定的商務邏輯處理常式會針對要同步處理的每一個資料列執行。 對其他應用程式或網路服務的複雜邏輯與呼叫可能會影響效能。 如需商務邏輯處理常式的詳細資訊，請參閱[在合併同步處理期間執行商務邏輯](merge/execute-business-logic-during-merge-synchronization.md)。  
  
 **本主題內容**  
  
-   **若要針對合併發行項實作商務邏輯處理常式，請使用：**  
  
     [複寫程式設計](#ReplProg)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="ReplProg"></a> 使用複寫程式設計  
  
#### <a name="to-create-and-deploy-a-business-logic-handler"></a>建立及部署商務邏輯處理常式  
  
1.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 中，針對 .NET 組件建立新的專案，其中包含實作此商務邏輯處理常式的程式碼。  
  
2.  針對下列命名空間加入此專案的參考。  
  
    |組件參考|位置|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM (預設安裝)|  
    |<xref:System.Data>|GAC (.NET Framework 的元件)|  
    |<xref:System.Data.Common>|GAC (.NET Framework 的元件)|  
  
3.  加入會覆寫 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 類別的類別。  
  
4.  實作 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> 屬性來指示要處理的變更類型。  
  
5.  覆寫 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 類別的下列其中一個或多個方法：  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> - 在同步處理期間認可資料變更時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> - 在上傳或下載 DELETE 陳述式期間發生錯誤時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> - 在上傳或下載 DELETE 陳述式時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> - 在上傳或下載 INSERT 陳述式期間發生錯誤時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> - 在上傳或下載 INSERT 陳述式時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> - 當發行者和訂閱者上發生衝突的 UPDATE 陳述式時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> - 當發行者和訂閱者上發生與 DELETE 陳述式衝突的 UPDATE 陳述式時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> - 在上傳或下載 UPDATE 陳述式期間發生錯誤時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> - 在上傳或下載 UPDATE 陳述式時叫用。  
  
6.  建立專案來建立商務邏輯處理常式組件。  
  
7.  將此組件部署在包含合併代理程式可執行檔 (replmerg.exe) 的目錄中 (它的預設安裝位置為 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM)，或是將它安裝在 .NET 全域組件快取 (GAC) 中。 只有當合併代理程式以外的應用程式需要存取此組件時，您才應該將此組件安裝在 GAC 中。 您可使用 .NET Framework SDK 中提供的全域組件快取工具 (**Gacutil.exe)** ，將此組件安裝在 GAC 中。  
  
    > [!NOTE]  
    >  您必須在合併代理程式執行所在的每一部伺服器上部署商務邏輯處理常式，其中包括使用 Web 同步處理時，主控 replisapi.dll 的 IIS 伺服器。  
  
#### <a name="to-register-a-business-logic-handler"></a>註冊商務邏輯處理常式  
  
1.  在發行者端，執行 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)，以確定此組件尚未註冊為商務邏輯處理常式。  
  
2.  在散發者上，執行[sp_registercustomresolver &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql)，指定的商務邏輯處理常式的易記名稱**@article_resolver**，值為`true`for **@is_dotnet_assembly**，組件的名稱**@dotnet_assembly_name**，和完整類別的名稱會覆寫<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule>如**@dotnet_class_name**.  
  
    > [!NOTE]  
    >  如果此組件未部署在與合併代理程式可執行檔相同的目錄中、與同步啟動合併代理程式之應用程式相同的目錄中，或是全域組件快取 (GAC) 中，您就必須將 **@dotnet_assembly_name**＞。 當您正在使用 Web 同步處理時，必須指定組件在 Web 伺服器上的位置。  
  
#### <a name="to-use-a-business-logic-handler-with-a-new-table-article"></a>搭配新的資料表發行項使用商務邏輯處理常式  
  
1.  執行 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 來定義發行項，並針對 **@article_resolver** 指定商務邏輯處理常式的易記名稱。 如需詳細資訊，請參閱 [定義發行項](publish/define-an-article.md)。  
  
#### <a name="to-use-a-business-logic-handler-with-an-existing-table-article"></a>搭配現有的資料表發行項使用商務邏輯處理常式  
  
1.  執行 [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)，並指定 **@publication**、**@article**、**@property** 的 **article_resolver** 值，以及 **@value** 的商務邏輯處理常式易記名稱。  
  
###  <a name="TsqlExample"></a> 範例 (複寫程式設計)  
 這個範例會示範建立稽核記錄的商務邏輯處理常式。  
  
 [!code-csharp[HowTo#rmo_BusinessLogicCode](../../snippets/csharp/SQL15/replication/howto/cs/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../snippets/visualbasic/SQL15/replication/howto/vb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 下列範例會在散發者上註冊商務邏輯處理常式組件，並將現有的合併發行項變更為使用這個自訂商務邏輯。  
  
 [!code-sql[HowTo#sp_RegisterBLH_10](../../snippets/tsql/SQL15/replication/howto/tsql/registerblh_10.sql#sp_registerblh_10)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
  
#### <a name="to-create-a-business-logic-handler"></a>建立商務邏輯處理常式  
  
1.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 中，針對 .NET 組件建立新的專案，其中包含實作此商務邏輯處理常式的程式碼。  
  
2.  針對下列命名空間加入此專案的參考。  
  
    |組件參考|位置|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM (預設安裝)|  
    |<xref:System.Data>|GAC (.NET Framework 的元件)|  
    |<xref:System.Data.Common>|GAC (.NET Framework 的元件)|  
  
3.  加入會覆寫 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 類別的類別。  
  
4.  實作 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> 屬性來指示要處理的變更類型。  
  
5.  覆寫 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 類別的下列其中一個或多個方法：  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> - 在同步處理期間認可資料變更時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> - 在上傳或下載 DELETE 陳述式期間發生錯誤時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> - 在上傳或下載 DELETE 陳述式時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> - 在上傳或下載 INSERT 陳述式期間發生錯誤時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> - 在上傳或下載 INSERT 陳述式時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> - 當發行者和訂閱者上發生衝突的 UPDATE 陳述式時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> - 當發行者和訂閱者上發生與 DELETE 陳述式衝突的 UPDATE 陳述式時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> - 在上傳或下載 UPDATE 陳述式期間發生錯誤時叫用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> - 在上傳或下載 UPDATE 陳述式時叫用。  
  
    > [!NOTE]  
    >  自訂商務邏輯未明確處理的任何發行項衝突，都會由此發行項的預設解決器所處理。  
  
6.  建立專案來建立商務邏輯處理常式組件。  
  
#### <a name="to-register-a-business-logic-handler"></a>註冊商務邏輯處理常式  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 類別的執行個體。 傳遞步驟 1 的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumBusinessLogicHandlers%2A> 並檢查傳回的 <xref:System.Collections.ArrayList> 物件，以確定此組件尚未註冊為商務邏輯處理常式。  
  
4.  建立 <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler> 類別的執行個體。 指定下列屬性：  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetAssemblyName%2A> - .NET 組件的名稱。 如果此組件未部署在與合併代理程式可執行檔相同的目錄中、與同步啟動合併代理程式之應用程式相同的目錄中或是 GAC 中，您就必須包含具有組件名稱的完整路徑。 當您搭配 Web 同步處理使用商務邏輯處理常式時，必須包含具有組件名稱的完整路徑。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetClassName%2A> - 覆寫 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 及實作商務邏輯處理常式之類別的完整名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> - 當您存取商務邏輯處理常式時所要使用的易記名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.IsDotNetAssembly%2A> -針對`true`。  
  
#### <a name="to-deploy-a-business-logic-handler"></a>部署商務邏輯處理常式  
  
1.  將此組件部署在合併代理程式執行所在的伺服器上，商務邏輯處理常式已在散發者上註冊時所指定的檔案位置內。 若為提取訂閱，代理程式會在訂閱者端執行；若為發送訂閱，代理程式會在散發者端執行。 當您正在使用 Web 同步處理時，此代理程式會在 Web 伺服器上執行。 如果在註冊商務邏輯處理常式時，組件名稱中未包含完整路徑，請將此組件部署在與合併代理程式可執行檔相同的目錄中，或是與同步啟動合併代理程式之應用程式相同的目錄中。 如果有多個應用程式使用相同的組件，您可能要將此組件安裝在 GAC 中。  
  
#### <a name="to-use-a-business-logic-handler-with-a-new-table-article"></a>搭配新的資料表發行項使用商務邏輯處理常式  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergeArticle> 類別的執行個體。 設定下列屬性：  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>設定為發行項名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>設定為發行集名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A>設定為發行集資料庫名稱。  
  
    -   將<xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A>設定為商務邏輯處理常式的易記名稱 ( <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>)。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.Article.Create%2A> 方法。 如需詳細資訊，請參閱 [定義發行項](publish/define-an-article.md)。  
  
#### <a name="to-use-a-business-logic-handler-with-an-existing-table-article"></a>搭配現有的資料表發行項使用商務邏輯處理常式  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergeArticle> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 屬性。  
  
4.  針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連接。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回`false`，在步驟 3 中的發行項屬性定義不正確，或發行項不存在。 如需詳細資訊，請參閱 [View and Modify Article Properties](publish/view-and-modify-article-properties.md)。  
  
6.  將 <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>設定為商務邏輯處理常式的易記名稱。 這是當註冊商務邏輯處理常式時，所指定之 <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> 屬性的值。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 這個範例是一個商務邏輯處理常式，它會記錄有關在訂閱者上插入、更新和刪除的資訊。  
  
 [!code-csharp[HowTo#rmo_BusinessLogicCode](../../snippets/csharp/SQL15/replication/howto/cs/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../snippets/visualbasic/SQL15/replication/howto/vb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 這個範例會在散發者上註冊商務邏輯處理常式。  
  
 [!code-csharp[HowTo#rmo_RegisterBLH_10](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_registerblh_10)]  
  
 [!code-vb[HowTo#rmo_vb_RegisterBLH_10](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_registerblh_10)]  
  
 此範例會變更現有的發行項來使用商務邏輯處理常式。  
  
 [!code-csharp[HowTo#rmo_ChangeMergeArticle_BLH](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## <a name="see-also"></a>另請參閱  
 [針對合併發行項實作自訂衝突解析程式](implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [偵錯商務邏輯處理常式 &#40;複寫程式設計&#41;](debug-a-business-logic-handler-replication-programming.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [複寫管理物件概念](concepts/replication-management-objects-concepts.md)  
  
  
