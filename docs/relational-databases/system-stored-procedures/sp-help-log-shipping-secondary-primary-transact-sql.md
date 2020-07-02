---
title: sp_help_log_shipping_secondary_primary （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_secondary_primary
- sp_help_log_shipping_secondary_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_secondary_primary
ms.assetid: 1310fdaf-edb5-4294-9739-7fb37c2c2cb5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c8876dd3a23d9efb1c658d2412efb169daef1b62
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85634397"
---
# <a name="sp_help_log_shipping_secondary_primary-transact-sql"></a>sp_help_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  這個預存程序會擷取次要伺服器上所指定主要資料庫的設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server' OR  
[ @primary_database = ] 'primary_database'  
```  
  
## <a name="arguments"></a>引數  
`[ @primary_server = ] 'primary_server'`記錄傳送設定中之主要實例的名稱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 。 *primary_server*是**sysname** ，不能是 Null。  
  
`[ @primary_database = ] 'primary_database'`這是主伺服器上的資料庫名稱。 *primary_database*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 結果集包含來自**backup_destination_directory** **secondary_id**、 **primary_server**、 **primary_database**、 **backup_source_directory**、 **file_retention_period**、 **copy_job_id**、 **restore_job_id**、 **monitor_server**、 **monitor_server_security_mode**、 **log_shipping_secondary**的資料行。  
  
## <a name="remarks"></a>備註  
 **sp_help_log_shipping_secondary_primary**必須從次要伺服器的**master**資料庫中執行。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行此程式。  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
