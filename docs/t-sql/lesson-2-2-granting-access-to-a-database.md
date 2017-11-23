---
title: "授與存取權的資料庫 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords: database access
ms.assetid: 686edfe2-3650-48a6-a2da-9d46fa211ad8
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 50badd521bde0d30021f7097040beb8492cb1d2e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="lesson-2-2---granting-access-to-a-database"></a>課程 2-2-授與資料庫的存取權
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]Mary 現在已具有存取權的這個執行個體[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，但是沒有存取資料庫的權限。 必須等到您將她授權為資料庫使用者之後，她才能存取預設的 **TestData** 資料庫。  
  
若要授與 Mary 存取權，請切換到 **TestData** 資料庫，然後使用 CREATE USER 陳述式將其登入對應至名為 Mary 的使用者。  
  
### <a name="to-create-a-user-in-a-database"></a>若要在資料庫中建立使用者  
  
1.  輸入並執行下列陳述式 (以您的電腦名稱取代 `computer_name` )，為 `Mary` 授與 `TestData` 資料庫的存取權。  
  
    ```  
    USE [TestData];  
    GO  
  
    CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
    GO  
  
    ```  
  
    現在 Mary 即具有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 `TestData` 資料庫兩者的存取權。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[建立檢視和預存程序](../t-sql/lesson-2-3-creating-views-and-stored-procedures.md)  
  
  
  
