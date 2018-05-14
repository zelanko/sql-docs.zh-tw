---
title: DBCC TRACEOFF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TRACEOFF_TSQL
- TRACEOFF
- DBCC TRACEOFF
- DBCC_TRACEOFF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- trace flags [SQL Server], disabling
- DBCC TRACEOFF statement
- disabling trace flags
ms.assetid: 1379afba-6480-454b-9c65-5e64cb4f3415
caps.latest.revision: 34
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: 43e463ca714dc293ef8de4239287e85f4b3c3791
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="dbcc-traceoff-transact-sql"></a>DBCC TRACEOFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

停用指定的追蹤旗標。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql
DBCC TRACEOFF ( trace# [ ,...n ] [ , -1 ] ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引數  
*trace#*  
這是要停用的追蹤旗標編號。  
  
**-1**  
在全域範圍內停用指定的追蹤旗標。  
  
WITH NO_INFOMSGS  
抑制所有嚴重性層級在 0 到 10 的參考用訊息。  
  
## <a name="remarks"></a>Remarks  
追蹤旗標是用來自訂特定性質以控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體運作方式。
  
## <a name="result-sets"></a>結果集  
DBCC TRACEOFF 會傳回：
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。
  
## <a name="examples"></a>範例  
下列範例會停用追蹤旗標 `3205`。
  
```sql
DBCC TRACEOFF (3205);   
GO  
```  
  
下列範例會先在全域範圍內停用追蹤旗標 `3205`。
  
```sql
DBCC TRACEOFF (3205, -1);   
GO  
```  
  
下列範例會在全域範圍內停用追蹤旗標 `3205` 和 `260`。
  
```sql
DBCC TRACEOFF (3205, 260, -1);  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[DBCC TRACESTATUS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
