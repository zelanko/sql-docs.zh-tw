---
title: p (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysopentapes
- sysopentapes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], sysopentapes system table
- sysopentapes system table
ms.assetid: c066ca9b-9cfd-46b1-90a3-5c8dc9e7b6ae
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c6f368356df76c68594443ac5a981ebf8f20bec2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260378"
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對目前開啟的每個磁帶裝置，各包含一個資料列。 這份檢視儲存在**主要**資料庫。  
  
> [!IMPORTANT]  
>  將這份系統資料表當做檢視表併入的目的，是為了與舊版相容。 請改用[sys.dm_io_backup_tapes &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md)動態管理檢視。  
  
> [!NOTE]  
>  您無法卸除**sysopentapes**檢視。  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar(64)**|開啟的磁帶裝置的實體檔案名稱。 如需有關開啟和釋出磁帶裝置的詳細資訊，請參閱[備份&#40;TRANSACT-SQL&#41; ](../../t-sql/statements/backup-transact-sql.md)和[還原&#40;TRANSACT-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)。|  
  
## <a name="permissions"></a>Permissions  
 使用者需要伺服器的 VIEW SERVER STATE 權限。  
  
  
