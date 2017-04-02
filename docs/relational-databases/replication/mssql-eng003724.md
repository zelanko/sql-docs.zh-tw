---
title: "MSSQL_ENG003724 | Microsoft Docs"
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
  - "MSSQL_ENG003724 錯誤"
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# MSSQL_ENG003724
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|3724|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|無法 %S_MSG %S_MSG '%.*ls'，因為它正用於複寫。|  
  
## 說明  
 當資料庫中的物件複寫時，被標示為複寫系統資料表中 **sysarticles** （針對快照集和交易式發行集） 或 **sysmergearticles** （適用於合併式發行集）。 如果您嘗試放入已複寫物件，便會發生這個錯誤。  
  
## 使用者動作  
 在放入資料庫物件之前，請先確定它並未複寫。 例如：  
  
-   如果在發行集資料庫中發生錯誤，請在放入該物件之前先從發行集中放入發行項。 如需詳細資訊，請參閱 [新增和卸除現有的發行集的文章](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
-   如果在訂閱資料庫中發生錯誤，請在放入該物件之前先放入訂閱。 如需詳細資訊，請參閱 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)。 針對交易式發行集的訂閱，可以將訂閱放入個別發行項，而非整個發行集。 如需詳細資訊，請參閱 [sp_dropsubscription & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)。  
  
 如果未複寫的資料庫中，會發生此錯誤，執行 [sp_removedbreplication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 若要確保資料庫中的物件未標示為複寫。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  