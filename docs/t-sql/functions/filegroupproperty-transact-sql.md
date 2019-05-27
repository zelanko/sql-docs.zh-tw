---
title: FILEGROUPPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ed5486e9f48bc0f0ca5ab4b6af031571f4f3580d
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2019
ms.locfileid: "65945944"
---
# <a name="filegroupproperty-transact-sql"></a>FILEGROUPPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

此函數會傳回所指定名稱的檔案群組屬性值與與檔案群組值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
FILEGROUPPROPERTY ( filegroup_name, property )  
```  
  
## <a name="arguments"></a>引數  
 *filegroup_name*  
類型是 **sysname** 的運算式，代表 `FILEGROUPPROPERTY` 傳回具名屬性資訊的檔案群組名稱。  
  
 *property*  
類型是 **varchar(128)** 的運算式，此運算式會傳回檔案群組屬性的名稱。 *Property* 可以傳回下列其中一個值：  
  
|ReplTest1|Description|傳回的值|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|檔案群組是唯讀的。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 無效的輸入。|  
|**IsUserDefinedFG**|檔案群組是使用者自訂檔案群組。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 無效的輸入。|  
|**IsDefault**|檔案群組是預設的檔案群組。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 無效的輸入。|  
  
## <a name="return-types"></a>傳回類型  
**int**  
  
## <a name="remarks"></a>Remarks  
*filegroup_name* 對應到 **sys.filegroups** 目錄檢視中的 **name** 資料行。  
  
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
 [FILEGROUP_ID &#40;Transact-SQL&#41;](../../t-sql/functions/filegroup-id-transact-sql.md)   
 [FILEGROUP_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/filegroup-name-transact-sql.md)   
 [中繼資料函數 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  
