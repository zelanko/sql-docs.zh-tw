---
title: DBCC HELP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DBCC HELP
- DBCC_HELP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC statement syntax information
- DBCC HELP statement
ms.assetid: 306092c6-4354-4e47-928b-606124fbdc6e
caps.latest.revision: 33
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: 83411da2404093e7187bedc26cfd72ddb3dc4341
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="dbcc-help-transact-sql"></a>DBCC HELP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

傳回指定 DBCC 命令的語法資訊。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DBCC HELP ( 'dbcc_statement' | @dbcc_statement_var | '?' )  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引數  
 *dbcc_statement* | *@dbcc_statement_var*  
 這是接收語法資訊之 DBCC 命令的名稱。 它只提供 DBCC 後面的 DBCC 命令部分，例如，只提供 CHECKDB 而不是 DBCC CHECKDB。  
  
 ?  
 傳回所有提供了說明的 DBCC 命令。  
  
 WITH NO_INFOMSGS  
 抑制所有嚴重性層級在 0 到 10 的參考用訊息。  
  
## <a name="result-sets"></a>結果集  
DBCC HELP 會傳回結果集，顯示指定 DBCC 命令的語法。
  
## <a name="permissions"></a>Permissions  
需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。
  
## <a name="examples"></a>範例  
### <a name="a-using-dbcc-help-with-a-variable"></a>A. 使用 DBCC HELP 搭配變數  
下列範例會傳回 DBCC `CHECKDB` 的語法資訊。
  
```sql  
DECLARE @dbcc_stmt sysname;  
SET @dbcc_stmt = 'CHECKDB';  
DBCC HELP (@dbcc_stmt);  
GO  
```  
  
### <a name="b-using-dbcc-help-with-the--option"></a>B. 使用 DBCC HELP 搭配 ?  選項  
下列範例會傳回所有提供了說明的 DBCC 陳述式。
  
```sql  
DBCC HELP ('?');  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
