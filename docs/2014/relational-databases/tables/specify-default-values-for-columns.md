---
title: 指定資料行的預設值 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], defaults
- default values
ms.assetid: 64514aed-b846-407b-992e-cf813f9a1a91
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8a02385a6cd12b85be1661c738488c000f810510
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68196719"
---
# <a name="specify-default-values-for-columns"></a>指定資料行的預設值
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中指定將在資料行中輸入的預設值。 如果您沒有指派預設值，而且使用者將資料行保留空白，則：  
  
-   如果設定了允許 Null 值的選項，會將 NULL 插入資料行。  
  
-   如果沒有設定允許 Null 值的選項，資料行將會保留空白，但是使用者必須在提供資料行的值之後，才能儲存資料列。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要指定預設值，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果 [預設值]**** 欄位中的輸入內容取代繫結的預設值 (顯示為沒有括弧)，系統會提示您解除繫結預設值，並使用新的預設值加以取代。  
  
-   若要輸入文字字串，請將此值放在單引號 (') 之中，不要使用雙引號 (")，因為它們是保留供引號識別碼使用。  
  
-   若要輸入數字預設值，請輸入數字，但不要加上引號。  
  
-   若要輸入物件/函數，請輸入物件/函數的名稱，但不要加上引號。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>若要指定資料行的預設值  
  
1.  在 [物件總管]  中，找到要變更小數位數的資料行，以滑鼠右鍵按一下包含該資料行的資料表，然後按一下 [設計]  。  
  
2.  選取您要指定預設值的資料行。  
  
3.  在 **[資料行屬性]** 索引標籤的 **[預設值或繫結]** 屬性中，輸入新的預設值。  
  
    > [!NOTE]  
    >  若要輸入數字預設值，請輸入數字。 若為物件或函數，請輸入其名稱。 若為英數字元預設值，請在單引號內部輸入值。  
  
4.  在 [檔案]  功能表上，按一下 [儲存 <資料表名稱>]   。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>若要指定資料行的預設值  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    CREATE TABLE dbo.doc_exz ( column_a INT, column_b INT) ;  
    GO  
    INSERT INTO dbo.doc_exz (column_a)VALUES ( 7 ) ;  
    GO  
    ALTER TABLE dbo.doc_exz  
    ADD CONSTRAINT col_b_def  
    DEFAULT 50 FOR column_b ;  
    GO  
  
    ```  
  
 如需詳細資訊，請參閱[ALTER TABLE &#40;transact-sql&#41;](/sql/t-sql/statements/alter-table-transact-sql)。  
  
###  <a name="TsqlExample"></a>  
