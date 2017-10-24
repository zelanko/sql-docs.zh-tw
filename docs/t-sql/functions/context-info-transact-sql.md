---
title: "CONTEXT_INFO (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd261b2f7f1cc4234792bec66c3662d6d9b8dcd8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="contextinfo--transact-sql"></a>CONTEXT_INFO (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回**context_info**設定目前工作階段或批次所使用的值[SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md)陳述式。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>傳回值
值**context_info**。
  
如果**context_info**未設定：
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回 NULL。  
-   在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]傳回唯一的工作階段專屬 GUID。  
  
## <a name="remarks"></a>備註  
Multiple Active Result Set (MARS) 可讓應用程式在同一個連接上同時執行多個批次或要求。 當 MARS 連接的其中一個批次執行 SET CONTEXT_INFO 時，CONTEXT_INFO 函數會在與 SET 陳述式相同的批次中執行時，傳回新的內容值。 新值不是由在該連接一或多個其他批次執行的 CONTEXT_INFO 函數所傳回，除非它們是在執行 SET 陳述式的批次完成後才啟動。
  
## <a name="permissions"></a>Permissions  
不需要任何特殊權限。 內容資訊也儲存在**sys.dm_exec_requests**， **sys.dm_exec_sessions**，和**sys.sysprocesses**系統檢視表，但直接查詢檢視需要 SELECT 和 VIEW SERVER STATE 權限。
  
## <a name="examples"></a>範例  
下列簡單範例會設定**context_info**值設定為`0x1256698456`，然後使用`CONTEXT_INFO`函式可擷取的值。
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[SET CONTEXT_INFO &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  

