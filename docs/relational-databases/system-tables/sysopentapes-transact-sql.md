---
description: sysopentapes (Transact-SQL)
title: sysopentapes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d97f19143a2d1128f6164543847cfbc27b275877
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473133"
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對目前開啟的每個磁帶裝置，各包含一個資料列。 這個視圖會儲存在 **master** 資料庫中。  
  
> [!IMPORTANT]  
>  將這份系統資料表當做檢視表併入的目的，是為了與舊版相容。 請改用 [sys. dm_io_backup_tapes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) 動態管理檢視。  
  
> [!NOTE]  
>  您無法卸載 **sysopentapes** view。  

  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**openTape**|**Nvarchar (64) **|開啟的磁帶裝置的實體檔案名稱。 如需開啟和釋放磁帶裝置的詳細資訊，請參閱 [BACKUP &#40;transact-sql&#41;](../../t-sql/statements/backup-transact-sql.md) 和 [RESTORE &#40;transact-sql&#41;](../../t-sql/statements/restore-statements-transact-sql.md)。|  
  
## <a name="permissions"></a>權限  
 使用者需要伺服器的 VIEW SERVER STATE 權限。  
  
  
