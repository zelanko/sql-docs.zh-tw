---
title: sysmail_help_configure_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_configure_sp
- sysmail_help_configure_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_configure_sp
ms.assetid: e598d4c8-3041-4965-b046-dce3a8e3d3e0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 307b1a1259210890d0b21abdc7a26f0e321e49b3
ms.sourcegitcommit: d855def79af642233cbc3c5909bc7dfe04c4aa23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87122685"
---
# <a name="sysmail_help_configure_sp-transact-sql"></a>sysmail_help_configure_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  顯示 Database Mail 的組態設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_help_configure_sp  [ [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @parameter_name = ] 'parameter_name'`要抓取之設定的名稱。 當指定時，會在** \@ parameter_value** OUTPUT 參數中傳回 configuration 設定的值。 當未指定任何** \@ parameter_name**時，這個預存程式會傳回包含實例中所有 Database Mail 設定的結果集。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 若未指定** \@ parameter_name** ，會傳回具有下列資料行的結果集。  
  
| 資料行名稱 | 資料類型 | 描述 |
| ----------- | --------- | ----------- |
|**paramname**|**nvarchar(256)**|組態參數的名稱。|  
|**paramvalue**|**nvarchar(256)**|組態參數值。|  
|**description**|**nvarchar(256)**|組態參數的描述。|  
  
## <a name="remarks"></a>備註  
 預存程式**sysmail_help_configure_sp**列出實例目前的 Database Mail 設定。  
  
 當指定了** \@ parameter_name** ，但沒有為** \@ parameter_value**提供輸出參數時，這個預存程式不會產生任何輸出。  
  
 預存程式**sysmail_help_configure_sp**在**msdb**資料庫中，而且是由**dbo**架構所擁有。 如果目前的資料庫不是**msdb**，就必須以三部分的名稱叫用此程式。  
  
## <a name="permissions"></a>權限  
 此程式的執行許可權預設為**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
