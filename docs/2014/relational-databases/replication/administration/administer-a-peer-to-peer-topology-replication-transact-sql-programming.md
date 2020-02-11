---
title: 管理點對點拓撲 (複寫 Transact-SQL 程式設計) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, peer-to-peer replication
ms.assetid: 4d0fa941-f9ea-4a14-aed9-34df593fc6f2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0cabfb4cd21de54dad2be1323fd29d8bb3bf076
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62629724"
---
# <a name="administer-a-peer-to-peer-topology-replication-transact-sql-programming"></a>管理點對點拓撲 (複寫 Transact-SQL 程式設計)
  管理點對點拓撲與管理一般的異動複寫拓撲類似，但有一些需要特殊考量的地方。 管理點對點拓撲的主要差別在於有些變更需要 *「停止」* (Quiesce) 系統。 停止系統包括停止所有節點上已發行資料表的活動，並確定每個節點已收到來自其他所有節點的所有變更。 如需詳細資訊，請參閱[停止複寫拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](quiesce-a-replication-topology-replication-transact-sql-programming.md)。  
  
> [!NOTE]  
>  在點對點拓撲中，散發者無法使用比提取訂閱者還舊的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本。  
  
### <a name="to-add-an-article-to-an-existing-configuration"></a>若要將發行項加入至現有的組態  
  
1.  停止系統。  
  
2.  停止拓撲中每個節點的「散發代理程式」。 如需詳細資訊，請參閱[複寫代理程式可執行檔概念](../concepts/replication-agent-executables-concepts.md)或[啟動和停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
3.  執行 CREATE TABLE 陳述式，在拓撲中的每個節點加入新資料表。  
  
4.  使用 [bcp 公用程式](../../../tools/bcp-utility.md)，以手動方式在所有節點大量複製新資料表的資料。  
  
5.  執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) ，在拓撲中的每個節點建立新發行項。 如需詳細資訊，請參閱 [定義發行項](../publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  在執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 之後，複寫會將發行項自動加入至拓撲中的訂閱。  
  
6.  重新啟動拓撲中每個節點的「散發代理程式」。  
  
### <a name="to-make-schema-changes-to-a-publication-database"></a>若要對發行集資料庫進行結構描述變更  
  
1.  停止系統。  
  
2.  執行資料定義語言 (DDL) 陳述式，修改已發行資料表的結構描述。 如需受支援結構描述變更的詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../publish/make-schema-changes-on-publication-databases.md)。  
  
3.  在已發行資料表上繼續活動之前，請再次停止系統。 如此可確保在複寫任何新的資料變更之前，所有節點都已接收到結構描述變更。  
  
## <a name="example"></a>範例  
 下列範例示範如何在擁有兩個節點的現有點對點複寫拓撲中，加入新的資料表發行項。  
  
 [!code-sql[HowTo#sp_addp2particle_createtables](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_createtables)]  
  
 [!code-sql[HowTo#sp_addp2particle_cmdline](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_cmdline)]  
  
 [!code-sql[HowTo#sp_addp2particle_createarticle](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_createarticle)]  
  
## <a name="see-also"></a>另請參閱  
 [複寫管理常見問題集](frequently-asked-questions-for-replication-administrators.md)   
 [SQL Server 資料庫的備份與還原](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [@loopback_detection](../transactional/peer-to-peer-transactional-replication.md)  
  
  
