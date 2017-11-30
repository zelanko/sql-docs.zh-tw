---
title: "sysmail_stop_sp (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
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
- sysmail_stop_sp_TSQL
- sysmail_stop_sp
dev_langs: TSQL
helpviewer_keywords: sysmail_stop_sp
ms.assetid: 045ee36f-5bf0-4626-b5ee-e84db06ce16f
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f707d12e77f366d34f48663f623145867bff5c5
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="sysmailstopsp-transact-sql"></a>sysmail_stop_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  停止外部程式使用的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 物件來停止 Database Mail。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_stop_sp  
```  
  
## <a name="arguments"></a>引數  
 無  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 這個預存程序處於**msdb**資料庫。  
  
 這個預存程序會停止存放外送訊息要求的 Database Mail 佇列，而且會關閉外部程式的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 啟用作業。  
  
 當佇列停止時，Database Mail 外部程式不會處理訊息。 這個預存程序可讓您停止 Database Mail 來進行疑難排解或維護。  
  
 若要啟動 Database Mail，請使用**sysmail_start_sp**。 請注意， **sp_send_dbmail**仍接受郵件時[!INCLUDE[ssSB](../../includes/sssb-md.md)]物件都已停止。  
  
> [!NOTE]  
>  這個預存程序只會停止 Database Mail 的佇列。 這個預存程序不會停用資料庫中的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 訊息傳遞。 這個預存程序不會停用 Database Mail 擴充預存程序來縮減介面區域。 若要停用擴充預存程序，請參閱[Database Mail Xp 選項](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)的**sp_configure**系統預存程序。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例示範中停止 Database Mail **msdb**資料庫。 這個範例假設您已啟用 Database Mail。  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_stop_sp ;  
GO  
```  
  
## <a name="see-also"></a>請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_start_sp &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [Database Mail 預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
