---
description: 'managed_backup fn_is_master_switch_on (Transact-sql) '
title: managed_backup fn_is_master_switch_on (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_is_master_switch_on
- fn_is_master_switch_on_TSQL
- smart_admin.fn_is_master_switch_on
- smart_admin.fn_is_master_switch_on_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_is_master_switch_on
- fn_is_master_switch_on
ms.assetid: e8c2108d-b104-46cb-9645-a15f46112c86
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b73778128e18d2937e2866ba697ab297698f6574
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419472"
---
# <a name="managed_backupfn_is_master_switch_on-transact-sql"></a>managed_backup fn_is_master_switch_on (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  傳回 SQL Server 執行個體上的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]作業狀態。  
  
 使用這個函數可取得[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的目前狀態。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
managed_backup.fn_is_master_switch_on ()  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引數  
 None  
  
## <a name="return-type"></a>傳回類型  
 **位**  
  
 1 = [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 作用中，0 = [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 已暫停。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要函數的 SELECT 權限。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 受控備份到 Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
