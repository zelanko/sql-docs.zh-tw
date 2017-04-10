---
title: "授與資料庫的存取權 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "資料庫存取"
ms.assetid: 686edfe2-3650-48a6-a2da-9d46fa211ad8
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 授與資料庫的存取權
Mary 現在已具有此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的存取權，但是沒有存取資料庫的權限。 必須等到您將她授權為資料庫使用者之後，她才能存取預設的 **TestData** 資料庫。  
  
若要授與 Mary 存取權，請切換到 **TestData** 資料庫，然後使用 CREATE USER 陳述式將其登入對應至名為 Mary 的使用者。  
  
### 若要在資料庫中建立使用者  
  
1.  輸入並執行下列陳述式 (以您的電腦名稱取代 `computer_name`)，為 `Mary` 授與 `TestData` 資料庫的存取權。  
  
    ```  
    USE [TestData];  
    GO  
  
    CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
    GO  
  
    ```  
  
    現在 Mary 即具有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 `TestData` 資料庫兩者的存取權。  
  
## 本課程的下一項工作  
[建立檢視和預存程序](../t-sql/creating-views-and-stored-procedures.md)  
  
  
  
