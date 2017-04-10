---
title: "移動資料庫檔案 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "災害復原 [SQL Server]，移動資料庫檔案"
  - "檔案 [SQL Server], 移動"
  - "資料檔案 [SQL Server]，移動"
  - "檔案移動 [SQL Server]"
  - "移動全文檢索目錄"
  - "移動資料庫"
  - "全文檢索目錄 [SQL Server], 移動"
  - "移動資料庫檔案"
  - "排程磁碟維護 [SQL Server]"
  - "移動檔案"
  - "重新定位資料庫檔案"
  - "計畫的資料庫重新定位 [SQL Server]"
  - "資料庫 [SQL Server]，移動"
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 移動資料庫檔案
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，您可以在 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 陳述式的 FILENAME 子句中指定新的檔案位置，以移動系統和使用者資料庫。 可以使用此方式來移動資料、記錄以及全文檢索目錄檔案。 在下列狀況下這個方法將非常有用：  
  
-   失敗復原。 例如，資料庫因硬體失敗而導致在質疑模式下或被關閉。  
  
-   計畫的重新放置。  
  
-   排程的磁碟維護重新放置。  
  
## 本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[移動使用者資料庫](../../relational-databases/databases/move-user-databases.md)|描述將使用者資料庫檔案和全文檢索目錄檔案移到新位置的程序。|  
|[移動系統資料庫](../../relational-databases/databases/move-system-databases.md)|描述將系統資料庫檔案移到新位置的程序。|  
  
## 另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [資料庫卸離與附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  