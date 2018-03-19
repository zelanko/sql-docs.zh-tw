---
title: CERTPRIVATEKEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTPRIVATEKEY
- CERTPRIVATEKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTPRIVATEKEY
ms.assetid: 33e0f01e-39ac-46da-94ff-fe53b1116df4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: df513e6ce63ff49e31ad05e5a4dca0372de69c83
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="certprivatekey-transact-sql"></a>CERTPRIVATEKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

以二進位格式傳回憑證的私密金鑰。 這個函數會採用三個引數。
-   憑證識別碼。  
-   由此函數傳回時，用來加密私密金鑰位元的加密密碼，如此一來，私密金鑰就不會以純文字格式公開給使用者。  
-   選擇性的解密密碼。 如果指定解密密碼，則會使用此密碼來解密憑證的私密金鑰，否則會使用資料庫主要金鑰。  
  
只有具有憑證之私密金鑰存取權的使用者才能使用這個函數。 這個函數會傳回 PVK 格式的私密金鑰。
  
## <a name="syntax"></a>語法  
  
```sql
CERTPRIVATEKEY   
    (  
          cert_ID   
        , ' encryption_password '   
      [ , ' decryption_password ' ]  
    )  
```  
  
## <a name="arguments"></a>引數  
*certificate_ID*  
憑證的 **certificate_id**。 這可從 sys.certificates 或是使用 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md) 函式取得。 *cert_id* 的類型為 **int**
  
*encryption_password*  
用來加密傳回之二進位值的密碼。
  
*decryption_password*  
用來解密傳回之二進位值的密碼。
  
## <a name="return-types"></a>傳回型
**varbinary**
  
## <a name="remarks"></a>Remarks  
**CERTENCODED** 及 **CERTPRIVATEKEY** 會一起用來傳回憑證的不同部分 (二進位格式)。
  
## <a name="permissions"></a>Permissions  
**CERTPRIVATEKEY** 可以公開使用。
  
## <a name="examples"></a>範例  
  
```sql
CREATE DATABASE TEST1;  
GO  
USE TEST1  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Use 5tr0ng P^55Words'  
GO  
CREATE CERTIFICATE Shipping04   
WITH SUBJECT = 'Sammamish Shipping Records',   
EXPIRY_DATE = '20141031';  
GO  
SELECT CERTPRIVATEKEY(CERT_ID('Shipping04'), 'jklalkaa/; uia3dd');  
```  
  
如需使用 **CERTPRIVATEKEY** 和 **CERTENCODED** 將憑證複製到其他資料庫的更複雜範例，請參閱 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md) 主題中的範例 B。
  
## <a name="see-also"></a>另請參閱
[安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)
[安全性函式 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
