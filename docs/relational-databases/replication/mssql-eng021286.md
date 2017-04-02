---
title: "MSSQL_ENG021286 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG021286 錯誤"
ms.assetid: b63620b7-1c6d-46f7-90ea-3a8e99af8de4
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# MSSQL_ENG021286
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|21286|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|衝突資料表 '%s' 不存在。|  
  
## 說明  
 如果發行項的衝突資料表中列出時會發生此錯誤 [sysmergearticles & #40。TRANSACT-SQL & #41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md) 實際上不存在。 嘗試為合併式複寫在已發行資料表中加入資料行，或從其中卸除資料行時，會發生此錯誤。  
  
## 使用者動作  
 執行 [DBCC CHECKDB & #40。TRANSACT-SQL & #41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 確認在遺失衝突資料表的資料庫上沒有資料一致性問題。  
  
 如果「訂閱者」上的衝突資料表已遺漏，則卸除訂閱然後重新建立它。 如果「發行者」上的衝突資料表已遺漏，則卸除所有訂閱，卸除發行集，然後重新建立發行集和所有訂閱。 如需詳細資訊，請參閱 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md) 和 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  