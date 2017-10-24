---
title: "卸除的外部檔案格式 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cf9009b-59f9-4aac-bef1-dcf2cf0708b2
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 9c30ce4ee5d28cb55b824827de6c89f8d673640c
ms.contentlocale: zh-tw
ms.lasthandoff: 10/24/2017

---
# <a name="drop-external-file-format-transact-sql"></a>卸除的外部檔案格式 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  移除 PolyBase 外部檔案格式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Drop an external file format  
DROP EXTERNAL FILE FORMAT external_file_format_name  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *external_file_format_name*  
 若要卸除的外部檔案格式名稱。  
  
## <a name="metadata"></a>中繼資料  
 若要檢視外部檔案格式使用一份[sys.external_file_formats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)系統檢視表。  
  
```  
SELECT * FROM sys.external_file_formats;  
```  
  
## <a name="permissions"></a>Permissions  
 需要改變任何外部檔案格式。  
  
## <a name="general-remarks"></a>一般備註  
 卸除的外部檔案格式並不會移除外部的資料。  
  
## <a name="locking"></a>鎖定  
 外部檔案格式物件上採用共用的鎖定。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-basic-syntax"></a>A. 使用基本語法  
  
```  
DROP EXTERNAL FILE FORMAT myfileformat;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE EXTERNAL FILE FORMAT &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  


