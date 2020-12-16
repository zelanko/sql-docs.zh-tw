---
description: 檢視定序資訊
title: 檢視定序資訊 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], view
ms.assetid: 1338b4ea-7142-44bc-a3b9-44e54431405f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 02cd93e23233d62ee28327e90742593cf6f0bf07
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460561"
---
# <a name="view-collation-information"></a>檢視定序資訊
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
    
<a name="Top"></a> 您可以使用 [物件總管] 功能表選項或使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視伺服器、資料庫或資料行的定序。  
  
##  <a name="how-to-view-a-collation-setting"></a><a name="Procedures"></a> 如何檢視定序設定  
 您可以使用下列其中一項：  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **在 [物件總管] 中檢視伺服器 (SQL Server 執行個體) 的定序設定**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在執行個體上按一下滑鼠右鍵，然後選取 [屬性]。  
  
 **在 [物件總管] 中檢視資料庫的定序設定**  
  
1.  在物件總管中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 [資料庫] ，然後在資料庫上按一下滑鼠右鍵，再選取 [屬性]。  
  
 **在 [物件總管] 中檢視資料行的定序設定**  
  
1.  在物件總管中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  依序展開 **[資料庫]**、特定資料庫及 **[資料表]**。  
  
3.  展開包含資料行的資料表，然後展開 **[資料行]**。  
  
4.  在資料行上按一下滑鼠右鍵，然後選取 [屬性]。 如果定序屬性為空白，則資料行不是字元資料類型。  
  
###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **檢視伺服器的定序設定**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後在工具列上按一下 **[新增查詢]**。  
  
2.  在查詢視窗中，輸入下列使用 SERVERPROPERTY 系統函數的陳述式。  
  
    ```sql  
    SELECT CONVERT (varchar(256), SERVERPROPERTY('collation'));  
    ```  
  
3.  或者，您可以使用 sp_helpsort 系統預存程序。  
  
    ```sql  
    EXECUTE sp_helpsort;  
    ```  
  
 **檢視 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後在工具列上按一下 **[新增查詢]**。  
  
2.  在查詢視窗中，輸入下列使用 SERVERPROPERTY 系統函數的陳述式。  
  
    ```sql  
    SELECT name, description FROM sys.fn_helpcollations();  
    ```  
  
 **檢視資料庫的定序設定**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後在工具列上按一下 **[新增查詢]**。  
  
2.  在查詢視窗中，輸入下列使用 sys.databases 系統目錄檢視的陳述式。  
  
    ```sql  
    SELECT name, collation_name FROM sys.databases;  
    ```  
  
3.  或者，您可以使用 DATABASEPROPERTYEX 系統函數。  
  
    ```sql  
    SELECT CONVERT (varchar(256), DATABASEPROPERTYEX('database_name','collation'));  
    ```  
  
 **檢視資料行的定序設定**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後在工具列上按一下 **[新增查詢]**。  
  
2.  在查詢視窗中，輸入下列使用 sys.columns 系統目錄檢視的陳述式。  
  
    ```sql  
    SELECT name, collation_name FROM sys.columns WHERE name = N'<insert character data type column name>';  
    ```  
  
 **檢視資料表與資料行的定序設定**  

1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後在工具列上按一下 **[新增查詢]**。  
  
2.  在查詢視窗中，輸入下列使用 sys.columns 系統目錄檢視的陳述式。  
  
    ```sql  
    SELECT t.name TableName, c.name ColumnName, collation_name  
    FROM sys.columns c  
    inner join sys.tables t on c.object_id = t.object_id;  
    ```  



## <a name="see-also"></a>另請參閱  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [定序優先順序 &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)      
 [sp_helpsort &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsort-transact-sql.md)  
  
  
