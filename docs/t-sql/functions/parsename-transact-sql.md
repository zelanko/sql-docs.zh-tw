---
title: PARSENAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b36e31e163999a6af70b498fef9d65c2ce0ae55
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "73843623"
---
# <a name="parsename-transact-sql"></a>PARSENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  傳回物件名稱的指定部分。 物件的可擷取部分有物件名稱、擁有者名稱、資料庫名稱和伺服器名稱。  
  
> [!NOTE]  
>  PARSENAME 函數並不會指出指定名稱的物件是否存在。 PARSENAME 只會傳回指定物件名稱的指定部份。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
PARSENAME ( 'object_name' , object_piece )   
```  
  
## <a name="arguments"></a>引數  
 '*object_name*'  
 這是要擷取指定物件部分的物件名稱。 *object_name* 是 **sysname**. 這個參數是一個選擇性限定的物件名稱。 如果限定了物件名稱的所有部分，這個名稱會有四個部分：伺服器名稱、資料庫名稱、擁有者名稱和物件名稱。  
  
 *object_piece*  
 這是要傳回的物件部分。 *object_piece* 的類型是 **int**它可以有下列這些值：  
  
 1 = 物件名稱  
  
 2 = 結構描述名稱  
  
 3 = 資料庫名稱  
  
 4 = 伺服器名稱  
  
## <a name="return-types"></a>傳回型別  
 **sysname**  
  
## <a name="remarks"></a>備註  
 如果符合下列條件之一，PARSENAME 會傳回 NULL：  
  
-   *object_name* 或 *object_piece* 是 NULL。  
  
-   發生語法錯誤。  
  
 要求的物件部分，長度為 0，且不是有效的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別碼。 長度為零的物件名稱會將完整名稱轉譯為無效。  
  
## <a name="examples"></a>範例  
 下列範例會利用 `PARSENAME` 來傳回 `Person` 資料庫中之 `AdventureWorks2012` 資料表的相關資訊。  
  
```  
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
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  

