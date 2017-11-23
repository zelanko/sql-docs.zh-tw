---
title: "sp_helpfile (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpfile
- sp_helpfile_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpfile
ms.assetid: 1546e0ae-5a99-4e01-9eb9-d147fa65884c
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 41f6330563349f6903b4514b1c8da3919e9dad0b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpfile-transact-sql"></a>sp_helpfile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回目前資料庫之相關檔案的實體名稱和屬性。 請利用這個預存程序來判斷伺服器所要附加或卸離的檔案名稱。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpfile [ [ @filename= ] 'name' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@filename =** ] **'***名稱***'**  
 這是目前資料庫中任何檔案的邏輯名稱。 *名稱*是**sysname**，預設值是 NULL。 如果*名稱*是未指定，會傳回目前資料庫中的所有檔案的屬性。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|邏輯檔案名稱。|  
|**fileid**|**smallint**|檔案的數值識別碼。 如果不會傳回*名稱*指定*。*|  
|**檔名**|**nchar(260)**|實體檔案名稱。|  
|**檔案群組**|**sysname**|檔案所屬的檔案群組。<br /><br /> NULL = 檔案是記錄檔。 它永遠不在檔案群組中。|  
|**大小**|**nvarchar （15)**|檔案大小 (以 KB 為單位)。|  
|**maxsize**|**nvarchar （15)**|檔案所能成長的大小上限。 這個欄位中的 UNLIMITED 值指出，檔案將成長到磁碟已滿。|  
|**成長**|**nvarchar （15)**|檔案的成長遞增。 這表示每次需要新空間時，檔案所增加的空間量。<br /><br /> 0 = 檔案是固定大小，不會成長。|  
|**使用方式**|**varchar(9)**|對於資料檔中，這個值是**'僅限資料'**和記錄檔的值是**僅限記錄'**。|  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中之檔案的相關資訊。  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfile;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [Database Engine 預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfilegroup &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料庫檔案與檔案群組](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
