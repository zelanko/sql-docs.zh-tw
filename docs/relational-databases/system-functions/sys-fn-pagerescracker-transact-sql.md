---
title: sys.fn_PageResCracker (Transact-SQL) | Microsoft Docs
description: Sys.fn_PageResCracker 系統函式的文件。
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_PageResCracker
- sys.fn_PageResCracker_TSQL
- fn_PageResCracker_TSQL
- sys.fn_PageResCracker
- sys.dm_db_page_info
dev_langs:
- TSQL
helpviewer_keywords:
- fn_PageResCracker function
- page_resource
- sys.fn_PageResCracker function
- sys.dm_db_page_info
- page info
author: bluefooted
ms.author: pamela
manager: amitban
ms.openlocfilehash: 2fc7136b60dba47813b9942316ee6fdfbc64f307
ms.sourcegitcommit: fc1739be9b2735b2bb469979936e76ca2a3830f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/03/2019
ms.locfileid: "58899704"
---
# <a name="sysfnpagerescracker-transact-sql"></a>sys.fn_PageResCracker (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

傳回`db_id`， `file_id`，並`page_id`針對給定`page_resource`值。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>引數  
*page_resource*    
是 8 位元組十六進位格式的資料庫頁面資源。
  
## <a name="tables-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|db_id|**ssNoversion**|資料庫識別碼|  
|file_id|**ssNoversion**|檔案識別碼|  
|page_id|**ssNoversion**|頁面識別碼|  
  
## <a name="remarks"></a>備註  
`sys.fn_PageResCracker` 用來將資料庫頁面的 8 位數十六進位表示法轉換成資料列集，其中包含資料庫識別碼，檔案識別碼和頁面的頁面識別碼。   

您可以取得有效的頁面資源中`page_resource`資料行[sys.dm_exec_requests &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)動態管理檢視或[sys.sysprocesses &#40;&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)系統檢視表。 如果使用無效的頁面資源傳回為 NULL。  
主要用法`sys.fn_PageResCracker`是用以協助這些檢視之間的聯結和[sys.dm_db_page_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)動態管理函數，以取得資訊 頁面上，例如它所屬的物件。
  
## <a name="permissions"></a>Permissions  
使用者需求`VIEW SERVER STATE`伺服器的權限。  
  
## <a name="examples"></a>範例  
`sys.fn_PageResCracker`函式可以用於搭配[sys.dm_db_page_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)若要疑難排解頁面相關的等候和中的封鎖[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  下列指令碼是如何使用這些函式，收集資料庫目前正在等候頁面資源的某些類型的所有作用中要求的頁面資訊的範例。 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_db_page_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [sys.sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
