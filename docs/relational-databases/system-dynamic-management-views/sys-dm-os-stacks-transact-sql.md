---
title: sys.dm_os_stacks (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_stacks
- dm_os_stacks_TSQL
- sys.dm_os_stacks
- sys.dm_os_stacks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_stacks dynamic management view
ms.assetid: a69b06c4-28f0-4535-8fa1-9f132db4d916
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c31bf39c4f133aa6f693614845cb54a5cf2bfc6f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899761"
---
# <a name="sysdmosstacks-transact-sql"></a>sys.dm_os_stacks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  這份動態管理檢視可供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在內部使用，以執行下列動作：  
  
-   追蹤偵錯資料，例如未完成的配置。  
  
-   在元件假設發出特定呼叫之處，假設或驗證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件使用的邏輯。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary(8)**|這項堆疊配置的唯一位址。 不可為 Null。|  
|**frame_index**|**int**|每一行代表一個函式呼叫，以遞增順序排序的特定框架索引時**stack_address**，會傳回完整呼叫堆疊。 不可為 Null。|  
|**frame_address**|**varbinary(8)**|函數呼叫的位址。 不可為 Null。|  
  
## <a name="remarks"></a>備註  
 **sys.dm_os_stacks** ，伺服器和其他元件的符號必須出現在伺服器上正確顯示的資訊。  
  
## <a name="permissions"></a>Permissions

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 上，需要資料庫中的 `VIEW DATABASE STATE` 權限。   


## <a name="see-also"></a>另請參閱  
  [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
