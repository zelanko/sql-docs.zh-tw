---
title: "FILE_NAME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILE_NAME_TSQL
- FILE_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file names
- file names [SQL Server], FILE_NAME
- IDs [SQL Server], files
- file IDs [SQL Server]
- names [SQL Server], files
- displaying file names
- identification numbers [SQL Server], files
- FILE_NAME function
- logical file names [SQL Server]
ms.assetid: 68b298aa-ce47-4af5-b59f-9a1b46d48326
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 0fcf9f37da268e266cb94037995f271c54536cb8
ms.contentlocale: zh-tw
ms.lasthandoff: 10/24/2017

---
# <a name="filename-transact-sql"></a>FILE_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回給定檔案識別碼 (ID) 的邏輯檔案名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
FILE_NAME ( file_id )   
```  
  
## <a name="arguments"></a>引數  
 *file_id*  
 這是要傳回檔案名稱的檔案識別碼。 *file_id*是**int**。  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar （128)**  
  
## <a name="remarks"></a>備註  
 *file_ID*對應於 sys.master_files 或 sys.database_files 目錄檢視中的 file_id 資料行。  
  
## <a name="examples"></a>範例  
 下列範例會傳回的檔案名稱`file_ID 1`和`file_ID`中[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]資料庫。  
  
```tsql  
SELECT FILE_NAME(1) AS 'File Name 1', FILE_NAME(2) AS 'File Name 2';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
File Name 1           File Name 2  
----------------      ------------------------  
AdventureWorks2012_Data   AdventureWorks2012_Log  

(1 row(s) affected)
``` 
  
## <a name="see-also"></a>另請參閱  
 [FILE_IDEX &#40;TRANSACT-SQL &#41;](../../t-sql/functions/file-idex-transact-sql.md)   
 [中繼資料函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  

