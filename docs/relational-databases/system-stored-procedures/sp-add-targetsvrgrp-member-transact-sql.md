---
description: sp_add_targetsvrgrp_member (Transact-SQL)
title: sp_add_targetsvrgrp_member (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_targetsvrgrp_member
- sp_add_targetsvrgrp_member_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_targetsvrgrp_member
ms.assetid: 5021ed5b-acca-4f8b-b9db-18733059c359
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 76553462908de6a611ad7cd418964e26b7760bdc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536776"
---
# <a name="sp_add_targetsvrgrp_member-transact-sql"></a>sp_add_targetsvrgrp_member (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將指定的目標伺服器加入指定的目標伺服器群組中。  
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_targetsvrgrp_member [ @group_name = ] 'group_name' , [ @server_name = ] 'server_name'   
```  
  
## <a name="arguments"></a>引數  
`[ @group_name = ] 'group_name'` 群組的名稱。 *group_name* 是 **sysname**，沒有預設值。  
  
`[ @server_name = ] 'server_name'` 應新增至指定群組的伺服器名稱。 *server_name* 是 **Nvarchar (30) **，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 目標伺服器可以是多個目標伺服器群組的成員。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行這個程式。  
  
## <a name="examples"></a>範例  
 下列範例會加入 `Servers Maintaining Customer Information` 群組，且會將 `LONDON1` 加入這個群組中。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_targetsvrgrp_member  
   @group_name = N'Servers Maintaining Customer Information',  
   @server_name = N'LONDON1' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_delete_targetsvrgrp_member &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetsvrgrp-member-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
