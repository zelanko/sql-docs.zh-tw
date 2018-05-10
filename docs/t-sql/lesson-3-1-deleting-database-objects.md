---
title: 刪除資料庫物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- deleting database objects
ms.assetid: dbb94fdf-c85b-477b-8e84-f830d259bade
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 379eedbd4fb8df885e98d12042679b5bf748291d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-3-1---deleting-database-objects"></a>課程 3-1 - 刪除資料庫物件
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
若要移除這個教學課程中的所有執行內容，原本只要刪除資料庫就可以了， 但是，在這個主題中，您將會逐步執行各個步驟，以反轉您在這個教學課程中所做的每一個動作。  
  
### <a name="removing-permissions-and-objects"></a>移除權限和物件  
  
1.  刪除物件之前，請先確定您是在正確的資料庫中：  
  
    ```  
    USE TestData;  
    GO  
    ```  
  
2.  使用 `REVOKE` 陳述式移除 `Mary` 對預存程序的執行權限：  
  
    ```  
    REVOKE EXECUTE ON pr_Names FROM Mary;  
    GO  
  
    ```  
  
3.  使用 `DROP` 陳述式移除 `Mary` 存取 `TestData` 資料庫的權限：  
  
    ```  
    DROP USER Mary;  
    GO  
  
    ```  
  
4.  使用 `DROP` 陳述式移除 `Mary` 存取這個 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]執行個體的權限：  
  
    ```  
    DROP LOGIN [<computer_name>\Mary];  
    GO  
  
    ```  
  
5.  使用 `DROP` 陳述式移除 `pr_Names`預存程序：  
  
    ```  
    DROP PROC pr_Names;  
    GO  
  
    ```  
  
6.  使用 `DROP` 陳述式移除 `vw_Names`檢視：  
  
    ```  
    DROP View vw_Names;  
    GO  
  
    ```  
  
7.  使用 `DELETE` 陳述式移除 `Products` 資料表中的所有資料列：  
  
    ```  
    DELETE FROM Products;  
    GO  
  
    ```  
  
8.  使用 `DROP` 陳述式移除 `Products` 資料表：  
  
    ```  
    DROP Table Products;  
    GO  
  
    ```  
  
9. 當您還在 `TestData` 資料庫中時，將無法移除這個資料庫；因此，請先將內容切換到其他資料庫，然後使用 `DROP` 陳述式移除 `TestData` 資料庫：  
  
    ```  
    USE MASTER;  
    GO  
    DROP DATABASE TestData;  
    GO  
  
    ```  
  
「撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式」教學課程到此結束。 請記住，這個教學課程只是簡短概觀，因此並不會描述陳述式的所有選項。 如果要設計和建立有效率的資料庫結構，以及設定資料的安全存取，則所需的資料庫將會比這個教學課程的所示範例更加複雜。  
  
## <a name="return-to-sql-server-tools-portal"></a>返回 SQL Server 工具入口網站  
[教學課程：撰寫國際性通用的 Transact-SQL 陳述式](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
## <a name="see-also"></a>另請參閱  
[REVOKE &#40;Transact-SQL&#41;](../t-sql/statements/revoke-transact-sql.md)  
[DROP USER &#40;Transact-SQL&#41;](../t-sql/statements/drop-user-transact-sql.md)  
[DROP LOGIN &#40;Transact-SQL&#41;](../t-sql/statements/drop-login-transact-sql.md)  
[DROP PROCEDURE &#40;Transact-SQL&#41;](../t-sql/statements/drop-procedure-transact-sql.md)  
[DROP VIEW &#40;Transact-SQL&#41;](../t-sql/statements/drop-view-transact-sql.md)  
[DELETE &#40;Transact-SQL&#41;](../t-sql/statements/delete-transact-sql.md)  
[DROP TABLE &#40;Transact-SQL&#41;](../t-sql/statements/drop-table-transact-sql.md)  
[DROP DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/drop-database-transact-sql.md)  
  
  
  
