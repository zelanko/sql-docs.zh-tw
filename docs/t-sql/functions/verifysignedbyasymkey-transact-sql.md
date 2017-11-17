---
title: "VERIFYSIGNEDBYASYMKEY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
- VERIFYSIGNEDBYASYMKEY_TSQL
- VERIFYSIGNEDBYASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- verifying digitally signed data for changes
- VERIFYSIGNEDBYASYMKEY
- testing digitally signed data for changes
- checking digitally signed data for changes
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 9f7c6e0b-5ba4-4dbb-994d-5bd59f4908de
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: da1bbf517ed81e1e39a7ba95db7af26eb2d18e77
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="verifysignedbyasymkey-transact-sql"></a>VERIFYSIGNEDBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  測試數位簽署的資料在簽署之後是否已經變更。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
VerifySignedByAsymKey( Asym_Key_ID , clear_text , signature )  
```  
  
## <a name="arguments"></a>引數  
 *Asym_Key_ID*  
 這是資料庫中的非對稱金鑰憑證識別碼。  
  
 *clear_text*  
 這是正在驗證的純文字資料。  
  
 *簽章*  
 這是附加在已簽署資料中的簽章。 *簽章*是**varbinary**。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
 簽章符合時傳回 1，否則傳回 0。  
  
## <a name="remarks"></a>備註  
 **VerifySignedByAsymKey**使用指定的非對稱金鑰的公開金鑰解密資料的簽章，並比較解密的值與新計算的 MD5 雜湊的資料。 如果值相符，簽章將確認為有效。  
  
## <a name="permissions"></a>Permissions  
 需要非對稱金鑰的 VIEW DEFINITION 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-testing-for-data-with-a-valid-signature"></a>A. 測試含有效簽章的資料  
 如果所選的資料在以非對稱金鑰 `WillisKey74` 簽署之後尚未變更，則下列範例會傳回 1。 如果資料已被竄改，則下列範例會傳回 0。  
  
```  
SELECT Data,  
     VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), SignedData,  
     DataSignature ) as IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
RETURN;  
```  
  
### <a name="b-returning-a-result-set-that-contains-data-with-a-valid-signature"></a>B. 傳回包含含有效簽章之資料的結果集  
 下列範例會傳回 `SignedData04` 中的資料列，它們包含自從以非對稱金鑰 `WillisKey74` 簽署之後尚未變更的資料。 這個範例會呼叫函數 `AsymKey_ID`，從資料庫取得非對稱金鑰的識別碼。  
  
```  
SELECT Data   
FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), Data,  
     DataSignature ) = 1  
AND Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ASYMKEY_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/asymkey-id-transact-sql.md)   
 [SIGNBYASYMKEY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

