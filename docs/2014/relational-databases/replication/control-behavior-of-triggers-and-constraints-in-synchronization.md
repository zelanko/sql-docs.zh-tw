---
title: 同步處理 （複寫 TRANSACT-SQL 程式設計） 期間控制觸發程序和條件約束的行為 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- identities [SQL Server replication]
- constraints [SQL Server], replication
- triggers [SQL Server], replication
- triggers [SQL Server replication]
- constraints [SQL Server replication]
- NOT FOR REPLICATION option
- NFR option
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 26d9a2431b91c1dc081345a06e7fe5a7533cbaa2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721518"
---
# <a name="control-the-behavior-of-triggers-and-constraints-during-synchronization-replication-transact-sql-programming"></a>在同步處理期間控制觸發程序和條件約束的行為 (複寫 Transact-SQL 程式設計)
  在同步處理期間，複寫代理程式會在複寫的資料表上執行 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)、[UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql) 和 [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql) 陳述式，這樣可能會讓這些資料表上的資料操作語言 (DML) 觸發程序得以執行。 在某些情況下，您可能需要在同步處理期間避免這些觸發程序的引發或避免條件約束的強制使用。 這個行為取決於觸發程序或條件約束的建立方式而定。  
  
### <a name="to-prevent-triggers-from-executing-during-synchronization"></a>在同步處理期間避免觸發程序的執行  
  
1.  在建立新的觸發程序時，請指定 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql) 的 NOT FOR REPLICATION 選項。  
  
2.  對於現有的觸發程序，則指定 [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql) 的 NOT FOR REPLICATION 選項。  
  
### <a name="to-prevent-constraints-from-being-enforced-during-synchronization"></a>在同步處理期間避免條件約束的強制使用  
  
1.  當建立新的 CHECK 或 FOREIGN KEY 條件約束時，請在 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) 的條件約束定義中指定 CHECK NOT FOR REPLICATION 選項。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料表 &#40;Database Engine&#41;](../tables/create-tables-database-engine.md)  
  
  
