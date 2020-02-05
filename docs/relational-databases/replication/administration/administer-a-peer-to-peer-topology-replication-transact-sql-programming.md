---
title: 管理點對點拓撲 (複寫 SP)
description: 了解如何使用複寫預存程序來管理點對點拓撲，例如新增發行項或進行結構描述變更。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 712a0514bf4fb9e4c66e0d6f7b0475ec5a957dde
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75322195"
---
# <a name="administer-a-peer-to-peer-topology-replication-transact-sql-programming"></a>管理點對點拓撲 (複寫 Transact-SQL 程式設計)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  管理點對點拓撲與管理一般的異動複寫拓撲類似，但有一些需要特殊考量的地方。 管理點對點拓撲的主要差別在於有些變更需要 *「停止」* (Quiesce) 系統。 停止系統包括停止所有節點上已發行資料表的活動，並確定每個節點已收到來自其他所有節點的所有變更。 如需詳細資訊，請參閱[停止複寫拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)。  
  
> [!NOTE]  
>  在點對點拓撲中，散發者無法使用比提取訂閱者還舊的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本。  
  
### <a name="to-add-an-article-to-an-existing-configuration"></a>若要將發行項加入至現有的組態  
  
1.  停止系統。  
  
2.  停止拓撲中每個節點的「散發代理程式」。 如需詳細資訊，請參閱[複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)或[啟動和停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
3.  執行 CREATE TABLE 陳述式，在拓撲中的每個節點加入新資料表。  
  
4.  使用 [bcp 公用程式](../../../tools/bcp-utility.md)，以手動方式在所有節點大量複製新資料表的資料。  
  
5.  執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) ，在拓撲中的每個節點建立新發行項。 如需詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  在執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 之後，複寫會將發行項自動加入至拓撲中的訂閱。  
  
6.  重新啟動拓撲中每個節點的「散發代理程式」。  

### <a name="to-make-schema-changes-to-a-publication-database"></a>若要對發行集資料庫進行結構描述變更  
  
1.  停止系統。  
  
2.  執行資料定義語言 (DDL) 陳述式，修改已發行資料表的結構描述。 如需受支援結構描述變更的詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
3.  在已發行資料表上繼續活動之前，請再次停止系統。 如此可確保在複寫任何新的資料變更之前，所有節點都已接收到結構描述變更。  
  
## <a name="example"></a>範例  
 下列範例示範如何在擁有兩個節點的現有點對點複寫拓撲中，加入新的資料表發行項。  
  
 [!code-sql[HowTo#sp_addp2particle_createtables](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_1.sql)]  
  
 [!code-sql[HowTo#sp_addp2particle_cmdline](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_2.sql)]  
  
 [!code-sql[HowTo#sp_addp2particle_createarticle](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_3.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [複寫管理常見問題集](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)   
 [SQL Server 資料庫的備份與還原](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [@loopback_detection](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
