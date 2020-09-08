---
description: sysmail_help_status_sp (Transact-SQL)
title: sysmail_help_status_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_status_sp
- sysmail_help_status_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_status_sp
ms.assetid: b44277c6-81e8-4b4d-85b3-a2f04d602e7a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b40f86ddb3fd349e11f25e655ac06e757c559a56
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89525325"
---
# <a name="sysmail_help_status_sp-transact-sql"></a>sysmail_help_status_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  顯示 Database Mail 佇列的狀態。 使用 **sysmail_start_sp** 啟動 Database Mail 佇列和 **sysmail_stop_sp** 以停止 Database Mail 佇列。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_help_status_sp  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**狀態**|**Nvarchar (7) **|Database Mail 的狀態。 可能的值為 [ **已啟動** ] 和 [ **已停止**]。|  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠存取此程式。  
  
## <a name="examples"></a>範例  
 下列範例會顯示 Database Mail 的狀態。  
  
```  
EXECUTE msdb.dbo.sysmail_help_status_sp ;  
GO  
```  
  
 結果集：  
  
```  
Status  
-------  
STARTED  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail 外部程式](../../relational-databases/database-mail/database-mail-external-program.md)   
 [sysmail_start_sp &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [sysmail_stop_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)  
  
  
