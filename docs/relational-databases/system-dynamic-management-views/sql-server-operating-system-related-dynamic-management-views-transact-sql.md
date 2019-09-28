---
title: 與作業系統相關的動態管理檢視 SQL Server （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operating systems [SQL Server], dynamic management objects
- SQL Operating System dynamic management objects [SQL Server]
- SQL OS dynamic management objects [SQL Server]
- dynamic management objects [SQL Server], SQL OS
ms.assetid: 3030c86a-0a74-4fed-ac0f-392e244cb965
author: stevestein
ms.author: sstein
ms.openlocfilehash: 862f54351eb67d2170d8e9806347eb8608178c23
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/27/2019
ms.locfileid: "71342044"
---
# <a name="sql-server-operating-system-related-dynamic-management-views-transact-sql"></a>SQL Server 作業系統相關的動態管理檢視 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

本節記載與 @no__t 0 作業系統（SQLOS）相關聯的動態管理檢視（DMV）。 SQLOS 負責管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定的作業系統資源。

SQLOS Dmv 會列在目錄中。 這些和都會命名為 `sys.dm_os_<description>`。

 下列 @no__t 0 作業系統相關的動態管理檢視會 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]。  
  
|||  
|-|-|  
|**sys.dm_os_function_symbolic_name**|**sys.dm_os_ring_buffers**|  
|**sys.dm_os_memory_allocations**|**sys.dm_os_sublatches**|  
|**sys.dm_os_worker_local_storage**||  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

