---
title: 資料庫識別碼 | Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- regular identifiers [SQL Server]
- identifiers [SQL Server]
- names [SQL Server], identifiers
- identifiers [SQL Server], about identifiers
- SQL Server identifiers
- Transact-SQL identifiers
- database objects [SQL Server], names
ms.assetid: 171291bb-f57f-4ad1-8cea-0b092d5d150c
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fbedcb09ba05ff427fbae722a9223d902f2c438d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71271965"
---
# <a name="database-identifiers"></a>資料庫識別碼

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  資料庫物件名稱又稱為識別碼。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的每一個物件都具有識別碼。 伺服器、資料庫與資料庫物件 (如資料表、檢視、資料行、索引、觸發程序、程序、條件約束、規則) 都可以有識別碼。 大多數物件都需要識別碼，但對部分物件如條件約束，則是選擇性的需求。

 定義物件時會建立物件識別碼。 之後就可以使用識別碼來參考物件。 例如，以下陳述式會建立具有識別碼 `TableX`的資料表，以及具有識別碼 `KeyCol` 與 `Description`的兩個資料行：

```sql
CREATE TABLE TableX
(KeyCol INT PRIMARY KEY, Description nvarchar(80))
```

 這個資料表也有一個未命名的條件約束。 `PRIMARY KEY` 條件約束沒有識別碼。

 識別碼的定序會隨定義的層級而不同。 執行個體層級物件 (如登入和資料庫名稱) 的識別碼會被指派執行個體的預設定序。 而資料庫中物件 (如資料表、檢視和資料行名稱) 的識別碼，則會被指派資料庫的預設定序。 例如，在區分大小寫定序的資料庫中，您可以建立名稱相同但大小寫不同的兩個資料表，但在不區分大小寫定序的資料庫中，就不可以建立名稱相同但大小寫不同的兩個資料表。

> [!NOTE]  
> 變數名稱或函數和預存程序的參數，必須符合 [!INCLUDE[tsql](../../includes/tsql-md.md)] 識別碼的規則。

## <a name="classes-of-identifiers"></a>識別碼的分類

 識別碼分為兩類：

 一般識別碼符合識別碼格式的規則。 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中使用一般識別碼時不以符號分隔。

```sql
SELECT *
FROM TableX
WHERE KeyCol = 124
```

 分隔識別碼則會括在雙引號 (") 或中括號 ([]) 中。 符合識別碼格式規則的識別碼不一定要以符號分隔。 例如：

```sql
SELECT *
FROM [TableX]         --Delimiter is optional.
WHERE [KeyCol] = 124  --Delimiter is optional.
```

 不符合所有識別碼規則的識別碼在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中一定要以符號分隔。 例如：

```sql
SELECT *
FROM [My Table]      --Identifier contains a space and uses a reserved keyword.
WHERE [order] = 10   --Identifier is a reserved keyword.
```

 一般識別碼與分隔識別碼都必須包含在 1 到 128 個字元之間。 至於本機暫存資料表，識別碼最多可有 116 個字元。

## <a name="rules-for-regular-identifiers"></a>一般識別碼的規則
 變數、函數及預存程序的名稱必須符合下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 識別碼規則。

1.  第一個字元必須是以下任一項：

    -   Unicode Standard 3.2 所定義的字母。 Unicode 的字母定義包括從 a 到 z 以及從 A 到 Z 的拉丁字元，還有其他語系中的字母字元。

    -   底線 (_)、@ 符號或數字符號 (#)。

         識別碼開頭的某些符號在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中有特殊意義。 以 @ 符號開頭的一般識別碼代表本機變數或參數，而且不能做為任何其他類型之物件的名稱。 開頭為 # 符號的識別碼代表暫存資料表或程序。 開頭為兩個 ## 符號的識別碼代表全域暫存物件。 雖然 # 符號或兩個 ## 符號字元可做為其他類型之物件的名稱開頭，但是不建議此用法。

         部分 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能的名稱會以兩個 @@ 符號為開頭。 為了避免與這些功能產生混淆，不應該使用以 @@ 為開頭的名稱。

2.  可包含的後續字元如下：

    -   Unicode Standard 3.2 所定義的字母。

    -   其他基本拉丁文或其他國家 (地區) 字集中的十進位數字。

    -   @ 符號、錢幣符號 ($)、數字符號或底線。

3.  識別碼不得為 [!INCLUDE[tsql](../../includes/tsql-md.md)] 保留字。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會保留大小寫版本的保留字。 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中使用識別碼時，如果識別碼與上述規則不符，您必須使用雙引號 ("") 或方括號 ([]) 加以分隔。 保留字取決於資料庫相容性層級。 這個層級可以使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 陳述式加以設定。

4.  不允許內嵌的空格或特殊字元。

5.  不允許補充字元。

 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中使用識別碼時，如果識別碼與上述規則不符，您必須使用雙引號 ("") 或方括號 ([]) 加以分隔。

> [!NOTE]
> 某些有關於一般識別碼格式的規則，取決於資料庫的相容性層級。 您可以使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)來設定這個層級。

## <a name="see-also"></a>另請參閱

- [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
- [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
- [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
- [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
- [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
- [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
- [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
- [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
- [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
- [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
- [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
- [保留關鍵字 &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
- [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
- [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
