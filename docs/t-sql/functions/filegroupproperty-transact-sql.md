---
title: "FILEGROUPPROPERTY (TRANSACT-SQL) |Microsoft 文件"
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
- FILEGROUPPROPERTY_TSQL
- FILEGROUPPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], property values
- FILEGROUPPROPERTY function
- viewing filegroup properties
- displaying filegroup properties
ms.assetid: b3a930e6-df05-4034-929c-f681f5f6fc6e
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 050ec0b7c3fdc9146a25b1b1f372ee4928d80c09
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="filegroupproperty-transact-sql"></a>FILEGROUPPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  如果與檔案群組和屬性名稱一起提供時，就傳回指定的檔案群組屬性值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
FILEGROUPPROPERTY ( filegroup_name , property )  
```  
  
## <a name="arguments"></a>引數  
 *filegroup_name*  
 這是類型的運算式**sysname** ，代表傳回具名的屬性資訊所屬的檔案群組的名稱。  
  
 *屬性*  
 這是類型的運算式**varchar （128)**包含要傳回之檔案群組屬性的名稱。 *屬性*可以是下列值之一。  
  
|值|Description|傳回的值|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|檔案群組是唯讀的。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 輸入無效。|  
|**IsUserDefinedFG**|檔案群組是使用者自訂檔案群組。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 輸入無效。|  
|**IsDefault**|檔案群組是預設的檔案群組。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 輸入無效。|  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>備註  
 *filegroup_name*對應至**名稱**中的資料行**sys.filegroups**目錄檢視。  
  
## <a name="examples"></a>範例  
 這個範例會傳回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中主要檔案群組的 `IsDefault` 屬性設定。  
  
```  
  
SELECT FILEGROUPPROPERTY('PRIMARY', 'IsDefault') AS 'Default Filegroup';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Default Filegroup   
---------------------   
1  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [FILEGROUP_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/filegroup-id-transact-sql.md)   
 [FILEGROUP_NAME &#40;TRANSACT-SQL &#41;](../../t-sql/functions/filegroup-name-transact-sql.md)   
 [中繼資料函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sys.filegroups &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  
