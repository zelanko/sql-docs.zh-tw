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
ms.openlocfilehash: c6fcaa491f7d42e255ed329a8e16798437aa2c7a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67936797"
---
# <a name="sysdm_exec_valid_use_hints-transact-sql"></a>sys.databases dm_exec_valid_use_hints （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

傳回[使用提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)支援的提示名稱。 它會針對每個資料列列出一個提示名稱。  
  
使用此 DMV 來查看使用提示標記法底下所有支援的提示清單。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|提示的名稱。|

如需每個提示的說明，請參閱[查詢提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)。

在 SP1 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]中引進。
  
## <a name="see-also"></a>另請參閱  
    
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [資料庫相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

