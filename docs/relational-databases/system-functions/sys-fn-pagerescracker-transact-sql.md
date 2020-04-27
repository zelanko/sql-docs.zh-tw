---
title: sys.databases fn_PageResCracker （Transact-sql） |Microsoft Docs
description: Sys. fn_PageResCracker 系統函數的檔。
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
ms.openlocfilehash: 6d8203979a0afdca1ae78b9bd51723c906c40ea2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "68267068"
---
# <a name="sysfn_pagerescracker-transact-sql"></a>sys.databases fn_PageResCracker （Transact-sql）
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

傳回指定`db_id` `page_resource`值`file_id`的、 `page_id`和。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>引數  
*page_resource*    
這是資料庫頁面資源的8位元組十六進位格式。
  
## <a name="tables-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|db_id|**int**|資料庫識別碼|  
|file_id|**int**|檔案識別碼|  
|page_id|**int**|頁面識別碼|  
  
## <a name="remarks"></a>備註  
`sys.fn_PageResCracker`是用來將資料庫頁面的8位元組十六進位表示轉換成包含頁面之資料庫識別碼、檔案識別碼和頁面識別碼的資料列集。   

您可以從 sys.databases 的資料`page_resource`行取得有效的頁面資源[dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)動態管理檢視或[sysprocesses &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)系統檢視。 如果使用不正確頁面資源，則傳回值為 Null。  
的主要用途`sys.fn_PageResCracker`是加速這些 views 與 sys.databases 之間的聯結， [dm_db_page_info &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)動態管理函數，以取得頁面的相關資訊，例如它所屬的物件。
  
## <a name="permissions"></a>權限  
使用者需要`VIEW SERVER STATE`伺服器的許可權。  
  
## <a name="examples"></a>範例  
函式可與 sys.databases 搭配使用， [dm_db_page_info &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)來針對頁面相關的等候和封鎖進行疑難排解[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `sys.fn_PageResCracker`  下列腳本是一個範例，說明如何使用這些函式來收集目前正在等待某種頁面資源類型之所有使用中要求的資料庫頁面資訊。 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>另請參閱  
 [dm_db_page_info &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [sysprocesses &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
