---
title: "其他非 SQL Server 訂閱者 | Microsoft Docs"
ms.custom: ""
ms.date: "03/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "非 SQL Server 訂閱者, 其他類型"
ms.assetid: 96b8beb9-38e8-4ce4-97ca-c0f8656b73b4
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# 其他非 SQL Server 訂閱者
  如需清單的非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 「 訂閱者 」 支援 [!INCLUDE[msCoName](../../../includes/msconame-md.md)], ，請參閱 [非 SQL Server 訂閱者](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。 本主題包含 ODBC 驅動程式和 OLE DB 提供者需求的資訊。  
  
## ODBC 驅動程式需求  
 ODBC 驅動程式：  
  
-   必須與 ODBC (層級 1) 相容。  
  
-   必須是安全執行緒散發者環境。  
  
-   必須能處理交易 (Transaction capable)。  
  
-   必須支援「資料定義語言」(Data Definition Language，DDL)。  
  
-   不能設定成唯讀。  
  
-   例如，必須支援長資料表名稱 **MSreplication_subscriptions**。  
  
## 使用 OLE DB 介面進行複寫  
 OLE DB Provider 必須支援下列物件，才能進行異動複寫：  
  
-   **資料來源** 物件  
  
-   **工作階段** 物件  
  
-   **命令** 物件  
  
-   **資料列集** 物件  
  
-   **錯誤** 物件  
  
### DataSource 物件介面  
 若要連接到某個資料來源，您必須具備下列介面：  
  
-   **IDBInitialize**  
  
-   **IDBCreateSession**  
  
-   **IDBProperties**  
  
 如果提供者支援 **IDBInfo** 介面， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用介面擷取例如引號的識別碼字元、 最大的 SQL 陳述式長度和最大資料表和資料行名稱的字元數的資訊。  
  
### Session 物件介面  
 以下是必要的介面：  
  
-   **IDBCreateCommand**  
  
-   **ITransaction**  
  
-   **ITransactionLocal**  
  
-   **IDBSchemaRowset**  
  
### Command 物件介面  
 以下是必要的介面：  
  
-   **ICommand**  
  
-   **ICommandProperties**  
  
-   **ICommandText**  
  
-   **ICommandPrepare**  
  
-   **IColumnsInfo**  
  
-   **IAccessor**  
  
-   **ICommandWithParameters**  
  
 **IAccessor** 才能建立參數存取子。 如果提供者支援 **IColumnRowset**, ，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會使用該介面，以判斷資料行是識別資料行。  
  
### Rowset 物件介面  
 以下是必要的介面：  
  
-   **IRowset**  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
 應用程式必須在訂閱資料庫中建立的複寫資料表內，開啟一個資料列集。 **IColumnsInfo** 和 **IAccessor** ，才能存取資料列集中的資料。  
  
### Error 物件介面  
 請使用以下介面來管理錯誤：  
  
-   **IErrorRecords**  
  
-   **IErrorInfo**  
  
 使用 **ISQLErrorInfo** 如果 OLE DB 提供者支援。  
  
 如需 OLE DB 提供者的詳細資訊，請參閱您 OLE DB 提供者所附的文件。  
  
## 另請參閱  
 [非 SQL Server 訂閱者](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)  
  
  