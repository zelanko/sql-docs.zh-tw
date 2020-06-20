---
title: 修改資料行 (Database Engine) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- modifying data types
- column data types [SQL Server]
- data types [SQL Server], columns
ms.assetid: b67b95c5-61ef-4bd8-9a3e-1640eb7583ac
author: stevestein
ms.author: sstein
ms.openlocfilehash: a73c25d91b742f1cc1f7edcc8a95cdf226b2683c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067966"
---
# <a name="modify-columns-database-engine"></a>修改資料行 (Database Engine)
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中修改資料行的資料類型。  
  
> [!WARNING]  
>  修改已經包含資料之資料行的資料類型可能會在現有資料轉換為新類型時，導致資料永久喪失。 此外，依據修改資料行的程式碼和應用程式可能會失敗。 這些包含查詢、檢視、預存程序、使用者自訂函數，以及用戶端應用程式。 注意，這些失敗會串聯。 例如，呼叫相依於已修改資料行之使用者自訂函數的預存程序可能會失敗。 在對資料行進行任何變更之前，請審慎考慮。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目來修改資料行的資料類型：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料表的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>若要修改資料行的資料類型  
  
1.  在 [物件總管]  中，找到要變更小數位數的資料行，以滑鼠右鍵按一下包含該資料行的資料表，然後按一下 [設計]  。  
  
2.  選取要修改資料類型的資料行。  
  
3.  在 [資料行屬性]  索引標籤中，按一下 [資料類型]  屬性的方格資料格，並且從下拉式清單中選擇新的資料類型。  
  
4.  在 [檔案]  功能表上，按一下 [儲存「資料表名稱」]。  
  
> [!NOTE]  
>  在修改資料行的資料類型時，資料表設計工具會套用所選取資料類型的預設長度，即使您已經指定另一個資料類型也是如此。 一定要在指定資料類型之後，設定所需值的資料類型長度。  
  
> [!WARNING]  
>  如果您嘗試修改與其他資料表相關之資料行的資料類型，資料表設計工具會要求您確認也會針對其他資料表中的資料行進行此變更。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-modify-the-data-type-of-a-column"></a>若要修改資料行的資料類型  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    CREATE TABLE dbo.doc_exy (column_a INT ) ;  
    GO  
    INSERT INTO dbo.doc_exy (column_a) VALUES (10) ;  
    GO  
    ALTER TABLE dbo.doc_exy ALTER COLUMN column_a DECIMAL (5, 2) ;  
    GO  
  
    ```  
  
 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)。  
  
  
