---
title: sys.sp_cdc_stop_job (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_stop_job_TSQL
- sys.sp_cdc_stop_job
- sp_cdc_stop_job_TSQL
- sp_cdc_stop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_stop_job
ms.assetid: 421fc21c-c7a4-407c-8b31-359273b68c63
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 22372eb9bbd32018e93cd8cd2230741656685987
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43026482"
---
# <a name="sysspcdcstopjob-transact-sql"></a>sys.sp_cdc_stop_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  停止目前資料庫的異動資料擷取清除或擷取作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_stop_job [ [ @job_type = ] 'job_type' ]  
```  
  
## <a name="arguments"></a>引數  
 [[  **@job_type=** ] **'* * * job_type&lt*']  
 要加入的作業類型。 *job_type&lt*已**nvarchar(20)** 預設值是**擷取**。 有效輸入如下**擷取**並**清除**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 管理員可以使用 sys.sp_cdc_stop_job 來明確停止擷取作業或清除作業。  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 固定資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會停止 `AdventureWorks2012` 資料庫的清除作業。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_stop_job @job_type = N'capture';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [dbo.cdc_jobs &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_start_job &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md)  
  
  
