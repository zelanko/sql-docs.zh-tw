---
title: 檢視及修改發行集屬性 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- viewing replication properties
- modifying replication properties, articles
- articles [SQL Server replication], modifying
- publications [SQL Server replication], properties
- articles [SQL Server replication], properties
- modifying replication properties, publications
- publications [SQL Server replication], modifying
ms.assetid: 27d72ea4-bcb6-48f2-b4aa-eb1410da7efc
caps.latest.revision: 43
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8168a9cb358f2be2a4b5c7c120ee06a8c10f7ccc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137045"
---
# <a name="view-and-modify-publication-properties"></a>檢視及修改發行集屬性
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中檢視及修改發行集屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
-   **若要檢視及修改發行集屬性，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   有些屬性在建立了發行集後無法再修改，而另一些當存在發行集的訂閱時便無法修改。 無法修改的屬性以唯讀顯示。  
  
###  <a name="Recommendations"></a> 建議  
  
-   建立發行集之後，某些屬性變更需要新的快照集。 如果發行集有訂閱，則某些變更還需要重新初始化所有訂閱。 如需詳細資訊，請參閱[變更發行集與發行項屬性](change-publication-and-article-properties.md)和[在現有發行集中新增和卸除發行項](add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 您可以在位於 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 與複寫監視器的 [發行集屬性 - \<發行集>] 對話方塊中，檢視及修改發行集屬性。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../monitor/start-the-replication-monitor.md)。  
  
 [發行集屬性 - \<發行集>] 對話方塊上包含下列頁面：  
  
-   **[一般]** 頁面包含發行集名稱和描述、發行集類型以及訂閱過期設定。  
  
-   **[發行項]** 頁面對應「新增發行集精靈」中的 **[發行項]** 頁面。 此頁面用於新增及刪除發行項，以及變更發行項的屬性與資料行篩選。  
  
-   **[篩選資料列]** 頁面對應「新增發行集精靈」中的 **[篩選資料表的資料列]** 頁面。 此頁面用於新增、編輯和刪除所有類型發行集的靜態資料列篩選，以及新增、編輯和刪除合併式發行集的參數化資料列篩選器和聯結篩選。  
  
-   **[快照集]** 頁面允許您指定快照集的格式和位置、是否應壓縮快照集，以及套用快照集前後要執行的指令碼。  
  
-   **[FTP 快照集]** 頁面 (針對快照式和交易式發行集，以及執行 SQL Server 2005 之前版本之「發行者」的合併式發行集) 允許您指定「訂閱者」是否可以透過「檔案傳輸通訊協定」(FTP) 下載快照集檔案。  
  
-   **[FTP 快照集和網際網路]** 頁面 (針對執行 SQL Server 2005 或更新版本之「發行者」的合併式發行集) 允許您指定「訂閱者」是否可以透過 FTP 下載快照集檔案，以及「訂閱者」是否可以透過 HTTP 同步處理訂閱。  
  
-   **[訂閱選項]** 頁面允許您設定套用至所有訂閱的一些選項。 選項視發行集類型的不同而不同。  
  
-   **[發行集存取清單]** 頁面允許您指定可存取發行集的登入和群組。  
  
-   **[代理程式安全性]** 頁面允許您存取執行以下代理程式之帳戶的設定，並與複寫拓撲中的電腦建立連接：所有發行集的「快照集代理程式」；所有交易式發行集的「記錄讀取器代理程式」；及允許佇列更新訂閱之交易式發行集的「佇列讀取器代理程式」。  
  
-   **[資料分割]** 頁面 (針對執行 SQL Server 2005 或更新版本之「發行者」的合併式發行集) 允許您指定至含參數化篩選之發行集的「訂閱者」是否可以在一個快照集不可用時要求另一個快照集。 它還允許您為一個或多個資料分割一次性或按循環排程產生快照集。  
  
#### <a name="to-view-and-modify-publication-properties-in-management-studio"></a>若要在 Management Studio 中檢視和修改發行集屬性  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下發行集，然後按一下 **[屬性]**。  
  
4.  必要時修改任何屬性，然後按一下 **[確定]**。  
  
#### <a name="to-view-and-modify-publication-properties-in-replication-monitor"></a>若要在複寫監視器中檢視和修改發行集屬性  
  
1.  展開「複寫監視器」左窗格中的「發行者」群組，然後展開一個「發行者」。  
  
2.  以滑鼠右鍵按一下發行集，然後按一下 **[屬性]**。  
  
3.  必要時修改任何屬性，然後按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式修改發行集及傳回其屬性。 您使用的預存程序將根據發行集的類型而定。  
  
#### <a name="to-view-the-properties-of-a-snapshot-or-transactional-publication"></a>檢視快照式或交易式發行集的屬性  
  
1.  執行 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)，針對 **@publication** 參數指定發行集的名稱。 如果您不指定這個參數，就會傳回發行者上與所有發行集有關的資訊。  
  
#### <a name="to-change-the-properties-of-a-snapshot-or-transactional-publication"></a>變更快照式或交易式發行集的屬性  
  
1.  執行 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)，在 **@property** 參數中指定要變更的發行集屬性，並在 **@value** 參數指定發行集的名稱。  
  
    > [!NOTE]  
    >  如果此變更將需要產生新的快照集，您也必須針對 **@force_invalidate_snapshot** 指定 **@force_invalidate_snapshot**的值，而如果此變更將需要重新初始化訂閱者，您就必須針對 **@force_invalidate_snapshot** 指定 **@force_reinit_subscription**。 如需當變更時需要新的快照集或重新初始化之屬性的詳細資訊，請參閱[變更發行集與發行項屬性](change-publication-and-article-properties.md)。  
  
#### <a name="to-view-the-properties-of-a-merge-publication"></a>檢視合併式發行集的屬性  
  
1.  執行 [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)，針對 **@publication** 參數指定發行集的名稱。 如果您不指定這個參數，就會傳回發行者上與所有發行集有關的資訊。  
  
#### <a name="to-change-the-properties-of-a-merge-publication"></a>變更合併式發行集的屬性  
  
1.  執行 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)，在 **@property** 參數中指定要變更的發行集屬性，並在 **@value** 參數指定發行集的名稱。  
  
    > [!NOTE]  
    >  若此變更將需要產生新的快照集，您也必須針對 **@force_invalidate_snapshot** 指定 **1** 的值，而如果此變更將需要重新初始化訂閱者，您就必須針對 **@force_reinit_subscription** 指定 **1** 的值。如需變更時需要新的快照集或重新初始化之屬性的詳細資訊，請參閱[變更發行集與發行項屬性](change-publication-and-article-properties.md)。  
  
#### <a name="to-view-the-properties-of-a-snapshot"></a>檢視快照集的屬性  
  
1.  執行 [sp_helppublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql)，針對 **@publication** 參數指定發行集的名稱。  
  
#### <a name="to-change-the-properties-of-a-snapshot"></a>變更快照集的屬性  
  
1.  執行 [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql)，針對適當的快照集參數指定一或多個新的快照集屬性。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個異動複寫範例會傳回發行集的屬性。  
  
 [!code-sql[HowTo#sp_helppublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changetranpub.sql#sp_helppublication)]  
  
 這個異動複寫範例會停用發行集的結構描述複寫。  
  
 [!code-sql[HowTo#sp_changepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changetranpub.sql#sp_changepublication)]  
  
 這個合併式複寫範例會傳回發行集的屬性。  
  
 [!code-sql[HowTo#sp_helpmergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changemergepub.sql#sp_helpmergepublication)]  
  
 這個合併式複寫範例會停用發行集的結構描述複寫。  
  
 [!code-sql[HowTo#sp_changemergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changemergepub.sql#sp_changemergepublication)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式修改發行集及存取其屬性。 用來檢視或修改發行集屬性的 RMO 類別，將取決於發行集的類型而定。  
  
#### <a name="to-view-or-modify-properties-of-a-snapshot-or-transactional-publication"></a>檢視或修改快照式或交易式發行集的屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別的執行個體、為發行集設定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性，以及將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為步驟 1 中所建立的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回`false`，是在步驟 2 中的發行集屬性定義不正確，或發行集不存在。  
  
4.  (選擇性) 若要變更屬性，請針對一或多個可設定的屬性設定新的值。 使用邏輯 AND 運算子 (`&`在 Microsoft Visual C# 和`And`在 Microsoft Visual Basic) 來判斷給定<xref:Microsoft.SqlServer.Replication.PublicationAttributes>值皆設<xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>屬性。 使用包含的邏輯 OR 運算子 (Visual C# 中的 `|` 和 Visual Basic 中的 `Or`)，並使用排除的邏輯 OR 運算子 (Visual C# 中的 `^` 和 Visual Basic 中的 `Xor`)，為 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 屬性變更 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 值。  
  
5.  （選擇性）如果您指定的值`true`如<xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>，呼叫<xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>方法來認可伺服器上的變更。 如果您指定的值`false`如<xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>（預設值），變更會立即傳送到伺服器。  
  
#### <a name="to-view-or-modify-properties-of-a-merge-publication"></a>檢視或修改合併式發行集的屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體、為發行集設定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性，以及將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為步驟 1 中所建立的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回`false`，是在步驟 2 中的發行集屬性定義不正確，或發行集不存在。  
  
4.  (選擇性) 若要變更屬性，請針對一或多個可設定的屬性設定新的值。 使用邏輯 AND 運算子 (Visual C# 中的 `&` 及 Visual Basic 中的 `And`)，以判斷是否已針對 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 屬性設定給定的 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 值。 使用包含的邏輯 OR 運算子 (Visual C# 中的 `|` 和 Visual Basic 中的 `Or`)，並使用排除的邏輯 OR 運算子 (Visual C# 中的 `^` 和 Visual Basic 中的 `Xor`)，為 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 屬性變更 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 值。  
  
5.  （選擇性）如果您指定的值`true`如<xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>，呼叫<xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>方法來認可伺服器上的變更。 如果您指定的值`false`如<xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>（預設值），變更會立即傳送到伺服器。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會設定交易式發行集的發行集屬性。 這些變更在明確傳送到伺服器之前，會先加以快取。  
  
 [!code-csharp[HowTo#rmo_ChangeTranPub_cached](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changetranpub_cached)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeTranPub_cached](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changetranpub_cached)]  
  
 此範例會停用合併式發行集的 DDL 複寫。  
  
 [!code-csharp[HowTo#rmo_ChangeMergePub_ddl](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changemergepub_ddl)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergePub_ddl](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changemergepub_ddl)]  
  
## <a name="see-also"></a>另請參閱  
 [發行資料和資料庫物件](publish-data-and-database-objects.md)   
 [變更發行集與發行項屬性](change-publication-and-article-properties.md)   
 [對發行集資料庫進行結構描述變更](make-schema-changes-on-publication-databases.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [在發行集中新增和卸除發行項 &#40;SQL Server Management Studio&#41;](add-articles-to-and-drop-articles-from-a-publication.md)   
 [檢視發行集的資訊並執行工作 &#40;複寫監視器&#41;](../monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [檢視和修改發行項屬性](view-and-modify-article-properties.md)  
  
  
