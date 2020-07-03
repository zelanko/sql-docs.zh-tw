---
title: sys.databases dm_os_enumerate_fixed_drives （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 09/18/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_enumerate_fixed_drives
- sys.dm_os_enumerate_fixed_drives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_enumerate_fixed_drives dynamic management view
ms.assetid: 2e27489e-cf69-4a89-9036-77723ac3de66
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c8b243a269454bb1480051f50ab52d83d5fde80b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898772"
---
# <a name="sysdm_os_enumerate_fixed_drives-transact-sql"></a>sys.databases dm_os_enumerate_fixed_drives （Transact-sql）

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

SQL Server 2019 中引進。

列舉掛接到磁碟機號的磁片區，例如 `C:\` 。

|資料行名稱|資料類型|描述|
|-----------------|---------------|-----------------|  
|`fixed_drive_path`|`nvarchar(512)`|磁片區的路徑，例如 `C:\` 。|  
|`drive_type`|`int`|磁片磁碟機類型的程式碼。 請[ `GetDriveTypeW` 參閱](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew)函式。|
|`drive_type_desc`|`nvarchar(512)`|磁片磁碟機類型的描述。 請[ `GetDriveTypeW` 參閱](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew)函式。|
|`free_space_in_bytes`|`bigint`|磁片可用空間（以位元組為單位）。|

## <a name="permissions"></a>權限

使用者必須具有 `VIEW SERVER STATE` 伺服器的許可權。

## <a name="see-also"></a>另請參閱  

 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [I/o 相關的動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
