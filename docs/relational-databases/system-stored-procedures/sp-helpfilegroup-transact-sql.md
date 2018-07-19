---
title: sp_helpfilegroup (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpfilegroup_TSQL
- sp_helpfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfilegroup
ms.assetid: 619716b5-95dc-4538-82ae-4b90b9da8ebc
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 61e297999776254e85372c4b6ce25927396fdff6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33260784"
---
# <a name="sphelpfilegroup-transact-sql"></a>sp_helpfilegroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回目前資料庫之相關檔案群組的名稱和屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpfilegroup [ [ @filegroupname = ] 'name' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@filegroupname =** ] **'***name***'**  
 這是目前資料庫中任何檔案群組的邏輯名稱。 *名稱*是**sysname**，預設值是 NULL。 如果*名稱*未指定，會列出目前資料庫中的所有檔案群組，並顯示只有第一個顯示的結果集的結果集一節。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**groupname**|**sysname**|檔案群組的名稱。|  
|**groupid**|**smallint**|數值檔案群組識別碼。|  
|**filecount**|**int**|檔案群組中的檔案數目。|  
  
 如果*名稱*已指定，會傳回一個資料列群組中每個檔案。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**file_in_group**|**sysname**|檔案群組中該檔案的邏輯名稱。|  
|**fileid**|**smallint**|數值檔案識別碼。|  
|**filename**|**nchar(260)**|檔案的實體名稱 (包含目錄路徑在內)。|  
|**size**|**nvarchar(15)**|檔案大小 (以 KB 為單位)。|  
|**maxsize**|**nvarchar(15)**|檔案的大小上限。<br /><br /> 這是檔案所能成長的大小上限。 這個欄位中的 UNLIMITED 值指出，檔案將成長到磁碟已滿。|  
|**成長**|**nvarchar(15)**|檔案的成長遞增。 這表示每次需要新空間時，檔案所增加的空間量。<br /><br /> 0 = 檔案是固定大小，不會成長。|  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-all-filegroups-in-a-database"></a>A. 傳回資料庫中所有的檔案群組  
 下列範例會傳回 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫中檔案群組的相關資訊。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup;  
GO  
```  
  
### <a name="b-returning-all-files-in-a-filegroup"></a>B. 傳回檔案群組中所有的檔案  
 下列範例會傳回 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫的 `PRIMARY` 檔案群組中之所有檔案的相關資訊。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup 'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料庫檔案與檔案群組](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
