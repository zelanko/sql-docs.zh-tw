---
title: 控制同步處理中觸發程序和條件約束的行為 |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
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
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5c50e85b407f260d9a6a1b70ec9481fa3dc1d671
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32954463"
---
# <a name="control-behavior-of-triggers-and-constraints-in-synchronization"></a>控制同步處理中觸發程序和條件約束的行為
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在同步處理期間，複寫代理程式會在複寫的資料表上執行 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)、[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) 和 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) 陳述式，這樣可能會讓這些資料表上的資料操作語言 (DML) 觸發程序得以執行。 在某些情況下，您可能需要在同步處理期間避免這些觸發程序的引發或避免條件約束的強制使用。 這個行為取決於觸發程序或條件約束的建立方式而定。  
  
### <a name="to-prevent-triggers-from-executing-during-synchronization"></a>在同步處理期間避免觸發程序的執行  
  
1.  在建立新的觸發程序時，請指定 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md) 的 NOT FOR REPLICATION 選項。  
  
2.  對於現有的觸發程序，則指定 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md) 的 NOT FOR REPLICATION 選項。  
  
### <a name="to-prevent-constraints-from-being-enforced-during-synchronization"></a>在同步處理期間避免條件約束的強制使用  
  
1.  當建立新的 CHECK 或 FOREIGN KEY 條件約束時，請在 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 的條件約束定義中指定 CHECK NOT FOR REPLICATION 選項。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料表 &#40;Database Engine&#41;](../../relational-databases/tables/create-tables-database-engine.md)  
  
  
