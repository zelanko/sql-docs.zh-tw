---
title: sp_drop_agent_parameter （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_drop_agent_parameter_TSQL
- sp_drop_agent_parameter
helpviewer_keywords:
- sp_drop_agent_parameter
ms.assetid: b99e65ff-9cca-4dce-a2ce-2968de23a76a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c284a3cb2601f66d48dd61ad7df6017052964aaa
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85860186"
---
# <a name="sp_drop_agent_parameter-transact-sql"></a>sp_drop_agent_parameter (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從**MSagent_parameters**資料表中的設定檔卸載一或所有參數。 這個預存程序執行於在任何資料庫執行代理程式的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_drop_agent_parameter [ @profile_id = ] profile_id  
    [ , [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @profile_id = ] profile_id`這是要卸載參數之設定檔的識別碼。 *profile_id*是**int**，沒有預設值。  
  
`[ @parameter_name = ] 'parameter_name'`這是要卸載之參數的名稱。 *parameter_name*是**sysname**，預設值是 **%** 。 如果為 **%** ，則會卸載指定之設定檔的所有參數。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_drop_agent_parameter**用於所有類型的複寫中。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_drop_agent_parameter**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
