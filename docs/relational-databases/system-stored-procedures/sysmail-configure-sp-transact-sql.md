---
title: sysmail_configure_sp & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_configure_sp_TSQL
- sysmail_configure_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_configure_sp
ms.assetid: 73b33c56-2bff-446a-b495-ae198ad74db1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: abe47df497b61d35c66bfebfb3ba5a75fad0e183
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588552"
---
# <a name="sysmailconfiguresp-transact-sql"></a>sysmail_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更 Database Mail 的組態設定。 使用指定的組態設定**sysmail_configure_sp**套用至整個[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_configure_sp [ [ @parameter_name = ] 'parameter_name' ]  
    [ , [ @parameter_value = ] 'parameter_value' ]  
    [ , [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>引數  
 [**@parameter_name** =] **'**_parameter_name_**'**  
 要變更的參數名稱。  
  
 [**@parameter_value** =] **'**_parameter_value_**'**  
 參數的新值。  
  
 [**@description** =] **'**_描述_**'**  
 參數的描述。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 Database Mail 使用下列參數：  
  
||||  
|-|-|-|  
|參數名稱|描述|預設值|  
|*AccountRetryAttempts*|外部郵件處理序嘗試利用指定設定檔中的每個帳戶來傳送電子郵件訊息的次數。|**1**|  
|*AccountRetryDelay*|在各次嘗試傳送訊息之間，外部郵件處理序所等待的時間 (以秒為單位)。|**5000**|  
|*DatabaseMailExeMinimumLifeTime*|外部郵件處理序維持使用中的最短時間 (以秒為單位)。 當 Database Mail 傳送許多訊息時，請增加這個值，使 Database Mail 保持在使用中，以避免頻繁的啟動和停止所帶來的負擔。|**600**|  
|*DefaultAttachmentEncoding*|電子郵件附件的預設編碼。|MIME|  
|*MaxFileSize*|附件的大小上限 (以位元組為單位)。|**1000000**|  
|*Sysmail_configure_sp*|無法作為電子郵件訊息附件來傳送的副檔名清單 (以逗號分隔)。|**exe、 dll、 vbs、 js**|  
|*LoggingLevel*|指定哪些訊息要記錄在 Database Mail 記錄中。 數值下列其中一項：<br /><br /> 1 - 這是標準模式。 只記錄錯誤。<br /><br /> 2 - 這是擴充模式。 記錄錯誤、警告和參考訊息。<br /><br /> 3 - 這是詳細資訊模式。 記錄錯誤、警告、參考訊息、成功訊息和其他內部訊息。 進行疑難排解時，請使用此模式。|**2**|  
  
 預存程序**sysmail_configure_sp**處於**msdb**資料庫中，擁有者**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 **A.設定 Database Mail 設為每個帳戶重試 10 次**  
  
 下列範例會顯示如何將 Database Mail 設為每個帳戶重試 10 次，之後，便認定無法連上這個帳戶。  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'AccountRetryAttempts', '10' ;  
```  
  
 **B.設定附件大小上限設為 2 mb**  
  
 下列範例會顯示如何將附件大小上限設為 2 MB。  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'MaxFileSize', '2097152' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_help_configure_sp &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sysmail-help-configure-sp-transact-sql.md)   
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
