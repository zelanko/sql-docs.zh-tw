---
title: 刪除邊緣條件約束 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- removing edge constraint
- deleting edge constraint, deleting connection constraint
- SQL Graph
- graph edge constraints
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3761d9e8507eb7051fe7a6cc39b83abfa091566d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774678"
---
# <a name="delete-edge-constraints"></a>刪除邊緣條件約束
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] 中刪除 (卸除) 邊緣條件約束。 
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目來刪除主索引鍵：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料表的 ALTER 權限。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-an-edge-constraint"></a>刪除邊緣條件約束
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例會先識別邊緣條件約束的名稱，然後刪除條件約束。  
  
    ```sql
    USE TEMPDB
    GO
    -- CREATE node and edge tables
    CREATE TABLE Customer
    (
        ID INTEGER PRIMARY KEY, 
        CustomerName VARCHAR(100)
    )
    AS NODE
    GO

    CREATE TABLE Product 
    (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
    ) AS NODE
    GO

    CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
    AS EDGE
    GO
    
    -- Return the name of edge constraint.
    SELECT name  
    FROM sys.edge_constraints  
    WHERE type = 'EC' AND parent_object_id = OBJECT_ID('bought');  
    GO  

    -- Delete the primary key constraint.  
    ALTER TABLE bought
    DROP CONSTRAINT EC_BOUGHT
    GO
    ```  
  
 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)、[sys.edge_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-edge-constraints-transact-sql.md) 和 [ssys.edge_constraint_clauses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-edge-constraint-clauses-transact-sql.md)
  
###  <a name="TsqlExample"></a>  
