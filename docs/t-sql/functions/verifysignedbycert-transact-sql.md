---
title: "VERIFYSIGNEDBYCERT (TRANSACT-SQL) |Microsoft 文件"
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
- VERIFYSIGNEDBYCERT
- VERIFYSIGNEDBYCERT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- digitally signed data for changes [SQL Server]
- verifying digitally signed data for changes
- testing digitally signed data for changes
- checking digitally signed data for changes
- VERIFYSIGNEDBYCERT
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 4e041f33-60c4-4190-91c7-220d51dd6c8f
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6267b5ca34c3e69af9611c2cdb4a607a7d539f00
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="verifysignedbycert-transact-sql"></a>VERIFYSIGNEDBYCERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  測試數位簽署的資料在簽署之後是否已經變更。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
VerifySignedByCert( Cert_ID , signed_data , signature )  
```  
  
## <a name="arguments"></a>引數  
 *Cert_ID*  
 這是資料庫中憑證的識別碼。 *Cert_ID*是**int**。  
  
 *signed_data*  
 這類型的變數**nvarchar**， **char**， **varchar**，或**nchar**包含已經使用憑證簽署的資料。  
  
 *簽章*  
 這是附加在已簽署資料中的簽章。 *簽章*是**varbinary**。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
 如果已簽署的資料不變，則傳回 1，否則傳回 0。  
  
## <a name="remarks"></a>備註  
 **VerifySignedBycert**使用指定的憑證的公開金鑰解密資料的簽章，並比較解密的值與新計算的 MD5 雜湊的資料。 如果值相符，簽章將確認為有效。  
  
## <a name="permissions"></a>Permissions  
 需要憑證的 VIEW DEFINITION 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-verifying-that-signed-data-has-not-been-tampered-with"></a>A. 驗證簽署的資料未遭竄改  
 下列範例會測試 `Signed_Data` 中的資訊，在利用名為 `Shipping04` 的憑證簽署之後，是否已經變更。 簽章是儲存在 `DataSignature` 中。 憑證 (`Shipping04`) 會傳遞至 `Cert_ID`，後者則會傳回資料庫中的憑證識別碼。 如果 `VerifySignedByCert` 傳回 1，表示簽章正確。 如果 `VerifySignedByCert` 傳回 0，表示 `Signed_Data` 中的資料，並不是產生 `DataSignature` 所用的資料。 在本例中，表示 `Signed_Data` 在簽署之後已經變更，或者 `Signed_Data` 是以不同的憑證簽署的。  
  
```  
SELECT Data, VerifySignedByCert( Cert_Id( 'Shipping04' ),  
    Signed_Data, DataSignature ) AS IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
### <a name="b-returning-only-records-that-have-a-valid-signature"></a>B. 只傳回具有有效簽章的記錄  
 這項查詢只會傳回自從使用憑證 `Shipping04` 簽署之後尚未變更的記錄。  
  
```  
SELECT Data FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByCert( Cert_Id( 'Shipping04' ), Data,   
    DataSignature ) = 1   
AND Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [CERT_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [SIGNBYCERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/signbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [卸除憑證 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
