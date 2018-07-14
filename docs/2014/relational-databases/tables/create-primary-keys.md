---
title: 建立主索引鍵 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- primary keys [SQL Server], creating
ms.assetid: 85c623ca-4656-4d70-a9db-ee4d897cd214
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9d4ba48188473aaa5286e8121bcbfcd3a9b50101
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177675"
---
# <a name="create-primary-keys"></a>建立主索引鍵
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中定義主索引鍵。 建立主索引鍵會自動建立對應的唯一叢集或非叢集索引。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **使用下列方法建立主索引鍵：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   一份資料表只能有一個 PRIMARY KEY 條件約束。  
  
-   PRIMARY KEY 條件約束內所定義的所有資料行，都必須定義成 NOT NULL。 如果未指定 Null 屬性，參與 PRIMARY KEY 條件約束的所有資料行，其 Null 屬性都會設成 NOT NULL。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 建立具有主索引鍵的新資料表，需要資料庫中的 CREATE TABLE 權限及建立資料表的結構描述之 ALTER 權限。  
  
 在現有資料表中建立主索引鍵需要此資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-primary-key"></a>若要建立主索引鍵  
  
1.  在物件總管 中，以滑鼠右鍵按一下要加入唯一條件約束的資料表，然後按一下 [設計]。  
  
2.  在 **[資料表設計工具]** 中，按一下要定義為主索引鍵的資料庫資料行的資料列選取器。 若要選取多個資料行，請按住 CTRL 鍵，同時按一下其他資料行的資料列選取器。  
  
3.  在資料行的資料列選取器中，按一下滑鼠右鍵，然後選取 [設定主索引鍵]。  
  
> [!CAUTION]  
>  若要重新定義主索引鍵，必須在建立新的主索引鍵前，先刪除所有現有主索引鍵的關聯性。 出現訊息警告您，這個程序中會自動刪除現有的關聯性。  
  
 主索引鍵資料行是由資料列選取器中的主索引鍵符號識別。  
  
 如果主索引鍵由一個以上的資料行組成，一個資料行中允許有重複的值，但是主索引鍵中所有資料行的組合值必須是唯一的。  
  
 如果您定義了複合索引鍵，主索引鍵中的資料行順序必須符合資料表所顯示的資料行順序。 然而，您可以在建立主索引鍵之後變更資料行的順序。 如需詳細資訊，請參閱 [修改主索引鍵](modify-primary-keys.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-primary-key-in-an-existing-table"></a>在現有的資料表建立主索引鍵  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例會在 `TransactionID`資料行上建立主索引鍵。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Production.TransactionHistoryArchive   
    ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID);  
    GO  
  
    ```  
  
#### <a name="to-create-a-primary-key-in-a-new-table"></a>在新的資料表建立主索引鍵  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例會建立資料表並在 `TransactionID` 資料行上定義主索引鍵。  
  
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
  
     如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)、[CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) 和 [table_constraint &#40;Transact-SQL&#41;](/sql/relational-databases/system-information-schema-views/table-constraints-transact-sql)。  
  
###  <a name="TsqlExample"></a>  
