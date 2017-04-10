---
title: "設定 Oracle 發行者的交易集作業 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_publisherproperty"
  - "Oracle 發行 [SQL Server 複寫], 設定"
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 設定 Oracle 發行者的交易集作業 (複寫 Transact-SQL 程式設計)
   **Xactset** 工作是由 Oracle 發行者建立交易集，「 記錄讀取器代理程式未連線到發行者時所執行的複寫建立的 Oracle 資料庫作業。 您可以使用複寫預存程序，以程式設計的方式從「散發者」啟用和設定此作業。 如需詳細資訊，請參閱 [效能微調 Oracle 發行者](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)。  
  
### 若要啟用交易集作業  
  
1.  在 Oracle 發行者上，設定 **job_queue_processes** 足夠的值，以允許 Xactset 作業執行的初始化參數。 如需有關此參數的詳細資訊，請參閱「Oracle 發行者」的資料庫文件。  
  
2.  在散發者 」 執行 [sp_publisherproperty & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 指定 Oracle 發行者的名稱 **@publisher**, ，值為 **xactsetbatching** 的 **@propertyname**, ，而值為 **啟用** 的 **@propertyvalue**。  
  
3.  在散發者 」 執行 [sp_publisherproperty & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 指定的 Oracle 簽發者名稱 **@publisher**, ，值為 **xactsetjobinterval** 的 **@propertyname**, ，和工作的間隔，以分鐘為單位的 **@propertyvalue**。  
  
4.  在散發者 」 執行 [sp_publisherproperty & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 指定 Oracle 發行者的名稱 **@publisher**, ，值為 **xactsetjob** 的 **@propertyname**, ，而值為 **啟用** 的 **@propertyvalue**。  
  
### 若要設定交易集作業  
  
1.  （選擇性）在散發者 」 執行 [sp_publisherproperty & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 針對 **@publisher**指定 Oracle 發行者的名稱。 這樣會傳回屬性的 **Xactset** 在 「 發行者 」 的工作。  
  
2.  在散發者 」 執行 [sp_publisherproperty & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 指定 Oracle 發行者的名稱 **@publisher**, ，正在設定之 Xactset 作業屬性名稱 **@propertyname**, ，與新設定 **@propertyvalue**。  
  
3.  (選擇性) 針對每個要設定的 Xactset 作業屬性重複步驟 2。 當變更 **xactsetjobinterval** 屬性，您必須重新啟動新的間隔才會生效 「 Oracle 發行者 」 上的作業。  
  
### 若要檢視交易集作業的屬性  
  
1.  在散發者 」 執行 [sp_helpxactsetjob](../../../relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql.md)。 針對 **@publisher**指定 Oracle 發行者的名稱。  
  
### 若要停用交易集作業  
  
1.  在散發者 」 執行 [sp_publisherproperty & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 指定的 Oracle 簽發者名稱 **@publisher**, ，值為 **xactsetjob** 的 **@propertyname**, ，且值為 **已停用** 的 **@propertyvalue**。  
  
## 範例  
 下列範例會啟用 `Xactset` 作業，並在執行之間設定三分鐘的間隔。  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../relational-databases/replication/codesnippet/tsql/configure-the-transactio_1.sql)]  
  
## 另請參閱  
 [Oracle 發行者的效能微調](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)   
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  