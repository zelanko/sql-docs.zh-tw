---
title: T-SQL 教學課程：刪除資料庫物件 | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting database objects
ms.assetid: ecf26dd5-4535-4ed6-86fc-c73f9d9dedec
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2b155862bd9983bc8b93b6088bfa6d5df254ffe7
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2019
ms.locfileid: "67579388"
---
# <a name="lesson-3-delete-database-objects"></a>第 3 課：刪除資料庫物件
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
在這個簡短的課程中，會移除您在第 1 課和第 2 課中所建立的物件，然後卸除資料庫。  
  
刪除物件之前，請先確定您是在正確的資料庫中：
  
  ```sql  
  USE TestData;  
  GO  
  ```  

## <a name="revoke-stored-procedure-permissions"></a>撤銷預存程序權限
  
使用 `REVOKE` 陳述式移除 `Mary` 對預存程序的執行權限：
  
  ```sql  
  REVOKE EXECUTE ON pr_Names FROM Mary;  
  GO  
  ```  
  
## <a name="drop-permissions"></a>卸除權限

1. 使用 `DROP` 陳述式移除 `Mary` 存取 `TestData` 資料庫的權限：
  
   ```sql  
   DROP USER Mary;  
   GO  
   ```  


2. 使用 `DROP` 陳述式移除 `Mary` 存取這個 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]執行個體的權限：
  
   ```sql  
   DROP LOGIN [<computer_name>\Mary];  
   GO   
   ```  
  
3. 使用 `DROP` 陳述式移除 `pr_Names`預存程序：  
  
   ```sql  
   DROP PROC pr_Names;  
   GO   
   ```  
  
4. 使用 `DROP` 陳述式移除 `vw_Names`檢視：  
  
   ```sql  
   DROP VIEW vw_Names;  
   GO  
   ```  

## <a name="delete-table"></a>刪除資料表
  
1. 使用 `DELETE` 陳述式移除 `Products` 資料表中的所有資料列：  
  
    ```sql  
    DELETE FROM Products;  
    GO  
    ```  
  
2.  使用 `DROP` 陳述式移除 `Products` 資料表：  
  
    ```sql  
    DROP TABLE Products;  
    GO    
    ```  

## <a name="remove-database"></a>移除資料庫
  
當您還在 `TestData` 資料庫中時，將無法移除這個資料庫；因此，請先將內容切換到其他資料庫，然後使用 `DROP` 陳述式移除 `TestData` 資料庫：  
  
  ```sql  
  USE MASTER;  
  GO  
  DROP DATABASE TestData;  
  GO   
  ```  
  
「撰寫 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式」教學課程到此結束。 請記住，這個教學課程只是簡短概觀，因此並不會描述陳述式的所有選項。 如果要設計和建立有效率的資料庫結構，以及設定資料的安全存取，則所需的資料庫將會比這個教學課程的所示範例更加複雜。  

  
  
