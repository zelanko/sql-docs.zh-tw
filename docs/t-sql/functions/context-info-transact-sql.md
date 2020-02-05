---
title: CONTEXT_INFO  (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b6278faa80721ce500257650db70359dcc740ee8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68132067"
---
# <a name="context_info--transact-sql"></a>CONTEXT_INFO  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此函數會傳回針對目前工作階段或批次所設定，或使用 **SET CONTEXT_INFO** 陳述式而衍生的 [context_info](../../t-sql/statements/set-context-info-transact-sql.md) 值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>傳回值
**context_info** 值。
  
若並未設定 **context_info**：
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，會傳回 NULL。  
-   在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，會傳回工作階段特定的 GUID。  
  
## <a name="remarks"></a>備註  
Multiple Active Result Set (MARS) 可讓應用程式在同一個連線上，同時執行多個批次或要求。 當其中一個 MARS 連線批次執行 SET CONTEXT_INFO 時，當 `CONTEXT_INFO` 函數在與 SET 陳述式相同的批次中執行時，`CONTEXT_INFO` 函數會傳回新的內容值。 如果 `CONTEXT_INFO` 函數在一或多個其他連線批次中執行時，`CONTEXT_FUNCTION` 不會傳回新的值，除非這些批次是在執行 SET 陳述式的批次完成之後才開始執行。
  
## <a name="permissions"></a>權限  
不需要任何特殊權限。 下列系統檢視表會儲存內容資訊，但直接查詢這些檢視表則需要 SELECT 和 VIEW SERVER STATE 權限：
- **sys.dm_exec_requests**
- **sys.dm_exec_sessions**
- **sys.sysprocesses**
  
## <a name="examples"></a>範例  
這個簡單的範例會先將 **context_info** 值設為 `0x1256698456`，再使用 `CONTEXT_INFO` 來擷取該值。
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
