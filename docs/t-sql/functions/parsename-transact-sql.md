---
title: "PARSENAME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 5664c0a98663897f1d0a3cfa46e8dabab0d6ef7a
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="parsename-transact-sql"></a>PARSENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

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
 這是要擷取指定物件部分的物件名稱。 *object_name*是**sysname**。 這個參數是一個選擇性限定的物件名稱。 如果限定了物件名稱的所有部分，這個名稱會有四個部分：伺服器名稱、資料庫名稱、擁有者名稱和物件名稱。  
  
 *object_piece*  
 這是要傳回的物件部分。 *object_piece*的型別**int**，而且可以有下列值：  
  
 1 = 物件名稱  
  
 2 = 結構描述名稱  
  
 3 = 資料庫名稱  
  
 4 = 伺服器名稱  
  
## <a name="return-types"></a>傳回類型  
 **nchar**  
  
## <a name="remarks"></a>備註  
 如果符合下列條件之一，PARSENAME 會傳回 NULL：  
  
-   任一*object_name*或*object_piece*是 NULL。  
  
-   發生語法錯誤。  
  
 要求的物件部份的長度為 0 並不是有效[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]識別項。 長度為零的物件名稱會將完整名稱轉譯為無效。  
  
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
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [系統函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  


