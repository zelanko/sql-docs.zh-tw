---
title: "建立主索引鍵 | Microsoft Docs"
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
- primary keys [SQL Server], creating
ms.assetid: 85c623ca-4656-4d70-a9db-ee4d897cd214
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f799919f1b0cd1006c144eeb9afbc1d69322423b
ms.lasthandoff: 04/11/2017

---
# <a name="create-primary-keys"></a>建立主索引鍵
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中定義主索引鍵。 建立主索引鍵會自動建立對應的唯一叢集或非叢集索引。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法建立主索引鍵：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   一份資料表只能有一個 PRIMARY KEY 條件約束。  
  
-   PRIMARY KEY 條件約束內所定義的所有資料行，都必須定義成 NOT NULL。 如果未指定 Null 屬性，參與 PRIMARY KEY 條件約束的所有資料行，其 Null 屬性都會設成 NOT NULL。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 建立具有主索引鍵的新資料表，需要資料庫中的 CREATE TABLE 權限及建立資料表的結構描述之 ALTER 權限。  
  
 在現有資料表中建立主索引鍵需要此資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-primary-key"></a>若要建立主索引鍵  
  
1.  在物件總管 中，以滑鼠右鍵按一下要加入唯一條件約束的資料表，然後按一下 [設計]****。  
  
2.  在 **[資料表設計工具]**中，按一下要定義為主索引鍵的資料庫資料行的資料列選取器。 若要選取多個資料行，請按住 CTRL 鍵，同時按一下其他資料行的資料列選取器。  
  
3.  在資料行的資料列選取器中，按一下滑鼠右鍵，然後選取 [設定主索引鍵]****。  
  
> [!CAUTION]  
>  若要重新定義主索引鍵，必須在建立新的主索引鍵前，先刪除所有現有主索引鍵的關聯性。 出現訊息警告您，這個程序中會自動刪除現有的關聯性。  
  
 主索引鍵資料行是由資料列選取器中的主索引鍵符號識別。  
  
 如果主索引鍵由一個以上的資料行組成，一個資料行中允許有重複的值，但是主索引鍵中所有資料行的組合值必須是唯一的。  
  
 如果您定義了複合索引鍵，主索引鍵中的資料行順序必須符合資料表所顯示的資料行順序。 然而，您可以在建立主索引鍵之後變更資料行的順序。 如需詳細資訊，請參閱 [修改主索引鍵](../../relational-databases/tables/modify-primary-keys.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-primary-key-in-an-existing-table"></a>在現有的資料表建立主索引鍵  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例會在 `TransactionID`資料行上建立主索引鍵。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Production.TransactionHistoryArchive   
    ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID);  
    GO  
  
    ```  
  
#### <a name="to-create-a-primary-key-in-a-new-table"></a>在新的資料表建立主索引鍵  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例會建立資料表並在 `TransactionID` 資料行上定義主索引鍵。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive1  
    (  
       TransactionID int NOT NULL,  
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)  
    );  
    GO  
  
    ```  
  
     如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)、[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 和 [table_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)。  
  
###  <a name="TsqlExample"></a>  
