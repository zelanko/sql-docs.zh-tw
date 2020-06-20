---
title: 刪除索引 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- deleting indexes
- dropping indexes
- indexes [SQL Server], dropping
- index deletions [SQL Server]
ms.assetid: fd38a0ed-26c4-4c76-9ef7-e0a16147329d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4552ba701782e5790f95f54c0c1c66f82573f1e3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025621"
---
# <a name="delete-an-index"></a>刪除索引
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中刪除 (卸除) 索引。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法刪除索引：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 使用此方法無法刪除以 PRIMARY KEY 或 UNIQUE 條件約束之結果所建立的索引。 而是必須刪除條件約束。 若要移除條件約束和對應的索引，請搭配 [中的 DROP CONSTRAINT 子句來使用](/sql/t-sql/statements/alter-table-transact-sql) ALTER TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)]。 如需詳細資訊，請參閱 [Delete Primary Keys](../tables/delete-primary-keys.md)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料表或檢視表的 ALTER 權限。 依預設，這個權限會授與 **系統管理員** 固定伺服器角色以及 **db_ddladmin** 和 **db_owner** 固定資料庫角色。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-an-index-by-using-object-explorer"></a>若要使用物件總管刪除索引  
  
1.  在 [物件總管] 中，展開包含您要刪除索引之資料表的資料庫。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  展開包含您要刪除之索引的資料表。  
  
4.  展開 **[索引]** 資料夾。  
  
5.  以滑鼠右鍵按一下您想刪除的索引，然後選取 [刪除]  。  
  
6.  在 **[刪除物件]** 對話方塊中，確認 **[要刪除的物件]** 方格中有正確索引，然後按一下 **[確定]** 。  
  
#### <a name="to-delete-an-index-using-table-designer"></a>使用資料表設計工具刪除索引  
  
1.  在 [物件總管] 中，展開包含您要刪除索引之資料表的資料庫。  
  
2.  展開 **[資料表]** 資料夾。  
  
3.  以滑鼠右鍵按一下包含您要刪除索引的資料表，然後按一下 [設計]。  
  
4.  在 [資料表設計工具]  功能表上，按一下 [索引/索引鍵]  。  
  
5.  在 [索引/索引鍵]  對話方塊中，選取要刪除的索引。  
  
6.  按一下 **[刪除]** 。  
  
7.  按一下 [關閉]  。  
  
8.  在 [檔案] 功能表上，選取 [儲存 _table_name_]。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-an-index"></a>若要刪除索引  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- delete the IX_ProductVendor_BusinessEntityID index  
    -- from the Purchasing.ProductVendor table  
    DROP INDEX IX_ProductVendor_BusinessEntityID   
        ON Purchasing.ProductVendor;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)。  
  
  
