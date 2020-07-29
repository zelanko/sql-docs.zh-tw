---
title: PARSENAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PARSENAME_TSQL
- PARSENAME
dev_langs:
- TSQL
helpviewer_keywords:
- PARSENAME function
- parsing [SQL Server], PARSENAME function
- names [SQL Server], objects
- objects [SQL Server], names
- part of object names [SQL Server]
ms.assetid: abf34f99-9ee9-460b-85b2-930ca5c4b5ae
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 915cf95799a80a0d8841206f4b23b04fba5fec5f
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87112376"
---
# <a name="parsename-transact-sql"></a>PARSENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  傳回物件名稱的指定部分。 物件可擷取的部分包含物件名稱、結構描述名稱、資料庫名稱及伺服器名稱。 
  
> [!NOTE]  
>  PARSENAME 函數並不會指出指定名稱的物件是否存在。 PARSENAME 只會傳回指定物件名稱的指定部份。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql 
PARSENAME ('object_name' , object_piece )
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數

*'object_name'* ：此參數存放為了擷取指定物件部分的物件名稱。 這個參數是一個選擇性限定的物件名稱。 若限定了物件名稱的所有部分，則此名稱會有四個部分：伺服器名稱、資料庫名稱、結構描述名稱及物件名稱。  ' Object_name ' 字串的每個部分都是 *sysname* 類型，這相當於 Nvarchar (128) 或 256 個位元組。 若字串的任何部分超過 256 個位元組，則 PARSENAME 會針對該部分傳回 Null，因為其不是有效的 sysname。
  
*object_piece*  
這是要傳回的物件部分。 *object_piece* 的類型是 **int**它可以有下列這些值：  
    1 = 物件名稱  
    2 = 結構描述名稱  
    3 = 資料庫名稱  
    4 = 伺服器名稱  
  
## <a name="return-type"></a>傳回類型

 **sysname**
  
## <a name="remarks"></a>備註

 如果符合下列條件之一，PARSENAME 會傳回 NULL：  
  
-   *object_name* 或 *object_piece* 是 NULL。  
  
-   發生語法錯誤。  
  
 要求的物件部分，長度為 0，且不是有效的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別碼。 長度為零的物件名稱會將完整名稱轉譯為無效。  
  
## <a name="examples"></a>範例

 下列範例會利用 `PARSENAME` 來傳回 `Person` 資料庫中之 `AdventureWorks2012` 資料表的相關資訊。  
  
```sql  
-- Uses AdventureWorks  
  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 1) AS 'Object Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 2) AS 'Schema Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 3) AS 'Database Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 4) AS 'Server Name';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
Object Name
------------------------------
DimCustomer

(1 row(s) affected)

Schema Name
------------------------------
dbo

(1 row(s) affected)

Database Name
------------------------------
AdventureWorksPDW2012

(1 row(s) affected)

Server Name
------------------------------
(null)

(1 row(s) affected)
```
  
## <a name="see-also"></a>另請參閱

- [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
- [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
- [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
- [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  

