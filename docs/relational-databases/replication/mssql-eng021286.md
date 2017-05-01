---
title: MSSQL_ENG021286 | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG021286 error
ms.assetid: b63620b7-1c6d-46f7-90ea-3a8e99af8de4
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 94e5042a99ef6ea6df482cf86323f9444e006dbd
ms.lasthandoff: 04/11/2017

---
# <a name="mssqleng021286"></a>MSSQL_ENG021286
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|21286|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|衝突資料表 '%s' 不存在。|  
  
## <a name="explanation"></a>說明  
 如果 [sysmergearticles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) 中所列發行項的衝突資料表實際上不存在，則會引發此錯誤。 嘗試為合併式複寫在已發行資料表中加入資料行，或從其中卸除資料行時，會發生此錯誤。  
  
## <a name="user-action"></a>使用者動作  
 在遺失衝突資料表的資料庫上執行 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)，以確認資料沒有不一致的問題。  
  
 如果「訂閱者」上的衝突資料表已遺漏，則卸除訂閱然後重新建立它。 如果「發行者」上的衝突資料表已遺漏，則卸除所有訂閱，卸除發行集，然後重新建立發行集和所有訂閱。 如需詳細資訊，請參閱[發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)以及[訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
