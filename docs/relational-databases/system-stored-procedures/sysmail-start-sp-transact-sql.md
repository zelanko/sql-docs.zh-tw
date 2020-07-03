---
title: sysmail_start_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_start_sp
- sysmail_start_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_start_sp
ms.assetid: 25fd7bb6-cfdd-463f-bea8-c6fcb805d3f5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e2986749f21982e5eee75772e794a9461545b967
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890834"
---
# <a name="sysmail_start_sp-transact-sql"></a>sysmail_start_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  啟動外部程式使用的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 物件來啟動 Database Mail。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_start_sp  
```  
  
## <a name="arguments"></a>引數  
 None  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，並未啟用或安裝 Database Mail。 請使用 Database Mail 組態精靈來啟用和安裝 Database Mail 物件。  
  
 這個預存程式是在**msdb**資料庫中。 這個預存程序會啟動存放外送訊息要求的 Database Mail 佇列，而且會啟用外部程式的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 啟動作業。  
  
 當啟動佇列時，Database Mail 外部程式可以處理訊息。 此程式可讓您在使用**sysmail_stop_sp**預存程式停止佇列之後，重新開機佇列。  
  
> [!NOTE]  
>  這個預存程序只會啟動 Database Mail 的佇列。 這個預存程序不會啟動資料庫中的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 訊息傳遞。  
  
## <a name="permissions"></a>權限  
 此程式的執行許可權預設為**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會示範如何啟動**msdb**資料庫中的 Database Mail。 這個範例假設您已啟用 Database Mail。  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_start_sp ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail XPs 伺服器設定選項](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)   
 [sysmail_stop_sp &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)   
 [Database Mail 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
