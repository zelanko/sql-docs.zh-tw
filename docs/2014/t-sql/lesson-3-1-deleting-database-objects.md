---
title: 刪除資料庫物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting database objects
ms.assetid: dbb94fdf-c85b-477b-8e84-f830d259bade
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a23d307cc33e5b8e59111819b245bc9df1df67df
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63063112"
---
# <a name="deleting-database-objects"></a>刪除資料庫物件
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
 [教學課程：撰寫 Transact-SQL 陳述式](tutorial-writing-transact-sql-statements.md)  
  
## <a name="see-also"></a>另請參閱  
 [REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql)   
 [DROP USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-user-transact-sql)   
 [DROP LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-login-transact-sql)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-procedure-transact-sql)   
 [DROP VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-view-transact-sql)   
 [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql)   
 [DROP TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-table-transact-sql)   
 [DROP DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)  
  
  
