---
description: FILEPROPERTYEX (Transact-SQL)
title: FILEPROPERTYEX (Transact-SQL) | Microsoft Docs
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILEPROPERTYEX_TSQL
- FILEPROPERTYEX
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file properties
- displaying file properties
- file properties [SQL Server]
- FILEPROPERTYEX function
- file names [SQL Server], FILEPROPERTYEX
author: stevestein
ms.author: sstein
ms.openlocfilehash: 802963395caa096d6a5e26a506e45d7c282ea7cc
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91114766"
---
# <a name="filepropertyex-transact-sql"></a>FILEPROPERTYEX (Transact-SQL)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  指定了目前資料庫中的檔案名稱和屬性名稱時，傳回指定的延伸檔案屬性值。 針對不在目前資料庫中的檔案，或不存在的延伸檔案屬性，會傳回 Null。 目前，延伸檔案屬性僅適用於 Azure Blob 儲存體中的資料庫。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
FILEPROPERTYEX ( name , property )  
```  
  
## <a name="arguments"></a>引數  
 *name*  
 這是包含傳回屬性資訊所屬的目前資料庫之相關聯檔案名稱的運算式。 *file_name* 為 **nchar(128)**。  
  
 *property*  
 這是包含要傳回之檔案屬性名稱的運算式。 *property* 為 **varchar(128)**，而且可以是下列值之一。  


  
|值|描述|
|-----------|-----------------|  
|**BlobTier**|目標 Azure 分頁 Blob 的階層。 僅適用於使用 Azure 分頁 Blob 儲存體的標準和一般用途資料庫。|
|**AccountType**|儲存體帳戶類型，指出其為 Blob 儲存體或檔案儲存體，以及其為進階還是標準儲存體。|
|**IsInferredTier**|指出階層是否為隱含 (推斷) 階層，其可能會隨著資料大小或明確 (固定) 階層而成長。|
|**IsPageBlob**|指出目標 Blob 是否為分頁 Blob。|
  
## <a name="return-types"></a>傳回型別  
 **sql_variant**  
  
## <a name="remarks"></a>備註  
 *file_name* 對應於 **sys.master_files** 或 **sys.database_files** 目錄檢視中的 **name** 資料行。  
  
## <a name="examples"></a>範例  
 下列範例會傳回資料庫檔案的設定：
```sql
SELECT s.file_id,
       s.type_desc,
       s.name,
       FILEPROPERTYEX(s.name, 'BlobTier') AS BlobTier,
       FILEPROPERTYEX(s.name, 'AccountType') AS AccountType,
       FILEPROPERTYEX(s.name, 'IsInferredTier') AS IsInferredTier,
       FILEPROPERTYEX(s.name, 'IsPageBlob') AS IsPageBlob
FROM sys.database_files AS s
WHERE s.type_desc IN ('ROWS', 'LOG');
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
file_id  type_desc  name  BlobTier  AccountType  IsInferredTier  IsPageBlob
--------------------------------------------------------------------------------------
1     ROWS      data_0  P30  PremiumBlobStorage  0   1
2     LOG       log     P30  PremiumBlobStorage  0   1

(2 rows affected)
```  
  
## <a name="see-also"></a>另請參閱  
 [FILEGROUPPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/filegroupproperty-transact-sql.md)   
 [中繼資料函數 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
