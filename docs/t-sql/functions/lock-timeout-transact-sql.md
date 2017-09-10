---
title: "@@LOCK_TIMEOUT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15ee9c5789ea6f1c7bbad6fc8caeabab14f3df4f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="locktimeout-transact-sql"></a>@@LOCK_TIMEOUT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回目前工作階段的目前鎖定逾時設定 (以毫秒為單位)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
@@LOCK_TIMEOUT  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>備註  
 SET LOCK_TIMEOUT 允許應用程式設定陳述式在封鎖的資源上，最大的等待時間。 當陳述式等待時間超出 LOCK_TIMEOUT 設定時，會自動取消封鎖的陳述式，且會傳回一則錯誤訊息給應用程式。  
  
 @@LOCK_TIMEOUT傳回-1 值，如果 SET LOCK_TIMEOUT 尚未執行目前的工作階段中。  
  
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
  
 這個範例會將 LOCK_TIMEOUT 設為 1800年毫秒，，然後呼叫@LOCK_TIMEOUT。  
  
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
 [SET LOCK_TIMEOUT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  
