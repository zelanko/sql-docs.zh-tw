---
title: 訂閱發行集 | Microsoft Docs
description: 了解 SQL Server 複寫中的訂閱類型、如何選擇所需要的類型，以及如何建立訂閱。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.conc.subtopubs.f1
helpviewer_keywords:
- subscriptions [SQL Server replication], about subscriptions
- pull subscriptions [SQL Server replication]
- subscriptions [SQL Server replication]
- push subscriptions [SQL Server replication], about push subscriptions
- merge replication subscribing [SQL Server replication]
- merge replication subscribing [SQL Server replication], about subscribing
- publications [SQL Server replication], subscribing
- push subscriptions [SQL Server replication]
- pull subscriptions [SQL Server replication], about pull subscriptions
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 088ee30a-05ab-47c4-92ed-316b93e12445
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 347566a8187cbe61132e1c7f024e3f0dc6cd814e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917718"
---
# <a name="subscribe-to-publications"></a>訂閱發行集
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  訂閱是指要求一份發行集中的資料和資料庫物件。 訂閱會定義將收到的發行集，以及收到的位置和時間。 規劃訂閱時，請考慮要執行代理程式處理的位置。 您選擇的訂閱類型會控制代理程式執行的位置。 若為發送訂閱，則「合併代理程式」或「散發代理程式」會在「散發者」執行；若為提取訂閱，則代理程式會在「訂閱者」執行。 建立訂閱之後，就不能變更訂閱的類型。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
|訂用帳戶|特性|使用時機|  
|------------------|---------------------|--------------|  
|發送訂閱|在發送訂閱中，「訂閱者」不需發出請求，「發行者」便會將變更傳播給「訂閱者」。 變更可以在需要時發散給「訂閱者」，或是根據排程發散給「訂閱者」。 「散發代理程式」或「合併代理程式」是在「散發者」中執行。|通常是連續或根據定期排程進行資料同步。<br /><br /> 發行集需要近乎即時移動資料。<br /><br /> 即使「散發者」的處理器額外負荷較高，也不會影響效能。<br /><br /> 最常搭配快照和異動複寫使用。|  
|提取訂閱|在提取訂閱中，「訂閱者」必須請求傳送「發行者」中的變更。 提取訂閱允許使用者在「訂閱者」中判斷何時要同步資料變更。 「散發代理程式」或「合併代理程式」是在「訂閱者」中執行。|資料通常是在需要時或根據排程進行同步處理，而不是持續進行。<br /><br /> 發行集擁有大量「訂閱者」，且 (或) 其需要過多資源，而無法在「散發者」執行所有代理程式。<br /><br /> 「訂閱者」是獨立的、中斷的以及/或機動的。 「訂閱者」將決定其連接及同步變更的時機。<br /><br /> 最常搭配合併複寫使用。|  
  
## <a name="merge-replication-subscription-types"></a>合併複寫訂閱類型  
 所有複寫類型都允許發送和提取訂閱。 合併複寫會使用另外兩個詞彙來區分訂閱︰客訂閱和主訂閱。 客訂閱和主訂閱類型都可搭配發送和提取訂閱使用。 客訂閱適用大部份的「訂閱者」，而主訂閱通常用於重新發行資料給其他「訂閱者」的「訂閱者」。 訂閱選擇也會影響衝突解決。  
  
## <a name="non-sql-server-subscribers"></a>非 SQL Server 訂閱者  
 Oracle 和 IBM DB2 都可使用發送訂閱來訂閱快照集和交易式發行集。 如需詳細資訊，請參閱 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。  
  
## <a name="creating-subscriptions"></a>建立訂閱  
 若要建立訂閱，您必須提供下列資訊︰  
  
-   發行集的名稱。  
  
-   「訂閱者」和訂閱資料庫的名稱。  
  
-   在「散發者」或「訂閱者」執行「散發代理程式」或「合併代理程式」。  
  
-   「散發代理程式」或「合併代理程式」會持續執行、定期執行，或是需要時才執行。  
  
-   「快照集代理程式」是否應該為訂閱建立初始快照集，以及「散發代理程式」或「合併代理程式」是否應該在「訂閱者」中套用該快照集。  
  
-   用來執行「散發代理程式」或「合併代理程式」的帳戶。  
  
-   合併複寫的訂閱類型為︰主或客。  
  
 **若要建立發送訂閱**  
  
 [建立發送訂閱](../../relational-databases/replication/create-a-push-subscription.md)  
  
 **若要檢視或修改發送訂閱屬性**  
  
 [檢視及修改發送訂閱屬性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)  
  
 **若要刪除發送訂閱**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:[刪除發送訂閱](../../relational-databases/replication/delete-a-push-subscription.md)  
  
> [!NOTE]  
>  刪除訂閱並不會移除「訂閱者」中已發行的物件。  
  
 **若要建立提取訂閱**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:[建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)  
  
 **若要檢視或修改提取訂閱屬性**  
  
 [檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  
  
 **若要刪除提取訂閱**  
  
 [刪除提取訂閱](../../relational-databases/replication/delete-a-pull-subscription.md)  
  
## <a name="see-also"></a>另請參閱  
 [保護訂閱者](../../relational-databases/replication/security/secure-the-subscriber.md)   
 [訂閱逾期與停用](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
