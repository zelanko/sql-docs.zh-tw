---
title: FILE_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0857a8982fe64d2e2461f5420588ea4a9c527556
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33054005"
---
# <a name="fileid-transact-sql"></a>FILE_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回目前資料庫中給定邏輯檔案名稱的檔案識別碼 (ID)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
FILE_ID ( file_name )  
```  
  
## <a name="arguments"></a>引數  
 *file_name*  
 這是 **sysname** 類型的運算式，代表傳回檔案識別碼的檔案名稱。  
  
## <a name="return-types"></a>傳回類型  
 **smallint**  
  
## <a name="remarks"></a>Remarks  
 *file_name* 對應於 sys.master_files 或 sys.database_files 目錄檢視中之 name 資料行中所顯示的邏輯檔案名稱。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，指派給全文檢索目錄的識別碼大於 32767。 由於 FILE_ID 函數的傳回類型是 **smallint**，所以此函數無法用於全文檢索檔案。 請改用 [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `AdventureWorks_Data` 檔案的檔案識別碼。  
  
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
  
  
