---
title: "修改資料行 (Database Engine) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying data types
- column data types [SQL Server]
- data types [SQL Server], columns
ms.assetid: b67b95c5-61ef-4bd8-9a3e-1640eb7583ac
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 736b83dffa241040cf08e7f7d9410eaab80649af
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="modify-columns-database-engine"></a>修改資料行 (Database Engine)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中修改資料行的資料類型。  
  
> [!WARNING]  
>  修改已經包含資料之資料行的資料類型可能會在現有資料轉換為新類型時，導致資料永久喪失。 此外，依據修改資料行的程式碼和應用程式可能會失敗。 這些包含查詢、檢視、預存程序、使用者自訂函數，以及用戶端應用程式。 注意，這些失敗會串聯。 例如，呼叫相依於已修改資料行之使用者自訂函數的預存程序可能會失敗。 在對資料行進行任何變更之前，請審慎考慮。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來修改資料行的資料類型：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>若要修改資料行的資料類型  
  
1.  在 [物件總管] 中，找到要變更小數位數的資料行，以滑鼠右鍵按一下包含該資料行的資料表，然後按一下 [設計]。  
  
2.  選取要修改資料類型的資料行。  
  
3.  在 [資料行屬性] 索引標籤中，按一下 [資料類型] 屬性的方格資料格，並且從下拉式清單中選擇新的資料類型。  
  
4.  在 [檔案]  功能表上，按一下 [儲存] *table name*。  
  
> [!NOTE]  
>  在修改資料行的資料類型時，資料表設計工具會套用所選取資料類型的預設長度，即使您已經指定另一個資料類型也是如此。 一定要在指定資料類型之後，設定所需值的資料類型長度。  
  
> [!WARNING]  
>  如果您嘗試修改與其他資料表相關之資料行的資料類型，資料表設計工具會要求您確認也會針對其他資料表中的資料行進行此變更。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>若要修改資料行的資料類型  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    CREATE TABLE dbo.doc_exy (column_a INT ) ;  
    GO  
    INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
    GO  
    ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;  
    GO  
  
    ```  
  
 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。  
  
  

