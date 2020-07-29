---
title: DATALENGTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATALENGTH_TSQL
- DATALENGTH
dev_langs:
- TSQL
helpviewer_keywords:
- number of bytes representing expression
- data types [SQL Server], length
- DATALENGTH function
- expressions [SQL Server], length
- lengths [SQL Server], data
ms.assetid: 00f377f1-cc3e-4eac-be47-b3e3f80267c9
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ac8f7372833d70a46e5ea3cb343641b02aa05120
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87113087"
---
# <a name="datalength-transact-sql"></a>DATALENGTH (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

此函式會傳回用來代表任何運算式的位元組數目。

> [!NOTE]
> 若要傳回字串運算式中的字元數目，請使用 [LEN](../../t-sql/functions/len-transact-sql.md) 函式。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```
DATALENGTH ( expression )   
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
*expression*  
任何資料類型的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。
  
## <a name="return-types"></a>傳回類型
如果 **expression** 具有 *nvarchar(max)* 、**varbinary(max)** 或 **varchar(max)** 資料類型，則為 **bigint**；否則為 **int**。
  
## <a name="remarks"></a>備註  
對於可以儲存可變長度資料的資料類型，`DATALENGTH` 會非常有用：
- **image**
- **ntext**
- **nvarchar**
- **text**
- **varbinary**
- **varchar**
  
針對 NULL 值，`DATALENGTH` 會傳回 NULL。
  
> [!NOTE]  
> 相容性層級可能會影響傳回值。 如需相容性層級的詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  

> [!NOTE]
> 使用 [LEN](../../t-sql/functions/len-transact-sql.md) 傳回編碼成所給定字串運算式的字元數目，使用 [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) 則傳回所給定字串運算式的大小 (以位元組為單位)。 取決於資料行中所使用的資料類型和編碼類型而，這些輸出可能會有所不同。 如需不同編碼類型之間儲存體差異的詳細資訊，請參閱[定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)。

## <a name="examples"></a>範例  
此範例會尋找 `Name` 資料表中 `Product` 資料行的長度：
  
```sql
USE AdventureWorks2016  
GO
SELECT length = DATALENGTH(EnglishProductName), EnglishProductName  
FROM dbo.DimProduct  
ORDER BY EnglishProductName;  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)
