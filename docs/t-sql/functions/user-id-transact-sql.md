---
title: "USER_ID (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- USER_ID
- USER_ID_TSQL
dev_langs: TSQL
helpviewer_keywords:
- USER_ID function
- identification numbers [SQL Server]
- IDs [SQL Server], databases
- users [SQL Server], database ID numbers
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
ms.assetid: 67fd29bc-eda9-4d4d-b148-5d3659181a43
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c8c8e07d6d58b6615ff5e4528556bf08e0b72c13
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="userid-transact-sql"></a>USER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回資料庫使用者的識別碼。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[DATABASE_PRINCIPAL_ID](../../t-sql/functions/database-principal-id-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
USER_ID ( [ 'user' ] )  
```  
  
## <a name="arguments"></a>引數  
 *使用者*  
 要使用的使用者名稱。 *使用者*是**nchar**。 如果**char**指定值，則它會隱含地轉換成**nchar**。 它必須用括號括住。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>備註  
 當*使用者*已省略，則會假設目前的使用者。 如果參數包含 NULL 一詞，即會傳回 NULL。當 USER_ID 在 EXECUTE AS 之後呼叫時，USER_ID 會傳回模擬內容的識別碼。  
  
 未對應至特定資料庫使用者的 Windows 主體藉由群組成員資格來存取資料庫時，USER_ID 會傳回 0 (public 的識別碼)。 如果這類主體建立物件而不指定結構描述，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會建立對應至 Windows 主體的隱含使用者和結構描述。 在這種情況下建立的使用者不能用來連接到資料庫。 對應至隱含使用者的 Windows 主體對 USER_ID 的呼叫會傳回隱含使用者的識別碼。  
  
 USER_ID 可用在選取清單、WHERE 子句及任何允許使用運算式的位置中。 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `AdventureWorks2012` 使用者 `Harold` 的識別碼。  
  
```  
USE AdventureWorks2012;  
SELECT USER_ID('Harold');  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [USER_NAME &#40;TRANSACT-SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [DATABASE_PRINCIPAL_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/database-principal-id-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
