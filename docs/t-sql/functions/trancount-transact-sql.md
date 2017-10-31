---
title: "@@TRANCOUNT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@TRANCOUNT_TSQL'
- '@@TRANCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@TRANCOUNT function'
- number of active transactions
- connections [SQL Server], active transactions
- active transactions
ms.assetid: b2638410-e410-4bd0-9b54-90096182b2b6
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 19713aeb9058e83f97500075a1024c6c715628e9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40trancount-transact-sql"></a>（& s) #x 40; & #x 40。TRANCOUNT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回已經針對目前連接進行的 BEGIN TRANSACTION 陳述式數目。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@TRANCOUNT  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>備註  
 BEGIN TRANSACTION 陳述式會遞增@TRANCOUNT1。 ROLLBACK TRANSACTION 會遞減 @@TRANCOUNT為 0 時，除了 ROLLBACK TRANSACTION *savepoint_name*，這並不會影響@TRANCOUNT。 COMMIT TRANSACTION 或 COMMIT WORK 遞減@TRANCOUNT1。  
  
## <a name="examples"></a>範例  
  
### <a name="a-showing-the-effects-of-the-begin-and-commit-statements"></a>A. 顯示 BEGIN 和 COMMIT 陳述式的作用  
 下列範例會顯示巢狀 `BEGIN` 和 `COMMIT` 陳述式對 `@@TRANCOUNT` 變數的影響。  
  
```  
PRINT @@TRANCOUNT  
--  The BEGIN TRAN statement will increment the  
--  transaction count by 1.  
BEGIN TRAN  
    PRINT @@TRANCOUNT  
    BEGIN TRAN  
        PRINT @@TRANCOUNT  
--  The COMMIT statement will decrement the transaction count by 1.  
    COMMIT  
    PRINT @@TRANCOUNT  
COMMIT  
PRINT @@TRANCOUNT  
--Results  
--0  
--1  
--2  
--1  
--0  
```  
  
### <a name="b-showing-the-effects-of-the-begin-and-rollback-statements"></a>B. 顯示 BEGIN 和 ROLLBACK 陳述式的作用  
 下列範例會顯示巢狀 `BEGIN TRAN` 和 `ROLLBACK` 陳述式對 `@@TRANCOUNT` 變數的影響。  
  
```  
PRINT @@TRANCOUNT  
--  The BEGIN TRAN statement will increment the  
--  transaction count by 1.  
BEGIN TRAN  
    PRINT @@TRANCOUNT  
    BEGIN TRAN  
        PRINT @@TRANCOUNT  
--  The ROLLBACK statement will clear the @@TRANCOUNT variable  
--  to 0 because all active transactions will be rolled back.  
ROLLBACK  
PRINT @@TRANCOUNT  
--Results  
--0  
--1  
--2  
--0  
```  
  
## <a name="see-also"></a>另請參閱  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [系統函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

