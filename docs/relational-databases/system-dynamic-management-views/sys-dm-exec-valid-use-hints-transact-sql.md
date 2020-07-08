---
title: sys.databases dm_exec_valid_use_hints （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_valid_use_hints
- sys.dm_exec_valid_use_hints_TSQL
- dm_exec_valid_use_hints
- dm_exec_valid_use_hints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_valid_use_hints management view
ms.assetid: 65d50589-39c2-4046-92b6-0c4587d8c593
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 5bcc9db1f2ff0b4395a68025e54b719dc25c31cd
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053454"
---
# <a name="sysdm_exec_valid_use_hints-transact-sql"></a>sys.databases dm_exec_valid_use_hints （Transact-sql）
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

傳回[使用提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)支援的提示名稱。 它會針對每個資料列列出一個提示名稱。  
  
使用此 DMV 來查看使用提示標記法底下所有支援的提示清單。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|提示的名稱。|

如需每個提示的說明，請參閱[查詢提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)。

在 SP1 中引進 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 。
  
## <a name="see-also"></a>另請參閱  
    
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [資料庫相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

