---
title: sysmail_help_status_sp (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c08985b4fe50a657c08de40f112776cf064b2846
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47614250"
---
# <a name="sysmailhelpstatussp-transact-sql"></a>sysmail_help_status_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示 Database Mail 佇列的狀態。 使用**sysmail_start_sp**可啟動 Database Mail 佇列並**sysmail_stop_sp**可停止 Database Mail 佇列。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_help_status_sp  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**狀態**|**nvarchar(7)**|Database Mail 的狀態。 可能的值為**STARTED**並**STOPPED**。|  
  
## <a name="permissions"></a>Permissions  
 根據預設，只有成員**sysadmin**固定的伺服器角色可以存取這個程序。  
  
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
 [sysmail_start_sp &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [sysmail_stop_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)  
  
  
