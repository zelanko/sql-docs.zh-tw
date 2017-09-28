---
title: "COL_NAME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COL_NAME
- COL_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- COL_NAME function
- column names [SQL Server]
- names [SQL Server], columns
ms.assetid: 214144ab-f2bc-4052-83cf-caf0a85c4cc6
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3028e409a8218b35bbf7cd4773e80ca27e8db8be
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="colname-transact-sql"></a>COL_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

從指定的對應資料表識別碼和資料行識別碼傳回資料行的名稱。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
COL_NAME ( table_id , column_id )  
```  
  
## <a name="arguments"></a>引數  
*table_id*  
這是包含資料行之資料表的識別碼。 *table_id*的型別**int**。
  
*column_id*  
這是資料行的識別碼。 *column_id*參數的類型是**int**。
  
## <a name="return-types"></a>傳回型別
**sysname**
  
## <a name="exceptions"></a>例外狀況  
當發生錯誤，或呼叫端沒有檢視物件的權限時，便會傳回 NULL。
  
使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，COL_NAME) 會在使用者不具有該物件任何權限時傳回 NULL。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。
  
## <a name="remarks"></a>備註  
*Table_id*和*column_id*參數會共同產生的資料行名稱的字串。
  
如需有關取得資料表和資料行識別碼的詳細資訊，請參閱[OBJECT_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/object-id-transact-sql.md).
  
## <a name="examples"></a>範例  
下列範例會傳回 `Employee` 資料庫的 `AdventureWorks2012` 資料表中第一個資料行的名稱。
  
```sql
USE AdventureWorks2012;  
GO  
SET NOCOUNT OFF;  
GO  
SELECT COL_NAME(OBJECT_ID('HumanResources.Employee'), 1) AS 'Column Name';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`Column Name`
  
-----------------\-
  
`BusinessEntityID`
  
## <a name="examples"></a>範例

[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

下列範例會傳回在範例中的第一個資料行名稱`Employee`資料表。
  
```sql
-- Uses AdventureWorks  
  
SELECT COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 1) AS FirstColumnName,  
COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 2) AS SecondColumnName;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
ColumnName          
------------   
BusinessEntityID  
```  
  
## <a name="see-also"></a>另請參閱
[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[中繼資料函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)  
[COL_LENGTH &#40;TRANSACT-SQL &#41;](../../t-sql/functions/col-length-transact-sql.md)
  
  


