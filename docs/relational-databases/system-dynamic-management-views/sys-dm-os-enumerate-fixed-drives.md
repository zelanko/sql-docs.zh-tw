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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fa5834c14bfb1fafe3123c28a60359d64d059dfc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "71342513"
---
# <a name="sysdm_os_enumerate_fixed_drives-transact-sql"></a>sys.databases dm_os_enumerate_fixed_drives （Transact-sql）

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

SQL Server 2019 中引進。

列舉掛接到磁碟機號的磁片`C:\`區，例如。

|資料行名稱|資料類型|描述|
|-----------------|---------------|-----------------|  
|`fixed_drive_path`|`nvarchar(512)`|磁片區的路徑，例如`C:\`。|  
|`drive_type`|`int`|磁片磁碟機類型的程式碼。 請[ `GetDriveTypeW`參閱](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew)函式。|
|`drive_type_desc`|`nvarchar(512)`|磁片磁碟機類型的描述。 請[ `GetDriveTypeW`參閱](/windows/win32/api/fileapi/nf-fileapi-getdrivetypew)函式。|
|`free_space_in_bytes`|`bigint`|磁片可用空間（以位元組為單位）。|

## <a name="permissions"></a>權限

使用者必須具有`VIEW SERVER STATE`伺服器的許可權。

## <a name="see-also"></a>另請參閱  

 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [I/o 相關的動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
