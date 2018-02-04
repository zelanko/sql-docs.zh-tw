---
title: "sys.fn_check_object_signatures (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fn_check_object_signatures_TSQL
- fn_check_object_signatures_TSQL
- fn_check_object_signatures
- sys.fn_check_object_signatures
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_check_object_signatures function
ms.assetid: 47509566-d3d7-46a9-89c1-91b4895d56b9
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: edc1fde552b2ce71fa6f58b69b7c0a6e878385fd
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysfncheckobjectsignatures-transact-sql"></a>sys.fn_check_object_signatures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  傳回所有可簽署物件的清單，並指出物件是否由指定的憑證或非對稱金鑰所簽署。 如果此物件是由指定的憑證或非對稱金鑰所簽署，它也會傳回此物件的簽章是否有效。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
fn_ check_object_signatures (   
    { '@class' } , { @thumbprint }   
  )   
```  
  
## <a name="arguments"></a>引數  
 {' @*類別*'}  
 識別所提供之指模的類型：  
  
-   'certificate'  
  
-   'asymmetric key'  
  
 @*類別*是**sysname**。  
  
 {@*指紋*}  
 用來加密金鑰的憑證 SHA-1 雜湊，或用來加密金鑰的非對稱金鑰 GUID。 @*憑證指紋*是**varbinary(20)**。  
  
## <a name="tables-returned"></a>傳回的資料表  
 下表列出的資料行， **fn_check_object_signatures**傳回。  
  
|資料行|型別|Description|  
|------------|----------|-----------------|  
|型別|**nvarchar(120)**|傳回類型描述或組件。|  
|entity_id|**int**|傳回所評估之物件的物件識別碼。|  
|is_signed|**int**|當此物件並非由提供的指模所簽署時，傳回 0。 當此物件是由提供的指模所簽署時，傳回 1。|  
|is_signature_valid|**int**|如果 is_signed 值是 1，就會在簽章無效時傳回 0。 當簽章有效時，則傳回 1。<br /><br /> 如果 is_signed 值是 0，則一律傳回 0。|  
  
## <a name="remarks"></a>備註  
 使用**fn_check_object_signatures**確認惡意使用者有尚未竄改物件。  
  
## <a name="permissions"></a>Permissions  
 需要憑證或非對稱金鑰的 VIEW DEFINITION。  
  
## <a name="examples"></a>範例  
 下列範例會尋找 `master` 資料庫的結構描述簽署憑證，然後針對由結構描述簽署憑證所簽署而且具有有效簽章的物件，傳回 `is_signed` 值 1 和 `is_signature_valid` 值 1。  
  
```  
USE master;  
-- Declare a variable to hold the thumbprint.  
DECLARE @thumbprint varbinary(20) ;  
-- Populate the thumbprint variable with the master database schema signing certificate.  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%' ;  
-- Evaluates the objects signed by the schema signing certificate  
SELECT type, entity_id, OBJECT_NAME(entity_id) AS [object name], is_signed, is_signature_valid  
FROM sys.fn_check_object_signatures ('certificate', @thumbprint) ;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [IS_OBJECTSIGNED &#40;Transact-SQL&#41;](../../t-sql/functions/is-objectsigned-transact-sql.md)  
  
  
