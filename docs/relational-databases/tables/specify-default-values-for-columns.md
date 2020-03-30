---
title: 指定資料行的預設值 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2020
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], defaults
- default values
ms.assetid: 64514aed-b846-407b-992e-cf813f9a1a91
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1544242905645fed5cb00fda3f7da0a06809326c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "79448487"
---
# <a name="specify-default-values-for-columns"></a>指定資料行的預設值

[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來指定將在資料表資料行中輸入的預設值。 您可以透過使用者介面的 [物件總管] 或提交 [!INCLUDE[tsql](../../includes/tsql-md.md)]，設定預設值。

如果您未將預設值指派給資料行，且使用者將資料行保留空白，則：

- 如果設定了允許 Null 值的選項，會將 NULL 插入資料行。

- 如果沒有設定允許 Null 值的選項，資料行將會保留空白，但是使用者必須在提供資料行的值之後，才能儲存資料列。

## <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項

在您開始之前，請留意下列限制和約束：

- 如果 [預設值]  欄位中的輸入內容取代繫結的預設值 (顯示為沒有括弧)，系統會提示您解除繫結預設值，並使用新的預設值加以取代。

- 若要輸入文字字串，請將此值放在單引號 (') 之中，不要使用雙引號 (")，因為它們是保留供引號識別碼使用。

- 若要輸入數字預設值，請輸入數字，但不要加上引號。

- 若要輸入物件/函數，請輸入物件/函數的名稱，但不要加上引號。

### <a name="security-permissions"></a><a name="Security"></a> 安全性權限

本文所述的動作需要資料表的 ALTER 權限。

## <a name="use-ssms-to-specify-a-default"></a><a name="SSMSProcedure"></a> 使用 SSMS 來指定預設值

您可以使用 [物件總管] 來指定資料表資料行的預設值。

### <a name="object-explorer"></a>物件總管

1. 在 [物件總管]  中，找到要變更小數位數的資料行，以滑鼠右鍵按一下包含該資料行的資料表，然後按一下 [設計]  。

2. 選取您要指定預設值的資料行。

3. 在 **[資料行屬性]** 索引標籤的 **[預設值或繫結]** 屬性中，輸入新的預設值。

   > [!NOTE]
   > 若要輸入數字預設值，請輸入數字。 若為物件或函數，請輸入其名稱。 若為英數字元預設值，請在單引號內部輸入值。

4. 在 [檔案]  功能表上，按一下 [儲存「資料表名稱」  ]  。

## <a name="use-transact-sql-to-specify-a-default"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL 來指定預設值

透過使用 SSMS 來提交 T-SQL，有許多不同的方式可用來指定資料行的預設值。

### <a name="alter-table-t-sql"></a>ALTER TABLE (T-SQL)

1. 在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。

2. 在標準列上，按一下 **[新增查詢]** 。

3. 複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。

   ```sql
   CREATE TABLE dbo.doc_exz (column_a INT, column_b INT); -- Allows nulls.
   GO
   INSERT INTO dbo.doc_exz (column_a) VALUES (7);
   GO
   ALTER TABLE dbo.doc_exz
     ADD CONSTRAINT DF_Doc_Exz_Column_B
     DEFAULT 50 FOR column_b;
   GO
   ```

<!--
The following two T-SQL code examples were offered by 'nycdotnet' (Steve) via public PR 1660, Feb 2019.
-->

### <a name="create-table-t-sql"></a>CREATE TABLE (T-SQL)

```sql
    CREATE TABLE dbo.doc_exz (
      column_a INT,
      column_b INT DEFAULT 50);
```

### <a name="named-constraint-t-sql"></a>具名 CONSTRAINT (T-SQL)

```sql
    CREATE TABLE dbo.doc_exz (
      column_a INT,
      column_b INT CONSTRAINT DF_Doc_Exz_Column_B DEFAULT 50);
```

如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。
