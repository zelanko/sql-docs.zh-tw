---
title: 複寫結構描述變更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], schema changes
- schemas [SQL Server replication], replicating changes
ms.assetid: c09007f0-9374-4f60-956b-8a87670cd043
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bec2f363cd8c4f7dea45935568a88722b19323fc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060422"
---
# <a name="replicate-schema-changes"></a>複寫結構描述變更
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中複寫結構描述變更。  
  
 如果您要針對發佈的發行項進行下列結構描述變更，則這些變更預設會傳播到 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者：  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要複寫結構描述變更，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   ALTER TABLE ...DROP COLUMN 陳述式一定會複寫至訂閱包含要卸除之資料行的所有「訂閱者」，即使您停用結構描述變更的複寫也是如此。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 如果您不想複寫發行集的架構變更，請在 [**發行集屬性- \<Publication> ** ] 對話方塊中停用架構變更的複寫。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](view-and-modify-publication-properties.md)＞。  
  
#### <a name="to-disable-replication-of-schema-changes"></a>若要停用結構描述變更的複寫  
  
1.  在 [**發行集屬性 \<Publication> -** ] 對話方塊的 [**訂閱選項**] 頁面上，將 [複寫**架構變更**] 屬性的值設定為**False**。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     若只要傳播特定的結構描述變更，請在結構描述變更之前將屬性設定為 **[True]** ，然後在進行變更後將屬性設定為 **[False]** 。 相反的，若要傳播大多數結構描述變更，而不是給定變更，請在結構描述變更之前將屬性設定為 **[False]** ，然後在進行變更後將屬性設定為 **[True]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來指定是否要複寫這些結構描述變更。 您使用的預存程序取決於發行集的類型而定。  
  
#### <a name="to-create-a-snapshot-or-transactional-publication-that-does-not-replicate-schema-changes"></a>建立不會複寫結構描述變更的快照式或交易式發行集  
  
1.  在發行集資料庫的發行者上，執行[sp_addpublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)，為** \@ replicate_ddl**指定**0**的值。 如需詳細資訊，請參閱[建立發行集](create-a-publication.md)。  
  
#### <a name="to-create-a-merge-publication-that-does-not-replicate-schema-changes"></a>建立不會複寫結構描述變更的合併式發行集  
  
1.  在發行集資料庫的發行者上，執行[sp_addmergepublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)，為** \@ replicate_ddl**指定**0**的值。 如需詳細資訊，請參閱[建立發行集](create-a-publication.md)。  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-snapshot-or-transactional-publication"></a>暫時停用快照式或交易式發行集的複寫結構描述變更  
  
1.  針對具有架構變更複寫的發行集，請執行[sp_changepublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)，為** \@ 屬性**指定**replicate_ddl**的值，並為** \@ 值**指定**0**的值。  
  
2.  在發行的物件上執行 DDL 命令。  
  
3.  選擇性藉由執行[sp_changepublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)來重新啟用複寫架構變更，為** \@ 屬性**指定**replicate_ddl**的值，並為** \@ 值**指定**1**的值。  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-merge-publication"></a>暫時停用合併式發行集的複寫結構描述變更  
  
1.  針對具有架構變更複寫的發行集，請執行[sp_changemergepublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)，為** \@ 屬性**指定**replicate_ddl**的值，並為** \@ 值**指定**0**的值。  
  
2.  在發行的物件上執行 DDL 命令。  
  
3.  選擇性藉由執行[sp_changemergepublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)來重新啟用複寫架構變更，為** \@ 屬性**指定**replicate_ddl**的值，並為** \@ 值**指定**1**的值。  
  
## <a name="see-also"></a>另請參閱  
 [對發行集資料庫進行結構描述變更](make-schema-changes-on-publication-databases.md)   
 [對發行集資料庫進行結構描述變更](make-schema-changes-on-publication-databases.md)  
  
  
