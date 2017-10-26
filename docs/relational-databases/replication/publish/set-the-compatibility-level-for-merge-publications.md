---
title: "設定合併式發行集的相容性層級 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [SQL Server], replication
- backward compatibility [SQL Server], replication
- publications [SQL Server replication], backward compatibility
ms.assetid: db47ac73-948b-4d77-b272-bb3565135ea5
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 99a56af259a4be7f07183f22874385b515d6c044
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="set-the-compatibility-level-for-merge-publications"></a>設定合併式發行集的相容性層級
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中設定合併式發行集的相容性層級。 合併式複寫使用發行集相容性層級，來確定發行集可在給定資料庫中使用的功能。  
  
 **本主題內容**  
  
-   **若要設定合併式發行集的相容性層級，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在「新增發行集精靈」的 **[訂閱者類型]** 頁面中設定相容性層級。 如需存取此精靈的詳細資訊，請參閱＜ [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)中設定合併式發行集的相容性層級。 建立發行集快照集後，可以提高相容性層級，但不能降低。 您可以在 [發行集屬性 - \<發行集>] 對話方塊的 [一般] 頁面上，增加相容性層級。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。 如果提高發行集的相容性層級，則對於執行相容性層級之前版本的伺服器，其上的所有現有訂閱均無法再同步處理。  
  
> [!NOTE]  
>  因為相容性層級對其他發行集屬性有影響，並且發行項屬性對其有效，所以不要變更相容性層級以及對話方塊中相同用途的其他屬性。 發行集的快照集應在變更屬性後重新產生。  
  
#### <a name="to-set-the-publication-compatibility-level"></a>若要設定發行集相容性層級  
  
-   在「新增發行集精靈」的 **[訂閱者類型]** 頁面中，選取發行集應支援的「訂閱者」類型。  
  
#### <a name="to-increase-the-publication-compatibility-level"></a>若要提高發行集相容性層級  
  
-   您可以在 [發行集屬性 - \<發行集>] 對話方塊的 [一般] 頁面上，選取 [相容性層級]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 合併式發行集的相容性層級可以在建立發行集時以程式設計方式加以設定，或是在之後以程式設計方式加以修改。 您可以使用複寫預存程序來設定或變更此發行集屬性。  
  
#### <a name="to-set-the-publication-compatibility-level-for-a-merge-publication"></a>設定合併式發行集的發行集相容性層級  
  
1.  在發行者上，執行 [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)，為 **@publication_compatibility_level** 指定值，好讓發行集與舊版的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 相容。 如需詳細資訊，請參閱 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### <a name="to-change-the-publication-compatibility-level-of-a-merge-publication"></a>變更合併式發行集的發行集相容性層級  
  
1.  執行 [sp_changemergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)，為 **@property** 指定 **publication_compatibility_level**，並為 **@value** 指定適當的發行集相容性層級。  
  
#### <a name="to-determine-the-publication-compatibility-level-of-a-merge-publication"></a>判斷合併式發行集的發行集相容性層級  
  
1.  執行 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)，指定所需的發行集。  
  
2.  在結果集的 **backward_comp_level** 欄中尋找發行集相容性層級。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會建立合併式發行集，並設定發行集相容性層級。  
  
```  
-- To avoid storing the login and password in the script file, the values   
-- are passed into SQLCMD as scripting variables. For information about   
-- how to use scripting variables on the command line and in SQL Server  
-- Management Studio, see the "Executing Replication Scripts" section in  
-- the topic "Programming Replication Using System Stored Procedures".  
  
--Add a new merge publication.  
DECLARE @publicationDB AS sysname;  
DECLARE @publication AS sysname;  
DECLARE @login AS sysname;  
DECLARE @password AS sysname;  
SET @publicationDB = N'AdventureWorks2012';   
SET @publication = N'AdvWorksSalesOrdersMerge'   
SET @login = $(Login);  
SET @password = $(Password);  
  
-- Create a new merge publication.   
USE [AdventureWorks2012]  
EXEC sp_addmergepublication   
@publication = @publication,   
-- Set the compatibility level to SQL Server 2014.  
@publication_compatibility_level = '120RTM';   
  
-- Create the snapshot job for the publication.  
EXEC sp_addpublication_snapshot   
@publication = @publication,  
@job_login = @login,  
@job_password = @password;  
GO  
```  
  
 此範例會變更合併式發行集的發行集相容性層級。  
  
> [!NOTE]  
>  如果發行集使用任何需要特定相容性層級的功能，則可能不允許變更發行集相容性層級。 如需詳細資訊，請參閱[複寫回溯相容性](../../../relational-databases/replication/replication-backward-compatibility.md)。  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
  
-- Change the publication compatibility level to   
-- SQL Server 2012.  
EXEC sp_changemergepublication   
@publication = @publication,   
@property = N'publication_compatibility_level',   
@value = N'110RTM';  
GO  
  
```  
  
 此範例會傳回合併式發行集的正確發行集相容性層級。  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
EXEC sp_helpmergepublication   
@publication = @publication;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
  

