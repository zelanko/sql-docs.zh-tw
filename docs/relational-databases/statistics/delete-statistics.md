---
title: "刪除統計資料 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-statistics
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statistics [SQL Server], deleting
- deleting statistics
ms.assetid: eccce0aa-591e-4a1d-bd10-373b022f8749
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 51349f58a29f7a0702e719f83e5f60632fb8d7c5
ms.lasthandoff: 04/11/2017

---
# <a name="delete-statistics"></a>刪除統計資料
  您可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，從資料表或檢視中刪除 (卸除) 統計資料，透過使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目卸除資料表或檢視的統計資訊：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   當您卸除統計資料時，請小心。 執行這個動作，可能會影響查詢最佳化工具所選擇的執行計畫。  
  
-   索引的統計資料無法利用 DROP STATISTICS 來卸除。 只要索引存在，就會保留統計資料。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料表或檢視表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-drop-statistics-from-a-table-or-view"></a>若要卸除資料表或檢視的統計資訊  
  
1.  在 **[物件總管]**中，按一下加號展開要在其中刪除統計資料的資料庫。  
  
2.  按一下加號展開 **[資料表]** 資料夾。  
  
3.  按一下加號展開要在其中刪除統計資料的資料表。  
  
4.  按一下加號展開 **[統計資料]** 資料夾。  
  
5.  以滑鼠右鍵按一下您想要刪除的統計資料物件，然後選取 [刪除]。  
  
6.  在 **[刪除物件]** 對話方塊中，確定已選取正確的統計資料，然後按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-drop-statistics-from-a-table-or-view"></a>若要卸除資料表或檢視的統計資訊  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- First, create two statistics named VendorCredit and CustomerTotal  
    -- The first statistic uses a random 50% sample of information provided from the Name and CreditRating columns in the Purchasing.Vendor table.  
    CREATE STATISTICS VendorCredit  
        ON Purchasing.Vendor (Name, CreditRating)  
        WITH SAMPLE 50 PERCENT  
    -- The second statistic uses all of the information from the CustomerID and TotalDue columns in the Sales.SalesOrderHeader table  
    CREATE STATISTICS CustomerTotal  
        ON Sales.SalesOrderHeader (CustomerID, TotalDue)  
        WITH FULLSCAN;  
    GO  
    -- This next statement drops both of the statistics created above. Note that the naming convention is [table_name].[statistics_name].  
    DROP STATISTICS Purchasing.Vendor.VendorCredit, Sales.SalesOrderHeader.CustomerTotal;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)。  
  
  
