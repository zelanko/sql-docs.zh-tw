---
title: 刪除發行項 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], dropping
- sp_droparticle
- sp_dropmergearticle
- deleting articles
- removing articles
- dropping articles
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4be2287a1c0d43ccfdfaeaca3378f6d10f100134
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882276"
---
# <a name="delete-an-article"></a>刪除發行項
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中刪除發行項。 如需可以卸除發行項的情況以及發行項是否需要新快照集或重新初始化訂閱的詳細資訊，請參閱[在現有發行集中加入和卸除發行項](add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式刪除發行項。 使用哪些預存程序要依發行項所屬的發行集類型而定。  
  
#### <a name="to-delete-an-article-from-a-snapshot-or-transactional-publication"></a>從快照式或交易式發行集中刪除發行項  
  
1.  從 **\@publication** 指定的發行集執行 [sp_droparticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql) 來刪除 **\@article** 指定的發行項。 為 **\@force_invalidate_snapshot** 指定 **1** 值。  
  
2.  (選擇性) 若要從資料庫完全移除發行的物件，請在發行集資料庫的發行者上執行 `DROP <objectname>` 命令。  
  
#### <a name="to-delete-an-article-from-a-merge-publication"></a>從合併式發行集中刪除發行項  
  
1.  從 **\@publication** 指定的發行集執行 [sp_dropmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql) 來刪除 **\@article** 指定的發行項。 必要時，請為 **\@force_invalidate_snapshot** 指定 **1** 值，並為 **\@force_reinit_subscription** 指定 **1** 值。  
  
2.  (選擇性) 若要從資料庫完全移除發行的物件，請在發行集資料庫的發行者上執行 `DROP <objectname>` 命令。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會刪除交易式發行集中的發行項。 由於這項變更會讓現有的快照集失效，所以請為 **\@force_invalidate_snapshot** 參數指定 **1** 值。  
  
 [!code-sql[HowTo#sp_droparticle](../../../snippets/tsql/SQL15/replication/howto/tsql/droptranpub.sql#sp_droparticle)]  
  
 下列範例會刪除合併式發行集中的兩個發行項。 由於這些變更會讓現有的快照集失效，所以請為 **\@force_invalidate_snapshot** 參數指定 **1** 值。  
  
 [!code-sql[HowTo#sp_dropmergearticle](../../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepub.sql#sp_dropmergearticle)]
 [!code-sql[HowTo#sp_dropmergearticle](../../../snippets/tsql/SQL15/replication/howto/tsql/dropmergearticles.sql#sp_dropmergearticle)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式刪除發行項。 用於刪除發行項的 RMO 類別，將取決於發行項所屬的發行集類型而定。  
  
#### <a name="to-delete-an-article-that-belongs-to-a-snapshot-or-transactional-publication"></a>刪除屬於快照式或交易式發行集的發行項  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransArticle> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 屬性。  
  
4.  針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連接。  
  
5.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認該發行項存在。 如果這個屬性的值為 `false`，則表示步驟 3 中的發行項屬性定義錯誤或是此發行項不存在。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> 方法。  
  
7.  關閉所有連接。  
  
#### <a name="to-delete-an-article-that-belongs-to-a-merge-publication"></a>刪除屬於合併式發行集的發行項  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergeArticle> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 屬性。  
  
4.  針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連接。  
  
5.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認該發行項存在。 如果這個屬性的值為 `false`，則表示步驟 3 中的發行項屬性定義錯誤或是此發行項不存在。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> 方法。  
  
7.  關閉所有連接。  
  
## <a name="see-also"></a>另請參閱  
 [在現有發行集中加入和卸除發行項](add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
