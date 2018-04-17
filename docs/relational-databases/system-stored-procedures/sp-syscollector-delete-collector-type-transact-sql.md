---
title: sp_syscollector_delete_collector_type (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_delete_collector_type
- sp_syscollector_delete_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_delete_collector_type
ms.assetid: 3f32905e-0005-42cb-aef1-7bd04c51fbac
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6afbae5b26890c0018f38550430c44a4c40fda1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spsyscollectordeletecollectortype-transact-sql"></a>sp_syscollector_delete_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  刪除收集器類型的定義。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_delete_collector_type [[ @collector_type_uid = ] 'collector_type_uid' ]  
          , [[ @name = ] 'name' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@collector_type_uid =** ] **'***collector_type_uid***'**  
 這是收集器類型的 GUID。 *collector_type_uid 是否*是**uniqueidentifier**而且必須具有值，如果*名稱*是 NULL。  
  
 [ **@name =** ] **'***name***'**  
 這是收集器類型的名稱。 *名稱*是**sysname**而且必須具有值，如果*collector_type_uid*是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 任一*collector_type_uid*或*名稱*必須有值，不能同時為 NULL。  
  
 如果這種集合類型的集合項目存在，這個程序將會擲回錯誤。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**dc_admin** （具有 EXECUTE 權限） 固定的資料庫角色，才能執行此程序。  
  
## <a name="example"></a>範例  
 此範例會刪除一般 T-SQL 查詢收集器型別。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_delete_collector_type @collector_type_uid = '302E93D1-3424-4be7-AA8E-84813ECF2419';  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)  
  
  
