---
title: sp_help_log_shipping_primary_secondary (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_primary_secondary
- sp_help_log_shipping_primary_secondary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_primary_secondary
ms.assetid: bc0044b4-7831-4ff9-8856-825c76aa9893
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c249564821f40bcd70bcfe367c4970727a5a01a0
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531530"
---
# <a name="sphelplogshippingprimarysecondary-transact-sql"></a>sp_help_log_shipping_primary_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這個預存程序會傳回給定主要資料庫的所有次要資料庫的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_log_shipping_primary_secondary  
[ @primary_database = ] 'primary_database'  
```  
  
## <a name="arguments"></a>引數  
`[ @primary_database = ] 'primary_database'` 是主要伺服器上名稱。 *primary_database&lt*已**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|**secondary_server**|第二個執行個體名稱[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]記錄傳送組態中。|  
|**secondary_database**|記錄傳送組態中之次要資料庫的名稱。|  
  
## <a name="remarks"></a>備註  
 **sp_help_log_shipping_primary_secondary**必須從執行**主要**主要伺服器上的資料庫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行此程序。  
  
## <a name="examples"></a>範例  
 此範例說明如何利用**sp_help_log_shipping_primary_secondary**擷取一份次要資料庫相關聯的主要資料庫[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]。  
  
```  
EXECUTE master.dbo.sp_help_log_shipping_primary_secondary @primary_database=N'AdventureWorks';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
