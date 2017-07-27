---
title: "刪除主索引鍵 | Microsoft 文件"
ms.custom: 
ms.date: 07/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing primary keys
- deleting primary keys
- primary keys [SQL Server], deleting
ms.assetid: c472e465-7bdd-4d74-8fc9-e47fca007ccb
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1dbc3eb4968f27665df80e414a590f8b4e3df7b4
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="delete-primary-keys"></a>刪除主索引鍵
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中刪除 (卸除) 主索引鍵。 刪除主索引鍵時，系統會刪除對應的索引。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來刪除主索引鍵：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-primary-key-constraint-using-object-explorer"></a>若要使用物件總管來刪除主索引鍵條件約束  
  
1.  在 [物件總管] 中，展開包含主索引鍵的資料表，然後展開 **[索引鍵]**。  
  
2.  以滑鼠右鍵按一下索引鍵，然後選取 [刪除]。  
  
3.  在 **[刪除物件]** 對話方塊中，確認指定了正確的索引鍵，然後按一下 **[確定]**。  
  
#### <a name="to-delete-a-primary-key-constraint-using-table-designer"></a>若要使用資料表設計工具來刪除主索引鍵條件約束  
  
1.  在物件總管中，以滑鼠右鍵按一下含有主索引鍵的資料表，然後按一下 [設計]。  
  
2.  在資料表方格中，以滑鼠右鍵按一下包含主索引鍵的資料列，然後選擇 [移除主索引鍵] 關閉設定。  
  
    > [!NOTE]  
    >  若要恢復此一動作，可將資料表關閉而不儲存變更。 如果恢復刪除主索引鍵的動作，將會遺失所有對資料表進行的其他變更。  
  
3.  在 [檔案]  功能表上，按一下 [儲存] *table name*。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-primary-key-constraint"></a>若要刪除主索引鍵條件約束  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例會先識別主索引鍵條件約束的名稱，然後再刪除條件約束。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Return the name of primary key.  
    SELECT name  
    FROM sys.key_constraints  
    WHERE type = 'PK' AND OBJECT_NAME(parent_object_id) = N'TransactionHistoryArchive';  
    GO  
    -- Delete the primary key constraint.  
    ALTER TABLE Production.TransactionHistoryArchive  
    DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID;   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) 和 [sys.key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)  
  
###  <a name="TsqlExample"></a>  
