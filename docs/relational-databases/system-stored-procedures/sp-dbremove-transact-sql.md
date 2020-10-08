---
description: sp_dbremove (Transact-SQL)
title: sp_dbremove (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbremove
- sp_dbremove_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbremove
ms.assetid: a8513f4a-c025-49c8-99c3-4c83cb7f51ed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c57b013e1c97a82200390b7b3876248c7099e863
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91807305"
---
# <a name="sp_dbremove-transact-sql"></a>sp_dbremove (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  移除資料庫及其所有相關檔案。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 我們建議您改用 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dbremove [ @dbname = ] 'database' [ , [ @dropdev = ] 'dropdev' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @dbname = ] 'database'` 這是要移除的資料庫名稱。 *資料庫* 是 **sysname**，預設值是 Null。  
  
`[ @dropdev = ] 'dropdev'` 這是針對回溯相容性而提供的旗標，目前會忽略此旗標。 *dropdev* 的值為 **dropdev**。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會移除名稱為 `sales` 的資料庫及其所有相關檔案。  
  
```  
EXEC sp_dbremove sales;  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)   
 [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
