---
title: 建立主索引鍵 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- primary keys [SQL Server], creating
ms.assetid: 85c623ca-4656-4d70-a9db-ee4d897cd214
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1ba50f7bc86377c8d49f954c813f0b2eb604ffe1
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67732232"
---
# <a name="create-primary-keys"></a>建立主索引鍵

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中定義主索引鍵。 建立主索引鍵會自動建立對應的唯一叢集索引，或若依此指定則建立非叢集索引。

## <a name="BeforeYouBegin"></a> 開始之前

### <a name="Restrictions"></a> 限制事項

- 一份資料表只能有一個 PRIMARY KEY 條件約束。

- PRIMARY KEY 條件約束內所定義的所有資料行，都必須定義成 NOT NULL。 如果未指定 Null 屬性，參與 PRIMARY KEY 條件約束的所有資料行，其 Null 屬性都會設成 NOT NULL。

### <a name="Security"></a> 安全性

#### <a name="Permissions"></a> 權限

建立具有主索引鍵的新資料表，需要資料庫中的 CREATE TABLE 權限及建立資料表的結構描述之 ALTER 權限。

在現有資料表中建立主索引鍵需要此資料表的 ALTER 權限。

## <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio

### <a name="to-create-a-primary-key"></a>若要建立主索引鍵

1. 在物件總管 中，以滑鼠右鍵按一下要加入唯一條件約束的資料表，然後按一下 [設計]  。
2. 在 **[資料表設計工具]** 中，按一下要定義為主索引鍵的資料庫資料行的資料列選取器。 若要選取多個資料行，請按住 CTRL 鍵，同時按一下其他資料行的資料列選取器。
3. 在資料行的資料列選取器中，按一下滑鼠右鍵，然後選取 [設定主索引鍵]  。

> [!CAUTION]
> 若要重新定義主索引鍵，必須在建立新的主索引鍵前，先刪除所有現有主索引鍵的關聯性。 出現訊息警告您，這個程序中會自動刪除現有的關聯性。

主索引鍵資料行是由資料列選取器中的主索引鍵符號識別。

如果主索引鍵由一個以上的資料行組成，一個資料行中允許有重複的值，但是主索引鍵中所有資料行的組合值必須是唯一的。

如果您定義了複合索引鍵，主索引鍵中的資料行順序必須符合資料表所顯示的資料行順序。 然而，您可以在建立主索引鍵之後變更資料行的順序。 如需詳細資訊，請參閱 [修改主索引鍵](../../relational-databases/tables/modify-primary-keys.md)。

## <a name="TsqlProcedure"></a> 使用 Transact-SQL

### <a name="to-create-a-primary-key-in-an-existing-table"></a>在現有的資料表建立主索引鍵

下列範例會在 AdventureWorks 資料庫的 `TransactionID` 資料行上建立主索引鍵。

```sql
ALTER TABLE Production.TransactionHistoryArchive
   ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID);
```

### <a name="to-create-a-primary-key-in-a-new-table"></a>在新的資料表建立主索引鍵

下列範例會建立一個資料表，並在 AdventureWorks 資料庫的 `TransactionID` 資料行上定義主索引鍵。

```sql
CREATE TABLE Production.TransactionHistoryArchive1
   (
      TransactionID int IDENTITY (1,1) NOT NULL
      , CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)
   )
;
```

### <a name="to-create-a-primary-key-with-nonclustered-index-in-a-new-table"></a>在新的資料表中建立具有非叢集索引的主索引鍵

下列範例會建立資料表，並在 AdventureWorks 資料庫的 `CustomerID` 資料行上定義主索引鍵，以及在 `TransactionID` 上定義叢集索引。

```sql
-- Create table to add the clustered index
CREATE TABLE Production.TransactionHistoryArchive1
   (
      CustomerID uniqueidentifier DEFAULT NEWSEQUENTIALID()
      , TransactionID int IDENTITY (1,1) NOT NULL
      , CONSTRAINT PK_TransactionHistoryArchive1_CustomerID PRIMARY KEY NONCLUSTERED (CustomerID)
   )
;

-- Now add the clustered index
CREATE CLUSTERED INDEX CIX_TransactionID ON Production.TransactionHistoryArchive1 (TransactionID);
```

## <a name="see-also"></a>另請參閱

- [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)
- [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 
- [table_constraint](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)
