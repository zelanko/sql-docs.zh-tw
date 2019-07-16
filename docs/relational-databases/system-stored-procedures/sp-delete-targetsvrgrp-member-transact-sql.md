---
title: sp_delete_targetsvrgrp_member (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_targetsvrgrp_member_TSQL
- sp_delete_targetsvrgrp_member
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetsvrgrp_member
ms.assetid: 178a38d9-9b19-4648-95d7-e1397110d14c
author: stevestein
ms.author: sstein
ms.openlocfilehash: dcf3788480a6e3dbb3bde20ef3f9e6a43269c9e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026735"
---
# <a name="spdeletetargetsvrgrpmember-transact-sql"></a>sp_delete_targetsvrgrp_member (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目標伺服器群組中移除目標伺服器。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_targetsvrgrp_member [ @group_name = ] 'group_name' , [ server_name = ] 'server_name'   
```  
  
## <a name="arguments"></a>引數  
`[ @group_name = ] 'group_name'` 群組的名稱。 *group_name*已**sysname**，沒有預設值。  
  
`[ @server_name = ] 'server_name'` 若要從指定的群組移除伺服器的名稱。 *server_name*已**nvarchar(30)** ，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>Permissions  
 若要執行這個預存程序，使用者必須授與**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會從 'Servers Maintaining Customer Information' 群組中，移除 `LONDON1` 伺服器。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_targetsvrgrp_member   
    @group_name = N'Servers Maintaining Customer Information',  
    @server_name = N'LONDON1';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_targetsvrgrp_member &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-add-targetsvrgrp-member-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
