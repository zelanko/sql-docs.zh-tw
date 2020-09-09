---
description: sp_droptype (Transact-SQL)
title: sp_droptype (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droptype_TSQL
- sp_droptype
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droptype
ms.assetid: e78464ac-2370-4c4e-9cc0-06aebc07cec5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d470c4f6f706db73f401511826a6dbcd5903d8d0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536145"
---
# <a name="sp_droptype-transact-sql"></a>sp_droptype (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從 **systypes**中刪除別名資料類型。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_droptype [ @typename = ] 'type'  
```  
  
## <a name="arguments"></a>引數  
`[ @typename = ] 'type'` 這是您所擁有的別名資料類型名稱。 *type* 是 **sysname**，沒有預設值。  
  
## <a name="return-code-type"></a>傳回碼類型  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 如果資料表或其他資料庫物件參考，則無法卸載 **類型** 別名資料類型。  
  
> [!NOTE]  
>  如果別名資料類型用於資料表定義中，或者如果有規則或預設值與它繫結，就無法卸除別名資料類型。  
  
## <a name="permissions"></a>權限  
 需要 **db_owner** 固定資料庫角色或 **db_ddladmin** 固定資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會卸除別名資料類型 `birthday`。  
  
> [!NOTE]  
>  這個別名資料類型必須已經存在，否則這個範例便會傳回錯誤訊息。  
  
```  
USE master;  
GO  
EXEC sp_droptype 'birthday';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的資料庫引擎預存程式 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_addtype &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addtype-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
