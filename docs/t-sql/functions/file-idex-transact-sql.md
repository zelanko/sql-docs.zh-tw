---
title: "FILE_IDEX (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 9a65a49a1e6d8c23a28b117fc90b0276ce185556
ms.contentlocale: zh-tw
ms.lasthandoff: 10/24/2017

---
# <a name="fileidex-transact-sql"></a>FILE_IDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

傳回目前資料庫中資料、記錄或全文檢索檔案之指定邏輯檔案名稱的檔案識別碼 (ID)。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
FILE_IDEX ( file_name )  
```  
  
## <a name="arguments"></a>引數  
 *file_name*  
 這是類型的運算式**sysname** ，代表要傳回檔案識別碼。 檔案名稱  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
 **NULL**錯誤  
  
## <a name="remarks"></a>備註  
 *file_name*對應到顯示中的邏輯檔案名稱**名稱**中的資料行[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)或[sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)目錄檢視。  
  
 FILE_IDEX 可以用在選取清單、WHERE 子句或運算式所允許的任何位置。 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-retrieving-the-file-id-of-a-specified-file"></a>A. 擷取指定檔案的檔案識別碼  
下列範例會傳回 `AdventureWorks_Data` 檔案的檔案識別碼。  
  
```tsql  
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
下列範例會傳回的檔案識別碼`AdventureWorks`選取邏輯檔案名稱，從記錄檔`sys.database_files`目錄的檢視，其中的檔案類型等於`1`（記錄）。  
  
```tsql  
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
下列範例會傳回全文檢索檔案的檔案識別碼選取邏輯檔案名稱，從`sys.database_files`目錄的檢視，其中的檔案類型等於`4`（全文檢索）。 如果全文檢索目錄不存在，此範例將會傳回 NULL。  
  
```tsql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## <a name="see-also"></a>另請參閱  
 [中繼資料函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  

