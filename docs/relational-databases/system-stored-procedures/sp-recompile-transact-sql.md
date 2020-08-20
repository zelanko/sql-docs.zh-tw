---
description: sp_recompile (Transact-SQL)
title: sp_recompile (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_recompile_TSQL
- sp_recompile
dev_langs:
- TSQL
helpviewer_keywords:
- sp_recompile
ms.assetid: 6192ca87-febd-4075-8199-14b4fa609b8c
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6bbf1e6b85b3071e0029d1fd294a8147b79d64fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473881"
---
# <a name="sp_recompile-transact-sql"></a>sp_recompile (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  在下次執行預存程序、觸發程序以及使用者定義函數時，重新編譯它們。 其運作方式是從程序快取中卸除現有的計畫，以便強制在下次執行程序或觸發程序時建立新的計畫。 在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 集合中，系統會記錄 SP:CacheInsert 事件而非 SP:Recompile 事件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
  
sp_recompile [ @objname = ] 'object'  
```  
  
## <a name="arguments"></a>引數  
 [ @objname =] '*object*'  
 目前資料庫中之預存程序、觸發程序、資料表、檢視表或使用者定義函數的限定或非限定名稱。 *物件* 是 **Nvarchar (776) **，沒有預設值。 如果 *object* 是預存程式、觸發程式或使用者定義函數的名稱，則會在下次執行時重新編譯預存程式、觸發程式或函數。 如果 *物件* 是資料表或視圖的名稱，則參考資料表或視圖的所有預存程式、觸發程式或使用者定義函數，都會在下次執行時重新編譯。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)  
  
## <a name="remarks"></a>備註  
 sp_recompile 只會在目前資料庫中尋找物件。  
  
 預存程序、觸發程序以及使用者定義函數所用的查詢，只在編譯時才會最佳化。 當資料庫進行會影響統計資料的索引或其他變更時，編譯過的預存程序、觸發程序以及使用者定義函數可能會降低效率。 您可以重新編譯處理資料表的預存程序和觸發程序來重新最佳化查詢。  
  
> [!NOTE]  
>  當重新編譯預存程序、觸發程序以及使用者定義函數有利時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動執行這個動作。  
  
## <a name="permissions"></a>權限  
 需要指定之物件的 ALTER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會在下次執行處理 `Customer` 資料表的預存程序、觸發程序以及使用者定義函數時，重新編譯它們。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'Sales.Customer';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
