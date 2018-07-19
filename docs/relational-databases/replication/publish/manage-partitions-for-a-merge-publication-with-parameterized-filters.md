---
title: 使用參數化篩選管理合併式發行集的資料分割 | Microsoft Docs
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
helpviewer_keywords:
- partitions [SQL Server replication]
- merge replication partitions [SQL Server replication], SQL Server Management Studio
- parameterized filters [SQL Server replication], partition management
ms.assetid: fb5566fe-58c5-48f7-8464-814ea78e6221
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b5194772695b8b63785bf82634e31873a7056390
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37359510"
---
# <a name="manage-partitions-for-a-merge-publication-with-parameterized-filters"></a>使用參數化篩選管理合併式發行集的資料分割
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中使用參數化篩選管理合併式發行集的資料分割。 參數化資料列篩選器可用來產生非重疊的資料分割。 這些資料分割可以限制為只有一個訂閱能收到給定資料分割。 在這種狀況中，大量的訂閱者會導致大量的資料分割，而這種情況則需要同等數量的資料分割快照集。 如需詳細資訊，請參閱＜ [參數化資料列篩選器](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
-   **若要使用參數化篩選管理合併式發行集的資料分割，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   如果您為複寫拓撲編寫指令碼 (建議您如此做)，則發行集指令碼將包含呼叫建立資料分割的預存程序。 指令碼提供所建立資料分割的參考，並提供必要時重新建立一或多個資料分割的方式。 如需詳細資訊，請參閱 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)。  
  
-   當發行集擁有會產生具有非重疊資料分割之訂閱的參數化篩選時，以及遺失了特定訂閱而需要重新建立時，您必須執行下列作業：移除先前訂閱的資料分割、重新建立訂閱，然後重新建立資料分割。 如需詳細資訊，請參閱＜ [參數化資料列篩選器](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞。 複寫會在發行集建立指令碼產生時，針對現有的「訂閱者」資料分割產生建立指令碼。 如需詳細資訊，請參閱 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 您可以在 [發行集屬性 - \<發行集>] 對話方塊的 [資料分割] 頁面上，管理資料分割。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。 您可以在此頁面中：建立和刪除資料分割；允許「訂閱者」初始化快照集產生和傳遞；為一個或多個資料分割產生快照集；清除快照集。  
  
#### <a name="to-create-a-partition"></a>若要建立資料分割  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [資料分割] 頁面上，按一下 [新增]。  
  
2.  在 **[加入資料分割]** 對話方塊中，輸入與您要建立之資料分割相關聯的 **[HOST_NAME()]** 和/或 **[SUSER_SNAME()]** 值。  
  
3.  選擇性地指定重新整理快照集的排程：  
  
    1.  選取 **[排程這個資料分割的快照集代理程式在下列時間執行]**  
  
    2.  接受重新重理快照集的預設排程，或按一下 **[變更]** 以指定其他排程。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-delete-a-partition"></a>若要刪除資料分割  
  
1.  在 **[資料分割]** 頁面上，從方格中選取一個資料分割。  
  
2.  按一下 **[刪除]**。  
  
#### <a name="to-allow-subscribers-to-initiate-snapshot-generation-and-delivery"></a>若要允許訂閱者初始化快照集的產生與傳遞  
  
1.  在 **[資料分割]** 頁面上，選取 **[新的訂閱者嘗試進行同步處理時，自動定義資料分割並依需要產生快照]**。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-generate-a-snapshot-for-a-partition"></a>若要產生資料分割的快照集  
  
1.  在 **[資料分割]** 頁面上，從方格中選取一個資料分割。  
  
2.  按一下 **[立即產生選取的快照集]**。  
  
#### <a name="to-clean-up-a-snapshot-for-a-partition"></a>若要清除資料分割的快照集  
  
1.  在 **[資料分割]** 頁面上，從方格中選取一個資料分割。  
  
2.  按一下 **[清除現有快照集]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 若要使用參數化篩選以更好的方式管理發行集，可以使用複寫預存程序，以程式設計的方式列舉現有的資料分割。 您也可以建立及刪除現有的資料分割。 您可取得下列有關現有資料分割的資訊：  
  
-   資料分割的篩選方式 (使用 [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md) 或 [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md))。  
  
-   產生資料分割快照集的工作名稱。  
  
-   上次執行資料分割快照集作業的時間。  
  
 雖然兩部分快照集的第二部份可以在初始化新訂閱時視需要而產生，但下列程序可用來控制產生此快照集的方式，並在最方便的時候預先產生此快照集。 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
#### <a name="to-view-information-on-existing-partitions"></a>若要在現有的資料分割上檢視資訊  
  
1.  在發行集資料庫的發行者端，執行 [sp_helpmergepartition &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)。 指定 **@publication**。 (選擇性) 指定 **@suser_sname** 或 **@host_name** ，以根據單一篩選準則僅傳回資訊。  
  
#### <a name="to-define-a-new-partition-and-generate-a-new-partitioned-snapshot"></a>若要定義新的資料分割並產生新的資料分割快照集  
  
1.  在發行集資料庫的發行者端，執行 [sp_addmergepartition &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)。 指定 **@publication**的發行集名稱，並針對下列其中一個項目定義資料分割的參數化值：  
  
    -   **@suser_sname** - 當參數化篩選是由 [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md) 所傳回的值定義時。  
  
    -   **@host_name** - 當參數化篩選是由 [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md) 所傳回的值定義時。  
  
2.  建立並初始化這個新資料分割的參數化快照集。 如需詳細資訊，請參閱 [使用參數化篩選建立合併式發行集的快照集](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
#### <a name="to-delete-a-partition"></a>若要刪除資料分割  
  
1.  在發行集資料庫的發行者端，執行 [sp_dropmergepartition &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md)。 指定 **@publication** 的發行集名稱，並針對下列其中一個項目定義資料分割的參數化值：  
  
    -   **@suser_sname** - 當參數化篩選是由 [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md) 所傳回的值定義時。  
  
    -   **@host_name** - 當參數化篩選是由 [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md) 所傳回的值定義時。  
  
     這也會移除資料分割的快照集作業和快照集檔案。  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 若要使用參數化篩選以更好的方式管理發行集，可以使用 Replication Management Objects (RMO)，以程式設計的方式建立新的「訂閱者」資料分割、列舉現有的「訂閱者」資料分割，以及刪除「訂閱者」資料分割。 如需有關如何建立「訂閱者」資料分割的詳細資訊，請參閱＜ [使用參數化篩選建立合併式發行集的快照集](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)＞。 您可取得下列有關現有資料分割的資訊：  
  
-   資料分割所根據的值和篩選函數。  
  
-   為「訂閱者」產生參數化快照集的作業名稱。  
  
-   上次執行參數化快照集作業的時間。  
  
#### <a name="to-view-information-on-existing-partitions"></a>若要在現有的資料分割上檢視資訊  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體。 設定發行集的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> 方法，並將結果傳遞到 <xref:Microsoft.SqlServer.Replication.MergePartition> 物件的陣列。  
  
5.  針對陣列中的每個 <xref:Microsoft.SqlServer.Replication.MergePartition> 物件，取得任何所要的屬性。  
  
#### <a name="to-delete-existing-partitions"></a>若要刪除現有的資料分割  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體。 設定發行集的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> 方法，並將結果傳遞到 <xref:Microsoft.SqlServer.Replication.MergePartition> 物件的陣列。  
  
5.  對於陣列中的每個 <xref:Microsoft.SqlServer.Replication.MergePartition> 物件，決定是否應該刪除資料分割： 這項決定通常是根據 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A> 屬性或 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A> 屬性的值而定。  
  
6.  在步驟 2 的 <xref:Microsoft.SqlServer.Replication.MergePublication.RemoveMergePartition%2A> 物件上呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication> 方法。 傳遞步驟 5 的 <xref:Microsoft.SqlServer.Replication.MergePartition> 物件。  
  
7.  針對每個刪除的資料分割重複步驟 6。  
  
## <a name="see-also"></a>另請參閱  
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
