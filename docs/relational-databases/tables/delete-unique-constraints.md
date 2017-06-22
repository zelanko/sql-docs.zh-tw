---
title: "刪除唯一的條件約束 | Microsoft 文件"
ms.custom: 
ms.date: 10/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing constraints
- UNIQUE constraints [SQL Server], deleting
- constraints [SQL Server], deleting
- deleting constraints
- constraints [SQL Server], unique
ms.assetid: 71e563fc-f5d7-4c2e-a42f-f0695a831f32
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 49169c8ac7e47e6b9d9efff891810c68372aa6c5
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="delete-unique-constraints"></a>刪除唯一的條件約束
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中刪除唯一條件約束。 刪除唯一條件約束會移除條件約束運算式所包含之資料行或資料行組合中輸入值的唯一性要求，並且刪除對應的唯一索引。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來刪除唯一條件約束：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-unique-constraint-using-object-explorer"></a>若要使用物件總管來刪除唯一條件約束  
  
1.  在 [物件總管] 中，展開包含唯一條件約束的資料表，然後展開 **[條件約束]**。  
  
2.  以滑鼠右鍵按一下索引鍵，然後選取 [刪除]。  
  
3.  在 **[刪除物件]** 對話方塊中，確認指定了正確的索引鍵，然後按一下 **[確定]**。  
  
#### <a name="to-delete-a-unique-constraint-using-table-designer"></a>若要使用資料表設計工具來刪除唯一條件約束  
  
1.  在物件總管中，以滑鼠右鍵按一下含有唯一條件約束的資料表，然後按一下 [設計]。  
  
2.  在 [資料表設計工具] 功能表中，按一下 [索引/索引鍵]。  
  
3.  在 [索引/索引鍵] 對話方塊中，從 [選取的主/唯一索引鍵和索引] 清單中選取唯一索引鍵。  
  
4.  按一下 **[刪除]**。  
  
5.  在 [檔案]  功能表上，按一下 [儲存]  *table name*。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-unique-constraint"></a>若要刪除唯一條件約束  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- Return the name of unique constraint.  
    SELECT name  
    FROM sys.objects  
    WHERE type = 'UQ' AND OBJECT_NAME(parent_object_id) = N' DocExc';  
    GO  
    -- Delete the unique constraint.  
    ALTER TABLE dbo.DocExc   
    DROP CONSTRAINT UNQ_ColumnB_DocExc;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) 和 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。  
  
###  <a name="TsqlExample"></a>  

