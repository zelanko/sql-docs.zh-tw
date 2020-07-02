---
title: sys.databases dm_os_stacks （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 869ebff08a3bb20ea531f3a1bdcdf59eafdcdceb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718759"
---
# <a name="sysdm_os_stacks-transact-sql"></a>sys.dm_os_stacks (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  這份動態管理檢視可供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在內部使用，以執行下列動作：  
  
-   追蹤偵錯資料，例如未完成的配置。  
  
-   在元件假設發出特定呼叫之處，假設或驗證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件使用的邏輯。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**stack_address**|**varbinary(8)**|這項堆疊配置的唯一位址。 不可為 Null。|  
|**frame_index**|**int**|每一行都代表一個函式呼叫，當特定**stack_address**以根據框架索引的遞增順序進行排序時，會傳回完整的呼叫堆疊。 不可為 Null。|  
|**frame_address**|**varbinary(8)**|函數呼叫的位址。 不可為 Null。|  
  
## <a name="remarks"></a>備註  
 **dm_os_stacks**要求伺服器和其他元件的符號必須存在於伺服器上，才能正確顯示資訊。  
  
## <a name="permissions"></a>權限

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在高階 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 層級上，需要 `VIEW DATABASE STATE` 資料庫的許可權。 在 [ [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   


## <a name="see-also"></a>另請參閱  
  [SQL Server 作業系統相關的動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
