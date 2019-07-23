---
title: FILE_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILE_ID
- FILE_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IDs [SQL Server], files
- file IDs [SQL Server]
- FILE_ID function
- names [SQL Server], files
- identification numbers [SQL Server], files
- file names [SQL Server], FILE_ID
ms.assetid: 6a7382cf-a360-4d62-b9d2-5d747f56f076
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 63744a6731e7c57a21a821ce7ab65cb49e095e67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071536"
---
# <a name="fileid-transact-sql"></a>FILE_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

對於目前資料庫元件檔案的給定邏輯名稱，此函式會傳回檔案識別碼 (ID)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
FILE_ID ( file_name )  
```  
  
## <a name="arguments"></a>引數  
*file_name*  
這是 **sysname** 類型的運算式，代表會傳回其檔案識別碼值 `FILE_ID` 之檔案的邏輯名稱。  
  
## <a name="return-types"></a>傳回類型  
**smallint**  
  
## <a name="remarks"></a>Remarks  
*file_name* 對應於 sys.master_files 或 sys.database_files 目錄檢視 name 資料行中所顯示的邏輯檔案名稱。  

如果 *file_name* 未對應於目前資料庫元件檔案的邏輯名稱，`FILE_ID` 會傳回 `NULL`。
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，指派給全文檢索目錄的識別碼超過 32767。 由於 `FILE_ID` 函數的傳回類型是 **smallint**，所以`FILE_ID` 不支援全文檢索檔案。 請改用 [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md)。  
  
## <a name="examples"></a>範例  
此範例會傳回 `AdventureWorks_Data` 檔案的檔案識別碼值，這是 `ADVENTUREWORKS2012` 資料庫的元件檔案。  

```sql  
USE AdventureWorks2012;  
GO  
SELECT FILE_ID('AdventureWorks2012_Data')AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2016 中已被取代的 Database Engine 功能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [FILE_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/file-name-transact-sql.md)   
 [中繼資料函數 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
