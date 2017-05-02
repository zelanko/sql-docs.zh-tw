---
title: "從資料表中刪除資料行 | Microsoft 文件"
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
- columns [SQL Server], deleting
- removing columns
- deleting columns
- dropping columns
ms.assetid: 0d8f6e4f-bc71-4fa3-8615-74249c8e072d
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 20aa31c62de21e9718f504538ae4199395a5dab0
ms.lasthandoff: 04/11/2017

---
# <a name="delete-columns-from-a-table"></a>從資料表中刪除資料行
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中刪除資料表資料行。  
  
> [!CAUTION]  
>  當您從資料表中刪除資料行時，就會從資料庫中刪除該資料行以及它所包含的所有資料。 這個動作無法恢復。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目從資料表中刪除資料行：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 您無法刪除具有 CHECK 條件約束的資料行。 您必須先刪除條件約束。  
  
 除非使用資料表設計工具，否則您無法刪除具有 PRIMARY KEY 或 FOREIGN KEY 條件約束或其他相依性的資料行。 使用 [物件總管] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]時，您必須先移除資料行的所有相依性。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-columns-by-using-object-explorer"></a>若要使用物件總管來刪除資料行  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在**物件總管**中，以滑鼠右鍵按一下您想要從中刪除資料行的資料表，然後選擇 [刪除]****。  
  
3.  在 **[刪除物件]** 對話方塊中，按一下 **[確定]**。  
  
 如果資料行包含條件約束或其他相依性， **[刪除物件]** 對話方塊將會顯示錯誤訊息。 請刪除參考的條件約束，藉以解決此錯誤。  
  
#### <a name="to-delete-columns-by-using-table-designer"></a>若要使用資料表設計工具來刪除資料行  
  
1.  在**物件總管**中，以滑鼠右鍵按一下您想要從中刪除資料行的資料表，然後選擇 [設計]****。  
  
2.  以滑鼠右鍵按一下您想要刪除的資料行，然後從捷徑功能表中選擇 [刪除資料行]****。  
  
3.  如果資料行參與關聯性 (FOREIGN KEY 或 PRIMARY KEY)，則會有訊息提示您確認是否要刪除選取的資料行及其關聯性。 選擇 [ **是**]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-columns"></a>若要刪除資料行  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE dbo.doc_exb DROP COLUMN column_b ;  
    ```  
  
 如果資料行包含條件約束或其他相依性，將會傳回錯誤訊息。 請刪除參考的條件約束，藉以解決此錯誤。  
  
 如需其他範例，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。  
  
##  <a name="FollowUp"></a>  
