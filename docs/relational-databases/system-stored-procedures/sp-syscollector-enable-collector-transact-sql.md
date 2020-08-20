---
description: sp_syscollector_enable_collector (Transact-SQL)
title: sp_syscollector_enable_collector (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_enable_collector
- sp_syscollector_enable_collector_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_enable_collector
- data collector [SQL Server], stored procedures
ms.assetid: 53ff2b0d-b7da-4e3d-8f3d-35e857bc3720
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3c7563b12214f52f1c89428f50a50dbd021cd467
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464018"
---
# <a name="sp_syscollector_enable_collector-transact-sql"></a>sp_syscollector_enable_collector (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  啟用資料收集器。 由於每部伺服器只有一個資料收集器，因此不需要使用任何參數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
dbo.sp_syscollector_enable_collector   
```  
  
## <a name="arguments"></a>引數  
 None  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 預設為伺服器上的資料收集器。  
  
## <a name="permissions"></a>權限  
 需要 **dc_admin** 或 **dc_operator** (具有 EXECUTE 權限) 固定資料庫角色中的成員資格，才能執行此程序。  
  
## <a name="examples"></a>範例  
 下列範例會啟用資料收集器。  
  
```sql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_enable_collector;  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
