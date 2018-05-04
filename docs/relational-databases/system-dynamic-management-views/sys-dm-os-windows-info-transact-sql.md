---
title: sys.dm_os_windows_info (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_windows_info
- dm_os_windows_info_TSQL
- sys.dm_os_windows_info
- sys.dm_os_windows_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_windows_info dynamic management view
ms.assetid: adc81283-fdc2-46c0-bb48-abe82bbf2459
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e4a61738fe95fd2c05686b1610d3d4ab1bd5103
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmoswindowsinfo-transact-sql"></a>sys.dm_os_windows_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回一個顯示 Windows 作業系統版本資訊的資料列。  
  
  僅適用於在 Windows 上執行的 SQL Server。 若要查看類似的資訊適用於非 Windows 主機，例如： Linux 上執行的 SQL Server 使用[sys.dm_os_host_info &#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)。 
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**windows_release**|**nvarchar(256)**|對於 Windows，傳回的版次號碼。 如需值和描述的清單，請參閱[作業系統版本 (Windows)](http://msdn.microsoft.com/library/ms724832\(VS.85\).aspx)。 不能是 NULL。|  
|**windows_service_pack_level**|**nvarchar(256)**| 適用於 Windows、 傳回 service pack 號碼。 不能是 NULL。 |  
|**windows_sku**|**int**|適用於 Windows、 會傳回 Windows 存貨保持單元 (SKU) 識別碼。 如需 SKU Id 和描述的清單，請參閱[GetProductInfo 函數](http://msdn.microsoft.com/library/ms724358.aspx)。 可為 Null。 |  
|**os_language_version**|**int**| 適用於 Windows、 會傳回作業系統的 Windows 地區設定識別碼 (LCID)。 如需 LCID 值和描述的清單，請參閱[microsoft 指派的地區設定識別碼](http://go.microsoft.com/fwlink/?LinkId=208080)。 不能是 NULL。|  
  
  
## <a name="permissions"></a>Permissions  
Sys.dm_os_windows_info 上的 SELECT 權限預設會授與 public 角色。 已被撤銷，需要在伺服器上的 VIEW SERVER STATE 權限。  

## <a name="limitations-and-restrictions"></a>限制事項
若要查看資訊在非 Windows 主機，例如： Linux 上執行的 sql 使用[sys.dm_os_host_info &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)。 
  
## <a name="examples"></a>範例  
 下列範例會傳回所有資料行從**sys.dm_os_windows_info**檢視。  
  
```  
SELECT windows_release, windows_service_pack_level, windows_sku, os_language_version  
FROM sys.dm_os_windows_info;  
```  
  
 範例結果集如下：  
  
 `windows_release  windows_service_pack_level   windows_sku   os_language_version`  
  
 `---------------  ---------------------------  ------------  -------------------`  
  
 `6.0              Service Pack 2                4            1033`  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)  
  
  

