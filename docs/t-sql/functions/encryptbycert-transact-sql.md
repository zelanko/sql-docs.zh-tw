---
title: "ENCRYPTBYCERT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYCERT
- ENCRYPTBYCERT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- certificates [SQL Server], encryption
- encryption [SQL Server], certificates
- ENCRYPTBYCERT function
ms.assetid: ab66441f-e2d2-4e3a-bcae-bcc09e12f3c1
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 20bb47de8ce928e623f34e4e99874f0598369729
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="encryptbycert-transact-sql"></a>ENCRYPTBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  以憑證的公開金鑰加密資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
EncryptByCert ( certificate_ID , { 'cleartext' | @cleartext } )  
```  
  
## <a name="arguments"></a>引數  
 *certificate_ID*  
 資料庫中的憑證識別碼。 **int**。  
  
 *純文字*  
 將以憑證加密的資料字串。  
  
 **@cleartext**  
 類型的變數**nvarchar**， **char**， **varchar**，**二進位**， **varbinary**，或**nchar**包含將使用憑證的公開金鑰加密的資料。  
  
## <a name="return-types"></a>傳回類型  
 **varbinary** 8,000 個位元組的大小上限。  
  
## <a name="remarks"></a>備註  
 這個函數是利用憑證的公開金鑰為資料加密。 加密文字只能利用對應的私密金鑰加以解密。 與利用對稱金鑰進行加密和解密相比，這種非對稱轉換的成本相當高。 如果您是使用大型資料集 (如資料表中的使用者資料)，不建議您使用非對稱式加密。  
  
## <a name="examples"></a>範例  
 這個範例利用稱為 `@cleartext` 的憑證加密儲存在 `JanainaCert02` 中的純文字。 加密的資料會插入 `ProtectedData04` 資料表中。  
  
```  
INSERT INTO [AdventureWorks2012].[ProtectedData04]   
    VALUES ( N'Data encrypted by certificate ''Shipping04''',  
    EncryptByCert(Cert_ID('JanainaCert02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [DECRYPTBYCERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/decryptbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [卸除憑證 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
