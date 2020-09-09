---
description: sp_syscollector_delete_collector_type (Transact-SQL)
title: sp_syscollector_delete_collector_type (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cc4cdc682ec2230b7d0f3136feb683789b38c06b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547329"
---
# <a name="sp_syscollector_delete_collector_type-transact-sql"></a>sp_syscollector_delete_collector_type (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  刪除收集器類型的定義。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_delete_collector_type [[ @collector_type_uid = ] 'collector_type_uid' ]  
          , [[ @name = ] 'name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @collector_type_uid = ] 'collector_type_uid'` 這是收集器型別的 GUID。 *collector_type_uid* 為 **uniqueidentifier** ，且 *名稱* 為 Null 時必須有值。  
  
`[ @name = ] 'name'` 這是收集器型別的名稱。 *名稱* 是 **sysname** ，而且如果 *collector_type_uid* 為 Null，則必須有值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 *Collector_type_uid*或*名稱*都必須有值，兩者都不能是 Null。  
  
 如果這種集合類型的集合項目存在，這個程序將會擲回錯誤。  
  
## <a name="permissions"></a>權限  
 需要 **dc_admin** (中具有 execute 許可權) 固定資料庫角色的成員資格，才能執行此程式。  
  
## <a name="example"></a>範例  
 此範例會刪除一般 T-SQL 查詢收集器型別。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_delete_collector_type @collector_type_uid = '302E93D1-3424-4be7-AA8E-84813ECF2419';  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
