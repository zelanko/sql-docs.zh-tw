---
title: 建立資料庫主要金鑰 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5d51012d037c04ea706feb0b7092f5eca6f09564
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034106"
---
# <a name="create-a-database-master-key"></a>建立資料庫主要金鑰
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ，建立 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中的資料庫主要金鑰。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   [若要使用 Transact-SQL 建立資料庫主要金鑰](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料庫的 CONTROL 權限。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-database-master-key"></a>若要建立資料庫主要金鑰  
  
1.  選擇密碼以加密即將儲存於資料庫的主要金鑰副本。  
  
2.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
3.  在標準列上，按一下 **[新增查詢]**。  
  
4.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- Creates a database master key for the "AdventureWorks2012" database.   
    -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."  
    USE AdventureWorks2012;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)。  
  
  
