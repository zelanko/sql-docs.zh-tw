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
manager: craigg
ms.openlocfilehash: 1a2c275604d9c74699eeb2b3c77a90e2d819fb6c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68199331"
---
# <a name="replicate-schema-changes"></a>複寫結構描述變更
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中複寫結構描述變更。  
  
 如果您想要針對發行的發行項進行以下的結構描述變更，這些變更預設會傳播到 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者：  
  
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
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   ALTER TABLE ...DROP COLUMN 陳述式一定會複寫至訂閱包含要卸除之資料行的所有「訂閱者」，即使您停用結構描述變更的複寫也是如此。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 如果您不想複寫發行集的結構描述變更，請在 [發行集屬性 - \<發行集>]  對話方塊中停用結構描述變更的複寫。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](view-and-modify-publication-properties.md)＞。  
  
#### <a name="to-disable-replication-of-schema-changes"></a>若要停用結構描述變更的複寫  
  
1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [訂閱選項]  頁面上，將 [複寫結構描述變更]  屬性的值設定為 [False]  。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     若只要傳播特定的結構描述變更，請在結構描述變更之前將屬性設定為 **[True]** ，然後在進行變更後將屬性設定為 **[False]** 。 相反的，若要傳播大多數結構描述變更，而不是給定變更，請在結構描述變更之前將屬性設定為 **[False]** ，然後在進行變更後將屬性設定為 **[True]** 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來指定是否要複寫這些結構描述變更。 您使用的預存程序取決於發行集的類型而定。  
  
#### <a name="to-create-a-snapshot-or-transactional-publication-that-does-not-replicate-schema-changes"></a>建立不會複寫結構描述變更的快照式或交易式發行集  
  
1.  在發行集資料庫的發行者端，執行 [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)，並針對 **@replicate_ddl** 指定值 **0**。 如需詳細資訊，請參閱[建立發行集](create-a-publication.md)。  
  
#### <a name="to-create-a-merge-publication-that-does-not-replicate-schema-changes"></a>建立不會複寫結構描述變更的合併式發行集  
  
1.  在發行集資料庫的發行者端，執行 [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)，並針對 **@replicate_ddl** 指定值 **0**。 如需詳細資訊，請參閱[建立發行集](create-a-publication.md)。  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-snapshot-or-transactional-publication"></a>暫時停用快照式或交易式發行集的複寫結構描述變更  
  
1.  如果是具有複寫結構描述變更的發行集，請執行 [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)，並針對 **@property** 指定值 **replicate_ddl** 的值，以及針對 **@value** 指定值 **0**。  
  
2.  在發行的物件上執行 DDL 命令。  
  
3.  (選擇性) 重新啟用複寫結構描述變更，其方式是執行 [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)，並針對 **@property** 指定值 **replicate_ddl**，以及針對 **@value** 指定值 **1**。  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-merge-publication"></a>暫時停用合併式發行集的複寫結構描述變更  
  
1.  如果是具有複寫結構描述變更的發行集，請執行 [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)，並針對 **@property** 指定值 **replicate_ddl** 的值，以及針對 **@value** 指定值 **0**。  
  
2.  在發行的物件上執行 DDL 命令。  
  
3.  (選擇性) 重新啟用複寫結構描述變更，其方式是執行 [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)，並針對 **@property** 指定值 **replicate_ddl**，以及針對 **@value** 指定值 **1**。  
  
## <a name="see-also"></a>另請參閱  
 [對發行集資料庫進行結構描述變更](make-schema-changes-on-publication-databases.md)   
 [對發行集資料庫進行結構描述變更](make-schema-changes-on-publication-databases.md)  
  
  
