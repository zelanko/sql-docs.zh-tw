---
title: FILE_IDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FILE_IDEX
- FILE_IDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILE_IDEX function
- IDs [SQL Server], files
- file IDs [SQL Server]
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_IDEX
ms.assetid: 7532fea5-ee5e-4edd-b98b-111a7ba56c8e
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 68291b7c53869161434441a590e9b678fc914572
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="fileidex-transact-sql"></a>FILE_IDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

傳回目前資料庫中資料、記錄或全文檢索檔案之指定邏輯檔案名稱的檔案識別碼 (ID)。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
FILE_IDEX ( file_name )  
```  
  
## <a name="arguments"></a>引數  
 *file_name*  
 這是 **sysname** 類型的運算式，代表傳回檔案識別碼的檔案名稱。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
 發生錯誤時傳回 **NULL**  
  
## <a name="remarks"></a>Remarks  
 *file_name* 對應於 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) or [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) 目錄檢視中之 **name** 資料行中所顯示的邏輯檔案名稱。  
  
 FILE_IDEX 可以用在選取清單、WHERE 子句或運算式所允許的任何位置。 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>A. 擷取指定檔案的檔案識別碼  
下列範例會傳回 `AdventureWorks_Data` 檔案的檔案識別碼。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX('AdventureWorks2012_Data') AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
### <a name="b-retrieving-the-file-id-when-the-file-name-is-not-known"></a>B. 當檔案名稱未知時，擷取檔案識別碼  
下列範例會從檔案類型等於 `1` (記錄) 的 `sys.database_files` 目錄檢視中，選取邏輯檔案名稱來傳回 `AdventureWorks` 記錄檔的檔案識別碼。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_IDEX((SELECT TOP (1) name FROM sys.database_files WHERE type = 1)) AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
2  
```  
  
### <a name="c-retrieving-the-file-id-of-a-full-text-catalog-file"></a>C. 擷取全文檢索目錄檔的檔案識別碼  
下列範例會從檔案類型等於 `4` (全文檢索) 的 `sys.database_files` 目錄檢視中，選取邏輯檔案名稱來傳回全文檢索檔的檔案識別碼。 如果全文檢索目錄不存在，此範例將會傳回 NULL。  
  
```sql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>另請參閱  
 [中繼資料函數 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
