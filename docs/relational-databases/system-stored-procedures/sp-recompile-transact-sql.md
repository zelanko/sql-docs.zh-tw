---
title: sp_recompile (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_recompile_TSQL
- sp_recompile
dev_langs:
- TSQL
helpviewer_keywords:
- sp_recompile
ms.assetid: 6192ca87-febd-4075-8199-14b4fa609b8c
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9407b4a091ab30e89d5480ab679c2a91ed13ab1d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43075210"
---
# <a name="sprecompile-transact-sql"></a>sp_recompile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在下次執行預存程序、觸發程序以及使用者定義函數時，重新編譯它們。 其運作方式是從程序快取中卸除現有的計畫，以便強制在下次執行程序或觸發程序時建立新的計畫。 在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 集合中，系統會記錄 SP:CacheInsert 事件而非 SP:Recompile 事件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
  
sp_recompile [ @objname = ] 'object'  
```  
  
## <a name="arguments"></a>引數  
 [ @objname=] '*物件*'  
 目前資料庫中之預存程序、觸發程序、資料表、檢視表或使用者定義函數的限定或非限定名稱。 *物件*已**nvarchar(776)**，沒有預設值。 如果*物件*預存程序、 觸發程序或使用者定義函數、 預存程序，觸發程序名稱，或函式將會在下次執行時重新編譯。 如果*物件*是資料表或檢視的所有預存的程序、 觸發程序的名稱或參考資料表或檢視表的使用者定義函式將會在執行下一次重新編譯。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)  
  
## <a name="remarks"></a>備註  
 sp_recompile 只會在目前資料庫中尋找物件。  
  
 預存程序、觸發程序以及使用者定義函數所用的查詢，只在編譯時才會最佳化。 當資料庫進行會影響統計資料的索引或其他變更時，編譯過的預存程序、觸發程序以及使用者定義函數可能會降低效率。 您可以重新編譯處理資料表的預存程序和觸發程序來重新最佳化查詢。  
  
> [!NOTE]  
>  當重新編譯預存程序、觸發程序以及使用者定義函數有利時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動執行這個動作。  
  
## <a name="permissions"></a>Permissions  
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
  
  
