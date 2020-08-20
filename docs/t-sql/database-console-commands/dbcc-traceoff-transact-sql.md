---
description: DBCC TRACEOFF (Transact-SQL)
title: DBCC TRACEOFF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: pmasl
ms.author: umajay
ms.openlocfilehash: 1b6990452c110cb012e206389a679688d2ff961d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479765"
---
# <a name="dbcc-traceoff-transact-sql"></a>DBCC TRACEOFF (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

停用指定的追蹤旗標。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
DBCC TRACEOFF ( trace# [ ,...n ] [ , -1 ] ) [ WITH NO_INFOMSGS ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
*trace#*  
這是要停用的追蹤旗標編號。  
  
**-1**  
在全域範圍內停用指定的追蹤旗標。  
  
WITH NO_INFOMSGS  
抑制所有嚴重性層級在 0 到 10 的參考用訊息。  
  
## <a name="remarks"></a>備註  
追蹤旗標是用來自訂特定性質以控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體運作方式。
  
## <a name="result-sets"></a>結果集  
DBCC TRACEOFF 會傳回：
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>權限  
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
  
  
