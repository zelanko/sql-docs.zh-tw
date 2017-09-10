---
title: "SET FMTONLY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FMTONLY_TSQL
- FMTONLY
- SET FMTONLY
- SET_FMTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server], only metadata returned
- SET FMTONLY statement
- FMTONLY option
ms.assetid: 02a1d9ac-2e58-433c-9a07-2c5a4a2214e1
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1cf925ce8ec9095acec90a34ed7d08f04826c2c1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-fmtonly-transact-sql"></a>SET FMTONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  只將中繼資料傳回用戶端。 可以用來測試回應的格式，而不需實際執行查詢。  
  
> [!NOTE]  
>  請勿使用這個功能。 這項功能已被取代[sp_describe_first_result_set &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)， [sp_describe_undeclared_parameters &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)， [sys.dm_exec_describe_first_result_set &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)，和[sys.dm_exec_describe_first_result_set_for_object &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SET FMTONLY { ON | OFF }   
```  
  
## <a name="remarks"></a>備註  
 當 SET FMTONLY 設為 ON 時，不會因為要求而處理任何資料列或將任何資料列傳給用戶端。  
  
 SET FMTONLY 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-view-the-column-header-information-for-a-query-without-actually-running-the-query"></a>答： 檢視不會實際執行查詢的查詢中的資料行的標頭資訊。  
 下列範例會將 `SET FMTONLY` 設定改成 `ON`，且會執行 `SELECT` 陳述式。 這項設定會使陳述式只傳回資料行資訊；不會傳回任何資料列。  
  
```  
USE AdventureWorks2012;  
GO  
SET FMTONLY ON;  
GO  
SELECT *   
FROM HumanResources.Employee;  
GO  
SET FMTONLY OFF;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-view-the-column-header-information-for-a-query-without-actually-running-the-query"></a>B. 檢視不會實際執行查詢的查詢中的資料行的標頭資訊。  
 下列範例會示範如何只傳回資料行標題 （中繼資料） 資訊的查詢。 批次開頭為 FMTONLY 設為 OFF，並變更 FMTONLY 設為 ON，SELECT 陳述式之前。 這會導致選取的陳述式來傳回僅資料行標頭。會不傳回任何資料列。  
  
```  
-- Uses AdventureWorks  
  
BEGIN  
    SET FMTONLY OFF;  
    SET DATEFORMAT mdy;  
    SET FMTONLY ON;  
    SELECT * FROM dbo.DimCustomer;  
    SET FMTONLY OFF;  
END  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  


