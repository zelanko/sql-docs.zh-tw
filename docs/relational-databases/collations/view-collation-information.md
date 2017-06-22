---
title: "檢視定序資訊 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collations [SQL Server], view
ms.assetid: 1338b4ea-7142-44bc-a3b9-44e54431405f
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: eebc43acb7df6cf2d63dbc6d8e0d1c4f25fa9476
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="view-collation-information"></a>檢視定序資訊
    
##  <a name="Top"></a> 您可以使用 [物件總管] 功能表選項或使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視伺服器、資料庫或資料行的定序。  
  
##  <a name="Procedures"></a> 如何檢視定序設定  
 您可以使用下列其中一項：  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **在 [物件總管] 中檢視伺服器 (SQL Server 執行個體) 的定序設定**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在執行個體上按一下滑鼠右鍵，然後選取 [屬性]。  
  
 **在 [物件總管] 中檢視資料庫的定序設定**  
  
1.  在物件總管中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 [資料庫] ，然後在資料庫上按一下滑鼠右鍵，再選取 [屬性]。  
  
 **在 [物件總管] 中檢視資料行的定序設定**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  依序展開 **[資料庫]**、特定資料庫及 **[資料表]**。  
  
3.  展開包含資料行的資料表，然後展開 **[資料行]**。  
  
4.  在資料行上按一下滑鼠右鍵，然後選取 [屬性]。 如果定序屬性為空白，則資料行不是字元資料類型。  
  
###  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **檢視伺服器的定序設定**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後在工具列上按一下 **[新增查詢]**。  
  
2.  在查詢視窗中，輸入下列使用 SERVERPROPERTY 系統函數的陳述式。  
  
    ```  
    SELECT CONVERT (varchar, SERVERPROPERTY('collation'));  
    ```  
  
3.  或者，您可以使用 sp_helpsort 系統預存程序。  
  
    ```  
    EXECUTE sp_helpsort;  
    ```  
  
 **檢視 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後在工具列上按一下 **[新增查詢]**。  
  
2.  在查詢視窗中，輸入下列使用 SERVERPROPERTY 系統函數的陳述式。  
  
    ```  
    SELECT name, description FROM sys.fn_helpcollations();  
    ```  
  
 **檢視資料庫的定序設定**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後在工具列上按一下 **[新增查詢]**。  
  
2.  在查詢視窗中，輸入下列使用 sys.databases 系統目錄檢視的陳述式。  
  
    ```  
    SELECT name, collation_name FROM sys.databases;  
    ```  
  
3.  或者，您可以使用 DATABASEPROPERTYEX 系統函數。  
  
    ```  
    SELECT CONVERT (varchar, DATABASEPROPERTYEX('database_name','collation'));  
    ```  
  
 **檢視資料行的定序設定**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後在工具列上按一下 **[新增查詢]**。  
  
2.  在查詢視窗中，輸入下列使用 sys.columns 系統目錄檢視的陳述式。  
  
    ```  
    SELECT name, collation_name FROM sys.columns WHERE name = N'<insert character data type column name>';  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [定序優先順序 &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [sp_helpsort &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsort-transact-sql.md)  
  
  
