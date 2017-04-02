---
title: "檢視已儲存的追蹤 (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "追蹤 [SQL Server], 檢視"
  - "顯示追蹤"
  - "檢視追蹤"
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
caps.latest.revision: 22
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 22
---
# 檢視已儲存的追蹤 (Transact-SQL)
  此主題描述如何使用內建函數來檢視已儲存的追蹤。  
  
### 若要檢視特定追蹤  
  
1.  執行 **fn_trace_getinfo**，並指定需要其資訊的追蹤識別碼。 此函數會傳回資料表，其中列出追蹤、追蹤屬性和屬性的相關資訊。  
  
     以下列方式叫用函數：  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### 若要檢視現有的所有追蹤  
  
1.  執行 **fn_trace_getinfo**，並指定 `0` 或 `default`。 此函數會傳回資料表，其中列出所有追蹤、追蹤屬性和這些屬性的相關資訊。  
  
     以下列方式叫用函數：  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## .NET Framework 安全性  
 若要執行內建函數 **fn_trace_getinfo**，使用者需要下列權限：  
  
 伺服器上的 ALTER TRACE。  
  
## 另請參閱  
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [使用 SQL Server Profiler 檢視和分析追蹤](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  