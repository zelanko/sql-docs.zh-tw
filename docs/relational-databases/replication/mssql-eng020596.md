---
title: "MSSQL_ENG020596 | Microsoft Docs"
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
  - "MSSQL_ENG020596 錯誤"
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG020596
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|20596|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|只有 '%s' 或 db_owner 的成員可以卸除匿名的代理程式。|  
  
## 說明  
 您沒有足夠的權限卸除匿名訂閱的代理程式。 呼叫時使用的登入 [sp_dropanonymousagent & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql.md) 必須是成員 **sysadmin** 散發者端的固定的伺服器角色或 **db_owner** 固定的資料庫角色中的散發資料庫或使用者必須是第一個執行代理程式的一個。  
  
## 使用者動作  
 使用適當的認證，登入並執行 **sp_dropanonymousagent**。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  