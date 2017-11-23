---
title: "sysmail_help_configure_sp (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_help_configure_sp
- sysmail_help_configure_sp_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmail_help_configure_sp
ms.assetid: e598d4c8-3041-4965-b046-dce3a8e3d3e0
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d799b3d4d319bfda84014e8b520008acdb2c6a30
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysmailhelpconfiguresp-transact-sql"></a>sysmail_help_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示 Database Mail 的組態設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_help_configure_sp  [ [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@parameter_name**  =] **'***parameter_name***'**  
 要擷取之組態設定的名稱。 當指定，則會傳回組態設定的值 **@parameter_value** 輸出參數。 若未 **@parameter_name** 指定，此預存程序傳回的結果集包含所有執行個體中的 Database Mail 組態設定。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 若未 **@parameter_name** 未指定，傳回含下列資料行的結果集。  
  
||||  
|-|-|-|  
|資料行名稱|資料類型|Description|  
|**paramname**|**nvarchar(256)**|組態參數的名稱。|  
|**paramvalue**|**nvarchar(256)**|組態參數值。|  
|**描述**|**nvarchar(256)**|組態參數的描述。|  
  
## <a name="remarks"></a>備註  
 預存程序**sysmail_help_configure_sp**列出執行個體目前的 Database Mail 組態設定。  
  
 當 **@parameter_name** 指定，但沒有輸出參數會提供如 **@parameter_value** ，此預存程序會產生任何輸出。  
  
 預存程序**sysmail_help_configure_sp**處於**msdb**資料庫，擁有者是**dbo**結構描述。 如果目前的資料庫不是，程序必須利用三部分名稱叫**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會顯示如何列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 Database Mail 組態設定。  
  
```  
EXECUTE msdb.dbo.sysmail_help_configure_sp ;  
```  
  
 範例結果集如下 (行的長度經過編輯)：  
  
```  
paramname                       paramvalue      description  
------------------------------- --------------- -----------------------------------------------------------------------------  
AccountRetryAttempts            1               Number of retry attempts for a mail server  
AccountRetryDelay               5000            Delay between each retry attempt to mail server  
DatabaseMailExeMinimumLifeTime  600             Minimum process lifetime in seconds  
DefaultAttachmentEncoding       MIME            Default attachment encoding  
LoggingLevel                    2               Database Mail logging level: normal - 1, extended - 2 (default), verbose - 3  
MaxFileSize                     1000000         Default maximum file size  
ProhibitedExtensions            exe,dll,vbs,js  Extensions not allowed in outgoing mails  
  
```  
  
## <a name="see-also"></a>請參閱＜  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail 預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
