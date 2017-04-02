---
title: "檢視 SQL Server 執行個體上的資料庫清單 | Microsoft Docs"
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
  - "目前的資料庫"
  - "目前位於伺服器上的資料庫 [SQL Server]"
  - "資料庫清單 [SQL Server]"
  - "檢視資料庫清單"
  - "顯示資料庫清單"
  - "資料庫 [SQL Server], 檢視"
  - "伺服器 [SQL Server], 列出的資料庫"
  - "列出資料庫"
ms.assetid: 7ee7a789-db36-4be9-8a0e-0362a1e152dd
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# 檢視 SQL Server 執行個體上的資料庫清單
  此主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來檢視 [!INCLUDE[tsql](../../includes/tsql-md.md)]執行個體上的資料庫清單。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **使用下列方法檢視 SQL Server 執行個體上的資料庫清單：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 如果 **sys.databases** 的呼叫端不是資料庫的擁有者，而且該資料庫不是 **master** 或 **tempdb**，那麼要查看對應資料列所需具備的最低權限，就是 ALTER ANY DATABASE 或 VIEW ANY DATABASE 伺服器層級權限，或是 **master** 資料庫中的 CREATE DATABASE 權限。 呼叫端所連接的資料庫，永遠可以在 **sys.databases**中進行檢視。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 若要檢視 SQL Server 執行個體上的資料庫清單  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  若要查看執行個體上所有資料庫的清單，請展開 **[資料庫]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 若要檢視 SQL Server 執行個體上的資料庫清單  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例會傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上的資料庫清單。 此清單包含資料庫名稱、其資料庫識別碼和建立資料庫的日期。  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT name, database_id, create_date  
FROM sys.databases ;  
GO  
  
```  
  
## 另請參閱  
 [資料庫和檔案目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  