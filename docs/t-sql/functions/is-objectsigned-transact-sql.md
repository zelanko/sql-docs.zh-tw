---
title: IS_OBJECTSIGNED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IS_OBJECTSIGNED
- IS_OBJECTSIGNED_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IS_OBJECTSIGNED function
ms.assetid: afbc4f7f-8266-4ee6-9802-14a2dbe69ef6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1891180d7fa3b1a064cf0cdebc5295303ecf7b5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086703"
---
# <a name="isobjectsigned-transact-sql"></a>IS_OBJECTSIGNED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指出物件是否由指定的憑證或非對稱金鑰所簽署。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
IS_OBJECTSIGNED (   
'OBJECT', @object_id, @class, @thumbprint  
  )   
```  
  
## <a name="arguments"></a>引數  
 **'OBJECT'**  
 安全性實體類別的類型。  
  
 *@object_id*  
 正在測試之物件的 object_id。 *@object_id* 的類型為 **int**。  
  
 *@class*  
 物件的類別：  
  
-   'certificate'  
  
-   'asymmetric key'  
  
 *@class* 為 **sysname**。  
  
 *@thumbprint*  
 物件的 SHA 指模。 *@thumbprint* 的類型為 **varbinary(32)** 。  
  
## <a name="returned-types"></a>傳回的類型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 IS_OBJECTSIGNED 會傳回下列值。  
  
|傳回值|Description|  
|------------------|-----------------|  
|NULL|物件未簽署，或物件無效。|  
|0|物件已簽署，但簽章無效。|  
|1|已簽署物件。|  
  
## <a name="permissions"></a>權限  
 需要憑證或非對稱金鑰的 VIEW DEFINITION。  
  
## <a name="examples"></a>範例  
  
### <a name="a-displaying-extended-properties-on-a-database"></a>A. 顯示資料庫的擴充屬性  
 下列範例會測試 **master** 資料庫中的 spt_fallback_db 資料表是否已由結構描述簽署憑證所簽署。  
  
```  
USE master;  
-- Declare a variable to hold a thumbprint and an object name  
DECLARE @thumbprint varbinary(20), @objectname sysname;  
  
-- Populate the thumbprint variable with the thumbprint of   
-- the master database schema signing certificate  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%';  
  
-- Populate the object name variable with a table name in master  
SELECT @objectname = 'spt_fallback_db';  
  
-- Query to see if the table is signed by the thumbprint  
SELECT @objectname AS [object name],  
IS_OBJECTSIGNED(  
'OBJECT', OBJECT_ID(@objectname), 'certificate', @thumbprint  
) AS [Is the object signed?] ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.fn_check_object_signatures &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-check-object-signatures-transact-sql.md)  
  
  
