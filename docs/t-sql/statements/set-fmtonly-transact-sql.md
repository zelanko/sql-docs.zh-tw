---
title: SET FMTONLY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 559edc2c3798529fda48930483e950fe79145791
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43068621"
---
# <a name="set-fmtonly-transact-sql"></a>SET FMTONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  只將中繼資料傳回用戶端。 可以用來測試回應的格式，而不需實際執行查詢。  
  
> [!NOTE]  
>  請勿使用這個功能。 這項功能已由 [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)、[sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)、[sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md) 及 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md) 取代。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SET FMTONLY { ON | OFF }   
```  
  
## <a name="remarks"></a>Remarks  
 當 SET FMTONLY 設為 ON 時，不會因為要求而處理任何資料列或將任何資料列傳給用戶端。  
  
 SET FMTONLY 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
## <a name="permissions"></a>[權限]  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-view-the-column-header-information-for-a-query-without-actually-running-the-query"></a>A. 檢視查詢的資料行標頭資訊，而不實際執行查詢。  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-view-the-column-header-information-for-a-query-without-actually-running-the-query"></a>B. 檢視查詢的資料行標頭資訊，而不實際執行查詢。  
 下列範例會示範如何只傳回查詢的資料行標頭 (中繼資料) 資訊。 批次一開始會將 FMTONLY 設為 OFF，並在 SELECT 陳述式之前將 FMTONLY 變更為 ON。 這可讓 SELECT 陳述式只傳回資料行資訊，而不會傳回任何資料列。  
  
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
  
  

