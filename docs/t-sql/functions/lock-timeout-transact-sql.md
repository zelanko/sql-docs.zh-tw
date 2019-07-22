---
title: '@@LOCK_TIMEOUT (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@LOCK_TIMEOUT'
- '@@LOCK_TIMEOUT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- '@@LOCK_TIMEOUT function'
- current lock time-out setting
- locking [SQL Server], time-outs
ms.assetid: 6bf8bf97-60b8-40c1-b89d-8f5a00bcae2e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 767ccc61139886a1e81bbeb390b89676267b0d79
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059898"
---
# <a name="x40x40locktimeout-transact-sql"></a>&#x40;&#x40;LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回目前工作階段的目前鎖定逾時設定 (以毫秒為單位)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@LOCK_TIMEOUT  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 SET LOCK_TIMEOUT 允許應用程式設定陳述式在封鎖的資源上，最大的等待時間。 當陳述式等待時間超出 LOCK_TIMEOUT 設定時，會自動取消封鎖的陳述式，且會傳回一則錯誤訊息給應用程式。  
  
 若尚未在目前工作階段中執行 SET LOCK_TIMEOUT，@@LOCK_TIMEOUT 會傳回 -1 值。  
  
## <a name="examples"></a>範例  
 這個範例顯示當未設定 LOCK_TIMEOUT 值時的結果集。  
  
```  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 以下為結果集：  
  
```  
Lock Timeout  
------------  
-1  
```  
  
 這個範例會將 LOCK_TIMEOUT 設為 1800 毫秒，然後呼叫 @@LOCK_TIMEOUT。  
  
```  
SET LOCK_TIMEOUT 1800;  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 以下為結果集：  
  
```  
Lock Timeout  
------------  
1800          
```  
  
## <a name="see-also"></a>另請參閱  
 [組態函式 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  
