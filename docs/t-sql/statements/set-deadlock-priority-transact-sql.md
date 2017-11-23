---
title: "SET DEADLOCK_PRIORITY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET DEADLOCK_PRIORITY
- DEADLOCK_PRIORITY_TSQL
- SET_DEADLOCK_PRIORITY_TSQL
- DEADLOCK_PRIORITY
dev_langs: TSQL
helpviewer_keywords:
- deadlocks [SQL Server], priority settings
- DEADLOCK_PRIORITY option
- locking [SQL Server], deadlocks
- priority deadlock settings [SQL Server]
- SET DEADLOCK_PRIORITY statement
ms.assetid: 810a3a8e-3da3-4bf9-bb15-7b069685a1b6
caps.latest.revision: "35"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aa43f93003240c41fefdc589392f936c60a2333d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="set-deadlockpriority-transact-sql"></a>SET DEADLOCK_PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  指定如果與另一個工作階段發生死結時，目前工作階段繼續處理的相對重要性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SET DEADLOCK_PRIORITY { LOW | NORMAL | HIGH | <numeric-priority> | @deadlock_var | @deadlock_intvar }  
  
<numeric-priority> ::= { -10 | -9 | -8 | … | 0 | … | 8 | 9 | 10 }  
```  
  
## <a name="arguments"></a>引數  
 LOW  
 指定如果目前的工作階段陷入死結，而其他陷入死結鏈結的工作階段的死結優先權設成 NORMAL 或 HIGH，或是大於 -5 的整數值，則目前工作階段將會是死結的犧牲者。 如果其他工作階段的死結優先權設為小於 -5 的整數值，則目前工作階段將不會是死結犧牲者。 另外它也會指定，如果另一個工作階段的死結優先權設為 LOW 或等於 -5 的整數值，則目前工作階段可以成為死結的犧牲者。  
  
 NORMAL  
 指定如果陷入死結鏈結的其他工作階段，其死結優先權設成 HIGH 或大於 0 的整數值，則目前工作階段將會是死結的犧牲者，但是如果其他工作階段的死結優先權設成 LOW 或是小於 0 的整數值，則目前工作階段不會是死結的犧牲者。 另外它也會指定，如果任何其他工作階段的死結優先權設為 NORMAL 或等於 0 的整數值，則目前工作階段可以成為死結的犧牲者。 NORMAL 是預設優先權。  
  
 HIGH  
 指定如果陷入死結鏈結的其他工作階段，其死結優先權設成 HIGH 或大於 5 的整數，目前工作階段便會成為死結犧牲者，如果另一個工作階段的死結優先權也設成 HIGH 或 5，目前工作階段可以成為死結的犧牲者。  
  
 \<優先權的數字 >  
 這是一個整數值範圍 (-10 至 10)，用來提供 21 個層級的死結優先權。 指定如果陷入死結鏈結的其他工作階段在執行較高的死結優先權值，目前工作階段便會成為死結犧牲者，如果其他工作階段所執行的死結優先權值低於目前工作階段的值，目前工作階段便不會成為死結犧牲者。 另外，它也指定如果另一個工作階段執行的死結優先權值與目前工作階段相同，目前工作階段可以成為死結的犧牲者。 LOW 對應於 -5，NORMAL 對應於 0，HIGH 對應於 5。  
  
 **@***deadlock_var*  
 這是指定死結優先權的字元變數。 這個變數必須設成 'LOW'、'NORMAL' 或 'HIGH' 值。 這個變數必須足以保存整個字串。  
  
 **@***deadlock_intvar*  
 這是指定死結優先權的整數變數。 這個變數必須設成 (-10 至 10) 範圍內的整數值。  
  
## <a name="remarks"></a>備註  
 當兩個工作階段都在等待存取對方所鎖定的資源時，便會出現死結。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體偵測到兩個工作階段發生死結時，它會選擇一個工作階段作為死結犧牲者來解決死結。 此時會回復犧牲者目前的交易，且會向用戶端傳回死結錯誤訊息 1205。 這個工作階段所持有的鎖定會全部釋出，讓其他工作階段繼續作業。  
  
 選擇哪個工作階段作為死結犧牲者，會隨著每個工作階段的死結優先權而不同：  
  
-   如果兩個工作階段的死結優先權相同，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體會選擇回復成本較低的工作階段作為死結的犧牲者。 例如，如果兩個工作階段的死結優先權都設成 HIGH，此時執行個體會選擇評估回復成本較低的工作階段來作為犧牲者。  
  
-   如果工作階段的死結優先權不同，就選擇死結優先權最低的工作階段來作為死結犧牲者。  
  
 SET DEADLOCK_PRIORITY 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會利用變數，將死結優先權設為 `LOW`。  
  
```  
DECLARE @deadlock_var NCHAR(3);  
SET @deadlock_var = N'LOW';  
  
SET DEADLOCK_PRIORITY @deadlock_var;  
GO  
```  
  
 下列範例將死結優先權設為 `NORMAL`。  
  
```  
SET DEADLOCK_PRIORITY NORMAL;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [@@LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  
