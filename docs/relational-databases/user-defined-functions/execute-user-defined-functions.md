---
title: 執行使用者定義函式 | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b028b6ab4da678444427682a635f679acce576ab
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68123578"
---
# <a name="execute-user-defined-functions"></a>執行使用者定義函數
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  使用 Transact-SQL 執行使用者定義函數。
  

> **注意** ︰造訪  [使用者定義的函式](user-defined-functions.md) 和 [Create Function (Transact SQL](../../t-sql/statements/create-function-transact-sql.md) 以取得使用者定義函式的詳細資訊。 
  
 
##  <a name="BeforeYouBegin"></a>開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 在 Transact-SQL 中，您可以使用 *value* 或 @*parameter_name*=*value*來提供參數。 來提供參數。參數不是交易的一部分；因此，如果交易中的參數變更之後再回復，參數值並不會還原為之前的值。 傳回呼叫端的值一定是模組傳回時的值。  
  
###  <a name="Security"></a> Security  
  
 執行 [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md) 陳述式不需要任何權限。 不過，您 **必須** 對 EXECUTE 字串內所參考的安全性實體具備權限。 例如，如果字串包含 [INSERT](../../t-sql/statements/insert-transact-sql.md) 陳述式，EXECUTE 陳述式的呼叫端就必須有目標資料表的 INSERT 權限。 遇到 EXECUTE 陳述式時會檢查權限，即使模組內包含 EXECUTE 陳述式也一樣。 如需詳細資訊，請參閱 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
### <a name="example"></a>範例 
  
這個範例會使用大部分 `ufnGetSalesOrderStatusText` 版本中都有提供的 `AdventureWorks`純量值函數。  此函數的目的是為了從指定整數傳回銷售狀態的文字值。  請將整數 1 到 7 傳遞給 **\@Status** 參數來改變範例。
  
~~~tsql
USE [AdventureWorks2016CTP3]
GO  

-- Declare a variable to return the results of the function. 
DECLARE @ret nvarchar(15);   

-- Execute the function while passing a value to the @status parameter
EXEC @ret = dbo.ufnGetSalesOrderStatusText 
    @Status = 5; 

-- View the returned value.  The Execute and Select statements must be executed at the same time.  
SELECT N'Order Status: ' + @ret; 

-- Result:
-- Order Status: Shipped
~~~
  
  
  
