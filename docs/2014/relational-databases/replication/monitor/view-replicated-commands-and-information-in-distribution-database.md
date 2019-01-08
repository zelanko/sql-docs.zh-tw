---
title: 檢視複寫的命令和其他資訊，在散發資料庫中 （複寫 TRANSACT-SQL 程式設計） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_browsereplcmds
- transactional replication, monitoring
- distribution databases [SQL Server replication], viewing replicated commands
- viewing replicated commands
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 87cb1034499afe331f78278b43986528a78d9674
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52758070"
---
# <a name="view-replicated-commands-and-other-information-in-the-distribution-database-replication-transact-sql-programming"></a>在散發資料庫中檢視複寫的命令和其他資訊 (複寫 Transact-SQL 程式設計)
  在使用異動複寫時，交易命令在傳播到所有「訂閱者」之前或在「訂閱者」端的「散發代理程式」 您可以使用複寫預存程序，以程式設計的方式檢視散發資料庫中的這些暫止命令。 如需詳細資訊，請參閱[複寫預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql)。  
  
### <a name="to-view-replicated-commands-from-all-transactional-publications-in-the-distribution-database"></a>若要在散發資料庫中檢視從所有交易式發行集所複寫的命令  
  
1.  在散發資料庫的「散發者」端，執行 [sp_browsereplcmds](/sql/relational-databases/system-stored-procedures/sp-browsemergesnapshotfolder-transact-sql)。  
  
### <a name="to-view-replicated-commands-in-the-distribution-database-from-a-specific-article-or-from-a-specific-database-published-using-transactional-replication"></a>若要在散發資料庫中，檢視從使用異動複寫所發行之特定發行項或特定資料庫複寫的命令  
  
1.  (選擇性) 在發行集資料庫的「發行者」端，執行 [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql)。 指定 **@publication** 和 **@article**＞。 請注意結果集中 **article id** 的值。  
  
2.  在散發資料庫的「散發者」端，執行 [sp_browsereplcmds](/sql/relational-databases/system-stored-procedures/sp-browsemergesnapshotfolder-transact-sql)。 (選擇性) 針對 **@article_id**＞。 (選擇性) 針對 **@publisher_database_id**指定發行集資料庫的識別碼，此識別碼可從 **sys.databases** 目錄檢視中的 [database_id](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 資料行取得。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](monitoring-replication-overview.md)  
  
  
