---
description: SCOPE_IDENTITY (Transact-SQL)
title: SCOPE_IDENTITY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SCOPE_IDENTITY
- SCOPE_IDENTITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identity columns [SQL Server], SCOPE_IDENTITY function
- SCOPE_IDENTITY function
- last-inserted identity values
- identity values [SQL Server], last-inserted
ms.assetid: eef24670-059b-4f10-91d4-a67bc1ed12ab
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: db39f526499581d105176fa7df6092b7b2edd567
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379933"
---
# <a name="scope_identity-transact-sql"></a>SCOPE_IDENTITY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回插入相同範圍之識別欄位中的最後一個識別值。 範圍是一個模組：預存程序、觸發程序、函數或批次。 因此，若兩個陳述式在相同預存程序、函式或批次中，它們就在相同範圍中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
SCOPE_IDENTITY()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別
 **numeric(38,0)**  
  
## <a name="remarks"></a>備註  
 SCOPE_IDENTITY、IDENT_CURRENT 和 @@IDENTITY 是類似的函式，因為它們會傳回插入識別欄位的值。  
  
 IDENT_CURRENT 不受範圍和工作階段的限制；它只限於指定的資料表。 IDENT_CURRENT 會傳回在任何工作階段和任何範圍中，產生給特定資料表的值。 如需詳細資訊，請參閱 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)。  
  
 SCOPE_IDENTITY 和 @@IDENTITY 會傳回目前工作階段任何資料表中所產生的最後一個識別值。 不過，SCOPE_IDENTITY 會傳回只在目前範圍內插入的值；@@IDENTITY 不限於特定範圍。  
  
 例如，有 T1 和 T2 兩份資料表，而且 T1 定義了 INSERT 觸發程序。 當資料列插入 T1 時，會引發觸發程序，且會在 T2 中插入一個資料列。 這個狀況說明兩個範圍：在 T1 插入，以及觸發程序在 T2 插入。  
  
 假設 T1 和 T2 都有識別欄位，在 T1 的 INSERT 陳述式結束時，@@IDENTITY 和 SCOPE_IDENTITY 會傳回不同的值。 @@IDENTITY 會傳回在目前工作階段中，跨越任何範圍所插入的最後一個識別欄位值。 這是在 T2 中插入的值。 SCOPE_IDENTITY() 會傳回在 T1 中插入的 IDENTITY 值。 這是相同範圍內所發生的最後一項插入。 如果在範圍內的識別欄位執行任何 INSERT 陳述式之前叫用 SCOPE_IDENTITY() 函式，則這個函式會傳回 Null 值。  
  
 失敗的陳述式和交易可能會變更資料表的目前識別，以及建立識別欄位值中的間距。 識別值永遠不會回復，即使試圖將值插入資料表的交易未獲認可，也是如此。 例如，如果 INSERT 陳述式因 IGNORE_DUP_KEY 違規而失敗，資料表的目前識別值仍會遞增。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-identity-and-scope_identity-with-triggers"></a>A. 使用 @@IDENTITY 和 SCOPE_IDENTITY 搭配觸發程序  
 下列範例會建立 `TZ` 和 `TY` 這兩份資料表，以及 `TZ` 的 INSERT 觸發程序。 當資料列插入 `TZ` 資料表時，會引發觸發程序 (`Ztrig`)，且會在 `TY` 中插入一個資料列。  
  
```sql  
USE tempdb;  
GO  
CREATE TABLE TZ (  
   Z_id  INT IDENTITY(1,1)PRIMARY KEY,  
   Z_name VARCHAR(20) NOT NULL);  
  
INSERT TZ  
   VALUES ('Lisa'),('Mike'),('Carla');  
  
SELECT * FROM TZ;  
```     
結果集：這是 TZ 資料表的樣子。  
  
```  
Z_id   Z_name  
-------------  
1      Lisa  
2      Mike  
3      Carla  
```  
```sql 
CREATE TABLE TY (  
   Y_id  INT IDENTITY(100,5)PRIMARY KEY,  
   Y_name VARCHAR(20) NULL);  
  
INSERT TY (Y_name)  
   VALUES ('boathouse'), ('rocks'), ('elevator');  
  
SELECT * FROM TY;  
```   
結果集：這是 TY 資料表的樣子：  
```  
Y_id  Y_name  
---------------  
100   boathouse  
105   rocks  
110   elevator  
```  

建立在資料列插入 TZ 資料表的同時，也會將資料列插入 TY 資料表的觸發程序。  
```sql  
CREATE TRIGGER Ztrig  
ON TZ  
FOR INSERT AS   
   BEGIN  
   INSERT TY VALUES ('')  
   END;  
```  
引發 (FIRE) 觸發程序，並判斷您可以使用 @@IDENTITY 和 SCOPE_IDENTITY 取得哪些識別值。   
```sql
INSERT TZ VALUES ('Rosalie');  
  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
/*SCOPE_IDENTITY returns the last identity value in the same scope. This was the insert on table TZ.*/`  
SCOPE_IDENTITY  
4  

/*@@IDENTITY returns the last identity value inserted to TY by the trigger. 
  This fired because of an earlier insert on TZ.*/
@@IDENTITY  
115  
```  
  
### <a name="b-using-identity-and-scope_identity-with-replication"></a>B. 使用 @@IDENTITY 和 SCOPE_IDENTITY() 搭配複寫  
 下列範例會說明如何針對為了合併式複寫而發行之資料庫的插入，使用 `@@IDENTITY` 和 `SCOPE_IDENTITY()`。 範例中的兩份資料表都位於 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫中：`Person.ContactType` 尚未發行，而 `Sales.Customer` 已發行。 合併式複寫會將觸發程序加入至發行的資料表。 因此，`@@IDENTITY` 可能會根據複寫系統資料表的插入 (而非使用者資料表的插入) 傳回值。  
  
 `Person.ContactType` 資料表的最大識別值為 20。 如果您將資料列插入此資料表，`@@IDENTITY` 和 `SCOPE_IDENTITY()` 就會傳回相同的值。  
  
```sql  
USE AdventureWorks2012;  
GO  
INSERT INTO Person.ContactType ([Name]) VALUES ('Assistant to the Manager');  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```  
SCOPE_IDENTITY  
21  
@@IDENTITY  
21
```  
  
 `Sales.Customer` 資料表的最大識別值為 29483。 如果您將資料列插入此資料表，`@@IDENTITY` 和 `SCOPE_IDENTITY()` 就會傳回不同的值。 `SCOPE_IDENTITY()` 會根據使用者資料表的插入傳回值，而 `@@IDENTITY` 會根據複寫系統資料表的插入傳回值。 您可以針對需要存取已插入識別值的應用程式，使用 `SCOPE_IDENTITY()`。  
  
```sql  
INSERT INTO Sales.Customer ([TerritoryID],[PersonID]) VALUES (8,NULL);  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 ```
 SCOPE_IDENTITY  
 29484  
 @@IDENTITY  
 89
 ```  
  
## <a name="see-also"></a>另請參閱  
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)  
  
  
