---
title: CONTEXT_INFO  (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONTEXT_INFO_TSQL
- CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- CONTEXT_INFO function
- Multiple Active Result Sets
- context information [SQL Server]
- MARS [SQL Server]
- session context information [SQL Server]
ms.assetid: 571320f5-7228-4b0e-9d01-ab732d2d1eab
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a647bc7ced2188a45183200f08400f5507f7b328
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="contextinfo--transact-sql"></a>CONTEXT_INFO  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回使用 [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md) 陳述式，針對目前工作階段或批次所設定的 **context_info** 值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>傳回值
**context_info** 的值。
  
若並未設定 **context_info**：
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，會傳回 NULL。  
-   在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，會傳回工作階段特定的 GUID。  
  
## <a name="remarks"></a>Remarks  
Multiple Active Result Set (MARS) 可讓應用程式在同一個連接上同時執行多個批次或要求。 當 MARS 連接的其中一個批次執行 SET CONTEXT_INFO 時，CONTEXT_INFO 函數會在與 SET 陳述式相同的批次中執行時，傳回新的內容值。 新值不是由在該連接一或多個其他批次執行的 CONTEXT_INFO 函數所傳回，除非它們是在執行 SET 陳述式的批次完成後才啟動。
  
## <a name="permissions"></a>Permissions  
不需要任何特殊權限。 內容資訊也是儲存在 **sys.dm_exec_requests**、**sys.dm_exec_sessions** 和 **sys.sysprocesses** 系統檢視中，但若要直接查詢檢視，就需要 SELECT 和 VIEW SERVER STATE 權限。
  
## <a name="examples"></a>範例  
下面這個簡單的範例會先將 **context_info** 值設為 `0x1256698456`，再使用 `CONTEXT_INFO` 函式來擷取該值。
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
