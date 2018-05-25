---
title: sys.dm_os_host_info (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sys.dm_os_host_info
- sys.dm_os_host_info_TSQL
- dm_os_host_info
- dm_os_host_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_host_info dynamic management view
ms.assetid: 9bb6ef86-957b-4ca1-ad20-ca2f8460a86d
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 0aa5f28f52c9d0df4e942809612e1ca59a1cb3c5
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmoshostinfo-transact-sql"></a>sys.dm_os_host_info (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

傳回一個資料列會顯示作業系統版本資訊。  
  
|資料行名稱 |資料類型 |Description |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar(256)** |一種作業系統： Windows 或 Linux |
|**host_distribution** |**nvarchar(256)** |作業系統的描述。 |
|**host_release**|**nvarchar(256)**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 作業系統版本 (版本號碼)。 如需值和描述的清單，請參閱[作業系統版本 (Windows)](http://msdn.microsoft.com/library/ms724832\(VS.85\).aspx)。 <br> 適用於 Linux，會傳回空字串。 |  
|**host_service_pack_level**|**nvarchar(256)**|Windows 作業系統的 Service Pack 層級。 <br> 適用於 Linux，會傳回空字串。 |  
|**host_sku**|**int**|Windows 庫存單位 (SKU) 識別碼。 如需 SKU Id 和描述的清單，請參閱[GetProductInfo 函數](http://msdn.microsoft.com/library/ms724358.aspx)。 可為 Null。 <br> 適用於 Linux，則傳回 NULL。 |  
|**os_language_version**|**int**|作業系統的 Windows 地區設定識別碼 (LCID)。 如需 LCID 值和描述的清單，請參閱[microsoft 指派的地區設定識別碼](http://go.microsoft.com/fwlink/?LinkId=208080)。 不可為 null。|  

## <a name="remarks"></a>備註  
此檢視是類似[sys.dm_os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)，加入資料行來區分 Windows 和 Linux。
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
`SELECT`權限`sys.dm_os_host_info`會授與`public`預設角色。 已被撤銷，需要`VIEW SERVER STATE`伺服器的權限。   
 
>  [!CAUTION]
>  版起[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]CTP 1.3 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 17 版需要`SELECT`權限`sys.dm_os_host_info`才能連接到[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 如果`SELECT`權限撤銷`public`，使用的登入`VIEW SERVER STATE`權限可以連線至最新版本的 SSMS。 (其他工具，例如`sqlcmd.exe`不可以連接`SELECT`權限`sys.dm_os_host_info`。)

  
## <a name="examples"></a>範例  
 下列範例會傳回所有資料行從**sys.dm_os_host_info**檢視。  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

以下是在 Windows 上設定的範例結果：
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |1033 |  

以下是在 Linux 上設定的範例結果：
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULL   |1033 |  

  
## <a name="see-also"></a>另請參閱  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
 

